---
layout: post
title: "Octopress-サイドバーにProfile追加"
date: 2016-08-30 13:23:53 +0000
comments: true
categories: [octopress]
---

デフォルトでプロフィール用のHTMLは以下の場所に作成されている。  
`source/_includes/custom/asides/about.html`  

### about.htmlファイルを編集

```
<section>
  <h1>About Me</h1>
  <p>A little something about me.</p>
</section>
```

<!--more-->

サイドバーにabout.htmlを追加する場合は`_config.yml`に追記

### _config.ymlの編集

サイドバーの先頭にプロフィールを表示させたいので、先頭に追記

```
# list each of the sidebar modules you want to include, in the order you want them to appear.
# To add custom asides, create files in /source/_includes/custom/asides/ and add them to the list like 'custom/asides/custom_aside_name.html'
# default_asides: [asides/recent_posts.html, asides/github.html, asides/delicious.html, asides/pinboard.html, asides/googleplus.html]
default_asides: [
  + custom/asides/about.html,
    asides/recent_posts.html,
    custom/asides/category_list.html,
    custom/asides/tag_cloud.html,
    asides/github.html, 
    asides/delicious.html,
    asides/pinboard.html, 
    asides/googleplus.html
    ]
```


サイドバーの`Recent Posts`の上に`Profile`で作成した`About Me`が表示される。

![octopress-sidebar-profile](https://i.gyazo.com/3e88876a3442a236f47464741b565551.png)





