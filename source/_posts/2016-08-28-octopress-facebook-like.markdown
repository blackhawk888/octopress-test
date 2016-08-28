---
layout: post
title: "octopress Facebook Like ボタン日本語化"
date: 2016-08-28 15:43:39 +0000
comments: true
categories: [octopress]
---

### FacebookのLikeボタン日本語化

以前外部サービス連携でFacebookボタンを追加したが[Like]、[share]と英語表記になっているので
日本語の[いいね]、[シェア]に変更

<!--more-->

### `source/_includes/facebook_like.html`の編集

```
- js.src = "//connect.facebook.net/en_US/all.js#appId=212934732101925&xfbml=1";
+ js.src = "//connect.facebook.net/ja_JP/all.js#appId=212934732101925&xfbml=1";
```
`en_US` を `ja_JP` に変更


**変更前**
![Facebook Like](https://i.gyazo.com/d1bf65d5bc104cbe2c271fd9dca76381.png)


**変更後**
![Facebook いいね](https://i.gyazo.com/209f66e232354b53fefa332f6e394dc8.png)

