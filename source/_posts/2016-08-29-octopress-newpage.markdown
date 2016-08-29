---
layout: post
title: "Octopress-新規ページ作成"
date: 2016-08-29 21:40:50 +0000
comments: true
categories: [octopress]
---

新規投稿`bundle exec rake new_post[title]`ではなく新規ページを作成する。

### 新規ページ作成

```
$ rake new_page[page_name]
Creating new page: source/[page_name]/index.markdown
```

<!--more-->

### 新規ページ編集

ナビゲーションバーから新規ページへのリンクを追加  
`source/_includes/custom/navigation.html`を編集

```
<ul class="main">
    <li><a href="{{ root_url }}/">Blog</a></li>
    <li><a href="{{ root_url }}/blog/archives">Archives</a></li>
    + <li><a href="{{ root_url }}/about">[new_page]</a></li>
</ul>
```

新規ページを編集  
`source/[new_page]/index.markdown`を編集

```
---
layout: page
title: "[new_page]"
date: 2016-08-29 21:30
comments: false
sharing: true
footer: true
---

###本文
hoge hoge

```

ナビゲーションバーに新しく作成したページのタイトルが表示されリンクをクリックいて
ページが遷移することを確認する。


