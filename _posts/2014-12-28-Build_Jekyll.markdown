---
layout: post
title: jekyll and github
date: 2014-12-28 10:43:00 +08:00
categories: [jekyll, github]
---
#### 標題 : {{page.title}} ####

剛開始使用 github page 的功能，為了提醒自己，同時也能幫助其他使用者，所以寫下這一篇文章。 
先列出目前為止看到相關的文章 

+ [jekylly](http://jekyllrb.com/docs/templates/) 
+ [在 Github 寫 blog](http://blog.bonereborn.com/github/2013/09/05/blogging-on-github/) 
+ [使用 Jekyll 與 GitHub Pages 架站](http://blog.lyhdev.com/2012/02/jekyll-github-pages.html) 
+ [博客當如駭客 - Github Pages & Jekyll](http://chchwy.github.io/2012/12/Blogging-Like-a-Hacker-Github-Pages.html) 
+ [搭建一个免费的，无限流量的 Blog----github Pages 和 Jekyll 入门](http://www.ruanyifeng.com/blog/2012/08/blogging_with_jekyll.html) 
+ [github page structure](https://github.com/mojombo/tpw) 
+ [使用 Github Pages 创建个人 Wiki](http://junnan.org/blog/2011-06-23-create-wiki-on-github-pages.html) 


理論上參考上述的文章，就可以順利產生自己的 github page。為了怕看不懂或者使用不順利，所以寫出我自己的 
步驟。 

1. 要有自己的 github 帳號，沒有的話直接申請即可。 
2. [新增](https://github.com/new) repostory，名稱就是 $username.github.io。 
3. 新增首頁 echo "test" > index.html
4. commit 後等一小段時間，輸入自己的 github page url "username.github.io"，就會出現剛剛的文字 test。

到這邊為止，應該都可以很順利完成，接著是美化頁面，因為 github 是使用 jekyll 處理頁面的 templates，所
以可以採用 jekyll 的 data structure 處理。data structure 如下：
    
    ├── 404.html
    ├── _config.yml
    ├── _includes
    │   ├── ga.html
    │   ├── header.html
    │   └── twitter.html
    ├── _layouts
    │   ├── default.html
    │   ├── error.html
    │   └── post.html
    ├── _posts
    │   └── 2014-12-28-Build_Jekyll.markdown
    ├── atom.xml
    ├── images
    │   ├── bowling_kata_in_java.png
    │   ├── jekyll_pygmentize.jpg
    │   ├── rails3beta.jpg
    │   └── rails3rc.jpg
    ├── index.html
    ├── javascript
    │   └── highlight.pack.js
    └── stylesheets
        ├── fonts
        │   ├── DroidSans-Bold-webfont.eot
        │   ├── DroidSans-Bold-webfont.svg
        │   ├── DroidSans-Bold-webfont.ttf
        │   ├── DroidSans-Bold-webfont.woff
        │   ├── DroidSans-webfont.eot
        │   ├── DroidSans-webfont.svg
        │   ├── DroidSans-webfont.ttf
        │   ├── DroidSans-webfont.woff
        │   ├── DroidSansMono-webfont.eot
        │   ├── DroidSansMono-webfont.svg
        │   ├── DroidSansMono-webfont.ttf
        │   └── DroidSansMono-webfont.woff
        ├── screen.css
        └── tomorrow_night.css


主要需要有 _layouts / _posts / _includes 這三個目錄，另外要設定 _config.yml，詳細設定上面參考的網頁
都有，所以這邊不多加贅述。如果都設定完成之後，應該就會有正常且漂亮的頁面出現了。

備註: 檔案名稱格式為 2014-12-28-"filename"
