---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#28 re:Invent 2020, A100 GPUインスタンス, DockerHub pull制限"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "re:Invent 2020申し込み開始, A100 GPUインスタンスのリリース, DockerHub pull制限を見落としていた件などについて話したよ。<br>小杉の音声が少し割れてしまったよ。"
abstract: "re:Invent 2020申し込み開始, A100 GPUインスタンスのリリース, DockerHub pull制限を見落としていた件などについて話したよ。<br>小杉の音声が少し割れてしまったよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-11-08T16:35:02+09:00
#date_end: 2020-11-06T01:05:02+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-11-06T01:05:02+09:00

authors: []
tags: []

# Is this a featured talk? (true/false)
featured: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

# Optional filename of your slides within your talk's folder or a URL.
url_slides:

url_code:
url_pdf:
url_video:

# Markdown Slides (optional).
#   Associate this talk with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

<iframe src="https://anchor.fm/mukiudo/embed/episodes/reInvent-2020--A100-GPU--DockerHub-pull-em67m8" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Notes

## [AWS re:Invent 2020 申し込み受け付け開始](https://reinvent.awsevents.com/)

> 11 月 30 日 (月) ～ 12 月 18 日 (金)  オンラインで開催！参加無料

* 日本語サイトは[こちら](https://aws.amazon.com/jp/about-aws/events/2020/reinvent/)
* リアルタイムでのライブ配信スケジュールは[こちら](https://reinvent.awsevents.com/keynotes/)
  - 日本との時差+17時間。例えばPSTで11/6 01:00はJSTで11/6 18:00。
  - 最初の基調講演は12/1 8:00AM(PST)開始なので、日本で生放送を見るなら12/1 01:00AM(JST)。
  - 基調講演は全部1:00AM(JST)
* アジアのタイムテーブル（再放送枠）は[こちら](https://reinvent.awsevents.com/agenda/asia-pacific/#agenda)
  - シンガポール時間で記載されてる。
  - 日本との時差+1時間。例えばSGTで10:00はJSTで11:00。
* 日本人による日本語でのセッションもあり（現在予定は10セッション） 
* ライブ配信、再放送枠は日本語字幕なし。  
  - 英語字幕はあるかも...？不明。
* 毎週土曜日に字幕入り（基調講演, リーダーシップセッションのみ）のオンデマンド配信もある。
  - すべてがオンデマンド配信されるかは未定。
* ブレイクアウトセッションが500以上。
  - オンデマンド, 字幕はないかも。
* 期間中の毎週火, 水, 木は日本語に寄るDaily re:Capも開催予定。
* オンライントレーニング企画あり。
* オンラインを補完する目的なのか、[コミュニティ企画](https://reinvent.awsevents.com/communities/)もある
* セッションカタログは11月中旬公開予定。


## [LambdaがAmazon MQのイベントソースマッピングに対応](https://awsapichanges.info/archive/changes/034487-lambda.html)

*  LambdaがAmazon MQのイベントソースマッピングに対応
  - SQSとMQ：機能は同じだが、業界標準のAPIやプロトコルに対応しているのはMQの方（SQSがAWS独自）
* オンプレでActiveMQとかRabbitMQなどのブローカーエンジンを使ったシステムのマイグレーションとかの設計時に選択肢として用意しておくとよいのでは


## [Amazon CloudWatch launches Metrics Explorer](https://aws.amazon.com/jp/about-aws/whats-new/2020/11/amazon-cloudwatch-launches-metrics-explorer/)

参考: [CloudWatchダッシュボードをタグベースで簡単に作成できるMetrics Explorerがリリースされました](https://dev.classmethod.jp/articles/cloudwatch-launches-metrics-explorer/)

* CWのダッシュボードが容易に追加できる
* タグベースでメトリクスを表示できる


## A100 GPUのクラウド提供開始

### [AWSでのA100 GPU提供](https://aws.amazon.com/jp/ec2/instance-types/p4/)

* P4dインスタンスが新登場(GPU系インスタンス、P3の後継)
* 最新Ampere世代のNVIDIA GPU
* 大規模な機械学習, 科学技術計算用途
* 対応サービスはEC2
* バージニア北部とオレゴンのみ
* 96CPU, 1.1TBメモリ, 8TB SSDの化け物インスタンス
* 3400円/時間くらい。

### [GCPでのA100 GPU提供](https://cloud.google.com/blog/products/compute/announcing-google-cloud-a2-vm-family-based-on-nvidia-a100-gpu)

* プライベートアルファで申し込み必要。今年中にGAになる予定。
* GCPではGPUの数などスペックを選べるっぽい。


## [Docker Hub、6カ月使われていないコンテナイメージの削除計画を保留に。従量課金ベースの料金プランを検討へ | Publickey](https://www.publickey1.jp/blog/20/docker_hub6_1.html)

色々紆余曲折あり。

* 無料プランで6ヶ月以上使われていないコンテナイメージを削除する計画は保留。
* 11月からpull回数には制限開始。
  - 匿名ユーザからは100回 / 6時間まで
  - 認証済み無料ユーザは200回 / 6時間まで

ただし、[オープンソースプロジェクトのユーザは無料で制限なしにする](https://www.publickey1.jp/blog/20/docker_hubdocker.html)。（申請が必要）

匿名ユーザはIPベースで回数制限を設けられるので、他人事ではない。  
（会社のグローバルIP, CIツールのIPプール, クラウドサービスのグローバルIPなどが影響）

回避策としては以下。

* docker loginする
  - 無料枠で足りない場合は有料プランを契約
* DockerHub以外のレジストリサービスにpullするイメージを退避

現在自分に適用されている制限を確認するには以下。（参考: [docker公式ドキュメント](https://matsuand.github.io/docs.docker.jp.onthefly/docker-hub/download-rate-limit/)）  

[ワンライナーで確認するGistあげました](https://gist.github.com/kosu9i/efb54c53d6442ce0bfb649c8542d9a8b)

```sh
# 匿名ユーザで確認する場合
$ TOKEN=$(curl "https://auth.docker.io/token?service=registry.docker.io&scope=repository:ratelimitpreview/test:pull" | jq -r .token)

# docker hubユーザで確認する場合
$ TOKEN=$(curl --user 'username:password' "https://auth.docker.io/token?service=registry.docker.io&scope=repository:ratelimitpreview/test:pull" | jq -r .token)
```

の後に

```sh
$ curl -v -H "Authorization: Bearer $TOKEN" https://registry-1.docker.io/v2/ratelimitpreview/test/manifests/latest 2>&1 | grep RateLimit

< RateLimit-Limit: 2500;w=21600
< RateLimit-Remaining: 2483;w=21600
```

上記、自分が試したときは2483回。`w=`は21600秒 = 6時間という意味。


## [AWSがDocker Hubの代替サービスを発表予告。パブリックにコンテナイメージを公開可能で50GBまで無料、AWSからなら何度でもプルし放題に | Publickey](https://www.publickey1.jp/blog/20/awsdocker_hub50gbaws.html)

* 毎月50GBまでpush可能。
* 匿名ユーザでpullする場合は毎月500GBの無料データ帯域幅。
  - Docker HubみたいにIPで制限するのか、など詳細は不明。  
    今後アナウンスがあるとのこと。
* AWSアカウントで認証すると毎月5TBデータ帯域幅まで無料。
  - ECRはプライベートのみ。
* AWS上のワークロードであれば制限なし。
