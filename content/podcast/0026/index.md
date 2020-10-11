---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#26 Anthos Day, Lambdaプレビュー機能, EventBridgeアップデート"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "小杉がAnthos Day, 加藤がLambda Extension, CloudWatch Lambda Insights,  EventBridgeアップデートについて話したよ。"
abstract: "小杉がAnthos Day, 加藤がLambda Extension, CloudWatch Lambda Insights,  EventBridgeアップデートについて話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-10-12T00:41:23+09:00
#date_end: 2020-10-12T00:41:23+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-10-12T00:41:23+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/Anthos-Day--Lambda--EventBridge-ekt89e" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Note

## [Google Cloud Anthos Day](https://cloudonair.withgoogle.com/events/gc-solution-event-anthosday-4?utm_source=google&utm_medium=email&utm_campaign=-&utm_content=gcblog)

過去アーカイブが見られる。  
今回はAnthosというより、GKEの事例集が多かった気がする。


## [VS Code内でブラウザ画面プレビューとDevTools表示、そのままコード編集もできるVS Code拡張「Microsoft Edge Tools for VS Code」正式版に － Publickey]( https://www.publickey1.jp/blog/20/vs_codedevtoolsvs_codemicrosoft_edge_tools_for_vs_code.html)

* フロントエンジニア向けの話
  - VS Codeのウインドウ内でライブリロード＆プレビューできる
* Edgeがヘッドレスブラウザとして動作
* 所感）別ウインドウにはできないので、デカイディスプレイが必要かもw


## [【新機能】Lambda Extensions(プレビュー版)がリリースされました！ | Developers.IO](https://dev.classmethod.jp/articles/lambda-extensions/)

* サーバレス構成アプリの運用者向けの話
  - Extension APIを通じて、Lambdaの初期化・シャットダウンフェーズに介入できる
    - フェーズとは
{{< figure src="https://docs.aws.amazon.com/lambda/latest/dg/images/Overview-Full-Sequence.png" title="引用: https://docs.aws.amazon.com/lambda/latest/dg/runtimes-extensions-api.html" numbered="true" lightbox="true" >}}
  - コード不要でインストゥルメンテーションできたりする。
  - DatadogやHashiCorpがLambda Layerとして拡張機能していて、利用可能となっている
    - 監視SaaSとの連携をしたり、初期化フェーズでシークレットを取得するといったステップが作れる


## [Announcing Amazon CloudWatch Lambda Insights (preview) ](https://aws.amazon.com/jp/about-aws/whats-new/2020/10/announcing-amazon-cloudwatch-lambda-insights-preview/)

* サーバレス構成アプリの運用者向け
    * >With Lambda Insights, you can use the multi-function view to understand how compute, memory allocation, and function duration changes over time to optimize Lambda function utilization.
    * CPU時間とかスレッド数、/tmpの使用量とかのメトリクスが取れるみたい
    * 監視が捗る

## [Amazon EventBridge がデッドレターキューのサポートを発表](https://aws.amazon.com/jp/about-aws/whats-new/2020/10/amazon-eventbridge-announces-support-dead-letter-queues/)

* バックエンドのエンジニア、アーキテクト向けの話
* EventBridgeって？
    * AWS環境で発生するイベントを、AWSサービスやSaaSのサービスと紐付けることができるサービス
        * 例）EC2の状態変更が発生したらKinesisストリームに流す
* DLQとは？
    * 失敗したキューのメッセージを保持する
    * キューのデバッグに使ったりするやつ
* で？
    * それがEventBridgeでもできるようになったので、ミッションクリティカルなシステムとかにも使っていけそうじゃない、など採用の幅が広がったんじゃないかな
