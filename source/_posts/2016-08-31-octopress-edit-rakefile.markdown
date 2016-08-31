---
layout: post
title: "Octopress-Rakefile編集"
date: 2016-08-31 19:06:16 +0000
comments: true
categories: [octopress]

---

新規作成時`bundle exec rake new_post[title]`に前回書いた`published`や`<--more-->`タグが初期値として
入ってくれたらよいと思うので`Rakefile`を修正する。
115行目あたりにかいてある。

{% codeblock lang:ruby Rakefile %}
post.puts "---"
post.puts "layout: post"
post.puts "title: \"#{title.gsub(/&/,'&amp;')}\""
post.puts "date: #{Time.now.strftime('%Y-%m-%d %H:%M:%S %z')}"
+ post.puts "author: [author]"
post.puts "comments: true"
+ post.puts "published: true
post.puts "categories: "
post.puts "---"
+ post.puts ""
+ post.puts "＜!--more--＞"
{% endcodeblock %}

<!--more-->

`published`の他に、`author`の項目があるのでそれも設定。
これで`bunde exec rake new_post[title]`を実行するとテンプレートとしてデフォルト
`published: true`と`author: [author]`と記事に頭で`<!—more—>`が初期値として入るようになるので
必要に併せて下書き中でdeployしたくなかったら`published: false`に変更し、`<!--more-->`タグの
位置も変更すればよい。