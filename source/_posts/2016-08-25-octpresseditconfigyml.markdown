---
layout: post
title: "octopressの日時表示設定"
date: 2016-08-25 20:15:39 +0000
comments: true
categories: ['octopress']
---

## 日時表示設定

投稿記事の日時はデフォルトで`AUG 25TH, 2016 3:00 PM`のような表示になっていが、
[rubyの時間表記表現](http://ruby-doc.org/core-1.9.2/Time.html#method-i-strftim) を使って 好きなように変更可能

### _config.yamlを編集

```ruby
- date_format: "ordinal"
+ date_format: "%Y年%m月%d日"
```
上記の設定で”2016年8月25日”というような表示になる
