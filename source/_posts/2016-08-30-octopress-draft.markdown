---
layout: post
title: "Octopress-下書きをdeployしないようにする"
date: 2016-08-31 15:59:56 +0000
comments: true
published: true
categories: [octopress]
---

下書きしていて完成してない状態でも、他の部分だけを公開したい時があると思う。  
その時はYAMLブロックに`published:false`加えるとそのファイルは`bundle exec rake generate`を実行すると
下書きは生成されないが、`bundle exec rake preview`をした時は表示される。


{% codeblock lang:ruby exsample.markdown %}
---
layout: post
title: "exsample"
date: 2016-08-31 08:42:56 +0000
comments: true
categories: [exsample]
published: false
---

### 下書き中
{% endcodeblock %}

<!--more-->

`bundle exec gen_deploy`は`generate`が失敗した場合でも`deploy`を実行するので 
`generate`失敗な形で投稿されてしまうことがある。
また下にある`published`のステートメントは最後の方に判断されるので、 後で投稿しようと思っている下書きがあって、
今書いているものを投稿しようと`bundle exec gen_deploy`すると、 中途半端な今の記事と後で投稿する予定だった
下書きの方が送られてしまうことがあるので ちょっとした変更以外は一旦`bundele exec generate`した方がよいかもしれない。