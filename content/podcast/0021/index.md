---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#21 "
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: ""
abstract: ""

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-08-22T15:03:51+09:00
#date_end: 2020-08-10T15:03:51+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-08-10T15:03:51+09:00

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

Coming Soon...

# Show Note

全部は話さないと思う。台本的に以下に列挙。


## [Amazonが量子コンピューティングサービス「Amazon Braket」の一般提供を開始（Gigazine）](https://gigazine.net/news/20200814-aws-general-availability-amazon-braket/)

* AWSの量子コンピューティングサービスAmazon BraketがGAに。
* D-Wave, IonQ, Rigettiが使える。
  - 利用可能な時間帯が決められている。
* [Amazon Braket Python SDK](https://github.com/aws/amazon-braket-sdk-python)がOSSで提供されている。
* [日本語のチュートリル的なブログ](https://aws.amazon.com/jp/blogs/news/amazon-braket-go-hands-on-with-quantum-computing/)もあるので、とりあえず触るにはこれを読むと良いかも。
* [料金に関するページ](https://aws.amazon.com/jp/braket/pricing/)を見たが、安いのか高いのか、ショットってなんだ、と全く分からん。まぁでも従量課金というのはAWSの他のサービスと同じ感覚で使えて良い。
* データ管理やログもAWS内で完結するのも強み。

量子コンピュータ、さっぱり分からないがAWSで使えるということで敷居が下がった感。  
D-Waveとか名前は知っていたものの、どこでどうすれば利用できるのかすら分からなかったので...


## [BigQuery がテーブルレベルのアクセス制御に対応（Google Cloudブログ）](https://cloud.google.com/blog/ja/products/data-analytics/introducing-table-level-access-controls-in-bigquery)

* 今まではデータセットまでしか細かい単位でACLが提供されていなかったが、テーブルにも対応。
* 今までは[承認済みビュー](https://cloud.google.com/blog/ja/products/data-analytics/introducing-table-level-access-controls-in-bigquery)というものを使ってテーブルへの読み取り専用権限を付与していたが、やや煩雑。（別のデータセットを用意しないといけない、とか）  
  これからはテーブルACLを使える。

細かい挙動について、わかりやすく検証してくれているブログ（Developers.IO）が[こちら](https://dev.classmethod.jp/articles/bigquery-table-acl-confirm/)


## [Docker Hub の新しいコンテナ・イメージ保管ポリシー（参考訳）（Qiita）](https://qiita.com/zembutsu/items/e92a2e2f46b147e5a206)

* Docker HubのFreeプランでは、6ヶ月間Inactiveなイメージが削除されるとのこと。2020年11月から。
* 古いイメージを残しておきたければプランをアップグレードしよう。
* Inactiveとは、push, pullがされていない状態のことらしい。


## [Oracle Cloud VMware Solution」正式リリース。他社との違いは、オンプレミスと同様にユーザーが管理できること](https://www.publickey1.jp/blog/20/oracle_cloud_vmware_solution.html)

* Oracle Cloud上でVMware環境を利用するサービスを正式リリース。
* AWS, Azure, GCPともにVMwareのフルマネージド環境は提供しているが、これとの違いは「フルマネージドではないこと」らしい。  
  つまり、自分たちでパッチ適用しないといけないが、その分オンプレミスのVMware環境との親和性が高くなるはず。

## [AWS、「Graviton2」搭載の「Amazon EKS」インスタンスを一般提供（ZDNet）](https://japan.zdnet.com/article/35158281/)

* EKSでもGraviton2が使えるようになった。
* x86系のインスタンスと比べて約20%安価とのこと。
* EC2では[一般用途M6g](https://aws.amazon.com/jp/ec2/instance-types/m6/), [コンピューティング最適化C6g](https://aws.amazon.com/jp/ec2/instance-types/c6/), [メモリ最適化R6g](https://aws.amazon.com/jp/ec2/instance-types/r6/)が使える。
* [Gravition2に関する日本語のウェビナー資料](https://d1.awsstatic.com/webinars/jp/pdf/services/20200707_BlackBelt_Graviton2.pdf)も公開されている。よくまとまっており、良い資料。
* Batchも対応しているとのこと。CodeBuildもArmイメージを選択可能。



## [クラウドネイティブな開発者は世界で650万人　半年間で3倍超に急増　400万人がサーバレスを利用（ITmedia）](https://www.itmedia.co.jp/news/articles/2008/20/news070.html)

* CNCFが調査した。調査資料は[こちら](https://www.cncf.io/wp-content/uploads/2020/08/CNCF-The-State-of-Cloud-Native-Development_FINAL_Q419.pdf)
* クラウドネイティブな開発者ってなに...？
  - `スケーラブルなアプリケーションをモダンで動的な環境（public, private, hybridなクラウド）で開発することに精通している人` らしい。
  - コンテナ、サービスメッシュ、マイクロサービスなどがキーワードになるらしい。


## [Amazon、AWSはMaaS構築の最適なプラットフォームと紹介](https://car.watch.impress.co.jp/docs/news/1271810.html)

* トヨタがMaaSの基盤としてAWSを活用しているという事例が公開。
* 上記のリンク先の記事にはスライドもたくさん載っているので、参考になる。
* MaaSというキーワードはこれからよく見るかもしれないので、ウォッチしておきたい。


## [Google Cloud Platformがアマゾンを抜きオンライン小売業におけるクラウドインフラのトッププロバイダーに（TechCrunch）](https://jp.techcrunch.com/2020/08/18/2020-08-17-canalys-google-is-top-cloud-infrastructure-provider-for-online-retailers/)

* タイトル通り。EC小売業でGCPのシェアがトップに。
* 小売業ではAmazonが3位, Azureが2位。
  - 小売業はAmazonに資金を提供したくない...なるほど。


## Professional Machine Learning Engineer BETA試験受けてきた

詳しくは[こちら](https://mukiudo.dev/post/gcp/0001-certification-ml-engineer/)

