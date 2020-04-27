---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Hugo + Academic + Netlifyでブログを構築"
subtitle: ""
summary: ""
authors: []
tags: ["Hugo", "Netlify"]
categories: ["Web"]
date: 2020-04-21T00:44:44+09:00
lastmod: 2020-04-21T00:44:44+09:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

# 欲しい物

* ブログ
* podcastの一覧
  + 配信はanchor.fmでやってリンクを埋め込む
* ポートフォリオ（optional）



上記の通りで、かつ静的サイトジェネレータを使ってみたかった。
色々事前に調べた結果、以下の構成が楽そうだったので採用することにした。

* Hugo
  * academicテーマを利用
* Netlify
* 静的ページ生成元のソースコードはGitHubで管理

[ここ](https://marumalog.hatenablog.jp/entry/2018/08/20/222601)を参考にした。



# Hugo


## インストール

Macでのinstall方法。  
[公式のQuick Start](https://gohugo.io/getting-started/quick-start/)参照。

```sh
$ brew install hugo
```

## テーマ

テーマは評判の良い[Academic](https://themes.gohugo.io/academic/)にしてみる。  
基本はポートフォリオ用のテーマ。  
ブログだけじゃなくて、色々コンテンツ置けそうという理由。




# Netlify

## Academicテーマのセットアップ

Netlifyを使うとAcademicのデプロイが超絶楽ちん。  
具体的には、Netlifyのページ上だけでデプロイが完了する。  
[Academic公式も推奨している](https://github.com/gcushen/hugo-academic#install-with-web-browser)ので、このやり方でいく。

1. [NetlifyにAcademicをデプロイするページ](https://app.netlify.com/start/deploy?repository=https://github.com/sourcethemes/academic-kickstart)へ移動して「Connect to GutHub」をクリック。
  GitHubでの認証を承認する。

  {{< figure src="connect_github.png" title="Connect to GitHub" numbered="true" lightbox="true" >}}

2. 「Repository name」にGitHubに登録したいリポジトリ名を入力。  
  ここで入力した名前で新規リポジトリが作成され、[academic-kickstart](https://github.com/sourcethemes/academic-kickstart)がforkされる様子。  
  さらに勝手にNetlifyと連携してくれる。（細かいところが気になるが、先に進む）  
  自分は `portfolio` というリポジトリ名にした。

  {{< figure src="repo_name.png" title="Repository name" numbered="true" lightbox="true" >}}

3. 下記のようになったら、もうAcademicのデフォルト状態でデプロイされている。  
  黒く塗りつぶしている箇所にリンクがあり、そこからアクセスできるはず。

  {{< figure src="overview.png" title="Overview" numbered="true" lightbox="true" >}}



リンクをクリックして、下記が閲覧できればOK。楽すぎる。

{{< figure src="academic_start_page.png" title="Academic Start Page" numbered="true" lightbox="true" >}}


## Academic内のコンテンツを編集

自分のGitHubに追加されたリポジトリ（自分は `portfolio` というリポジトリ名にした）をclone。

```sh
$ git clone https://github.com/[ユーザ名]/portfolio.git
```

試しにAcademicのトップに表示されているAuthorの名前を変えてみる。

`content/authors/admin/_index.md` の中にある  
```
# Display name
title: Nelson Bighetti
```
のところを
```
# Display name
title: Test
```
に変える。

この変更をGitHubのmasterにpushし、しばらく経つとNetlifyに自動で反映される。  
楽すぎる...

{{< figure src="update_author.png" title="Update Author" numbered="true" lightbox="true" >}}


## 独自ドメインの設定

自分はGoogle Domainsで取得していた。  

[ここ](https://qiita.com/NaokiIshimura/items/64e060ccc244e38d0c15)を参考にして独自ドメインをNetlifyに登録。

Google DomainsだとALIAS, ANAMEレコードが使えないので、Netlify側でDNS設定をした。  
[ここ](https://www.ravness.com/2018/07/netlifydomain/)参照。  
また、NetlifyのDNSを使うとCDNの恩恵を得られるとか。

Google Domainsで以下を実施。

1. DNSSECを無効化。
2. 「ネームサーバー」で「カスタムネームサーバーを使用する」に変更し、  
  Netlifyの「Check DNS configuration」を押すと出てくるDNSサーバを追加。  
```
dns1.p02.nsone.net
dns2.p02.nsone.net
dns3.p02.nsone.net
dns4.p02.nsone.net
```
3. ドメインが浸透し、HTTPS化まで完了したことがNetlify画面から確認できたら  
  独自ドメインでアクセスできるようになるはず。（自分の場合は大体10〜20分でできた）


