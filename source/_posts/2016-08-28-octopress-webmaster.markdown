---
layout: post
title: "Octopress-Googleウェブマスターツール登録"
date: 2016-08-28 20:47:11 +0000
comments: true
categories: [octopress]
---

### Googleウェブマスターツールとは

Googleウェブマスターツールは、Googleが公式で提供するウェブ担当者・管理者のためのツール

Googleウェブマスターツールに登録することで、

- 自分のサイトをGoogleの検索エンジンに早く見つけてもらえる
- どんなキーワードで表示されているかが分かる
- そのページがよく検索されているのかがわかる
- サイトの集客をアップさせたり、SEOにも役立つ


<!--more-->

手順は以下のとおり

- [Googleアカウント](https://www.google.com/webmasters/tools/home?hl=ja)でログイン
- サイトのドメインを入力
- [確認方法]タブのHTML ファイルをアップロードにチェック
- 確認ファイル(googleXXXXXXXXXXX.html)が作成されるので`_deploy` ディレクトリにコピーし、リモートにプッシュ

上記の手順で確認用URLが表示されるのでアップロードが正しく行われたことの確認を行い、問題なければ確認ボタンを押すことで所有権を紐付ける。  
ただしこの方法では、次回記事をデプロイした時に確認用ファイルが消されてしまうので、確認用ファイルをリモートにプッシュする方法ではなく
メタ タグをサイトのホームページに追加する方法にする

以下手順

- [確認方法]タブのHTMLタグにチェック
- meta タグが作成されるので、コピーする。
- source/_includes/head.html にメタタグを貼り付ける。

```
<!DOCTYPE html>
<!--[if IEMobile 7 ]><html class="no-js iem7"><![endif]-->
<!--[if lt IE 9]><html class="no-js lte-ie8"><![endif]-->
<!--[if (gt IE 8)|(gt IEMobile 7)|!(IEMobile)|!(IE)]><!--><html class="no-js" lang="en"><!--<![endif]-->
<head>
  <meta charset="utf-8">
+ <meta name="google-site-verification" content="XXXXXXXXXXXX_XXXXXXXXXXXXXXXXXXXX" />
  <title>{% if page.title %}{% if site.titlecase %}{{ page.title | titlecase }}{% else %}{{ page.title }}{% endif %} - {% endif %}{{ site.title }}</title>
  <meta name="author" content="{{ site.author }}">

  {% capture description %}{% if page.description %}{{ page.description }}{% else %}{{ content | raw_content }}{% endif %}{% endcapture %}
  <meta name="description" content="{{ description | strip_html | condense_spaces | truncate:150 }}">
  {% if page.keywords %}<meta name="keywords" content="{{ page.keywords }}">{% endif %}
```

- デプロイ
- Googleウェブマスターツールのサイトの画面で[確認]をクリックし所有権を紐付ける。




