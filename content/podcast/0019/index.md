---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#19 【GCP】AutoML"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "小杉がGCPのAutoMLについて話したよ。<br/>サービスの内容というより、主に使い所とか考え方について話したよ。"
abstract: "小杉がGCPのAutoMLについて話したよ。<br/>サービスの内容というより、主に使い所とか考え方について話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-07-26T01:08:00+09:00
#date_end: 2020-07-25T03:09:41+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-07-25T03:09:41+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/GCPAutoML-eh7pv0" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# 話したこと

## 小ネタ

### 大手サービスのAWSからの移行

#### Minecraft

参考: [Microsoft will complete the migration of Minecraft to Azure by the end of 2020](https://mspoweruser.com/microsoft-migrate-minecraft-azure-2020/)

マイクラでは今までAWS使っていたけど、2020年中にAzureに移行するとのこと。  
AWSでは以下のサービスを利用していた。

* Amazon EC2
* Amazon Elastic Block Store(EBS)
* Amazon Relational Database Service (RDS)
* Amazon S3
* AWS Elastic Load Balancing

かなり基本的な構成。Realmsというマイクラ用のサーバを運用していたらしい。


#### Dropbox

AWSからの移行といえば[Dropboxの自社DC移行](https://postd.cc/inside-the-magic-pocket/)が有名。

Dropboxは自社開発であるMagic Pocketというストレージサービスを運用。
Magic Pocketの詳しい日本語記事は[こちら](https://postd.cc/inside-the-magic-pocket/)

Dropboxほどの大規模なサービスとなると自社で最適化したストレージを運用するほうがコストも信頼性も改善されるということ。


### AWS Lambda Provisioned Concurrency

参考: [AWS Lambdaが提供するProvisioned Concurrencyという機能を簡単に説明してみる](https://www.keisuke69.net/entry/2020/07/21/193701)  

LambdaにはProvisioned Concurrencyというのがある。  
[Cloud Runの回](https://mukiudo.dev/podcast/0017/)でも少し話したが、ゼロスケールするサーバレスにはコールドスタートがつきもの。  
Provisioned Concurrencyはコールドスタートを緩和する機能。

要はお金を事前に払っておいてLambdaをウォームアップしてくれるもの。  
メモリ * 時間 * 同時実行数で[料金](https://aws.amazon.com/jp/lambda/pricing/#Provisioned_Concurrency_Pricing)が決まるっぽい。  
あらかじめバーストしそうなことが予測できる場合には、その直前にProvisioned Concurrencyを予約しておく、みたいな使い方はうまそう。  


### CDK for Terraform

参考: [AWS CDKでTerraformによるプロビジョニングが可能な「CDK for Terraform」が発表](https://codezine.jp/article/detail/12605)
参考: [AWS CDKでプロバイダーとしてTerraformが使える！！CDK for Terraformが発表されました！！](https://dev.classmethod.jp/articles/cdk-for-terraform/)

Terraformの開発元[HashiCorpが開発中](https://www.hashicorp.com/blog/cdk-for-terraform-enabling-python-and-typescript-support/)。まだアルファ版。

CDKでGCPを構築できるようになるかもしれない...？


### Cloud Next OnAir

[Cloud Next OnAir](https://cloud.withgoogle.com/next/sf/japan#productivity-collaboration)はじまった。


## 本ネタ

### AutoML

#### 概要

データさえ用意すれば、機械学習のモデルをよしなに作ってくれるサービス。

GCPで提供しているのは以下。

* AutoML Vision
  - Classification
  - Object Detection
* AutoML Video Intelligence（ベータ版）
  - Classification
  - Object Tracking
* AutoML Natural Language
* AutoML Translation
* AutoML Tables（ベータ版）

クラウド上にREST APIやバッチ推論環境のサービングもやってくれる。

GCPでは、モデルをカスタマイズできないML用のAPIも用意されている。  
AutoMLはこれらでカスタムモデルを作成して使えるサービス、という見方もできる。


AWSにも、AutoMLのようにカスタムモデルを作れるサービスはある。（詳細は触ったことないので不明...）
* 画像・動画を扱うAmazon Rekognition
* 時系列データを扱うAmazon Forecast
* レコメンドのAmazon Personalize

など。というかAWSでは他にも色々あって、カスタムモデルを作れる分野が多そう。  
[MLサービス一覧](https://aws.amazon.com/jp/machine-learning/)で各サービスの説明に「カスタムモデル」という記載があればできそう。


#### ユースケース

以下、個人的な考え。

データサイエンティスト（つまり自分でモデルを作れる人）向けではないと思う。  
かといって「機械学習って何？」っていうレベルだと扱うのは厳しい。

最低限、以下のようなことを検討できるリテラシは必要。

* 解きたい課題と、AutoMLが提供しているモデルがマッチするか？
* データの質・量は十分か？
* リークは起こっていないか？
* 結果の評価は適切に行えているか？

また、機械学習のモデリングに費やす時間は、プロジェクト全体の一部に過ぎない。  
AutoMLはモデル作成、デプロイ、管理、評価周りを便利にしてくれるが  
おそらく一番大変であるデータの準備部分の面倒は見てくれない。

よく「AutoMLでデータサイエンティストを置き換える」という論調を耳にするが、**それは現状できない**と思う。  

じゃあどういうユースケースがあるかというと  
「機械学習の基本的な用途は分かっていて、アプリケーション開発もできる。でも自分でモデルを作成しチューニングする能力は低い」  
という人・組織には、よくマッチすると思う。


#### 費用

* まぁまぁ高いけど、やってくれることを考えるとお得ではある。
* VisionのObject Detectionでは学習データ500枚くらいで、1モデル作るのに￥7,000くらいかかった。  
* かかる費用（= ノード時間 * 単価）は、学習データやラベルの量、学習の収束具合による。


#### 使い方

文字に起こすのが面倒なので、くわしくはpodcastにて...


#### 意見交換

* 画像系MLでなにかやりたいことある？
  - Classification, Object Detectionが当てはまればAutoML試してアプリ作ってみても良いかも
