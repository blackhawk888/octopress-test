---
layout: post
title: "Octopressにタグクラウドとカテゴリーリストを追加する"
date: 2016-08-26 23:17:49 +0000
comments: true
categories: ['octopress']
---

### タグリストをサイバーに表示させる。

Octopressのデフォルトのサイドメニューは`Recent Posts`のみの表示  

![Recent posts](https://i.gyazo.com/cf857d8c62f5f7564ddbd25c9c754f90.png)

<!--more-->

記事を新規投稿するときにYAML FRONT MATTERで`categories`を設定しているので、サイドメニューにCategoriesを表示させる。  

Octopress向けに公開されているプラグインを使ってサイドメニューにカテゴリーリストとタグクラウドを実装

#### tokkonopapa/octopress-tagcloud プラグイン
[https://github.com/tokkonopapa/octopress-tagcloud](https://github.com/tokkonopapa/octopress-tagcloud)  

tokkonopapa/octopress-tagcloudのソースコードをcloneしてファイルを配布する。

```
$ git clone https://github.com/tokkonopapa/octopress-tagcloud.git
$ cp -p octopress-tagcloud/plugins/tag_cloud.rb plugins/
$ cp -p octopress-tagcloud/source/_includes/custom/asides/* source/_includes/custom/asides/
```
```
.
├─ plugins/
│  └── tag_cloud.rb
└─ source/
   └─ _includes/
      └─ custom/
         └─ asides/
            ├─ category_list.html
            └─ tag_cloud.html
```

`_config.yml`に`tokkonopapa/octopress-tagcloud` プラグインで生成する静的ファイルを
サイドメニューのコンテンツとして使用するための設定を記述  

`_config.yml`に`default_asides:`から始まる行があるが、サイドメニューに表示するHTMLファイルを配列で記述する。  

```
default_asides: [
    asides/recent_posts.html,
  + custom/asides/about.html,
  + custom/asides/tag_cloud.html
]
```

![octopress-tagcloud](https://i.gyazo.com/ef6d723b6ff2a154a49890d11c3c006d.png)