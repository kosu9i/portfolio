---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#27 Coming Soon"
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
date: 2020-10-17T15:20:18+09:00
#date_end: 2020-10-17T15:20:18+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-10-17T15:20:18+09:00

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


## [AWS Dev Day Online Japan](https://aws.amazon.com/jp/about-aws/events/2020/devday/)

基調講演とワークショップに参加した。

* 基調講演あつかった。6人とも素晴らしい人達で、共通して情熱と視野の広さを感じた。
  - 複数のスキルの掛け算みたいな話が示し合わせたように出ていて共感。
* オンラインのセッションはライブ感がないので、対話形式の基調講演はとても良かった。  
  視聴者からの質問をトークに交えていたのも良かった。
* 通訳の人すごい。  
* 普段Twitterでよく見ているAWS Japanの人たちの人となりが分かってよかった。
* アンケートに回答するとアーカイブへのリンクをもらえるらしい。


## [Amazon SageMaker が今後も機械学習のトップランナーであり続けることの宣言と、GPU インスタンス料金の最大 18% 引き下げのお知らせ](https://aws.amazon.com/jp/blogs/news/amazon-sagemaker-leads-way-in-machine-learning/)

* 2017年にSageMakerがリリースされ、様々な業界で利用されてきた。  
  「SageMaker によって、機械学習プロセスの各ステップから差別化につながらない負担の大きな作業が排除されます。」
* SageMakerの貢献度が高い5項目
  - 安全かつ信頼性の高い機械学習モデルの構築が高速化する
    - スケーラブルな推論API, Model Monitorなど
  - 機械学習モデルを独自の方法で構築する
    - 組み込み or 独自アルゴリズムの選択, AutoPilot, 自動パラメータチューニングなど
  - コストを削減する
    - 学習ジョブ, 推論APIをマネージドな環境で構築可能
    - Batchなど他のサービスのほうがインスタンス料金は低いが、SageMaker SDKの利用などにより開発・メンテナンスコストは抑えられるはず（個人の見解）
  - セキュアかつコンプライアントな機械学習システムを構築する
    - 一般的なAWSのセキュリティポリシーと同様のことを言っていると思われる（個人の見解）
  - データに注釈を付け、ヒューマンインザループを維持する
    - Ground Truth
