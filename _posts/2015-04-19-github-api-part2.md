---
layout: post
title: github api
date: 2015-04-19 11:11:00 +08:00
categories: [git]
---
#### 標題 : {{page.title}} ####

這次要介紹的是 pull request api, 為什麼會特別講到這一個 api 呢? 因為目前工作上大多數的時候都是 fork 一份 code,
等到修改完成後，再透過透過網頁 pull request 進行 code review 以及 merge。
也因為這樣，必須將畫面從 terminal 暫時切回 browser，久而久之，會有一種時常被中斷的感覺，就像是要睡覺一直被吵醒。

進而研究了一下目前是不是有方法可以直接從 terminal 直接下 command 就能夠達到我們的目的，google 告訴我們很多想要的結果，像是 hub，
就可以達到我們想要的目標，但是呢，需要裝 GO，這樣讓我覺得不太合適，因為這樣又多了一個 dependency, 需要安裝額外的東西，而其他的
幾乎都是模擬瀏覽器點擊，所以，還是決定自己去寫一個只需要執行 bash，就可以做到這件事情的工具，目前寫好了初版，放在[這]()。

  首先，請參考 [github api v3 - pull request](https://developer.github.com/v3/pulls/#create-a-pull-request) 中介紹
的內容：

> The Pull Request API allows you to list, view, edit, create, and even merge pull requests.
> Comments on pull requests can be managed via the Issue Comments API.

我們將會使用 create 的 api 產生新的 pull request。

首先，需我們需要 [github api access token](http://iamsleep.github.io/2015/01/12/github-api/#disqus_thread)，
有了 token 後，輸入 `git config --global user.token`。再來是確定有裝 [jq](http://stedolan.github.io/jq/)。
接著執行git-pr，輸入 message 以及 title 後，送出即可。
