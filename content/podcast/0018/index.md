---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#18 【AWS】CDKによる開発でハマったこと"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "加藤がCDKによる開発でハマったことについて話したよ。"
abstract: "加藤がCDKによる開発でハマったことについて話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-07-20T00:43:00+09:00
#date_end: 2020-07-19T21:59:43+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-07-19T21:59:43+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/AWSCDK-egv092" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# 話したこと

## 雑談

### AWSOME DAY

* 2020/8/5（水）15:00-17:40 オンライン
* 対象はAWS初心者
* 詳細と申込みは[こちら](https://pages.awscloud.com/JAPAN-event-OE-awsomeday-online-20200805-reg-event-LP.html)

### BigQuery Omni

* まずはプライベートアルファ版での提供。
* AWS, Azure上にあるデータを使ってBigQueryが利用できる。
  - Anthosを使ってマルチクラウド化。
  - 正確にはAzureはまだ。そもそもAnthosがプレビュー対応だから。
* BigQueryはストレージとクエリエンジン（Dremel）した設計にしてあるため、実現できるとか。
* 公式ブログは[こちら](https://cloud.google.com/blog/ja/products/data-analytics/introducing-bigquery-omni)

### Cloud RunがGitHubと連携

* 前回話したCloud RunのソースリポジトリとしてGitHubも対応したとか。
* 公式ドキュメントは[こちら](https://cloud.google.com/run/docs/continuous-deployment-with-cloud-build)

### Professional Machine Learning Engineer

* GCPの新しい認定資格[Professional Machine Learning Engineer](https://cloud.google.com/certification/machine-learning-engineer)がベータ版にてリリース。
* ベータ版は期間限定。1回しか受けられない。
  - 今回は多分8/21まで。
* ベータ版試験は期間が終わったら全員同時に合否判定される。
* 英語版のみ。
* 試験時間は4時間...！
* ベータ版でも受かれば正式の認定が得られる。
* ベータ版試験の内用をもとに正式版の試験内容（合否ラインとか多分問題の内容とか）が決められる。

### Pinpointで月1250ドル（およそ13万円）のオプションをポチってしまった話

加藤くんのやっちまった話。


## 本題

### CDKによる開発でハマったこと

以下、トピックのみ抜粋。詳細はpodcastにて...

* 「CDKではできないこと」を気づくのに時間がかかった。
* 「CDKでできる」が、ドキュメントの探し方が分からなかった。

上記を踏まえて、情報の探し方など共有したい知見を話した。

podcast内で話した内容に関連するドキュメントは以下。

* [AWS CDK API Reference](https://docs.aws.amazon.com/cdk/api/latest/docs/aws-construct-library.html)
* [aws-chatbot module - AWS CDK](https://docs.aws.amazon.com/cdk/api/latest/docs/aws-chatbot-readme.html)
* [aws-sqs module - AWS CDK](https://docs.aws.amazon.com/cdk/api/latest/docs/aws-sqs-readme.html)
* [aws-lambda module - AWS CDK](https://docs.aws.amazon.com/cdk/api/latest/docs/aws-lambda-readme.html)
* https://docs.aws.amazon.com/cdk/latest/guide/cfn_layer.html

詳しいブログへのリンクは[こちら](https://dev.classmethod.jp/articles/cdk-how-to-reseach-method/)。
