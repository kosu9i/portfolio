---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#32 Coming Soon"
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
date: 2020-12-02T22:39:07+09:00
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

# Show Notes

今回もre:Inventネタ。

re:Inventキャッチアップつらい問題...

例年は現地で数日間集中してだったのが、オンラインだと無限にセッション見れるかつ3週間ということで頑張ろうとするとキリがない。
Twitterとか見てると最初からみんな飛ばし過ぎなような...？

re:Inventがオンラインで3週間という人類がいまだかつて経験したことのない事態に  
身体がもたない人が続出するのでは...？という心配すらある。    
（ていうかオンラインで在宅からだと普通の仕事もあんのよ...）

テンションがあがるのは分かるのだが、最新情報を追うだけが主目的ではないはず。  
少し冷静になって、身体に無理がない程度にキャッチアップしていくのが良いかと思われる。

ここでも自分たちが興味のあるものに絞る。


## re:Invent情報収集おすすめリンク

最初に情報収集としておすすめリンクをまとめて貼っておく。

* [AWS What's New Feed](https://aws.amazon.com/new/?nc1=h_ls)
  + 公式の最新情報フィード
  + 言語設定は英語にしておくべし
* [AWS News Blog](https://aws.amazon.com/blogs/aws/)
  + 公式のブログ
  + re:Invent中はすごい勢いで更新される
  + 言語設定は英語にしておくべし
* [Twitterハッシュタグ #reinvent](https://twitter.com/search?q=%23reInvent&src=recent_search_click)
* [Developers.IO produced by Classmethod re:Invent 2020用ページ](https://dev.classmethod.jp/referencecat/aws-reinvent-2020/)
  + 言わずとしれたクラスメソッド社のre:Invent 2020用ページ
  + re:Invent中はすごい勢いで更新される。
  + ここを見ておけば、だいたい日本語でのキャッチアップできるのではという安心感。
  + 社員の皆さん、無理はせずお身体には気をつけてください...


## SageMaker周辺アップデート

12/2の最初のCEO Andy Jassy Key Noteで発表された。  
Ken Noteの内容は[re:Invent 2020 Liveblog: Andy Jassy Keynote](https://aws.amazon.com/jp/blogs/aws/reinvent-2020-liveblog-andy-jassy-keynote/)で記事にされている。

Machine LearningのKey Noteは2週目に控えているが、早くもAI/Machine Learning系でアップデートがたくさん公開されている。  
[SageMakerの英語トップページ](https://aws.amazon.com/sagemaker/?nc1=h_ls)も更新されており「Prepare」と「Deploy & Manage」のところが強化されているのが分かる。

{{< figure src="toppage.png" title="SageMakerの英語版トップページが更改された" numbered="true" lightbox="true" >}}


ここではSageMakerの新3機能について。

---

### [Amazon SageMaker Data Wrangler](https://aws.amazon.com/sagemaker/data-wrangler/)

Key Noteで↓と言われていた。
> Data preparation is the next frontier, and it is hard. 

その通りで、GCPのAutoMLやSageMaker Autopilotのようにモデリングを自動化してくれる機能はたくさん出てきている。

ただ機械学習やデータ分析で本当に大変なのはデータ準備のところで、これに大半の時間を費やす。  
SageMaker Data Wranglerはそのあたりを楽にしようというサービス。

具体的には以下のようなことをやってくれる。

* **Prepare data for ML in minutes**
  * 複数データソース（Amazon S3, Amazon Athena, Amazon Redshift, AWS Lake Formation, and Amazon SageMaker Feature Store）からのインポートをSageMaker Studio内で楽に。
  * 300程度のデータ変換機能が用意されており、1clickで自動適用される。
    - convert column type, one hot encoding, impute missing data with mean or median, rescale columns, and data/time embeddings...
    - カラムの型変換, one-hot encoding, 欠損データの補完, スケーリング, 時刻データの変換（？）
  * 変換結果の可視化 + 手動での修正。
{{< figure src="prepare.png" title="Prepare data for ML in minutes" numbered="true" lightbox="true" >}}
* **Quickly estimate ML model accuracy**
  * 変換後のデータがおかしなことになっていないか解析が可能。
  * モデル学習前に解析できるのか、学習後なのか詳細はまだ触れていないので不明。
{{< figure src="data_analysis.png" title="Quickly estimate ML model accuracy" numbered="true" lightbox="true" >}}
* **From preparation to production with a single click**
  * 上記のデータ加工をnodebookやpython scriptの形でexportできる。
  * Workflowとしても定義できる。
{{< figure src="export.png" title="From preparation to production with a single click" numbered="true" lightbox="true" >}}


これらで準備ができたら、今までのSageMaker Autopilotなりで学習ということだろうと思う。

ただ、こういった内容のサービス自体は目新しいものではない。  
GCPでは[DataPrep](https://cloud.google.com/dataprep)という同等のサービスが以前から提供されているし、  
AWSでも[AWS Data Wrangler](https://aws.amazon.com/jp/blogs/news/launch-aws-data-wrangler-v1-0/)というPythonライブラリが提供されていた。

今回のアップデートでは、これらの機能がSageMaker Studioに統合されたというのが主旨だろうと思う。  
実際、GCPでは1つのUIで統合されてはおらず、DatePrep => DataFlow => AI Platformのようにサービスを行き来する必要はあるが  
SageMaker Studioはそれらをすべて同じUIで利用できるようにする、というのが昨年からの思想だと思われる。（~~使っている人が周りにいるかというとあまり聞いたこと無いが~~）

---

### [SageMaker Feature Store](https://aws.amazon.com/sagemaker/feature-store/)

機械学習に必要なデータ特性を「特徴量（Feature）」と呼ぶ。  
文字通り、このFeatureを保存するのがSageMaker Feature Store。

このFeatureは実験を繰り返す過程でコロコロ変わるし、「このモデルってどの特徴量で作られたんだっけ？」となっていくのはよくある困りごと。  
また、学習時と推論時で同じ加工をした特徴量を扱う必要がある。

これらの特徴量を管理するのがFeature Storeで、これも発想自体は新しいものではなく  
同じくSageMaker Studio内で統合して使えるようになったのが利用者にとっては嬉しいポイント。

* **Ingest data from many sources**
  + ストリーミングAPIで動画, 音声などのデータも取り込める。
  + Data Wranglerで加工したデータも保存できる。
* **Search and discovery**
  + 保存した特徴量の検索ができる
  + タグなどのメタ情報を付与できる
{{< figure src="feature_store_search.png" title="Search and discovery" numbered="true" lightbox="true" >}}
* **Ensure Feature Consistency**
  + 学習と推論時の特徴量は同じである必要があるが、扱うデータ量やそれに必要なストレージも異なる。この差異を吸収する。
  + 具体的にどうするのかはまだ触っていないので不明...
* **Feature standardization**
  + 特徴量の定義を一元的に管理する（？）
  + 例として「温度」が摂氏 or 華氏、とか「日付」が「date-month-year」or「month-date-year」とか。
  + これも具体的にどうするのかはまだ触っていないので不明...
{{< figure src="feature_store_standardizasion.png" title="Feature standardization" numbered="true" lightbox="true" >}}

---

### [Amazon SageMaker Pipelines](https://aws.amazon.com/sagemaker/pipelines/)

MLのCI/CDパイプライン。  
要はここまでに出てきたデータ準備+加工, 前処理, 学習, 評価, モデル管理などをワークフローとして定義し管理する。

* **Compose, manage, and reuse ML workflows**
  + python SDKによりMLのworkflowを定義, 保存, 管理できる。
  + workflowの可視化もできる。
  + 入出力データとも紐付けて管理できそう。
{{< figure src="pipeline_workflow.png" title="Compose, manage, and reuse ML workflows" numbered="true" lightbox="true" >}}
* **Choose the best models for deploying into production**
  + モデルのバージョン管理。
  + ベストモデルを選択し、デプロイ出来る。
* **Automatic tracking of models**
  + workflow実行時の監査ログやメタ情報などトラッキング。
{{< figure src="pipeline_tracking.png" title="Automatic tracking of models" numbered="true" lightbox="true" >}}
* **Bring CI/CD to machine learning**
  + CI/CDの概念をMLに持ち込んだぞ、ってこと。

これも概念としては新しいものではなく(ry

同様のツールとしては[MLflow](https://mlflow.org/)や[kubeflow](https://www.kubeflow.org/)などがあげられると思う。  
kubeflowは「[AI Platform Pipelines](https://cloud.google.com/blog/ja/products/ai-machine-learning/introducing-cloud-ai-platform-pipelines)」の一部としてGCPのマネージド・サービスとしても提供されている。


## その他AI/Machine Learning関連アップデート

気になったやつをダイジェストで。（詳しくはまだ調べられていない）

---

### [Amazon Lookout for Vision – New ML Service Simplifies Defect Detection for Manufacturing](https://aws.amazon.com/jp/blogs/aws/amazon-lookout-for-vision-new-machine-learning-service-that-simplifies-defect-detection-for-manufacturing/)

{{< figure src="lookout_vision.png" title="Lookout Vision" numbered="true" lightbox="true" >}}

* 製造業の画像認識に特化している。
* 少ない枚数の教師データで学習が可能（最低30枚とか言っている）
* おそらくclassificationのみ
* エッジ推論するためのモデルダウンロードはできず、クラウド経由のみっぽい。
* [developer向けのドキュメント](https://docs.aws.amazon.com/lookout-for-vision/index.html)もすでに公開されている。

同様のサービスとしてはGCPの[AutoML Vision](https://cloud.google.com/vision/automl/docs)や  
AWSだと[Amazon Rekognition Custom Labels](https://aws.amazon.com/jp/rekognition/custom-labels-features/)。  

---

### [New – Amazon Lookout for Equipment Analyzes Sensor Data to Help Detect Equipment Failure](https://aws.amazon.com/jp/blogs/aws/new-amazon-lookout-for-equipment-analyzes-sensor-data-to-help-detect-equipment-failure/)

{{< figure src="lookout_equipment.png" title="Lookout Equipment" numbered="true" lightbox="true" >}}

* 産業機器などでの故障を検知する？
* 1つのMLモデルで300種類以上の機器の状態を評価できるとのこと。
* 一見、後述の「Monitron」とセットのように見えるが、直接的な記載は見当たらず  
  おそらく独立したサービス。

特にMonitronとの関係性がよく分からん...  

---

### [Amazon Monitron](https://aws.amazon.com/jp/monitron/)

{{< figure src="monitron.png" title="Amazon Monitron" numbered="true" lightbox="true" >}}
{{< figure src="monitron_system.png" title="Amazon Monitron概要図" numbered="true" lightbox="true" >}}

* 同じく産業機器の状態を監視できるIoT機器。
* Monitron Gatewayを通してAWSにセンサデータを送信
* AWS側でML-basedな解析
* モバイルappも提供される予定（Android, iOS）

---

### [AWS Trainium](https://aws.amazon.com/jp/machine-learning/trainium/)

* 推論には[AWS Inferentia](https://aws.amazon.com/jp/machine-learning/inferentia/)というのがあったが、今度は学習に特化したチップ。
* [AWS Neuron SDK](https://aws.amazon.com/jp/machine-learning/neuron/)ってのが必要。
* 2021年から使えるようになるらしい。現在[プレビュー版申し込み中](https://pages.awscloud.com/trainium-preview.html)。



