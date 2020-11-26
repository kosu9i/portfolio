---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#30 Coming Soon"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary:
abstract:

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-11-26T23:00:09+09:00
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


## [CKAD体験記書いた](https://mukiudo.dev/post/k8s/0001-ckad/)

CKADの受験記を書いた。
