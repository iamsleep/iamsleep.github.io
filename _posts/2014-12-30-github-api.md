---
layout: post
title: github api
date: 2014-12-30 12:43:00 +08:00
categories: [git]
---
#### 標題 : {{page.title}} ####

研究了一下怎麼使用github api，api 的 [schema](https://developer.github.com/v3/#schema) 分成兩種

1. api.github.com
2. yourdomain.com/api/v3

兩種方式都可以使用，第一種是使用Oauth，點選 "Developer applications" 的 "Register new application"， 
填寫 application name、Home page url、application description、Authorization callback URL，這邊我的 Authorization callback URL 填寫是 http://127.0.0.1， 
其餘都是隨意填寫。

填寫完畢後，想要透過這一個 application 使用 Oauth 的人，需要打兩次 command，順帶說明一下，client_id / redirect_uri / client_secret 是從註冊的 application 那邊得到。 
首先是取得使用 Oauth 的權限，用下面的指令之後，需要由 web 點選同意後才可以進行下一步。

{% highlight ruby %}
curl -H "https://git.corp.yahoo.com/login/oauth/authorize?client_id=****&redirect_uri=http://127.0.0.1" 
{% endhighlight %}

同意後再使用下面的指令，就可以取得 access token 

curl -H "https://git.corp.yahoo.com/login/oauth/access_token?client_id=****&client_secret=****&code=****" 

最後就可以使用 api 囉 

curl -H "Authorization: token **********" http://yourdomain

這邊我使用的是第二種，需要申請個人的 access token，要到這個[連結](https://github.com/settings/applications)，
然後選擇 "Personal access tokens" 點選 Generate new token，產生一串的 serial number，

接著使用 access token 試著打 api

curl -u **********:x-oauth-basic  https://yourdomain 

待續...
