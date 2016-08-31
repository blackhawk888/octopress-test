---
layout: post
title: "Octopress-サイドバーにGravatar追加"
date: 2016-08-30 16:00:38 +0000
comments: true
categories: 
---

サイドバーにProfileを表示させるようにしたのでついでにGravatarも表示させてみる。

[Gravatarに開発者向け資料](https://ja.gravatar.com/site/implement/)があったので
見てみるとJSONでプロフィール情報を返すAPIを提供しているようなのでそれ使って情報を持ってきて、
画面に反映させなきゃいけないと思っていてGithubを眺めていたらOctopressでGravatarを表示させる
プラグインがあったのでそれを使用してみることにした。  

<!--more-->

[joet3ch/gravatar-octopress](https://github.com/joet3ch/gravatar-octopress)  
簡単に説明するとGravatarの画像をimgタグでひっぱってこれるようになるので、
それを参考にしつつ、souce/_include/custom/asides/about.html を編集するという流れ。

以下手順


### インストール

```
$ git clone https://github.com/joet3ch/gravatar-octopress.git
```

### `gravatar.html`を`_includes/custom/asides`にコピー

```
$ cd gravatar-octopress
$ cp gravatar.html [directory_name]/_includes/custom/asides
```

### _config.ymlに追記


{% codeblock lang:yml _config.yml %}
 + # Gravatar  
 + gravatar_email: youraddress@example.com

{% endcodeblock %}


### _config.ymlのdefault\_asides変数にgravatar.htmlを追加

```
# list each of the sidebar modules you want to include, in the order you want them to appear.
# To add custom asides, create files in /source/_includes/custom/asides/ and add them to the list like 'custom/asides/custom_aside_name.html'
# default_asides: [asides/recent_posts.html, asides/github.html, asides/delicious.html, asides/pinboard.html, asides/googleplus.html]
default_asides: [
  + custom/asides/about.html,
    asides/recent_posts.html,
    custom/asides/category_list.html,
    custom/asides/tag_cloud.html,
    asides/github.html, 
    asides/delicious.html,
    asides/pinboard.html, 
    asides/googleplus.html
    ]
```

**Gravatar導入前**

![Gravatar導入前](https://i.gyazo.com/26245cde8185fad41104a09e79e3a8cc.png)

**Gravatar導入後**

![Gravatar導入後](https://i.gyazo.com/0211d5f0a5057fcf087250a9248d0b6c.png)

Gravatarの画像がProfileの上に来ているので`config.yml`の`asides`に設定するのではなく
`souce/_include/custom/asides/about.html `を編集するように変更。

### _config.ymlの編集

```
# list each of the sidebar modules you want to include, in the order you want them to appear.
# To add custom asides, create files in /source/_includes/custom/asides/ and add them to the list like 'custom/asides/custom_aside_name.html'
# default_asides: [asides/recent_posts.html, asides/github.html, asides/delicious.html, asides/pinboard.html, asides/googleplus.html]
default_asides: [
  - custom/asides/about.html,
    asides/recent_posts.html,
    custom/asides/category_list.html,
    custom/asides/tag_cloud.html,
    asides/github.html, 
    asides/delicious.html,
    asides/pinboard.html, 
    asides/googleplus.html
    ]
```

### souce/_include/custom/asides/about.html編集

`about.html`を以下のように変更

```
<section>
  <h1>Profile</h1>
  {% if site.gravatar_email %}
    <img src="{% gravatar_image %}" alt="Gravatar of {{site.author}}" title="Gravatar of {{ site.author }}" align="left" style="margin-right:10px;" />
  {% endif %}
  Hoge Hoge
  <br clear="left">
</section>

```

**about.html編集後**

![about.html編集後](https://i.gyazo.com/8459f225d4670991f1b76d844b772e6f.png)

Gravatarの画像イメージサイズは`gravatar.html`を編集することで可能

```
<img src="{% gravatar_image 200 %}" alt="Gravatar of {{ site.author}} " title="Gravatar of {{ site.author }}" />
```