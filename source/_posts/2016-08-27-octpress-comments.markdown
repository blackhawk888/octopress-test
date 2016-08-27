---
layout: post
title: "Octopressにコメントを追加"
date: 2016-08-27 10:41:24 +0000
comments: true
categories: ['octopress']
---

### コメント欄を追加

このブログは個人備忘録として書いているので特にコメント欄は必要ないとは思うが、
今後導入するかどうかわからないので実際に導入して確認したので忘れないうちに書いておく。  

コメントはデフォルトで[Disqus](https://disqus.com/)というサービスを利用できる。  
基本的にはコメントをブログと切り離して管理しブログパーツでコメント欄を提供してくれるサービス。  
`_config.yml`にコメントの`id`を設定することで使用可能。  
手順は以下のとおり

<!--more-->

- [Disqus](https://disqus.com/)にログイン
- Disqus上にてコメントサービスを使うサイトを登録
- 登録が完了すると設定ページが表示されるので、ここで設定をしつつ、ページ中段に表示されている`Shortname`の文字列を確認
- shortnameを`_config.yml`に入力
- deploy

DISQUS導入は_config.ymlファイルにDISQUSで取得した`Shortname`を記載するのみで完了

`_config.yml` の`disqus_short_name`に自分のサイトの`Shortname`を指定

```ruby
# Disqus Comments
disqus_short_name: sitesshortname
disqus_show_comment_count: false
```

上記を設定すると`source/_include/disqus.html`によって`disqus`用のコードを生成してくれる。

![Disqus Comments](https://i.gyazo.com/82f9217e4935ccc5f3dcb1599384a682.png)

`disqus_show_comment_count`は任意でコメント欄のオン/オフは投稿記事単位で設定可能
`disqus_show_comment_count` はDISQUSコメント欄を導入するページのヘッダにコメント欄へのリンクを表示させるかどうかを指定する項目。

**disqus_show_comment_count: trueのとき**

![disqus_show_comment_count: ture](https://i.gyazo.com/7232f4714811db0bcea23e041556a481.png)


**disqus_show_comment_count: falseのとき**

![disqus_show_comment_count: false](https://i.gyazo.com/29fc1be984bb3130d74343aa94c4943b.png)

`shortname`を後で確認したくなった場合は、Disqusで登録したサイトを選択し、右上にある`Setting`に移動すると表示される。

