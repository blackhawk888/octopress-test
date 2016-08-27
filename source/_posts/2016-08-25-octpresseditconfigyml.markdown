---
layout: post
title: "octopressの日時表示設定"
date: 2016-08-25 20:15:39 +0000
comments: true
categories: ['octopress']
---

## 日時表示設定

投稿記事の日時はデフォルトで`AUG 25TH, 2016 3:00 PM`のような表示になっているが、
[rubyの時間表記表現](http://ruby-doc.org/core-1.9.2/Time.html#method-i-strftim) を使って 好きなように変更可能

<!-- more -->

### _config.yamlを編集

```ruby
- date_format: "ordinal"
+ date_format: "%Y年%m月%d日" # e.g. 2016年08月25日
```
上記の設定で`2016年08月25日 8:15 PM`というような表示になる。  

時間が12時間表記で気に入らなかったので24時間表記表示にするため`_config.ymlを編集`

```ruby
  date_format: "%Y年%m月%d日" # e.g. 2016年08月25日
+ time_format: "%H:%M:%S"     # 24 hour time
```
表示が`2016年08月25日 20:15:39`というような表示になる。

