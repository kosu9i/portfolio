---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#30 re:Invent 2020セッションカタログ, AWS障害, AWSアップデート情報, etc"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "AWSのアップデート情報などを中心にざっくばらんに話したよ。"
abstract: "AWSのアップデート情報などを中心にざっくばらんに話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-11-27T22:05:09+09:00
#date_end: 2020-11-26T23:00:09+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-11-26T23:00:09+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/reInvent-2020--AWS--AWS--etc-en1p11" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Notes

## [re:Invent セッションカタログ公開](https://reinvent.awsevents.com/)

もうすぐ！（NOV. 30 – DEC. 18, 2020）

* セッションカタログが公開中
* ログインするとセッションを検索できるようになる
* Japaneseで検索することも可能
* ただ英語だけを表示することができず、[Bookmarkletの形でjavascriptを公開](https://gist.github.com/mikkotikkanen/ee3bfd4e2f36ce86f9a954991c5fa3b6)してくれている人がいる。  
  参考: [AWS re:Invent 2020のセッションカタログで『英語』セッションのみを絞込検索する #reinvent](https://dev.classmethod.jp/articles/aws-reinvent-2020-hacks-search-only-english-sessions/)


## [AWSで大規模な障害が発生中、多数のサービスがあおりを受ける事態に | Gigazine](https://gigazine.net/news/20201126-amazon-web-services-outage/)

* US-EAST-1（バージニア北部）で障害発生。
* 割と大規模で全復旧まで十数時間かかった様子。

> [RESOLVED] Increased Error Rates in US-EAST-1
4:00 AM PST: We have restored all traffic to Kinesis Data Streams via all endpoints, and have resolved the error rates invoking CloudWatch APIs. All services are now operating normally. We have identified the root cause of the Kinesis Data Streams event, and have completed immediate actions to prevent recurrence.

とあった。たしかに↑のGigazineの影響を受けた企業のTweetをみるとIoT絡みが多い感じ。
`Kinesis Data Streams API` が原因のようだが、US-EAST-1ではいろんなAWSサービスが止まった。  
アジアリージョンとかではCloudFrontのみ影響があったらしい。

GCPはCloud Nextの前はよく落ちるという都市伝説があるが、re:Invent関係あるのか...？信じるか信じないかは(ry


## [AWS Step Functions が Amazon API Gateway サービスとの統合サポートを開始](https://aws.amazon.com/jp/about-aws/whats-new/2020/11/aws-step-functions-supports-amazon-api-gateway-service-integration/)

* 2020/11/17発表
* API Gatewayも対応した
* 既存のワークフローにAPI Gatewayが追加可能になったので、楽になるかも
* 補足：AWS Step Functionsについて
	* APワークフローの構築ができる
	* 個人的には、REST APIを使っていて、30秒以上かかる処理をする場合に、Lambda使えないけどサーバレスにしたい（Batch使わない）場合にStepFunctionsを使う
	* 別々なLambdaの実行履歴をタイムラインで見れるのが魅力
	* アップデート前だと、Lambdaの他にSQS、ECSに対応していた


## [Introducing Amazon Managed Workflows for Apache Airflow (MWAA)](https://aws.amazon.com/jp/blogs/aws/introducing-amazon-managed-workflows-for-apache-airflow-mwaa/)

* Apache AirflowのAWSマネージドサービスが公開。
* Workerノードがオートスケールしてくれる。
* GCPには[Cloud Composer](https://cloud.google.com/composer)ってのがあった。


## [Amazon S3 Storage Lens の紹介 — オブジェクトストレージに組織全体にわたる可視性を](https://aws.amazon.com/jp/blogs/news/s3-storage-lens/)

* S3の利用状況を可視化
* アカウントごとだけではなく、Organizationで可視化できる
* すでに全リージョンで利用可能
* ダッシュボードを作成した後、48時間後に表示されるようになる
* 費用は無料版と有料版2種類用意されている。
  + `Free Metrics`: 15種類のメトリクスを提供する無料版。データ保持は14日間。
  + `Advanced metrics and recommendations`: すべての使用状況とアクティビティメトリクス (データ保持期間は15か月)およびコンテキストに応じたレコメンデーションが29種類。追加料金がかかる。
* 料金は現在英語ページのみで公開。`$0.20 per million objects monitored per month`とのこと。  
  [ここ](https://aws.amazon.com/s3/pricing/?nc1=h_ls)の「Management & analytics」タブにある。

{{< figure src="snapshot.jpg" title="引用: https://aws.amazon.com/jp/blogs/news/s3-storage-lens/" numbered="true" lightbox="true" >}}


## [AWS、Alexaのクラウド処理をGPUから独自チップに切り替え　高速化でサーバコストを大幅削減 | ITmedia](https://www.itmedia.co.jp/news/articles/2011/18/news119.html)

AlexaのText-to-speech処理を今までGPUでやってきたが、独自のASIC「AWS Inferentia」に変更。  
このInferentiaはインスタンスとしても提供されており、`inf1.xlarge`などで利用可能。  
推論特化GPUのNvidia T4を使える`g4dn.xlarge`と比較すると40%くらい安い。さらにスループットはInferentiaの方が30%高いと主張しているとのこと。


## [CKAD体験記書いた](https://mukiudo.dev/post/k8s/0001-ckad/)

CKADの受験記を書いた。


## Advent Calendar書いてくよ

Podcastで2つ

* [Podcastな Advent Calendar 2020](https://adventar.org/calendars/5457)の12/6（土）
  - 自分のPodcastを配信する目的（ポエム）
* [ポッドキャスト配信について語る Advent Calendar 2020](https://adventar.org/calendars/5597)の12/24（木）
  - 低予算そこそこ音質で始めるpodcast

自作キーボードで1つ
* [キーボード #2 Advent Calendar 2020](https://adventar.org/calendars/5307)
  - パーツ寄せ集めで始めた自作キーボード（初心者）の12/13（日）
