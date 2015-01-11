---
layout: post
title: github api
date: 2015-01-09 08:11:00 +08:00
categories: [git]
---
#### 標題 : {{page.title}} ####

##簡介##
研究了一下怎麼使用github api，api 的 [schema](https://developer.github.com/v3/#schema) 分成兩種

1. api.github.com
2. yourdomain.com/api/v3

兩種方式都可以使用，首先介紹第一種是使用Oauth，點選 "Developer applications" 的 "Register new application"， 
填寫 application name、Home page url、application description、Authorization callback URL，這邊我的 Authorization callback URL 填寫是 http://127.0.0.1， 
其餘都是隨意填寫。

填寫完畢後，想要透過這一個 application 使用 Oauth 的人，需要打兩次 command，順帶說明一下，client_id / redirect_uri / client_secret 是從註冊的 application 那邊得到。 
首先是取得使用 Oauth 的權限，用下面的指令之後，需要由 web 點選同意後才可以進行下一步。

{% highlight bash %}
curl -H "https://git.corp.yahoo.com/login/oauth/authorize?client_id=****&redirect_uri=http://127.0.0.1"
{% endhighlight %}

同意後再使用下面的指令，就可以取得 access token 

{% highlight bash %}
curl -H "https://git.corp.yahoo.com/login/oauth/access_token?client_id=****&client_secret=****&code=****"
{% endhighlight %}

最後就可以使用 api 囉 

{% highlight bash %}
curl -H "Authorization: token **********" http://yourdomain/api/v3/apiname
{% endhighlight %}

到這邊為止是屬於第一種使用 Oauth 的方式。 

接著是第二種，需要申請個人的 access token，要到這個[連結](https://github.com/settings/applications)，
然後選擇 "Personal access tokens" 點選 Generate new token，填寫 "Token description"，選擇需要使用的 scope，如下圖 

![My helpful screenshot]({{ site.url }}/images/github-personal-token.jpg)


接著使用 access token 試著打 api

{% highlight bash %}
curl -s -H "Authorization: token 1859f787a2ae0d0808ab4252d044e439e7ffb876" https://api.github.com/users/iamsleep/repos
{% endhighlight %}

會拿到一串 jason format 的資料如下，再來就看個人怎麼處理了，因為我目前只是想要同時 fetch 所以會用到的 source code ...
{% highlight json linenos %}
  {
    "id": 4365511,
    "name": "vim",
    "full_name": "iamsleep/vim",
    "owner": {
      "login": "iamsleep",
      "id": 1548631,
      "avatar_url": "https://avatars.githubusercontent.com/u/1548631?v=3",
      "gravatar_id": "",
      "url": "https://api.github.com/users/iamsleep",
      "html_url": "https://github.com/iamsleep",
      "followers_url": "https://api.github.com/users/iamsleep/followers",
      "following_url": "https://api.github.com/users/iamsleep/following{/other_user}",
      "gists_url": "https://api.github.com/users/iamsleep/gists{/gist_id}",
      "starred_url": "https://api.github.com/users/iamsleep/starred{/owner}{/repo}",
      "subscriptions_url": "https://api.github.com/users/iamsleep/subscriptions",
      "organizations_url": "https://api.github.com/users/iamsleep/orgs",
      "repos_url": "https://api.github.com/users/iamsleep/repos",
      "events_url": "https://api.github.com/users/iamsleep/events{/privacy}",
      "received_events_url": "https://api.github.com/users/iamsleep/received_events",
      "type": "User",
      "site_admin": false
    },
    "private": false,
    "html_url": "https://github.com/iamsleep/vim",
    "description": "vim",
    "fork": false,
    "url": "https://api.github.com/repos/iamsleep/vim",
    "forks_url": "https://api.github.com/repos/iamsleep/vim/forks",
    "keys_url": "https://api.github.com/repos/iamsleep/vim/keys{/key_id}",
    "collaborators_url": "https://api.github.com/repos/iamsleep/vim/collaborators{/collaborator}",
    "teams_url": "https://api.github.com/repos/iamsleep/vim/teams",
    "hooks_url": "https://api.github.com/repos/iamsleep/vim/hooks",
    "issue_events_url": "https://api.github.com/repos/iamsleep/vim/issues/events{/number}",
    "events_url": "https://api.github.com/repos/iamsleep/vim/events",
    "assignees_url": "https://api.github.com/repos/iamsleep/vim/assignees{/user}",
    "branches_url": "https://api.github.com/repos/iamsleep/vim/branches{/branch}",
    "tags_url": "https://api.github.com/repos/iamsleep/vim/tags",
    "updated_at": "2014-12-16T03:39:22Z",
    "pushed_at": "2014-12-16T03:39:22Z",
    "git_url": "git://github.com/iamsleep/vim.git",
    "ssh_url": "git@github.com:iamsleep/vim.git",
    "clone_url": "https://github.com/iamsleep/vim.git",
    "svn_url": "https://github.com/iamsleep/vim",
    "homepage": "",
    "size": 3152,
    "stargazers_count": 0,
    "watchers_count": 0,
    "language": "VimL",
    "has_issues": true,
    "has_downloads": true,
    "has_wiki": true,
    "has_pages": false,
    "forks_count": 0,
    "mirror_url": null,
    "open_issues_count": 0,
    "forks": 0,
    "open_issues": 0,
    "watchers": 0,
    "default_branch": "master",
    "permissions": {
      "admin": true,
      "push": true,
      "pull": true
    }
  }
{% endhighlight %}
 
 
## 應用 ##
> 接下來我們可以有幾種應用，不過我們需要先準備一個可以 parse json format 的工具， 
> 選擇自己喜歡的方式，看是要自己寫 script 或是用現成的工具，這邊使用的是 [jq](http://stedolan.github.io/jq/) 

第一種，假設想要下載 github 上的 repostory，比如找出目前我的目錄或者某個 group 有哪些 repostories，並且同時 clone
{% highlight bash %}
curl -s -H "Authorization: token 6f3627f72b69b953e53d2a1418c5bfd9b8a6d41f"  https://api.github.com/users/iamsleep/repos  | jq -r '.[].ssh_url' | xargs -n 1 -P 10 git clone
{% endhighlight %}

{% highlight bash %}
curl -s -H "Authorization: token 6f3627f72b69b953e53d2a1418c5bfd9b8a6d41f"  https://api.github.com/orgs/test/repos  | jq -r '.[].ssh_url' | xargs -n 1 -P 10 git clone
{% endhighlight %}


第二種，搜尋 repository ，通常我們只記得片段的 component 名稱，這時候透過 [search](https://developer.github.com/v3/search/) 的功能相當方便，列出所有可能的 repositories， 
這邊要注意的是 default search result 是 30 個，目前上限是 100，所以有可能會有漏掉，這點要特別注意。
{% highlight bash linenos %}
curl -s -H "Authorization: token 6f3627f72b69b953e53d2a1418c5bfd9b8a6d41f" "https://api.github.com/api/v3/search/repositories?q=ecpayment" | jq -r '.items[].ssh_url' 
{% endhighlight %}

第三種，使用 api tag，對於管理很多 repository 的使用者來說，如果能透過 api 做到某些事情是很方便也節省時間，所以如果可以同時間把大量要同一時間要 release 的 repository 都下好 tag ，
真的是在節省時間不過。可以參考 [git tag](https://developer.github.com/v3/git/tags/)

附註
1. [如何移除 jq 的output 中的 double quote](https://github.com/stedolan/jq/wiki/FAQ) 
2. [xargs 使用 parallel](http://offbytwo.com/2011/06/26/things-you-didnt-know-about-xargs.html)