* GPUインスタンス料金の引き下げ!!
  - 下記の通り（p2はK80, p3はV100。p3のスペックは[こちら](https://aws.amazon.com/jp/about-aws/whats-new/2019/10/introducing-amazon-sagemaker-mlp3dn24xlarge-instances/)）
    - ml.p2.xlarge	-11%
    - ml.p2.8xlarge	-14%
    - ml.p2.16xlarge	-18%
    - ml.p3.2xlarge	-11%
    - ml.p3.8xlarge	-14%
    - ml.p3.16xlarge	-18%
    - ml.p3dn.24xlarge	-18%
  - SageMakerのインスタンス料金表は[こちら](https://aws.amazon.com/jp/sagemaker/pricing/)
  - [GCP AI PlatformのGPU利用料金](https://cloud.google.com/ai-platform/training/pricing?hl=ja)のほうが半額近く安い。  
    ただ、SageMakerはスポットインスタンスが使うとかなり安くなる。
  

## [AmazonがECSでEC2 Inf1インスタンスのサポートを発表（InfoQ）](https://www.infoq.com/jp/news/2020/10/amazon-ecs-ec2-inf1/)

* 機械学習の推論に特化した[inf1インスタンス](https://aws.amazon.com/jp/ec2/instance-types/inf1/)というのがあり、それがECSで利用可能に。
* GPUではない。独自のInferentiaと呼ばれるチップを採用。
* 確かに安い。速度測定して使えそうなワークロードは移行して良いかも。
* [AWS Neuron SDK](https://github.com/aws/aws-neuron-sdk)というものでモデルをコンパイルする必要あり。


## [AWS、独自開発したARMベースの「Graviton 2」プロセッサを、「Amazon ElastiCache」のデフォルトプロセッサに（Publickey）](https://www.publickey1.jp/blog/20/awsarmgraviton_2amazon_elasticache.html)

ElasticCacheでGraviton 2が採用。

> マネージドサービスであれば、ユーザーにとってちゃんとサービスが動いてくれさえすればプロセッサは何が使われていても気にしません。より安く使えればそれでよいのです。それが、Amazon ElastiCacheでGraviton 2プロセッサをデフォルトにした理由でしょう。

うむ。


## [Google、最適化されたコンテナイメージを生成する「buildpacks」をオープンソースで公開。Dockerfile不要でJavaやGo、Node.jsをコンテナへビルド（Publickey）](https://www.publickey1.jp/blog/20/googlebuildpacksdockerfilejavagonodejs.html)

* Dockerfile不要でDockerイメージが作れるツールをOSSで公開。
* GCPではCloud Run, Anthos, GKEで利用可能。
* もともとはHerokuが開発・利用していたものがCNCFで採用。
* Googleが[公開](https://github.com/GoogleCloudPlatform/buildpacks)
* Go、Java、Node、Python、.NETに対応。バージョンは[こちら](https://github.com/GoogleCloudPlatform/buildpacks#general-builder-and-buildpacks)を参照。
* buildpacksのイメージ, コンテナを[拡張することもできるっぽい](https://github.com/GoogleCloudPlatform/buildpacks#extending-the-run-image)。


## [KubernetesのPodやネットワークをわざと落としまくってカオスエンジニアリングのテストができる「Chaos Mesh」がバージョン1.0に到達（Publickey）](https://www.publickey1.jp/blog/20/kubernetespodchaos_mesh10.html)

* k8sクラスタの一部に障害を起こすテスティングツール。
* Netflixが開発。Netflixは本番環境に対してこれを適用している。
* AWS上で障害を発生させる[Chaos Monkey](https://www.publickey1.jp/blog/12/chaos_monkeynetflix.html), [Chaos Kong](https://www.publickey1.jp/blog/15/chaos_kongnetflix.html)というツールもある。
* ちょっと最近クラウドの障害が目立つので、良いプロダクトかも。


## [日本マイクロソフト、ニューノーマル時代のDX支援プロジェクト「Azure Base」をスタート（クラウドWatch）](https://cloud.watch.impress.co.jp/docs/news/1282972.html)

* [AWS Loft](https://aws.amazon.com/jp/start-ups/loft/tokyo/)のAzure版と言えそう。
* 全国10箇所に展開。
* インターネット上に「Vitual Azure Base」も開発中。12月にリリース予定。
> 10拠点のうち、Daikanyama Base（代官山）、Osaka Base（大阪）、Saga Base（佐賀）の3拠点が日本マイクロソフト直営。Sapporo Base（札幌）、Kanazawa Base（金沢）、Seaside Base（芝浦）、Yokkaichi Base（四日市）、Kobe Base（神戸）、Fukuoka Base（福岡）、Okinawa Base（沖縄市）の7拠点がパートナーによって運営される。
> 2021年春ごろには、Hiroshima Base（広島）とIse Base（伊勢）の2拠点もオープンする予定。


## [クラウド政府共通基盤が稼働、AWSが日本政府に食い込めた真相（日経XTECH）](https://xtech.nikkei.com/atcl/nxt/column/18/00001/04732/)

> 総務省が構築した中央省庁向けの「第2期政府共通プラットフォーム」がAWSのパブリッククラウド上で運用開始されたと発表

AWSパブリックセクターが2017年から提案を開始。大きく2つの壁があった。

> よく言われるのは、AWSのような外資系企業に政府システムを委ねるには、セキュリティーや国家安全保障の観点が採用の壁になるという考え方だ。とはいえ「中央省庁では外部のITベンダー出身で、パブリッククラウドに触れたことがあるCIO補佐官が活動するようになっている。クラウドに対する心理的な抵抗感は徐々に薄れていた」（宇佐見執行役員）

また、事前に費用を確定（「5年間のシステム提供一式で◯億円」など）する慣行があった。  
これはクラウドの従量課金体系と相容れない。

> これについて、AWSやパートナー企業、政府の間で検討を重ね、「単価契約」方式を採ることにした。AWSと政府の間にAWSサービスを再販するパートナー企業が入る。パートナー企業は「AWSの仮想マシンの定価は1カ月1台当たり◯円だが、手数料や大量購入割引のために◯％の割増・割引をする」として決めた単価を提示する。

> AWSジャパンの宇佐見執行役員は「使った分しかお金がかからないのはクラウドのメリットそのもの。我々としては、これだけ売上高が上がるはずだという皮算用をしているわけではない」と余裕を見せる。一方で、固定価格のシステム販売という官需で安定的な売り上げを得てきた日本のITベンダーにとって、パブリッククラウドの従量課金に順応するのは大変かもしれない。

工程管理をNTTデータ, プラットフォームの運用管理はNEC, 調達とコスト精算は日立システムズが担当。  
（参考: [日本政府、AWSベースの情報システム基盤を運用開始　デジタルシフトの起爆剤になるか（ITmedia）](https://news.yahoo.co.jp/articles/6e4f8cb821628ea043f49a5ebebf93d642f02361)）

東京と大阪のマルチリージョンで運用を計画しているっぽい。
