---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#38 GCPでのETLいろいろ - Dataproc編"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "小杉が時事ネタ + GCP Dataprocについて話したよ。駆け足でしゃべったから若干聞き苦しいかもごめんですよ。加藤は寝不足で声が暗いよ。"
abstract: "小杉が時事ネタ + GCP Dataprocについて話したよ。駆け足でしゃべったから若干聞き苦しいかもごめんですよ。加藤は寝不足で声が暗いよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2021-01-29T10:10:00+09:00
#date_end: 2021-01-27T20:15:14+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2021-01-27T20:15:14+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/GCPETL---Dataproc-epkdkv" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Notes

## Parlerの続報

* 「[多くのサービスから排除されたSNS「Parler」のCEOが「復活することはないかもしれない」とコメント | Gugazine](https://gigazine.net/news/20210114-parler-ceo-says-may-not-return/)」したり
* 「[愛国者の拠点となったソーシャルメディアParlerのAWS復帰要求を裁判所が却下 | TechCrunch](https://jp.techcrunch.com/2021/01/22/2021-01-21-judge-denies-parlers-bid-to-make-amazon-restore-service/)」されたり
  - ParlerがAWSを訴えたが却下された
  - Parler側の提示した根拠がかなり貧弱だった様子。
  > 「誤解のないようにいうと、裁判所はこの時点でParlerによる実質的な基本的主張を棄却していない」。つまりこれは主張の内容を否定するものでも、それが実質的であることを仮定するものでもない。しかしParlerは、この種の法的介入の根拠を示すために必要なものを提示する には「程遠かった」
* 「[極右に人気のSNS「Parler」がロシア企業頼みで“復活”を模索？ それでも問題の解決にならない理由 | WIRED](https://wired.jp/2021/01/25/parler-russia-privacy/)」だったり
  - ロシアのCDN DDoS-Guardを通してサービス再開（DDoS-Guardがホスティングしているわけではないそう）

今回のAWSからのBANに対して、念の為補足しておくと少なくともAWSの主張としては「Parlerが暴力的なコンテンツをコントロールできなかったことによる利用規約違反」によってBANしているのであり、言語統制やなんらかの政治的な意図を伴ったBANではないということ。  
それとは別に「テックジャイアントが力を持ちすぎている」ことに関する是非はずっと議論されており、これからもされると思われ。

この辺りの話については「[Off Topic](https://anchor.fm/mikirepo/episodes/50-SNS-ep46i2)」さんがとても分かりやすく話してくれているので、おすすめ。↓

<iframe src="https://anchor.fm/mikirepo/embed/episodes/50-SNS-ep46i2/a-a4clnha" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>


## [AWSをElasticが名指しで非難。ElasticsearchとKibanaのライセンスを、AWSが勝手にマネージドサービスで提供できないように変更へ | Publickey](https://www.publickey1.jp/blog/21/awselasticelasticsearchkibanaaws.html)

ElasticsearchとKibanaのライセンスを、商用サービス化を制限するSSPLとElastic Licenseのデュアルライセンスに変更。
背景にはAWSがElasticsearchとKibanaをマネージドサービスとして提供し続けてきたことに対する反発が。

Elastic社のCEOがAWSにブチギレながらライセンス変更のアナウンスをしたブログが[こちら](https://www.elastic.co/jp/blog/why-license-change-AWS)

パブリッククラウドベンダーがOSSにフリーライドしている問題に対する動きは前々から活発化していた。（参考: [「Redis、MongoDB、Kafkaらが相次いで商用サービスを制限するライセンス変更。AWSなどクラウドベンダによる「オープンソースのいいとこ取り」に反発 | Publickey」](https://www.publickey1.jp/blog/19/redismongodbkafkaaws.html)）

SSPLとはMongoDBが2018年に作成したライセンスで
* サービス提供する際に、サービス提供元が周辺プログラムを含めてソースコードを公開するか、ライセンス料を払うかどちらか選ぶ。
* 他のソフトウェアに対する制限を設けているという点で[OSDの9条](https://opensource.org/docs/osd#not-restrict-other-software)に反しており、OSSライセンスではないという見方が一般的。

OSSコミュニティとクラウドベンダの間には色々因縁があったけど、Googleは[2019年にOSSベンダーとの戦略的提携を発表](https://www.itmedia.co.jp/news/articles/1904/10/news090.html)していたり、AWSも[Grafanaとはパートナーシップを結んで](https://grafana.com/blog/2020/12/15/announcing-amazon-managed-service-for-grafana/)いたり。

今回の件では、AWSは[ElasticsearchとKibanaのライセンス変更前のコードからforkしたOSSを公開することで対応](https://aws.amazon.com/jp/blogs/news/aws-policy-for-elasticsearch-licence-change/)。

2019年にAWSが公開した[Open Distro for Elasticsearch](https://opendistro.github.io/for-elasticsearch/)（参考:[「AWSが、Elasticsearchのコードにはプロプライエタリが混在しているとして、OSSだけで構成される「Open Distro for Elasticsearch」を作成し公開 | Publickey」](https://www.publickey1.jp/blog/19/awselasticsearchossopen_distro_for_elasticsearch.html)）とは別だけど、元にはしているらしいし、今後どうなるかは不明。

参考: [AWS、商用サービス化を制限するライセンス変更に対抗し「Elasticsearch」をフォーク、独自のオープンソース版へ | Publickey](https://www.publickey1.jp/blog/21/awselasticsearch.html)

こじれている...


## 本ネタ

自ブログの投稿「[GCP上でのETLいろいろ](https://mukiudo.dev/post/gcp/0002-etl-on-gcp/)」からGCP Dataproc, Data Fusionあたりまで。

