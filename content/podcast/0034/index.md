---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#35 re:Invent 2020 振り返り"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "re:Invent 2020を自分たちなりに振り返ったよ。キャッチアップの量が多すぎて、ざっくりとしか話せなかったよ。詳細はまたの機会に配信とかしたいと思うよ。"
abstract: "re:Invent 2020を自分たちなりに振り返ったよ。キャッチアップの量が多すぎて、ざっくりとしか話せなかったよ。詳細はまたの機会に配信とかしたいと思うよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-12-22T10:03:00+09:00
#date_end: 2020-12-22T10:03:00+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-12-21T00:21:38+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/reInvent-2020-eo3k7a" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Notes

## re:Invent 2020 一段落

* 11/30 - 12/18 まる3週間のセッションが終わった。
  - 発表されたアップデート数: 180（昨年は87）
  - Key note: 5セッション
  - Leadership Session: 多分18セッション
  - Breakout Session: 500くらい
* ログインするとアーカイブが視聴できる。
  - かなり多くのセッションで正確な英語字幕ついている。
* 2021/1/12-14の3日間, 約200セッションまだあるよ。

### ざっとした所感

* 3週間長いようで長かった。密度も濃い。
* アーカイブ版は英語字幕が正確で助かる。
* Keynoteで新機能だけを追うのではなく、リーダーシップセッションやBreakout Sessionで有益な活用事例をちゃんと追いたい。
* セッション以外のコンテンツ（LearningやConnection）は全然参加できなかった。
* お祭り感すごい。高揚感ある。いつか現地で見たくなった。
* データ活用、AI/MLは今年も盛り上がっていた。Redshiftもアップデートが多かったみたい。
  - まったく新しいコンセプトの機能というより、ML業界全体で必要とされているものをAWSやSageMakerに持ってきたという印象。
  - 特定の業界（コンタクトセンター、製造業、ヘルスケア）に特化したサービス展開をしているのも印象的だった。

あほみたいな所感ばかりだけど。

### 今からキャッチアップするための参考リンク

