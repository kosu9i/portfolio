---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#14 【AWS】Well-Architected"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "小杉がAWS Well-Architectedについて話したよ。"
abstract: "小杉がAWS Well-Architectedについて話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-06-08T00:39:00+09:00
#date_end: 2020-06-06T16:43:02+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-06-06T16:43:02+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/AWSWell-Architected-ef3v8t" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# 話したこと

## 概要

[AWS Well-Architected](https://aws.amazon.com/jp/architecture/well-architected/)というものがある。  
要はAWSで最適なアーキテクチャを構築するためのガイドラインを体系的にまとめたもの、という感じ。

* 今構築しているアーキテクチャが最適なのか？
* これから構築するシステムにふさわしいAWSサービス・アーキテクチャは？

などに対応したいときに活用できそう。

ざっくりした構成は以下。

* [Well-Architectedフレームワーク](https://d1.awsstatic.com/whitepapers/ja_JP/architecture/AWS_Well-Architected_Framework.pdf?sc_icampaign=aware_well_architected_jp_wa_framework&sc_ichannel=ha&sc_icontent=awssm-3366&sc_iplace=content&trk=awssm-3366_aware_well_architected_jp_wa_framework)
  - Well-Architectedについての概要をまとめたドキュメント。
  - 最初にざっと読むもの。ただ、多分抽象的すぎて具体的なイメージは沸きづらい。
  - 5つの柱（後述）について概要が書いてある。各柱にもさらに詳細化したホワイトペーパーがある。
* [Well-Architected Tool](https://aws.amazon.com/jp/well-architected-tool/)
  - Well-Architectedに基づいているかどうかをチェックするツール。
  - 自動チェックをしてくれるとかではなく、質問に答えていくチェックリストみたいなイメージ。
* Well-Architected レンズ
  - 適用領域（例：サーバレス、HPC、IoTなど）ごとに詳細化されたホワイトペーパーがある。
  - 結構具体的（各サービスの仕様詳細までは書かれてないので別途チェックが必要だが）なので  
    各領域のアーキテクチャを考える際にはある程度参考になりそう。  
    個人的にはWell-Architectedを活用する際にはこれを見るべし、と感じる。
* その他
  - [トレーニング](https://www.aws.training/Details/Curriculum?id=12033)
    - E-learning。動画に表示される資料は日本語化されてるけど、音声は英語。
    - 大体全部で2時間くらい。
    - 無料。
  - [AWSソリューション](https://aws.amazon.com/jp/solutions/)
    - AWSを利用したアーキテクチャの事例集。
    - 各事例のドキュメント、CloudFormation template、ソースコード、がセットになっている。
    - かなり多くの事例が載っており、超勉強になりそう。

全体的に初心者が取り組んでも具体的なイメージが沸かないし、対処も厳しいと思う。（自分のことを言っている）  
なので、技術マネージャーとかがAWSアーキテクチャを俯瞰してチェックしたいときなどに活用するものと理解している。  

## Well-Architected フレームワーク

Well-Architectedの骨子となるドキュメント。（PDFは[ここ](https://d1.awsstatic.com/whitepapers/ja_JP/architecture/AWS_Well-Architected_Framework.pdf?sc_icampaign=aware_well_architected_jp_wa_framework&sc_ichannel=ha&sc_icontent=awssm-3366&sc_iplace=cta&trk=awssm-3366_aware_well_architected_jp_wa_framework)）  
90ページ弱あるが、基本の部分は最初の半分くらい。  
残りの後半は後述のWell-Architected Toolでチェックされる質問集とそれに対するベストプラクティスが記載されており、正直これらは読んでもよく分からない気がする...（日本語も分かりづらい）  
この後半をマジメに読むくらいなら、後述の[Well-Architected Tool](https://aws.amazon.com/jp/well-architected-tool/)を実際に使ってみたら良いと思う。

Well-Architecteフレームワークは以下の5つの柱で構成されている。

* 運用上の優秀性
* セキュリティ
* 信頼性
* パフォーマンス効率
* コスト最適化

ぶっちゃけ内容はざっくりしすぎていて、具体的なイメージは湧きづらい。  
AWSをある程度触ってみてから、知識を体系的にまとめたいときに読むと良いかも。  
また、AWS初心者でも最初に読むと「AWSってこういう感じで使うのか」の感覚は伝わるかもしれない。（ご多分に漏れず、AWSドキュメント特有の用語群につまづく可能性は大）

誤解を恐れずに超絶簡素にまとめると、  
「**CloudFormation, IAM, CloudWatch, Auto Scaling, マネージドサービスをちゃんと使えよ**」になると思う。（これらのサービス名が随所に出てくる）

もし初心者がこれらを手っ取り早く習得したい場合、超絶おすすめなのが
[Architecting on AWS](https://aws.amazon.com/jp/training/course-descriptions/architect/)の研修を受けること。  
お値段は高い...20万くらいする。  
個人的に出費するのは大変だが、会社負担で研修を受けられる企業はあると思うし、費用の価値は十分にあると思う。  
[APN](https://aws.amazon.com/jp/partners/apn-partner-central/)に参加している企業に勤めていたら半額以上の割引キャンペーンが行われることもあるので要チェック。  
3日間のトレーニングで、AWSのアーキテクチャをハンズオンありで学んだ後、Well-Architectedについても学習するので知識の定着度が高い。オススメできる数少ない研修だと思う。  
ちなみにこの研修は[AWS認定ソリューションアーキテクト - アソシエイト](https://aws.amazon.com/jp/certification/certified-solutions-architect-associate/)の資格対策としても代表的なものであるし、資格受験用のバウチャー付きコースもあったはず。


## 蛇足：そもそもなんでクラウド使うの？

少し蛇足で何を今更という話を...

「なんでクラウド？」に対して、これも超絶誤解を恐れずに言うと「落ちないシステムを構築するため（落ちないとは言ってない）」だと思っている。  
（※個人の見解）  
当然オンプレで落ちないものを構築できないという意味ではないし、クラウドを使えば落ちなくなるという意味でもない。  

Twitterの「バルス」祭りを思い浮かべると分かりやすいが、急激なスパイクが起こり得るサービスで  
その最大値に合わせたシステムを物理的に構築しようとすると、あらかじめ膨大な数のマシンを用意する必要がある。  
また、それらのマシンは平常時には供給過多となり無駄なコストである。  
代わってクラウドのインフラストラクチャを使えば「必要なときに必要なだけ使える」という特性を活かし、過負荷に耐えうるシステムを**現実的なコストで**構築可能である。

もちろんシステムが落ちる原因は過負荷だけではない。  
データの消失、ネットワークダウン、セキュリティの穴など様々あるが  
これらの対処も物理的に冗長化するより**現実的なコストで**、 クラウドで構築できることが多いと思う。

まぁいくら**現実的なコスト**とは言っても、その見極めは難しく  
コスト以外にもシステムにはいろいろな問題が介在するため  
実際にはクラウド使っておけば良いという話ではないのは、言うまでもないが...  
~~そんなこんなで今日もどこかのクラウドシステムが落ちている。~~


閑話休題、そんな落ちないシステムアーキテクチャをAWSで構築するためのガイドラインがWell-Architectedであると言える。


## Well-Architected Tool

[Trusted Advisor](https://aws.amazon.com/jp/premiumsupport/technology/trusted-advisor/)みたいに自動で各チェックをしてくれるようなものではなく、  
手動で質問に答えていって、チェックリストを作るもの。

よく日本の大企業で、幹部の承認を得るために「セキュリティチェックリスト」みたいなの作ると思うけど、それのAWS版って感じ。  
~~リストをExcelで管理し、[「ヨシ！」](https://twitter.com/karaage_rutsubo/status/1157112554910437377?s=20)が蔓延り、形骸化待ったなしのリストを作るよりは1000倍良いと思われる。~~

* システムの技術的要素というよりは、「プロジェクトとしてちゃんとこの辺意識しているか？」を問われるものが多い。
* 日本語対応している。が、分かりづらい...。一応、詳細の補足情報はあるので何とか分かる。
* 質問が結構ある。途中で保存してやめられる。
* 最終的にスコア化される。メンテナンスして改善したらスコアもあがってく。
* リスクの高い未チェック項目については、アラートが表示される。  
  それに対する対応案（CloudWatchとかConfig使ったらええで、とか）が列挙されたドキュメントにも飛べる。
* レポートとしてエクスポートも出来る。

{{< figure src="tools-dashboard.png" title="Well-Architected Tool例" numbered="true" lightbox="true" >}}


## Well-Architected レンズ

適用領域ごとにホワイトペーパーが用意されている。  
前述のフレームワークやToolは抽象的なチェックをするためのものだと感じるが、  
レンズは少し具体的になっており、実際に使えるホワイトペーパーという感じがする。  
「○○なシステム組みたいけど、使えそうなAWSサービス・アーキテクチャはどんなんだ？」というときに読むと良さそう。

2020年6月現在、提供されているのは以下。（PDF資料にリンクしている）  

* [サーバーレスアプリケーション](https://d1.awsstatic.com/whitepapers/ja_JP/architecture/AWS-Serverless-Applications-Lens.02.10.2020.pdf)
* [ハイパフォーマンスコンピューティング (HPC)](https://d1.awsstatic.com/whitepapers/architecture/AWS-HPC-Lens.pdf)
* [IoT (モノのインターネット)](https://d1.awsstatic.com/whitepapers/architecture/AWS-IoT-Lens.pdf)
* [機械学習](https://d1.awsstatic.com/whitepapers/architecture/wellarchitected-Machine-Learning-Lens.pdf)
* [金融サービス](https://d1.awsstatic.com/whitepapers/architecture/wellarchitected-Financial-Services-Industry-Lens.pdf)
* [分析](https://d1.awsstatic.com/whitepapers/architecture/wellarchitected-Analytics-Lens.pdf)

PDF版とKindle版の資料リンクがある。  
サーバレスアプリケーションだけ日本語対応しており、あとは全部英語。

ちなみにサーバレスのレンズについては、前述のWell-Architected Toolのチェックリストにも組み込むことができるようになっている。（参考: [AWSブログ](https://aws.amazon.com/jp/blogs/news/new-serverless-lens-in-aws-well-architected-tool/)）


## まとめ

ここまで書いておいて何だが、Well-Architectedは利用必須なものではないと思う。  
AWSと長く付き合っていくうえで、たまにこういうのがあったなと思い返し読んでは  
自分の構築したアーキテクチャを見直してみると、何らかの反省や新しい発見があるかもしれない。

また、Well-ArchitectedはAWS利用前提で書かれたドキュメントであるが  
その根底にある考え方は他ベンダのクラウド（GCP, Azureなど）でも使えるし  
ひいてはオンプレミスだろうが役に立つものだと思うので、どこかで一読しておいても損はないと思った。

あと[AWSソリューション](https://aws.amazon.com/jp/solutions/)良さそうだから、ちゃんと利用しよう。
