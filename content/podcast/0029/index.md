---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#29 CKAD, CloudRun新機能, AWSアップデート, Google Cloud Shell Editor, etc"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "タイトルどおり、ざっくばらんに話したよ"
abstract: "タイトルどおり、ざっくばらんに話したよ"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-11-16T10:00:00+09:00
#date_end: 2020-11-15T20:47:25+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-11-15T20:47:25+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/CKAD--CloudRun--AWS--Google-Cloud-Shell-Editor--etc-emhbmj" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Notes

## [KubeCon + CloudNativeCon North America 2020](https://events.linuxfoundation.org/kubecon-cloudnativecon-north-america/)

* CNCFが主催。k8sを中心としたエコシステム全般のカンファレンス。
* [申し込み](https://events.linuxfoundation.org/kubecon-cloudnativecon-north-america/register/)が必要。基調講演だけなら無料。それ以外のコンテンツは$100。


## CKADの話

* 来週、[CKAD](https://training.linuxfoundation.org/ja/certified-kubernetes-application-developer-ckad-jp/)っていうk8sのアプリケーション開発者向けの資格を受験する。
* CKAD-jpっていうのもあるけど、CKADで登録してしまった。
  + 試験問題はJapaneseを選べるらしい。
* 選択形式ではなくハンズオンの試験。
* 合格した場合の認定は3年間。合否判定は36時間以内にメールされるとのこと。
* 今は完全オンラインで実施するため、試験場所など環境を確保する必要あり。
* 試験対策としては[UdemyのCKAD専用コース](https://www.udemy.com/course/certified-kubernetes-application-developer/)がおすすめ。


## Cloud Runアップデート関連

前も少し話した事の詳細

### [60 を超える Google Cloud ソースのイベントで Cloud Run をトリガーする | Google Cloud blog](https://cloud.google.com/blog/ja/products/serverless/build-event-driven-applications-in-cloud-run)

* 60以上のGCPリソースからCloudRunをトリガできるようになる
  * Eventarc。現在プレビュー版。
* [CloudEvents](https://cloudevents.io/)という仕様に準拠している。
  * CNCFが策定するイベントデータの標準仕様。昨年v1.0になった。
  * 各種言語のSDKが提供されており、それでやり取りできる。

### [Cloud Run での正常なシャットダウンに関する詳細情報 | Google Cloud blog](https://cloud.google.com/blog/ja/products/application-development/graceful-shutdowns-cloud-run-deep-dive)

* スケールダウン時のコンテナシャットダウンで終了処理を書けるようになった。
  + サーバトラブル時などは保証されない。
* SIGTERMをハンドルし、10秒の猶予が与えられる。
  + 10秒でも終わらない場合はSIGKILLされる。
* 例は以下。
> * モニタリング データをフラッシュする  
> * コンテナの終了をロギングする  
> * ファイル ディスクリプタまたはデータベース接続を終了する  
* よくある失敗として、Dockerfile内のENTRYPOINTをarrayで指定していないため  
  bash経由でプロセスが起動されてしまうことがある。  
  bash経由で起動されたプロセスにはbashからSIGTERMが転送されないため終了処理を行えない。  
  必ずENTRYPOINT, CMDはarrayで書くこと。
> NG: ENTRYPOINT node server.js  # これは ENTRYPOINT ["/bin/sh", "-c", "node server.js"]と解釈される。  
> OK: ENTRYPOINT ["python", "server.js"]
* ソースコード的には単にSIGTERMのハンドラを定義しておくことになる。

## [Athenaがフェデレーテッドクエリに対応](https://aws.amazon.com/jp/about-aws/whats-new/2020/11/aws-what-s-new-for-athena-federated-query/)

Amazon Athena adds support for running SQL queries across relational, non-relational, object, and custom data sources. 

* Redshiftやオンプレ、Redisなど複数のデータソースから対してSQLの1クエリで同時に取得できる機能
* フェデレーテッドクエリの参考記事：https://aws.amazon.com/jp/blogs/news/query-any-data-source-with-amazon-athenas-new-federated-query/


## [Lambda ExtentionsでDatadogやNew Relic等の3rd party製プロダクトにログを直接送信できるようになった](https://aws.amazon.com/jp/about-aws/whats-new/2020/11/aws-lambda-send-logs-custom-destinations/)

AWS Lambda now makes it easier to send logs to custom destinations 

* これまではLambda側、もしくはCWLog側からひと手間かけて収集が必要だったが、それが要らなくなった
* 参考：https://dev.classmethod.jp/articles/cons-of-lambda-extensions/


## [DDBのデータをS3にエクスポートできるようになった](https://aws.amazon.com/jp/about-aws/whats-new/2020/11/now-you-can-export-your-amazon-dynamodb-table-data-to-your-data-lake-in-amazon-s3-to-perform-analytics-at-any-scale/)

Now you can export your Amazon DynamoDB table data to your data lake in Amazon S3 to perform analytics at any scale 

* DDBのデータをS3にエクスポートできるようになった（新UIから）
* 既存のDBからテストデータを作るのとかちょっと楽になるかも

## [Lightsailでコンテナ作れるようになった](https://aws.amazon.com/jp/about-aws/whats-new/2020/11/announcing-amazon-lightsail-containers/)

Announcing Amazon Lightsail Containers, an easy way to run containerized applications on the cloud 

* Lightsailでコンテナ作れるようになった
* Lightwailは初心者でも簡単に月額で使えるインスタンス作ったりできるサービス
* かんたんにサクッとコンテナ作るのにはいいかも


## [Google、VSCodeの代替を狙う「Eclipse Theia」コードエディタをクラウド統合開発環境として採用。Google Cloud Shellに統合を発表 | Publickey](https://www.publickey1.jp/blog/20/googlevscodeeclipse_theiagoogle_cloud_shell.html)

* [Eclipse Theia](https://github.com/eclipse-theia/theia)はVS CodeのOSS版とも言えるIDEライクなエディタ。
  + ローカルアプリケーション, Webベースどちらもある。
  + VS Codeの拡張はVisual Studio Marketplaceで配布されているが、このマーケットプレイスでは  
    VS Code以外へのインストールをライセンスで禁止している。  
    Eclipse Foundationはオープンなマーケットプレイス[Open VSX Registry](https://open-vsx.org/)で拡張を提供している。
* Goole Cloud Shell Editorとしてすでに利用可能だけど、まだ不安定...
* GCPのサービスとの連携がスムーズ。
  + とくにCloud Run, GKEなどクラウドネイティブなアプリケーション開発を促進することを意識しているっぽい。
* MSはGithub Codespaces, AWSはCloud9
  + Gitpodは同じくTheiaベース。[Typefoxという企業が最近OSSとして公開](https://www.publickey1.jp/blog/20/githubgitlabwebidegitpodgithub_codespaces.html)した。
