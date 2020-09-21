---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#24 Coming Soon"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "Coming Soon"
abstract: "Coming Soon"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-09-21T18:00:16+09:00
#date_end: 2020-09-21T18:00:16+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-09-21T18:00:16+09:00

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

# Show Note

## ピックアップニュース

### [EKSおよびAWS Fargateで実行されているコンテナがAmazon Elastic File Systemを使用できるようになった（InfoQ）](https://www.infoq.com/jp/news/2020/09/aws-fargate-amazon-efs/)

- タイトル通り。データ永続化に便利かも。
  - S3やDynamoDBなど他のデータ格納サービスを利用せず、ファイルシステムとしてマウントしたい場合。
- 今まではEC2のワーカーノード経由でEFSを利用できたが、これからはKubernetes APIを利用して直接EFSを利用可能。


### [Microsoftの量子コンピューティング環境「Azure Quantum」登場（ITmedia）](https://techtarget.itmedia.co.jp/tt/news/2008/28/news01.html)

* AWSに続き、Azureでも量子コンピューティングのクラウド利用をプレビュー版で提供開始。
* [Azure Quantum](https://azure.microsoft.com/ja-jp/services/quantum/)
* QDK（Quantum Development Kit）というSDKと新言語Q#がGithubで公開。  
  参考: [Q# プログラミング言語と QDK とは](https://docs.microsoft.com/ja-jp/quantum/overview/what-is-qsharp-and-qdk)


### [実現されつつあった「量子コンピュータ」は、放射線によって機能が制限されると判明（ナゾロジー）](https://nazology.net/archives/67684)

* 量子コンピュータでは「量子もつれ」を維持する時間が大事になってくる。
* 「量子もつれ」が宇宙放射線をはじめとした環境放射線により深刻な影響を受けやすい。  
  MITがこの影響を調査。
* 調査結果として、地球の地表においては4マイクロ秒が量子もつれの状態維持の限度であることが分かった。
  - 計算上は200マイクロ秒の維持が可能
  - これを避けるには2トンの鉛で覆う（実験と同じ条件下）か地表奥深くに埋めるしかない。

なんの事やらさっぱり分からんが、とにかくデリケートである、と...  
であれば、量子コンピューティングはクラウドのような利用形態がしばらく主流になりそう。


### [Google Cloud Healthcare APIが一般利用可能に（InfoQ）](https://www.infoq.com/jp/news/2020/08/google-healthcare-api-ga/)

* [Cloud Healthcare API](https://cloud.google.com/healthcare)がGAに
* ヘルスケアのサービスはAWSやAzureでもあるらしい。
* `HL7、FHIR、DICOMなどの主要なヘルスケアデータタイプを取り込んで管理するための堅牢でスケーラブルなインフラストラクチャソリューション` らしい。


### [Google Cloud、「Google Cloud App Modernization Program（CAMP）」を発表（@IT）](https://www.atmarkit.co.jp/ait/articles/2009/03/news062.html)

* 以下の3本柱でモダナイゼーションを支援
  - データドリブンの評価とベンチマーク
    - 評価方法を提供？Google社員が評価をしてくれる、とかではないと思われ。
  - 最新でなおかつ拡張可能なプラットフォーム
    - GCPの各種サービス（特にコンテナ関連。GCR, Cloud Build, GKE, Cloud Run, Anthosなど）のことを指していると思われ。
  - 実績のあるプラクティス、ソリューション、レコメンデーション
    - GCPのベストプラクティスをまとめたもの？
* [公式ブログ](https://cloud.google.com/blog/ja/products/application-development/google-camp-shows-you-how-to-operate-at-scale)も参照
* AWSのWell Architected FrameworkのGCPアプリケーションモダナイゼーション版、と理解。


### [Google Cloud Anthos Day](https://cloudonair.withgoogle.com/events/gc-solution-event-anthosday-4)

ライブ配信日時：2020 年 10 月 8 日（木）11:00 - 18:30


### [ソフトバンクが約4兆2000億円でArmをNVIDIAに売却（Gigazine）](https://gigazine.net/news/20200914-nvidia-arm-softbank/)

大変話題に。

NVIDIAはArmの中立性を守ると宣言しているがどうなるか。

[NvidiaによるArm買収の分かりやすい解説](https://www.axion.zone/explanation-of-nvidia-and-arm-deal/)という記事が読み応えもありわかりやすかった。おすすめ。  
この記事の著者[Takushi Yoshidaさん](https://www.axion.zone/author/yoshi/)は他にもこの界隈の記事を書いているので、時間があるときに読みたい。  
[AWS Gravitonに関する記事](https://www.axion.zone/aws-gravitontoha/)も書かれており、よさげ。


### [年収1000万円超えが狙える「クラウドエンジニア資格」とは？（TechTarget）](https://techtarget.itmedia.co.jp/tt/news/2009/12/news01.html)

> 北米で高い給与の獲得を見込める上位10個のIT資格のうち、4資格はクラウド関連だった。1位はGoogleの認定資格である「Professional Cloud Architect」で、保持者の平均年収は15万2129ドル（約1615万円）だった。Amazon Web Services（AWS）の認定資格である「AWS Certified Solutions Architect - Associate」「AWS Certified SysOps Administrator - Associate」「AWS Certified Developer - Associate」の3種類は、約13万ドル（約1380万円）の年収に結び付く。

え...？という感じ。  
もしかして...日本の年収、低すぎ？


### [クラウドデータウェアハウスのSnowflake、上場初日の株価が急騰（ZDNet）](https://japan.zdnet.com/article/35159735/)

人気のDWH、Snowflakeが上場。


### [Google Cloud API Gateway の公開ベータ版がリリース](https://cloud.google.com/blog/ja/products/serverless/google-cloud-api-gateway-is-now-available-in-public-beta)

[Cloud Endpoints](https://cloud.google.com/endpoints?hl=ja)との違いがわかっていない...  
基本的にはCloud Endpointsの後継となるという話もどこかで聞いたなレベル。


## Cloud Runアップデート

[Cloud Next OnAir](https://cloud.withgoogle.com/next/sf/sessions?session=SVR224-JP#cloud-ai)でのセッションでCloud Runのアップデートが色々あり、よさそうだった。

* Enterprise対応強化
  - GAでSLA 99.95%
  - VPCアクセス
    - VPCの中にあるプライベートバックエンドサービスに接続できるようになった。
  - Gradual Rollouts & Rollback
    - Blue/Greenデプロイの操作をgcloudコマンドから実行可能。
  - [Cloud Artifact Registry](https://cloud.google.com/artifact-registry?hl=ja)のサポート
    - Artifact Registryとは、Countainer Registryの進化系。より細かいアクセス制御が可能、など。
  - マルチリージョンロードバランシング
    - Cloud CDN
      - Cloud RunからCache-Controlヘッダ（キャッシュの生存期間など）を指定してレスポンス。
    - Identity Aware Proxy
      - IAMでHTTPレイヤのアクセス制御
    - Cloud Armor
      - DDoS防御やIPでのファイアウォール
* Developerのための機能強化
  - Infrastructure as Codeが強化
    - yamlでデプロイ
  - Cloud Codeインテグレーション
    - VS Code, IntelliJなどIDE拡張
  - Cloud Buildpacks
    - Dockerfileなしでコードだけデプロイすれば良い。Lambdaのコンテナ版みたいな感じ。
    - Go, Node.js, Python, Java, .NET Coreに対応。
  - ソースコンテキスト
    - コンテナのメタ情報（CPUの数や開放しているポートなど）を表示
  - CI/CDのUIがコンソールに追加
    - Cloud Buildとの連携がしやすくなった。
  - Events for Cloud Run
    - イベントトリガー（GCSのアップロード、Pub/Sub、Audit loggingなど）が増えた。
    - CNCF準拠のため、移行も楽そう。
  - Cloud Workflows
    - Step Functionsみたいな感じ。
* 今後のロードマップ
  - リソース上限が増加（RAM 4GB, 4CPU）
  - リクエストタイムアウトが1時間に増加。
  - スケールアウト時の最小インスタンスを指定可能に。
    - コールドスタートを防止できる。
  - SIGTERMのエラーハンドリング
    - エラー処理時にCPUが最大10秒割り当てられる。
  - gRPCサポート
  - サーバサイドストリーミング
    - ストリーミングレスポンスを返すことができるようになる。
