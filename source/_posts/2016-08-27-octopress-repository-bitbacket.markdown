---
layout: post
title: "OctopressでsourceをBitbucket管理"
date: 2016-08-27 15:47:33 +0000
comments: true
categories: [octopress, bitbacket]
---

###ソース情報はBitbucketで管理

このブログはOctopressでGithubでホスティングしているが、ソースコードもGithubにpushしている。  
GitHubはいいサービスだと思うのですが、ソースコードの共有が前提となっていて、
無料プランでは非公開リポジトリを作ることができない。  

<!--more-->

BitbucketはGitHubと同じ、バージョン管理ツールのリポジトリを預かってくれるホスティングサービス。  
5ユーザーまでであれば、非公開レポジトリの数は無制限となっており、公開リポジトリがひとつもなくても構いません。  
Bitbacketのアカウントも取得しているのでソースコードをBitbacketで管理する方法も忘れないように書いておこうと思う。

### Bitbucketでのリポジトリ作成・設定

- BitBucketにログインして、リポジトリ作成
- [Repository name] - [GithubのRipository name]
- [アクセスレベル] - [これは非公開リポジトリです]にチェック
- [リポジトリタイプ] - [Git]

### リモートととして登録

```
$ git remote add bitbucket git@bitbucket.org:[username]/[username].github.io.git
$ git push  bitbucket source
```

上記の設定で現在リモートとして `origin`、`octopress`、`bitbucket` の3つが登録されることとなる。  

```
% git remote -v
bitbucket       git@bitbucket.org:[username]/[username].github.io.git (fetch)
bitbucket       git@bitbucket.org:wivern888/[username].github.io.git (push)
octopress       git://github.com/imathis/octopress.git (fetch)
octopress       git://github.com/imathis/octopress.git (push)
origin          git@github.com:[username]/[username].github.io.git (fetch)
origin          git@github.com:[username]/[username].github.io.git (push)
```

記事の投稿をデプロイする場合は`bundle exec rake deploy`でバックアップは`git push bitbacket source`でBitbacketできるようになる。








