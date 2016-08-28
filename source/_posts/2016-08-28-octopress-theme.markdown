---
layout: post
title: "octopress-theme変更"
date: 2016-08-28 19:09:08 +0000
comments: true
categories: [octopress]
---

### Octopressのテーマを変更

今回casperというテーマに変更してみる。
基本Githubにある`README.md`の手順どおりに進めればよい。

### Installing

```
$ cd <octopress directory>
$ git clone https://github.com/jkrmr/casper .themes/casper
$ rake install['casper']
$ rake generate
```

<!--more-->

### Updating

```
$ cd <octopress directory>/.themes/casper
$ git pull
$ rake install['casper']
# regenerate, make changes, etc...
```

**変更前**
![octopress default](https://i.gyazo.com/88ee966373339447f99a2e68651eef5a.png)

**変更後(casper)**
![octopress casper](https://i.gyazo.com/df4e94a0feb5a90f467e7c80c925bab2.png)

**変更後(octostrap3)**
![octopress octostrap3](https://i.gyazo.com/c2f349654d830dde84fd2e1780df8326.png)