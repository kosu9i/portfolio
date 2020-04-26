---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Remote Desktop on GCE"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-27T01:46:07+09:00
lastmod: 2020-04-27T01:46:07+09:00
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

# GCEでリモートデスクトップしてみた

ちょっとハイスペックなUbuntu Desktopが必要になった。  
ローカルのマシンだとめぼしいモノがなかったので、GCEでリモートデスクトップを試みた。

GCEを選択した理由は以下。

* AWSの無料枠だとEC2でt2.micro 750時間/月で、選択肢がなかった。
* WorkspacesだとUbuntuが選べない
* GCPの無料枠は$300クレジット/年があり、1月の上限額は設けられておらず使いやすい。
    + n1-standard-4は4CPU, 15GBメモリで月に$150（1時間あたり$0.2）くらい。   
      使うときだけ起動していれば、無料枠内で十分いけるはず。

# GCPにWorkspacesみたいのないのか？

結論から言うと、ない。  
近いソリューションとして、[Chrome Remote Desktop](https://cloud.google.com/solutions/chrome-desktop-remote-on-compute-engine?hl=ja)を利用する手がある。  

* が、Ubuntu 18.04ではこれがうまくいかなかった。
* 16.04では一応いけた。
* 楽なことは楽だが、結局細かい調整しようとすると設定ファイルやミドルウェアのインストール、セットアップをしなければならなくてめんどかった。

# 結局...

RDPサーバをGCE上のUbuntuにセットアップして使うことにした。  

* RDP
    + Microsoftが開発したプロトコル
    + Windowsには標準でクライアントがあり、Mac, Linuxでもクライアントアプリケーションは提供されている。
    + 画面を転送しないため、基本的に低遅延
* VNC
    + クロスプラットフォーム
    + プロトコル的には暗号化されない。SSHやVPNでトンネルしてやる必要がある。
    * 画面を転送する

# GCEの話を少し

* 無料枠が使いやすい。ちょっと制限はあるけど。
    + CPU 8個まで
    + VMインスタンスにGPUはアタッチできない。（AI Platformでは無料枠でも使えるので便利）
* ssh鍵の転送が楽
    + gcloudコマンドで勝手に管理してくれる
    + Googleアカウントで管理できる
* ブラウザベースでのssh接続も可能
* 最初からパブリックIPが振られている

# 付随してGCPについて少し

* 前述の通り、無料枠が使いやすい。
* ずっと無料枠、っていうのもある。（下記、1月あたり）
    + GCE f1-micro（1CPU メモリ0.6GB HDD16GB）
    + GCS 5GB（米国リージョンのみ）
    + Cloud Functions 200万回呼び出し
    + BigQuery 1TB
* Cloud Shellってのが結構便利
    + 無料
    + 5GBの永続ストレージ
* 無料枠$300を超えても、自動的には課金されない。アカウントを有料版にアップデートする必要あり。
    + 有料版アカウントにアップデート後、↑の「ずっと無料枠」は上限を超えると自動的に課金される。






