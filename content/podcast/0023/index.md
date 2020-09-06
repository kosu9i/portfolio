---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "0023"
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
date: 2020-09-06T21:26:00+09:00
#date_end: 2020-09-06T21:26:00+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-09-06T21:26:00+09:00

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
であれば、クラウドのような利用形態がしばらくは主流になることは間違いなさそう。


### [AWS、コンテナ実行に最適化したLinux OS「Bottlerocket」正式版リリース（Pulickey）](https://www.publickey1.jp/blog/20/awslinux_osbottlerocket.html)

* コンテナ実行に特化したLinuxベースのコンテナホスト用OS。
* セキュリティが重視されている。ブート時の自己整合性チェックや、SELinuxのアクセス制御など。
* 現在はEKS, ECSで利用可能。
* [Githubにて公開中](https://github.com/bottlerocket-os)。

参考公式ブログ:
* [Bottlerocket – コンテナホスティング用オープンソース OS](https://aws.amazon.com/jp/blogs/news/bottlerocket-open-source-os-for-container-hosting/)
* [Bottlerocket: 特定目的のコンテナオペレーティングシステム](https://aws.amazon.com/jp/blogs/news/bottlerocket-a-special-purpose-container-operating-system/)


### [EKSおよびAWS Fargateで実行されているコンテナがAmazon Elastic File Systemを使用できるようになった（InfoQ）](https://www.infoq.com/jp/news/2020/09/aws-fargate-amazon-efs/)

タイトル通り。データ永続化に便利かも。


### [グーグル、「Cloud AI」を拡充--コンタクトセンターや文字認識、MLOps向け機能を強化（ZDNet）](https://japan.zdnet.com/article/35159135/)

Cloud AIが色々拡充。多分Cloud Next OnAirで発表もされている。

* [Contact Center AI](https://cloud.google.com/solutions/contact-center)
  - 対話のDialogflow
  - 音声認識や音声合成を組み合わせてコンタクトセンターを自動化
  - 関連: [Google Cloudで企業が独自の合成音声の作成が可能に](https://jp.techcrunch.com/2020/09/03/2020-09-01-google-cloud-lets-businesses-create-their-own-text-to-speech-voices/)
* [AI Platform](https://cloud.google.com/ai-platform)
  - MLOps向け機能を強化
  - Continuous Monitoring（モデルパフォーマンスの監視）を2020年末までに利用可能になる見込み


### [Google Cloud Healthcare APIが一般利用可能に（InfoQ）](https://www.infoq.com/jp/news/2020/08/google-healthcare-api-ga/)

* [Cloud Healthcare API](https://cloud.google.com/healthcare)がGAに
* ヘルスケアのサービスはAWSやAzureでもあるらしい。
* `HL7、FHIR、DICOMなどの主要なヘルスケアデータタイプを取り込んで管理するための堅牢でスケーラブルなインフラストラクチャソリューション` らしい。


### [Google Cloud、「Google Cloud App Modernization Program（CAMP）」を発表（@IT）](https://www.atmarkit.co.jp/ait/articles/2009/03/news062.html)

* 以下の3本柱でモダナイゼーションを支援
  - データドリブンの評価とベンチマーク
  - 最新でなおかつ拡張可能なプラットフォーム
  - 実績のあるプラクティス、ソリューション、レコメンデーション
* [公式ブログ](https://cloud.google.com/blog/ja/products/application-development/google-camp-shows-you-how-to-operate-at-scale)も参照


### [Google Cloud Anthos Day](https://cloudonair.withgoogle.com/events/gc-solution-event-anthosday-4)

ライブ配信日時：2020 年 10 月 8 日（木）11:00 - 18:30


## Cloud Runアップデート

[Cloud Next OnAir](https://cloud.withgoogle.com/next/sf/sessions?session=SVR224-JP#cloud-ai)でのセッションでCloud Runのアップデートが色々あり、よさそうだった。

* Enterprise対応強化
  - Blue/Greenデプロイの機能強化
  - マルチリージョンロードバランシング
  - VPCアクセス
  - Cloud CDN, Identity Aware Proxy, Cloud Armorなど対応
* Developerのための機能強化
  - Infrastructure as Codeが強化
  - Cloud Buildpacks
    - コードだけデプロイすれば良い。Lambdaのコンテナ版みたいな感じ？
  - Events for Cloud Run
    - イベントトリガーが増えた
  - Cloud Workflows
    - Step Functionsみたいな感じ？
* 今後のロードマップ
  - RAMが最大4GB, 最大4CPUに増加
  - リクエストタイムアウトが1時間に増加
  - 最小インスタンスを指定可能に。
    - コールドスタートを防止
  - SIGTERMのエラーハンドリング
    - エラー処理時にCPUが最大10秒割り当てられる
  - gRPCサポート
  - サーバサイドストリーミング

