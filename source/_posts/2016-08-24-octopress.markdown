---
layout: post
title: "OctopressとGithub Pagesを使ったブログの作成"
date: 2016-08-25 15:00:37 +0000
comments: true
categories: ['octopress']
---

## Octopressの特徴

-  Octopress は jekyll を使って作るブログ構築用フレームワーク
-  Markdown記法で書ける
-  静的ファイル →　軽い

今回はブログ記事そのものは [GitHub Pages](https://pages.github.com/)にホスティングする。

## GitHub Pagesの特徴

- GitHubが提供するホスティングサービス
- ウェブページをインターネット上に公開することができる。
- プロジェクトのウェブページをGit/GitHubのリポジトリを用いて、公開することが可能(プロジェクトの場合はプロジェクトリポジトリの gh-pages ブランチで行う)
- HTML,CSS, JavaScriptを配置することが出来るので、ブログだけではなくGitHub Pages だけで静的なページを作成することができる。

今回はプロジェクトのウェブページを公開するプロジェクトサイト（Project site）ではなくユーザのウェブページを公開するユーザサイト（User site）[username].github.io
でアクセスできるようにする。


## Octopressのインストール

octopress を GitHub からクローンしてくる

```bash
$ git clone git://github.com/imathis/octopress.git octopress

Cloning into 'octopress'...
remote: Counting objects: 5685, done.
remote: Compressing objects: 100% (2262/2262), done.
remote: Total 5685 (delta 3247), reused 5225 (delta 2933)
Receiving objects: 100% (5685/5685), 1.21 MiB | 435 KiB/s, done.
Resolving deltas: 100% (3247/3247), done.

$ cd octopuress
```

必要な gem をインストールする

```ruby
bundle --path vendor/bundle
```

Octopressをセットアップ(`bundel exec rake install`)する前にoctpressディレクトリのRakefileを修正する。
通常の場合そのまま`bundle ecec rake install`して問題ないがCloud9を使用いているためその後の`bundle exec rake preview`を
実行してプレビューが見れない為の対処

```ruby
themes_dir      = ".themes"   # directory for blog files
 new_post_ext    = "markdown"  # default new post file extension when using the new_post task
 new_page_ext    = "markdown"  # default new page file extension when using the new_page task
-server_port     = "4000"      # port for preview server eg. localhost:4000
+server_host     = ENV['IP'] ||= '0.0.0.0'     # server bind address for preview server
+server_port     = ENV['PORT'] ||= "4000"      # port for preview server eg. localhost:4000


 desc "Initial setup for Octopress: copies the default theme into the path of Jekyll's generator. Rake install defaults to rake install[classic] to install a different theme run rake install[some_theme_name]"
@@ -78,7 +79,7 @@ task :preview do
   system "compass compile --css-dir #{source_dir}/stylesheets" unless File.exist?("#{source_dir}/stylesheets/screen.css")
   jekyllPid = Process.spawn({"OCTOPRESS_ENV"=>"preview"}, "jekyll --auto")
   compassPid = Process.spawn("compass watch")
-  rackupPid = Process.spawn("rackup --port #{server_port}")
+  rackupPid = Process.spawn("rackup --host #{server_host} --port #{server_port}")

   trap("INT") {
     [jekyllPid, compassPid, rackupPid].each { |pid| Process.kill(9, pid) rescue Errno::ESRCH }
```

Octopressをセットアップ

```ruby
$ bundle exec rake install
```

プレビューする  
`http://localhost:4000/` にアクセスすると、ブログのプレビューを見ることが出来る。  
今回はCloud9をしようしているので`https://workspace_name-account_name.c9users.io`でアクセする

```ruby
$ bundle exec rake preview
```
[![https://gyazo.com/bdc0552c1f616a24f83ba55e74b21f52](https://i.gyazo.com/bdc0552c1f616a24f83ba55e74b21f52.png)](https://gyazo.com/bdc0552c1f616a24f83ba55e74b21f52)


## GitHubにリポジトリを作成

[username].github.io
という名前でリポジトリを作る。


## Octopress の初期設定

`bundle exec rake setup_github_pages` タスクを実行し GitHub Pages にデプロイするファイルを生成する。  
この時、[username].github.io のように GitHub Pages のリポジトリを git か https プロトコルを指定する  

```ruby
% bundle exec rake setup_github_pages

Enter the read/write url for your repository
(For example, 'git@github.com:[username]/[username].github.io.git)
           or 'https://github.com/[username]/[username].github.io')
Repository url: git@github.com:srym/srym.github.io.git
Added remote git@github.com:srym/srym.github.io.git as origin
Set origin as default remote
Master branch renamed to 'source' for committing your blog source files
rm -rf _deploy
mkdir _deploy
cd _deploy
Initialized empty Git repository in /Users/shiroyama/playGround/octopress/_deploy/.git/
[master (root-commit) dacfaa2] Octopress init
 1 file changed, 1 insertion(+)
 create mode 100644 index.html
cd -

---
## Now you can deploy to git@github.com:srym/srym.github.io.git with `rake deploy` ##
```

これによって、以下のことが行われる。

- `git@github.com:[username]/[username].github.io.git` が `origin` `remote` として追加される
- `_deploy/` ディレクトリがリポジトリの `master` ブランチに設定される
- 親ディレクトリは `source` というブランチになる

```ruby
% git remote -v
octopress       git://github.com/imathis/octopress.git (fetch)
octopress       git://github.com/imathis/octopress.git (push)
origin          git@github.com:[username]/[username].github.io.git (fetch)
origin          git@github.com:[username]/[username].github.io.git (push)
```

###  _config.yml を編集

_config.ymlファイルにてブログのタイトル、サブタイトル、筆者を設定する。

```ruby
# _config.yml

url: http://[username].github.io
title: ブログのタイトル
subtitle: ブログのサブタイトル
author: 筆者
simple_search: http://google.com/search
description:
```

## 記事の投稿

### 記事を書く

Rake タスクで記事のひな形が生成される。
new_postの後には記事のタイトルを指定。英数字のみ使用可

```ruby
% bundle exec rake new_post[title]

mkdir -p source/_posts
Creating new post: source/_posts/YYYY-MM-DD-title.markdown
```

`source/_posts/YYYY-MM-DDD-title.markdown`というファイルが生成されるので内容をマークダウンで記述する。
またファイル上部にはブログのメタ情報がYAML FRONT MATTERで記述されているので適宜編集する。

```
source/
└── _post/
    └── YYYY-MM-DD-post-title.markdown
```


```yaml
---
layout: post
title: "'記事のタイトル'"
date: 2016-08-25 00:00:00 +0900
comments: true
categories:
---
ここ以下に内容をマークダウンで書く
```

ここで、title を日本語にすれば良い

ブログのカテゴリ(categories)は以下のように色々な方法で指定できる。

```yaml
# One category
categories: octopress

# Multiple categories example 1
categories: [octopress, jekyll,]

# Multiple categories example 2
categories:
- octopress
- jekyll
```

## Github Pagesにデプロイする

### ページの生成

```ruby
$ bundle exec rake generate

## Generating Site with Jekyll
    write source/stylesheets/screen.css
Configuration file: /home/ubuntu/workspace/octopress/_config.yml
            Source: source
       Destination: public
      Generating... 
                    done.
 Auto-regeneration: disabled. Use --watch to enable.

```

### Github Pagesにデプロイ
```
$ bundle exec rake deploy

## Deploying branch to Github Pages 
## Pulling any updates from Github Pages 
cd _deploy
There is no tracking information for the current branch.
Please specify which branch you want to merge with.
See git-pull(1) for details.

~略~

## Pushing generated _deploy website
Username for 'https://github.com': Githubのユーザアカウントを入力
Password for 'https://wivern888#gmail.com@github.com': パスワードを入力

Counting objects: 24, done.
Delta compression using up to 8 threads.
Compressing objects: 100% (17/17), done.
Writing objects: 100% (24/24), 9.98 KiB | 0 bytes/s, done.
Total 24 (delta 11), reused 0 (delta 0)
remote: Resolving deltas: 100% (11/11), completed with 2 local objects.
To https://github.com/blackhawk888/blackhawk888.github.io.git
   b6205ae..f7112f2  master -> master

## Github Pages deploy complete
cd -

```
 http://[username].github.ioにアクセスし作成したブログの記事が表示されるのを確認する。
 
デプロイ時には、下記コマンドを実行するが、これによって、`_deploy/` 以下にサイトのコンテンツ一式がビルドされ、その内容が GitHub に `push` されます。
http://[username].github.io/ にアクセスすると、ローカルまたはCloud9でpreview した画面と同じ内容が表示されるようになる。

```
$ bundle exec rake generate
$ bundle exec rake deploy
```

また上記コマンドを別々に実行しなくても以下のコマンドでビルド及びデプロイを同時に行うことができる。

```
$ bundle exec rake gen_deploy
```

最後に、ソースコードを管理するために、`source` ブランチも `push` しておく

```
$ git add .
$ git commit -m 'message'
$ git push origin source
```


