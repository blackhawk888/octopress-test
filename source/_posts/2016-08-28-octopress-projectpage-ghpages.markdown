---
layout: post
title: "OctopressをGitHubのProject Pageで作成"
date: 2016-08-28 14:56:55 +0000
comments: true
categories: [octopress]
---

### Project Page (gh-pages) にデプロイする場合

Github Pagesでサイトを公開する場合は`[username].github.io`というリポジトリを作成し、
デプロイすることで`https://[username].github.io`でアクセスすることができるが、任意のリポジトリを作成し、
Project Page(gh-pages)にデプロイすることもできる。

<!--more -->

ユーザのウェブページを公開するユーザサイト（User site）[username].github.io でアクセスとの違いは、
URlが`https://[username].github.io/[repository_name/]`になることと
`[username].github.io` リポジトリのときとは異なり、`_deploy/` ディレクトリは `gh-pages` ブランチに設定される。  

Octopressのインストールは以前書いたとおり`git clone`するだけ。  
あとは必要な`gem`を`bundle --path vendor/bunde`、`bundel exec rake install`でインストール。    

事前にGithubでリポジトリを作成しておく。

```
$ rake setup_github_pages
Repository url: git@github.com:[username]/[username].github.io.git
```

上記によって、以下のことが行われる。

- `git@github.com:[username]/[username].github.io.git` が `origin remote` として追加される
- `_deploy/` ディレクトリがリポジトリの `gh-pages` ブランチに設定される
- 親ディレクトリは `source` ブランチになる

ソースコードを管理するため、remote のリポジトリURLを設定

```
$ git remote add origin git@github.com:[username]/[repository_name].git 
$ git config branch.master.remote origin
```
