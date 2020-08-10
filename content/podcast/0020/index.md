---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#20 【雑談回】クラウド関連ニュース色々"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "クラウド関連のニュースについてピックアップして色々話したよ。"
abstract: "クラウド関連のニュースについてピックアップして色々話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-08-10T15:03:51+09:00
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

**Coming soon...**

# Show Note

全部は話してないと思う。台本的に以下に列挙。


## AWSのマルチクラウド

* 近年、ITmediaがやたらとAWSのマルチクラウド遅れ（？）を取り上げている。（参考:「 [AWSが「マルチクラウド」に消極的なままだと何が起こるのか？
](https://techtarget.itmedia.co.jp/tt/news/2008/03/news01.html)」）
* GCPはAnthos, AzureはAzure Arcってのでマルチクラウド推進している。
  - いずれもKubernetesをAWS含むマルチプラットフォームに展開するサービス。
  - Azure Arcは中でAzure SQL Databaseとかを利用できるみたい。
* どうでも良いけどITmediaの会員登録って...

## AWS新リリースいろいろ

ここ2週間くらい、やたらとリリース情報があった気がする。興味のあったものを抜粋。

### 「[AWS、機械学習によるオンライン不正検出サービス「Fraud Detector」を一般提供](https://japan.zdnet.com/article/35157387/)」

* 機械学習を用いた不正検出のSaaS

### 「[Amazon Translate が Office Open XML ドキュメントの翻訳のサポートを開始](https://aws.amazon.com/jp/about-aws/whats-new/2020/07/amazon-translate-now-supports-translation-of-office-open-xml-documents/?nc1=h_ls)」

* Officeファイルの機械翻訳サービスは他にも結構ある、というかOffice 365だと本体に備わっていたりするので需要がどれくらいあるか分からんが...

### 「[AWS Step Functions が Amazon SageMaker Processing のサポートを追加](https://aws.amazon.com/jp/about-aws/whats-new/2020/08/aws-step-functions-adds-support-for-amazon-sagemaker-processing/)」
* 多分SageMakerから直接実行するSDKが用意された、とかだと思われ。  
  でも[AWS Step Functions Data Science Python SDK](https://aws-step-functions-data-science-sdk.readthedocs.io/en/stable/)って前からあったような...？
* 前処理部分担当の「SageMaker Processing」を上記のSDKから実行できるようになった、ということかな？
* 触ってみないとメリデメがわからないが、MLのパイプライン管理は煩雑になりやすいので使いこなすと便利かも。

### 「[Amazon S3 の機能が AWS Toolkits for Visual Studio Code でご利用可能に](https://aws.amazon.com/jp/about-aws/whats-new/2020/07/amazon-s3-features-now-available-aws-toolkits-for-visual-studio-code/)」
* [AWS Toolkit for Visual Studio Code](https://aws.amazon.com/jp/visualstudiocode/)に新機能として加わった。
* VSCodeどんどん便利になってくね。

### 「[Amazon 新コマンドラインツール AWS Copilot 発表](https://www.infoq.com/jp/news/2020/08/amazon-introduces-aws-copilot/)」
* ECS, Fargateを操作するCLI。
* 「[Docker DesktopとAmazon ECS（Elastic Container Service）が連係可能に。DockerとAWSが協業](https://www.publickey1.jp/blog/20/docker_desktopamazon_ecselastic_container_servicedockeraws.html)」というのもあった。  
  なんか最近ECSはじめAWSとdockerの連携がアツイ感じ？

### 「[AWS、独自開発したARMプロセッサ「Graviton 2」ベースのAmazon RDS MySQL/PostgreSQLをプレビュー開始。ARMはXeonを上回れるのか？](https://www.publickey1.jp/blog/20/awsarmgraviton_2amazon_rds_mysqlpostgresqlarmxeon.html)」
* Graviton2とは、AWSが独自開発しているARMベースのプロセッサ。

### 「[AWS Community Builders開始。AWSに関する情報発信やコミュニティへの貢献に情熱を持つ人をAWSが支援](https://www.publickey1.jp/blog/20/aws_community_buildersawsaws.html)」

> AWS Community Buildersに申し込んで承認を受けた人に対して、AWSの新サービス情報や関連情報の提供、AWSや専門家からの技術指南、活動支援のためのクレジットの提供などが行われる  
> 参加費は無料で18歳以上なら申し込み可能。ただし申込者に対して、ブログやプレゼンテーション、AWSのフォーラムやStackOverflowなどで積極的な情報提供やAWSコミュニティでの活動、オープンソースへの貢献などが行われているかどうかなど、活動に関する審査が年に2回行われる


## re: Invent 2020

[公式サイト](https://reinvent.awsevents.com/)

* 2020/11/30から2020/12/18まで。3週間開催。
* オンラインかつ無料。
* Subscribeしたんだけど、音沙汰なし...よくわからず。


## BigQuery Omni

「[Google「BigQuery Omni」に関する素朴な疑問を、米国の総責任者にぶつけてみました](https://www.atmarkit.co.jp/ait/articles/2007/28/news106.html)」

* 料金体系は既存のBigQueryと同じにするかもらしい。とはいえ、S3自体の料金やリージョンの関係もあるので今は検討中とのこと。
* 「マルチクラウドに未来がある」（by デバンジャン・サハ（Debanjan Saha）氏）
  - 他のデータ関連製品もマルチクラウド化する意欲あり。市場の動向を見極めたい。
* 「BigQueryは最高。Dataflowも最高」（by サハ氏 ※意訳）
* ちなみにサハ氏は前AWSにいた人らしい。


## Cloud Hero 2020

* [グローバル開催](https://go.qwiklabs.com/cloudheronext?utm_source=studyjam&utm_medium=lp&utm_campaign=Next20)
  - 1週間でQwiklabsをやる。
  - 各Lab 5回まで実施可能。
  - ほぼ自動化を極めるゲーム。
* [日本開催](https://inthecloud.withgoogle.com/noa-learning-program-jp/index.html)
  - 8/4 インフラストラクチャ編, 8/18 データ分析編の2days
  - 3時間でQwiklabsをやる。
  - ほぼ手の速さと正確さを極めるゲーム。（できるなら自動化してもよし）

賞品は何がもらえるのか不明。


## その他

### 「[Amazon・Microsoft・Alphabet・Apple・Facebookの収益源が何かをグラフで見比べてわかること](https://gigazine.net/news/20200806-big-tech-billions/)」

* Amazon
  - 全体収益: 約30兆円
  - AWS: 12.5%
  - ECが50%で最大の割合
* Alphabet
  - 全体収益: 約17兆円
  - GCP: 5.5%
  - ほぼ広告事業
* Microsoft
  - 全体収益: 約13兆円
  - Azure: 25.9%
  - クラウド事業が最大の割合

参考として、AWS, GCP, Azureの2019年シェアは、32.3%, 16.9%, 5.8%らしい。  
参考: 「[19年のクラウドインフラ市場、AWSの首位揺るがず　世界シェアの約3割占める　Azureが約2割で猛追](https://www.itmedia.co.jp/news/articles/2002/13/news117.html)」


### Canonのデータ消失

* [キヤノンの写真クラウド「image.canon」、保存データの一部が消失](https://www.itmedia.co.jp/news/articles/2008/05/news067.html)
* [キヤノンUSAがサイバー攻撃を受け10TBのデータが盗難、米報道](https://news.yahoo.co.jp/articles/86bb542d7ab7d6619ed2228095fee6e432147611)
  - Mazeによる攻撃とみられている。
  - キャノンUSAの公式コメントはまだなし。

一応、上記の2件は無関係とのこと。
