---
layout: post
title: "Octopress 続きを読む(Moreタグ)の設定"
date: 2016-08-26 17:16:35 +0000
comments: true
categories: ['octopress']
---

### `<!--more-->`タグの追加
ブログを表示すると公開済の記事が時系列順にタイトルと本文が全て表示されるので、
ブログを表示した時に本文を全て表示するのではなく一部だけを表示しておき、
全ての本文を読むには「続きを読む >>」と書かれたリンクをクリックした時に
表示させるよう`<!--more-->`タグを設置する。

<!--more-->

 `bundel exec rake  new_post[title]`で作成後、`source/_posts/`に`source/_posts/YYYY-MM-DDD-title.markdown`ファイルができ
 記事の途中に以下を追記する。
 
 ```ruby
 <!-- more -->
 ```
 ただし上記の追記だけでは表示が`”Read on →“`になってるので`_config.yml`の`excerpt_link`を変更する。

```ruby
- excerpt_link: "Read on &rarr;"  # "Continue reading" link text at the bottom of excerpted articles
+ excerpt_link: "続きを読む &raquo;"  # "Continue reading" link text at the bottom of excerpted articles
```

