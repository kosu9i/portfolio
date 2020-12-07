---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#33 re:Invent 2020 week1 気になったところピックアップ + ざっと感想 + week2に向けて"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "re:Invent 2020 week1 気になったところピックアップ + ざっと感想 + week2について話したよ。"
abstract: "re:Invent 2020 week1 気になったところピックアップ + ざっと感想 + week2について話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2021-12-07T09:52:00+09:00
#date_end: 2020-12-02T22:39:07+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-12-02T22:39:07+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/reInvent-2020-week1-----week2-enf2mi" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Notes

今回もre:Inventネタ。


## 先週までのre:Invent所感

* Key Noteではアップデート情報が山程でた。  
  特に1発目のAndy Jassy Key Noteでは27個もアップデートがあったみたい。  
  + 参考: [AWSのCEOがre:Inventで発表した約30の新サービス一覧](https://japan.zdnet.com/article/35163273/)
  + キャッチアップかなり大変。
{{< figure src="launches.png" title="27 Launches" numbered="true" lightbox="true" >}}
* 2発目のKey NotesであるAWS Partner Keynoteではそこまで多くの新機能発表はなかったようで、少し落ち着いた感じだった。（失礼）
* [classmethod社のYoutube Live副音声](https://www.youtube.com/channel/UCU7WS2W00hmVFrR640ZCYPQ)がおもしろくて良い。
* コンテナ周りだとAWS SAの方々が配信されている[[Japanese] re:Invent Containers Recap! - Week 1](https://www.youtube.com/watch?v=bhuoSuavCLQ&feature=youtu.be)がわかりやすく良い。
  + re:Inventに限らず、定期的に `#ContainersFromTheCouch` というタグで配信をしているらしい。
* ちなみにKey Noteの再放送枠では正確な英語の字幕がついている！ + 再生速度も変えられる。


## 今週開催されるre:Invent Key Note

今週開催される基調講演をおさらい。

### [Machine Learning Keynote](https://virtual.awsevents.com/media/1_07cg4srl)

* LIVE 日本時間 2020/12/9（水）00:45 AM - 3:00 AM
* 再放送枠は以下
  + DEC 9, 2020 | 9:00 AM - 11:00 AM JST
  + DEC 9, 2020 | 5:00 PM - 7:00 PM JST

### [Infrastructure Keynote](https://virtual.awsevents.com/media/1_qsv5itu8)

* LIVE 日本時間 2020/12/11（金）00:30 AM - 2:30 AM
* 再放送枠は以下
  + DEC 11, 2020 | 9:00 AM - 10:30 AM JST
  + DEC 11, 2020 | 5:00 PM - 6:30 PM JST


## [SageMaker Feature Store](https://aws.amazon.com/sagemaker/feature-store/)補足

[前回配信](https://mukiudo.dev/podcast/0032/)でSageMaker Feature Storeについて話したが実際に触ってみたりしたので追加で補足。  

Feature Storeは具体的には以下のようなことをやってくれる。

* 特徴量そのものはS3などのストレージにすべて保存される。  
  + オンラインStoreではレイテンシが少ないストレージに保存（主に推論時に活用）
  + オフラインStoreではレイテンシよりも容量重視ストレージに保存（主に学習時に活用）
* Feature StoreのSDKを介して、各特徴量をSave, Loadして機械学習プログラムの中で利用する。
* メタデータを元にSageMaker Studio内でグルーピング、検索できるようになっている。  

触ってみた記事がdevelopers.ioにあったので紹介:「[Amazon SageMaker Feature StoreのExampleを実行してみた](https://dev.classmethod.jp/articles/try-sagemaker-feature-store/)」  
同記事内でふれられているが、SageMakerには[公式サンプル集](https://sagemaker-examples.readthedocs.io/en/latest/index.html)があり、そこに[Fraud Detection with Amazon SageMaker FeatureStore](https://github.com/aws/amazon-sagemaker-examples/blob/master/sagemaker-featurestore/sagemaker_featurestore_fraud_detection_python_sdk.ipynb)が追加されている。

また、一般的な「Feature Store」についての参考情報を以下に。

* [GCPでもFeature Storeは今後提供される予定](https://cloud.google.com/blog/ja/products/ai-machine-learning/key-requirements-for-an-mlops-foundation)。（今年末までの提供されるとあるが果たして...）  
  + kubeflowに[Feast](https://www.kubeflow.org/docs/components/feature-store/overview/)というのがあるらしいので、それをマネージドで提供する？
  + [Introducing Feast: an open source feature store for machine learning](https://cloud.google.com/blog/products/ai-machine-learning/introducing-feast-an-open-source-feature-store-for-machine-learning)  
* [What are Feature Stores and Why Are They Critical for Scaling Data Science?](https://towardsdatascience.com/what-are-feature-stores-and-why-are-they-critical-for-scaling-data-science-3f9156f7ab4)
* [ML Engineer Guide: Feature Store vs Data Warehouse](https://www.logicalclocks.com/blog/feature-store-vs-data-warehouse)
  + Feature StoreとDWHの違い


## [Amazon Lookout for Vision – New ML Service Simplifies Defect Detection for Manufacturing](https://aws.amazon.com/jp/blogs/aws/amazon-lookout-for-vision-new-machine-learning-service-that-simplifies-defect-detection-for-manufacturing/)補足

こちらも前回配信に対して補足。

* 製造業の画像認識に特化している。
  - AI/MLというより、Factory Automationの中の一つという位置づけの様子。  
    参考: [AWS、産業分野向けの機械学習サービス発表--機器の異常検知など効率化](https://japan.zdnet.com/article/35163235/)
* すでにパブリックプレビューとして東京リージョンでも利用可能。
* 少ない枚数の教師データで学習が可能（最低30枚とか言っている）
* おそらくclassificationのみ
  - => YES
* エッジ推論するためのモデルダウンロードはできず、クラウド経由のみっぽい。
  - => YES
* [developer向けのドキュメント](https://docs.aws.amazon.com/lookout-for-vision/index.html)もすでに公開されている。
* 評価用のダッシュボードも用意されている。
* 間違った予測結果をAWS Consoleの評価画面上で修正し、学習データに加えて再学習することができる。  
  - 学習に加えたデータを正しく推論できるのは当然なので、再学習後は新しい評価データを用意しないとダメ。
* 推論APIをデプロイすることもできる。また、ステータス確認用（どれくらい異常が検知されているか、など）のダッシュボードもある。

同様のサービスとしてはGCPの[AutoML Vision](https://cloud.google.com/vision/automl/docs)や  
AWSだと[Amazon Rekognition Custom Labels](https://aws.amazon.com/jp/rekognition/custom-labels-features/)。  


## [Amazon Lookout for Equipment](https://aws.amazon.com/jp/blogs/aws/new-amazon-lookout-for-equipment-analyzes-sensor-data-to-help-detect-equipment-failure/)と[Amazon Monitron](https://aws.amazon.com/jp/monitron/)の違い

* Lookout for Equipment
  + 自分たちでセンサーデータを用意したり、学習・推論するところも自前。  
  + 現在は米国東部 (バージニア北部)、アジアパシフィック (ソウル)、および欧州 (アイルランド)でプライベートプレビュー版として利用可能（申請が必要）。  
    参考: [新機能 – Amazon Lookout for Equipment でセンサーデータを分析し、機器の故障検出に役立てる](https://aws.amazon.com/jp/blogs/news/new-amazon-lookout-for-equipment-analyzes-sensor-data-to-help-detect-equipment-failure/)
    - 申請してみたけど、自社が製造業じゃないから無理かも...（ログをどういう形で取得しているか、など結構踏み込んで聞かれた）  
      うちは受託開発なのでダミーデータで評価したいとか適当に書いて出してみた。
* Monitron
  + センサー、センサーデータをAWSに送信するGateway, ML-basedな解析機能, モバイルappなど、AWSがワンストップで面倒を見てくれる。
  + 現在はバージニア北部のみで利用可能（申請は不要。ただ↓のセンサーをAmazonで購入する必要がありそう）。  
    参考: [Amazon Monitron, a Simple and Cost-Effective Service Enabling Predictive Maintenance](https://aws.amazon.com/jp/blogs/aws/amazon-monitron-a-simple-cost-effective-service-enabling-predictive-maintenance/)
  + IoT機器は[Amazonで売っている](https://www.amazon.com/dp/B0851JTCC1)

以下の概要図が違いを端的に表していると思う。（オレンジ部分が当該サービスの担当範囲と思われる）

{{< figure src="lookout_for_equipment_summary.png" title="Lookout for Equipment概要図" numbered="true" lightbox="true" >}}
{{< figure src="monitron_system.png" title="Amazon Monitron概要図" numbered="true" lightbox="true" >}}


## [AWS Panorama Appliance: コンピュータービジョンアプリケーションをエッジへ](https://aws.amazon.com/jp/blogs/news/using-computer-vision-applications-at-the-edge/)

* こちらも製造業向けのコンピュータビジョンを支援するプロダクト。
  + コンセプトとしては、既存の工場内カメラに接続してデータを集約し、AWSクラウド側で何かしらのCV処理（SageMakerをバックエンドにすることも想定されている）を行う。
  + 用途としてはライン上の外観検査だけではなく、工場内の人員の動きや、小売店での顧客動向など幅広い。
* [AWS Panorama Appliance](https://aws.amazon.com/jp/panorama/)と[AWS Panorama Device SDK](https://aws.amazon.com/jp/panorama/panorama-device-sdk/)から構成される。
  + Panorama Applianceは申請が必要なプレビュー版。
  + SDKはこれから公開される。
* [AWS Panorama pricing](https://aws.amazon.com/jp/panorama/pricing/)で費用を確認できる。結構高い。
  + production: $4,000 + カメラストリームごとに月$8.33
  + develop: $2,499
* 高いのでプレビュー版申込みはやめといた。


## [Amazon CodeGuru](https://aws.amazon.com/codeguru/)アップデート

ML-basedなコード解析機能。

* Python対応
  + いままではJava, その他のJVM言語のみだった
  + パブリックプレビューですでに使える様子。
* セキュリティに関する解析
  + 自動的にセキュリティ観点での解析が追加されるっぽい。
  + 追加料金は不要。
  + 参考: [Amazon CodeGuru Reviewer announces Security Detectors to help improve code security](https://aws.amazon.com/about-aws/whats-new/2020/12/amazon-codeguru-reviewer-announces-security-detectors-improve-code-security/)


## [Amazon DevOps CodeGuru](https://aws.amazon.com/jp/devops-guru/)

アプリケーションの性能を監視し、問題点の抽出や改善提案など。

* パブリックプレビューですでに使える様子。
  + US East (N. Virginia), US East (Ohio), US West (Oregon), Europe (Ireland), and Asia Pacific (Tokyo)
* Amazon CloudWatch、AWS Config、AWS CloudTrail、AWS CloudFormation、AWS X-Ray などの運用系サービスのメトリクスやイベントを収集し異常を検出  
  らしい。  
  参考: [アプリケーションの異常を自動検出するサービス “Amazon DevOps Guru” プレビュー開始 #reinvent](https://dev.classmethod.jp/articles/now-in-preview-amazon-devops-guru/)
* 参考: [New- Amazon DevOps Guru Helps Identify Application Errors and Fixes](https://aws.amazon.com/jp/blogs/aws/amazon-devops-guru-machine-learning-powered-service-identifies-application-errors-and-fixes/)
* コスト: [Amazon DevOps Guru pricing](https://aws.amazon.com/jp/devops-guru/pricing/)
  - リソースごとの1時間ごとに費用がかかる
  - 結構安い（$0.0028 - $0.0042 per Resource per Hour）

{{< figure src="guru_devops.png" title="Amazon DevOps CodeGuru概要図" numbered="true" lightbox="true" >}}