* 年明けにre:Invent Recapシリーズが開催されるので、興味のある人は[申込みページ](https://pages.awscloud.com/JAPAN-event-OE-reinvent-recap-2021-reg2-event.html)から。
  - 日本語Webinar
  - 技術領域別だけではなく、業界別に開催されるのが特徴的
* [Developers.IO produced by Classmethod re:Invent 2020用ページ](https://dev.classmethod.jp/referencecat/aws-reinvent-2020/)
  - Youtube Liveで開催された[re:Growth 2020 Online](https://dev.classmethod.jp/news/201218-regrowth-online/)もおすすめ
* [AWS What's New Feed](https://aws.amazon.com/new/?nc1=h_ls)
* [AWS News Blog](https://aws.amazon.com/blogs/aws/)
  - 日本語ブログのre:Inventタグがついた一覧は[こちら](https://aws.amazon.com/jp/blogs/news/category/events/reinvent/)
  - 日本語訳の記事も続々と出ている。
* その他、AWSの中の人達が独自にReCapやったり、Black Belt公開されていたりするので、関心のある機能をググればなにか引っかかる情報が出ていると思われる。

## re:Invent Keynoteざっとおさらい

Keynoteはリアルタイムで更新されていたLiveblogというのが概要としてまとまっている。

### [re:Invent 2020 Liveblog: Andy Jassy Keynote](https://aws.amazon.com/jp/blogs/aws/reinvent-2020-liveblog-andy-jassy-keynote/)

* 新機能が一番発表されたのでは。約30個。
  + 参考: [AWSのCEOがre:Inventで発表した約30の新サービス一覧](https://japan.zdnet.com/article/35163273/)
* このペースで3週間もつのか...？と不安がよぎった初日だった。

### [re:Invent 2020 Liveblog: Partner Keynote](https://aws.amazon.com/jp/blogs/aws/reinvent-2020-liveblog-partner-keynote/)

* 新機能の発表というよりはパートナーシップをどう強化しているかなど取り組みに関するものが多かった。
* とはいえ、[AWS Saas Boost](https://aws.amazon.com/jp/about-aws/whats-new/2020/12/introducing-aws-saas-boost/)という個人的には気になるアップデートもあった。
  - 参考: [ソフトウェアをSaaS化するための移行を加速するOSS環境などを提供するAWS SaaS Boostがプレビューででました！ #reinvent](https://dev.classmethod.jp/articles/preview-aws-saas-boost/)


### [re:Invent 2020 Liveblog: Machine Learning Keynote](https://aws.amazon.com/jp/blogs/aws/reinvent-2020-liveblog-machine-learning-keynote/)

* MLをどう活用するか、とかTenetという言葉（主義とか信条とかいう意味。スローガンみたいなもの）を使って語っていた。
* このTenetに紐付ける形で新機能の発表が結構あった。

以下、参考リンク。

* Developers.ioにML関連をまとめてくれている記事がある。  
  [【レポート】 AWS re:Invent 2020 Machine Learning Keynote #reinvent #KEY005](https://dev.classmethod.jp/articles/sesson-report-aws-reinvent-2020-machine-learning-keynote/)
  - とてもよく簡潔にまとまっている。
  - 安定のクオリティと速さ。
* [Julien Simon Youtube Channel](https://www.youtube.com/channel/UCVonoXm3SI_Q0ZNHd5JPawA)
  - AWSエバンジェリストのJulien Simon氏のYoutubeチャネル
  - SageMakerのデモ動画がたくさんあがっている。
  - 時間も数十分のものが多く見やすい。英語も聞き取りやすい。


### [re:Invent 2020 Liveblog: Infrastructure Keynote](https://aws.amazon.com/jp/blogs/aws/reinvent-2020-liveblog-infrastructure-keynote/)

* 新機能の発表というよりはAWSのインフラがどう活用されている、どう支えているかなどの話が多かった
  - AWS独自チップの話。Graviton2や機械学習用チップHabana Gaudi, Trainiumなど。
    - 全然話逸れるけど、[MicrosoftもARMベースの独自チップ作る報道](https://www.bloomberg.com/news/articles/2020-12-18/microsoft-is-designing-its-own-chips-for-servers-surface-pcs)...
  {{< figure src="reinvent-infra-keynote-0017.jpg" title="Mac Instanceの中身 引用: https://aws.amazon.com/jp/blogs/aws/reinvent-2020-liveblog-infrastructure-keynote/" numbered="true" lightbox="true" >}}
  - Mac InstanceがラックにMac miniを詰め込んでいる画像が出て話題になった。
  - Nitroの話。
  - 環境への配慮
* 最初のコンサート中に「ギターが2つあってMulti-AZですね」みたいなジョークがblogに書かれていた。お祭り感で浮かれている。
{{< figure src="band_az.png" title="Multi-AZ Guitars" numbered="true" lightbox="true" >}}


### [re:Invent 2020 Liveblog: Werner Vogels Keynote](https://aws.amazon.com/jp/blogs/aws/reinvent-2020-liveblog-werner-vogels-keynote/)

* 今までの近未来的なステージではなく工場のようなところで撮影されていたのが印象的。
  {{< figure src="reinvent-dev-keynote-0019.jpg" title="Werner Vogels Keynote 引用: https://aws.amazon.com/jp/blogs/aws/reinvent-2020-liveblog-werner-vogels-keynote/" numbered="true" lightbox="true" >}}
* あまり聴いてないので自信がないが、多分DevOps界隈の話が多めだった気がする。
* 大きめの新機能の発表もあった。
  - [AWS Fault Injection Simulator (coming in 2021)](https://aws.amazon.com/jp/fis/)
    - AWSでカオスエンジニアリング
  - [Announcing Amazon Managed Service for Grafana (in Preview)](https://aws.amazon.com/jp/blogs/aws/announcing-amazon-managed-grafana-service-in-preview/)
    - Grafanaはログデータ可視化ツール。kibanaみたいなもの。
  - [Join the Preview – Amazon Managed Service for Prometheus (AMP)](https://aws.amazon.com/jp/blogs/aws/join-the-preview-amazon-managed-service-for-prometheus-amp/)
    - 監視ツール


## 個人的に気になったアップデートなど（小杉）

### マネジメントコンソールのアップデート

* [AWS CloudShell – AWS リソースへのコマンドラインアクセス](https://aws.amazon.com/jp/blogs/news/aws-cloudshell-command-line-access-to-aws-resources/)
* ヘッダに検索窓がついた

{{< figure src="console.png" title="マネコンが変わった" numbered="true" lightbox="true" >}}

つまり...GCPのコンソールみたいになった。Cloud Shellでは以下の違いはあるが。
* GCPはリージョンを気にせず利用できる。AWS Cloud Shellはリージョンごとに永続化ディスクが異なる。
  - ユーザの場所からよしなにプロビジョニングされる（なぜか台湾が多いけど）
  - GCPは5GBの永続化ストレージ。AWSは1GB。
* GCPはCloud Shell Editorも提供されている
* スペック（どちらも実際に起動してコマンドで確認したもの。公式には不明）
  - GCP: 2vCPU, 8GBメモリだった（過去には1vCPU, 1.7GBでブーストモードもあるという記事もあったがよく分からず）
  - AWS: 2vCPU, 4GBメモリだった


### [ECR Public Resistory](https://aws.amazon.com/jp/ecr/)

* 以前からDockerHubの制限に伴ってアナウンスされていたものの一般公開。
  - 今までDockerイメージのパブリックレジストリはほぼDocker Hub一択だったけど、ここにAWSやGitHubが参入。
* イメージのホスト（イメージ開発者側）
  - 1GBにつき$0.10/月
  - 無料枠として月$50
* イメージのpull（イメージ利用側）
  - Anonymousユーザ
    - 月に500GB転送までOK。超えると何らかの制限（どんな制限かは発表なし）
    - アクセス元のIPアドレスで判別というはDocker Hubと同じ
  - AWS認証済みユーザ
    - 月に5TB転送まで無料でOK。それ以上は$0.09/GB。
    - AWSリージョン内からならすべて無料。


### [AWS Fault Injection Simulator (coming in 2021)](https://aws.amazon.com/jp/fis/)

* AWS上でカオスエンジニアリング
* 2021年に提供開始予定
* カオスエンジニアリングの停止やロールバックなど制御するための機能もあり。
* ドキュメントには`Amazon EC2, Amazon EKS, Amazon ECS, and Amazon RDS`とが記載されていたが、どのコンポーネントが対応されるかは不明。

カオスエンジニアリングといえばNetflix。以前紹介した[Chaos Monkey](https://github.com/Netflix/SimianArmy)などのOSSもある。


### [AWS BatchのFargate対応](https://aws.amazon.com/jp/about-aws/whats-new/2020/12/severless-batch-scheduling-with-aws-batch-and-aws-fargate/)

* 今までのはECS on EC2だったが、Fargateに対応。
* これによってゼロスケール、コールドスタートへの対応が容易になりサーバレス感。
* FargateはGPU使えないので、Deep Learningの学習用途では変わらずSageMaker一択。


### [SaaS Boost](https://aws.amazon.com/jp/partners/saas-boost/)

* SaaS化する際の面倒事（バージョンの管理、マルチテナント、モニタリング、課金など）を便利にしてくれる。
* 現在は申請ありのプレビュー版
* 公式ブログ: [Transforming Your Monolith to SaaS with AWS SaaS Boost](https://aws.amazon.com/jp/blogs/apn/transforming-your-monolith-to-saas-with-aws-saas-boost/)


### [Cloud Audit Academy](https://aws.amazon.com/compliance/auditor-learning-path/?nc1=h_ls)

[re:Growth](https://dev.classmethod.jp/news/201218-regrowth-online/)のセキュリティセッションで知った。

* 「Security and Compliance Domains」
* [Cloud Audit Academy](https://aws.amazon.com/compliance/auditor-learning-path/?nc1=h_ls)のページで言語をEnglishにすると最新の情報になる。
* [無料の3時間トレーニング（英語）](https://www.aws.training/Details/eLearning?id=41556)がある。良さそう。


### ML Keynote関連

#### [Amazon SageMaker Pipelines](https://aws.amazon.com/jp/sagemaker/pipelines/)

正確にはML Keynoteでの発表ではないが。

* SageMakerのパイプラインを組むには今まではStep Functionsを使っていたのをSageMaker Studioと統合する形で使えるようになった。
  - それ以下でもそれ以上でもないように見える...
* SageMaker samplesにも早速サンプルnotebookが提供されている。  
  Step Functionsでも同じデータセットを使ったサンプルが提供されているので比較しやすい。
  - [Step Functionsのサンプルnotebook](https://github.com/aws-samples/amazon-sagemaker-examples-jp/tree/master/step-functions-data-science-sdk)
  - [SageMaker Pipelinesのサンプルnotebook](https://github.com/aws/amazon-sagemaker-examples/tree/master/sagemaker-pipelines/tabular/abalone_build_train_deploy)


#### [Amazon SageMaker Simplifies Training Deep Learning Models With Billions of Parameters](https://aws.amazon.com/jp/blogs/aws/amazon-sagemaker-simplifies-training-deep-learning-models-with-billions-of-parameters/)

* Distributed TrainingをSageMaker上で簡単に行えるようにする
  - 前からあったような気もするが、[DLフレームワークでの新しい対応があるとのこと](https://aws.amazon.com/jp/about-aws/whats-new/2020/12/introducing-distributed-training-on-amazon-sagemaker/)
* 個別のDLフレームワークでも簡単にできるようにはなっているはずなので、恩恵が小さいような気もしている。
* 異なるDLフレームワークでも同じお作法で並列化できるならうれしいかも？
* Keynoteを通して時間削減の話をたくさんしていたのでその一環か。
  - Data Wranglerとかで作業効率化
  - Distributed Trainingで処理効率化


#### [Amazon SageMaker Clarify](https://aws.amazon.com/jp/sagemaker/clarify/)

* Bias Detection across the end-to-end ML workflow
  - バイアスはMLワークフローの色んな所で入り込む。それを検知する。
  - 例えば男女比率や年齢の分布が偏っている、など学習前に検出できるものもある。
  - 学習後の推論結果に対するバイアス（特定のグループに特定の結果を返してしまう、とか）も検出。
  - ClarifyとSageMaker Model Monitorが統合されているのでアラートもあげやすい。
* 公式ブログ: [New – Amazon SageMaker Clarify Detects Bias and Increases the Transparency of Machine Learning Models](https://aws.amazon.com/jp/blogs/aws/new-amazon-sagemaker-clarify-detects-bias-and-increases-the-transparency-of-machine-learning-models/)


#### [Deep Profiling for SageMaker Debugger](https://aws.amazon.com/jp/sagemaker/debugger/)

* DebuggerにDLのCPU, GPU, などのプロファイラが追加
* 公式ブログ: [New – Profile Your Machine Learning Training Jobs With Amazon SageMaker Debugger](https://aws.amazon.com/jp/blogs/aws/profile-your-machine-learning-training-jobs-with-amazon-sagemaker-debugger/)


#### [Amazon SageMaker Edge Manager](https://aws.amazon.com/jp/sagemaker/edge-manager/)

* AWS IoT, GreengrassをMLに持ち込んできたという話だと思う。
* [AWS Systems Manager Fleet Manager](https://aws.amazon.com/jp/blogs/news/new-aws-systems-manager-fleet-manager/)との関連もあるかも。まとめて要チェック。
* EdgeのCI/CDを管理
* EdgeへのMLデプロイを簡単にしてくれたり管理してくれたり
* いままでもNeoってのがあったが、これはモデルの圧縮・コンパイル
* 公式ブログ: [Amazon SageMaker Edge Manager Simplifies Operating Machine Learning Models on Edge Devices](https://aws.amazon.com/jp/blogs/aws/amazon-sagemaker-edge-manager-simplifies-operating-machine-learning-models-on-edge-devices/)
* [サンプルnotebook](https://github.com/aws/amazon-sagemaker-examples/tree/master/sagemaker_edge_manager)もあるけど、Edgeに見立てたEC2をSSMで制御してたりして微妙...


#### [Amazon Lookout for Metrics](https://aws.amazon.com/jp/lookout-for-metrics/features/)

* [Lookout for Equipment](https://aws.amazon.com/jp/lookout-for-equipment/)というのが製造業向けの異常検知として提供開始されたが、これを汎用化したもの。
* 購買トランザクション、顧客獲得率など時系列データ 
* ベストなAnomaly Detectアルゴリズムを自動で選定してくれる
* Amazon ConsoleやAPIからダッシュボードにアクセス可能


#### [Amazon HealthLake](https://aws.amazon.com/jp/healthlake/)

* ヘルスケアのデータは複雑だから分析をサポート
  - 電子カルテみたいなのをイメージすると分かりやすい。いろんなフォーマット, 型など。
* Store, Transform, analyze
* ペタバイトスケーリング
* GCPでもヘルスケアの分析サポートサービス出てたはず
* 公式ブログ: [Making sense of your health data with Amazon HealthLake](https://aws.amazon.com/jp/blogs/machine-learning/making-sense-of-your-health-data-with-amazon-healthlake/)


#### [Amazon SageMaker JumpStart](https://aws.amazon.com/jp/blogs/news/amazon-sagemaker-jumpstart-simplifies-access-to-prebuilt-models-and-machine-learning-models/)

* AWSが事前に用意したモデルのコレクションやMLワークフローをそのまま or カスタマイズして使える。
* SageMaker Studioから使う。
  - なんか今年のアップデートは特にStudioを意識したものが多い
* 単にnotebookが用意されているだけではなく、Cloud Formationで必要なリソースをデプロイしてくれる。
  - GCPの似たサービスでは[AI Hub](https://cloud.google.com/ai-hub/?hl=ja)というのがある。


## 個人的に気になったアップデートなど（加藤）

### サーバレス関連のアップデート内容

- Lambdaがコンテナイメージに対応
    - 今までzipでデプロイしていたのが、ECRのurlでデプロイできるイメージ
    - /tmp以外はRead-Onlyなどの要件あり
    - CDKにも対応
- Lambda Extentions
    - Lambda Extentions APIを使って実装したPGをLambda Layerとしてデプロイ
    - モニタリングツールなどの外部ツールをLambda実行環境内部に統合
    - Lambdaの実行ステップ

    ![kato/Untitled.png](kato/Untitled.png)

    - Extentionsが作用できる部分（緑色）

    ![kato/Untitled%201.png](kato/Untitled%201.png)

- Amazon CloudWatch Lambda Insights
    - Lambdaのパフォーマンスメトリクスとか使える
- イベントソースにApache KafkaとMQが追加
    - Apache Kafka：メッセージングサービス
    - MQ：同じく。
- AWS Signerを使ってLambdaのコード署名が可能に
    - コードが変更されてないことの確認
    - 自分でhashとかとらなくていい
- Lambdaの課金単位が100msから1msに
- Lambdaのメモリ上限が10GBに、vCPUの上限が6に拡張
- Runtime Interface Clients

    > Lambdaのパッケージフォーマットとしてコンテナイメージを利用する場合、コンテナイメージはLambdaのランタイムAPIと連携して動作する必要があります。このランタイムAPIとの連携を容易にするため、AWSからAWS Lambda Runtime Interface Clients (RIC)というツールが提供されます。

    - 【速報】Lambdaのパッケージフォーマットとしてコンテナイメージがサポートされるようになりました！！ #reinvent | [Developers.IO](http://developers.io/) [https://dev.classmethod.jp/articles/lambda-support-oci-container-image/](https://dev.classmethod.jp/articles/lambda-support-oci-container-image/)
- Runtime Interface Emulator

    > コンテナイメージのサポートに伴い、AWS Lambda Runtime Interface Emulator (RIE)というツールの提供が開始されます。RIEはローカル環境で実行可能な軽量ウェブサーバーで、受け付けたHTTPリクエストをLambdaのイベントデータと同じJSON形式に変換する機能を持ちます。RIEを導入したコンテナイメージをビルドすることで、ローカル環境でも簡単にLambda用コンテナイメージのテストが可能です。

    - 【速報】Lambdaのパッケージフォーマットとしてコンテナイメージがサポートされるようになりました！！ #reinvent | [Developers.IO](http://developers.io/) [https://dev.classmethod.jp/articles/lambda-support-oci-container-image/](https://dev.classmethod.jp/articles/lambda-support-oci-container-image/)
- SNSのFIFOトピックサポート
- SQSのFIFOキュー ハイスループットモード（プレビュー）

    ![kato/Untitled%202.png](kato/Untitled%202.png)

- SFのExpressモードの同期呼び出し

    ![kato/Untitled%203.png](kato/Untitled%203.png)

- AWS Amplify Admin UI
- AWS Proton
- AWS SaaS Boost

### 参考

- CM re:Growth 2020 Online 〜AWS re:Inventから見えるAWSの未来〜 #cmregrowth - YouTube [https://www.youtube.com/watch?v=9Hx9TyPa9gk&feature=youtu.be](https://www.youtube.com/watch?v=9Hx9TyPa9gk&feature=youtu.be)
- AWS Lambdaの裏側をなるだけ詳しく解説してみる - Sweet Escape [https://www.keisuke69.net/entry/2020/09/29/131203](https://www.keisuke69.net/entry/2020/09/29/131203)


## 告知

近日、podcast名を変更すると思います。
