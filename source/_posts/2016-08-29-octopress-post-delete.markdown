---
layout: post
title: "Octopress 記事の削除"
date: 2016-08-29 20:21:05 +0000
comments: true
categories: [octopress]
---

該当するmarkdownファイルを削除しデプロイするだけ。  
ディレクトリの場所: `source/_posts/`

```
$ rm source/_posts/post-title.markdown
$ rake gen_deploy
```