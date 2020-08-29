---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#22 ピックアップニュース + Jetsonの話"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "クラウドにまつわる気になるニュースをピックアップ + ちょっとだけJetsonについての体験談を話したよ。"
abstract: "クラウドにまつわる気になるニュースをピックアップ + ちょっとだけJetsonについての体験談を話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-08-30T00:49:53+09:00
#date_end: 2020-08-29T13:34:53+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-08-29T13:34:53+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/Jetson-eir74i" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Note

## ピックアップニュース

### [AWS DEV DAY Online Japan](https://aws.amazon.com/jp/about-aws/events/2020/devday/)

* 2020/10/20（火）〜22（木）のオンライン開催。
* 多分developer寄りのセッションが多いイベント。
* Javaの生みの親James Goslingの登壇がある。

イベントと関係ないけど、[builders.flash](https://aws.amazon.com/jp/builders-flash/)なるメルマガ（Webマガ？）があることを知った。  
月イチでアップデート内容が送られてきたり、ハンズオン記事を試せるAWSクーポンがもらえたりするらしい。
[登録ページ](https://pages.awscloud.com/dev-magazine-mail-member.html)から登録できる。


### [IaaS型クラウドにおけるAWSのシェアは45％、Azureが18％で2位、3位はアリババ。2020年8月のガートナー調査（Publickey）](https://www.publickey1.jp/blog/20/iaasaws45azure182320208.html)

* **IaaS型クラウド** という枠組みではAWS, MS, Alibaba, Google, Tencentのシェア順
* Paasなどを含めると見慣れた順位になる（AWs, MS, Google,...）


### [トヨタとAWSが業務提携を拡大！モビリティサービス・プラットフォーム「MSPF」を強化（自動運転LAB.）](https://jidounten-lab.com/u_toyota-aws-mspf)

* いわゆるコネクテッドカーの基盤をAWSで。
* トヨタとAWSの連携が強化。
* トヨタは2016年頃、Azureと組んでいたらしい。


### [Docker Hubがコンテナイメージの保存期間に加えてPull回数にも上限を設定すると発表（Gigazine）](https://gigazine.net/news/20200826-docker-hub-update-policy/)

* 前回のpodcastでDocker Hubでinactiveなimageを6ヶ月で削除するという話をしたが、  
  無料プランではpull数の制限も加わるらしい。
  - 無料ユーザー(匿名)：6時間あたり100回まで
  - 無料ユーザー(登録済み)：6時間あたり200回まで
  - ProおよびTeamプランユーザー：無制限
* 一部のユーザが想定以上に大量のpullをしていることへの対処みたい。

関係ないけど[Github Packages](https://github.com/features/packages)というDocker Hubに似たレジストリサービスもあるらしい。  
無料枠だとちょっとサイズが少なめ。


### [Microsoft、「Azure Cosmos DB」のサーバレス価格モデルのプレビューを開始（@IT）](https://www.atmarkit.co.jp/ait/articles/2008/21/news042.html)

* フルマネージドNoSQL Azure Cosmos DBのサーバレス価格モデルをプレビュー開始。
* 事前にスループットをプロビジョニングするのではなく、使用した分だけ課金される。
  - [DynamoDBのオンデマンドキャパシティモード](https://aws.amazon.com/jp/dynamodb/pricing/)みたいなもの。
* バーストが小さかったり、開発途中のサービス、だったりがユースケースとのこと。


### [Google、クラウド型の専用ゲームサーバをリリース　Kubernetes環境で実行、大規模・多人数参加型ゲームの基盤に（ITmedia CLOUD USER）](https://www.itmedia.co.jp/news/articles/2008/25/news062.html)

* Google Cloud Game Serversという名前。
* ゲームサーバのマネジメントサービス。
* [Agones](https://cloud.google.com/blog/ja/products/gcp/introducing-agones-open-source-multiplayer-dedicated-game-server-hosting-built-on-kubernetes)というKubernetesで動作するゲームサーバのOSSがベースとなっている。
  - ゲームサーバのプロセスはステートフルだけど寿命が短い、ということでk8sが適している模様。


### [「脱クラウド」「オンプレミス回帰」を失敗させない2つの考慮点（ITmedia TechTarget）](https://techtarget.itmedia.co.jp/tt/news/2008/24/news04.html)

「時期や必要な専門知識の見極め」と「移行ツールの評価」が大事、らしい。以上。


### [「AWS Controllers for Kubernetes」(ACK)、AWSが公開。KubernetesからAWSのサービスを定義可能（Publickey）](https://www.publickey1.jp/blog/20/aws_controllers_for_kubernetesackawsawskubernetes.html)

* k8sから直接AWSのサービス（S3, SNS, SQS, DynamoDB, ECR, API Gateway）のリソースを定義できるようになる。
* 今までは「AWS Service Operator」というのがあったらしいが、これの後継となる。
* CFnを使わなくてもAWSリソースの管理ができるようになる。
* とりあえずディベロッパープレビューでの公開。


### [マイクロソフト、「Azure」などの障害情報提供を改善する取り組み（ZDNet）](https://japan.zdnet.com/article/35158420/)

* [グローバルなStatusページ](https://status.azure.com/ja-jp/status)ではなく、ユーザ個別に影響あるところを通知するようにするとのこと。
* 小規模でも自分のところに影響ある障害の通知がされることをユーザは求めている。


### [Google ドライブ・Gmailなどで発生した大規模障害の原因と対策をGoogleが説明（Gigazine）](https://gigazine.net/news/20200827-google-cloud-issue-summary/)

* 2020/8/19〜20にかけてGSuite, GCPで大規模障害が発生。  
  [障害レポート（PDF）](https://static.googleusercontent.com/media/www.google.com/ja//appsstatus/ir/bd9m3vkqwpvkk4j.pdf)が公開された。
* Googleの色々なサービスで共通のBLOB分散システムが使用されている。
  - トラフィックの増加によりメタデータサービスに負荷がかかった。
  - リトライや再起動のプロセスも雪だるま式に増加。
  - GCSは影響が小さかった。GCSはアメリカのマルチリージョン以外はメタデータレイヤーを他のサービスと分離されている。

関係ないけど[Googleのポストモーテムテンプレが紹介されているページ](https://rework.withgoogle.com/jp/guides/foster-an-innovative-workplace/steps/learn-from-failures/)があったので貼っておく。


## Jetsonを触っている話

* 最近[Jetson AGX Xavier](https://www.nvidia.com/ja-jp/autonomous-machines/embedded-systems/jetson-agx-xavier/)を使っている。
* ARMアーキテクチャでのビルドつらい話。
  - 多分Cloud Buildなど別環境でビルドした方がいい。  
    参考: [クラウド上でARM用コンテナをビルドする](https://note.com/kikuzokikuzo/n/na2e82c1c8835)
* Jetsonでnginx経由のtensorflowを使うときは注意が必要。
  - おそらくARM版のnginx実装の影響か、モデルロード時とpredict実行時にsessionが分かれてしまう。  
    そのため、明示的にsessionを同じものを使うよう実装しないと動かない。
