---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#42 AWSでのCI/CD Codeなんちゃら系のサービスまとめ"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "小杉がAWSでのCi/CD系サービスについて話したよ。Codeなんちゃらって名前が多すぎだよ。"
abstract:

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2021-03-30T21:39:51+09:00
#date_end: 2021-03-30T21:39:51+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2021-03-30T21:39:51+09:00

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

# Show Notes

AWS上でCI/CDを行うサービスを整理。

## そもそもCI/CDのおさらい

参考: [Red Hat DEVOPS CI/CDとは](https://www.redhat.com/ja/topics/devops/what-is-ci-cd)

{{< figure src="ci-cd-flow-desktop_1.png" title="引用: https://www.redhat.com/ja/topics/devops/what-is-ci-cd" numbered="true" lightbox="true" >}}

* Continuous Integration
  - ビルドやテストを自動化
* Continuous Deployment
  - CIをパスしたら本番環境へ自動的にデプロイ
* Continuous Delivery
  - Continuous Deploymentほど自動化されていない。  
    例えば本番環境へのリリース前に人手の承認を挟むなど。


## AWSのCodeなんちゃら全体像

AWSにはCodeナンチャラっていうサービスがたくさんある。  
ほとんどがCI/CDに関わるものなのだがまずは一旦概観を整理する。

AWSのCodeなんちゃら系サービス全体像。[[AWS Black Belt Online Seminar] AWS CodeDeploy](https://d1.awsstatic.com/webinars/jp/pdf/services/20210126_BlackBelt_CodeDeploy.pdf)より引用。

{{< figure src="aws_code_services.png" title="引用: https://d1.awsstatic.com/webinars/jp/pdf/services/20210126_BlackBelt_CodeDeploy.pdf" numbered="true" lightbox="true" >}}

CI/CDを実施するうえで主要なコンポーネントは以下。  
Code兄弟とも呼ばれているらしい。

* [AWS CodeCommit](https://aws.amazon.com/jp/codecommit/)
  - AWS内に構築されるプライベートgitリポジトリ
  - Pipelineを作成するうえではGitHubなど他のリポジトリを使ってもOK
* [AWS CodeBuild](https://aws.amazon.com/jp/codebuild/)
  - CIを担当
* [AWS CodeDeploy](https://aws.amazon.com/jp/codedeploy/)
  - CDを担当
* [AWS CodePipeline](https://aws.amazon.com/jp/codepipeline/)
  - CI/CD一連の処理をパイプライン化
  - 途中に人手の承認を挟むことも可能（Continuous Deliveryに対応）

その他、Codeなんちゃら。必要に応じて。

* [AWS CodeArtifact](https://aws.amazon.com/jp/codeartifact/)
  - パッケージ化したものを配布（pip, npm, mavenなど）
* [AWS CodeGuru](https://aws.amazon.com/jp/codeguru/)
  - 機械学習を使ったコードレビューをしてくれる
  - 脆弱性やパフォーマンスのチェックも
  - Java, Pythonに対応（2021年3月現在）
  - 100行ごとに$0.5前後（ボリュームディスカウントあり）
* [AWS CodeStar](https://aws.amazon.com/jp/codestar/)
  - CI/CDをテンプレートから構築できる
  - CodeCommit, CodeBuild, CodePipeline, CodeDeploy or CloudFormation, CloudWatch
  - 手っ取り早く構築したい人向け
* [AWS Cloud9](https://aws.amazon.com/jp/cloud9/)
  - Codeなんちゃらではないけど、WebブラウザベースのIDE
  - モブプロなどに便利
  - AWSサービスとシームレスな連携

## CodeCommit

{{< figure src="codecommit-compare-branches.png" title="引用: https://docs.aws.amazon.com/ja_jp/codecommit/latest/userguide/how-to-compare-commits.html" numbered="true" lightbox="true" >}}

プライベートなGitリポジトリ。GitHubみたいなもの ~~だけど、GitHubほど使いやすくはない。~~

* 基本的な機能はある
  - ソースのプレビュー, ブラウザ上での編集
  - プルリクエスト
  - ブラウザ上でレビューコメント
  - 承認ルールの設定
  - 通知（SNS, AWS Chatbot）
    - コメントがあったとき, mergeされたとき, など設定可能
  - SSH公開鍵での認証
* 個人的に微妙な点
  - Issue Trackerとの連携がない
    - CodeStarでJIRAとは連携できる（参考: [AWS が CodeStar を発表、JIRA との連携も可能に](https://blog.evangelism.jp/entry/integration-aws-codestar-jira-software)）
  - notebookのプレビューがない
  - 通知のリンクが微妙
    - コメントに紐付いていないなど
  - 承認ルールが細かく設定できない
    - 必須のレビューアを設定できない
* 他のCodeなんちゃらがGitHubなど他のリポジトリにも対応しているので、気に食わないなら他リポジトリを使ってもOK
* [料金](https://aws.amazon.com/jp/codecommit/pricing/)は割と安めだから気にしなくて良いレベル
  - 5人までタダ
  - 5人以上の場合は1ユーザごとに月1ドル


## CodeBuild

{{< figure src="codebuild.png" title="引用: https://www.slideshare.net/AmazonWebServicesJapan/20201125-aws-black-belt-online-seminar-aws-codebuild" numbered="true" lightbox="true" >}}

AWSにおけるCIの肝となるサービス。  
AWSの各種サービスと連携しやすいCIツールという感じ。


### 基本機能

* フルマネージドなビルド環境を得られる（使った分だけ課金）
* ビルド環境としてAmazon Linux2, Ubuntu, Windows Serverを選べる
  - インスタンスタイプは数種類から選択、費用は1分あたりで課金（参考: [AWS CodeBuild の料金](https://aws.amazon.com/jp/codebuild/pricing/)）
  - Windows Serverを使えるリージョンは限られている
  - カスタムのビルド用imageも使える
* ビルド手順や設定を `buildspec.yaml` （ファイル名は変更可能）に記載してリポジトリに置いて設定を書く
  - ビルドの前後処理, ビルドコマンド, など
  - AWSコンソール上を書いていくこともできる
* ビルド環境のインスタンススペックも数種類から選べる
  - もちろん使い終わったらインスタンスは自動削除される
* ビルド環境のランタイムは色々選択できる（参考: [Docker images provided by CodeBuild](https://docs.aws.amazon.com/codebuild/latest/userguide/build-env-ref-available.html)）
  - 例えばnodejs, python, javaなど
  - ビルドや自動テストに必要なランタイムを選択する
* S3, CodeCommit, GitHub, GithHub Enterprise, BitBucketなどのソースを指定可能
  - OAuthで認可
* 手動実行, 定期実行, Webhookによるトリガ実行（GitHub, Bitbucket）, 特定のbranchでのトリガ実行, など
  - 手動はマネコン or CLI
  - もちろんCodePipelineからも呼び出せる
* Cloud Watchや各種通知との連携
  - ビルドが終わったら通知など
* 費用は [こちら](https://aws.amazon.com/jp/codebuild/pricing/)
  - 最小インスタンスで大体30円/h, 中くらいのインスタンスで120円/hくらい

### buildspec.yml

[ここ](https://docs.aws.amazon.com/ja_jp/codebuild/latest/userguide/build-spec-ref.html)にbuildspec.ymlの仕様ドキュメントあり。

* 色々項目はあるけど必須は `version` と `phases` だけ
  - versionは0.1 or 0.2なので基本的には0.2にしとけばOK
  - phasesに具体的なビルド作業を書いていく。
* `phases` には `install` => `pre_build` => `build` => `post_build` の純で書いていく
  - `install`: ビルドに必要なものをinstallしていく。`runtime-versions` てのを指定するとあらかじめ提供されているランタイム一式（java, python, androidとか）が構築される
  - `pre_build`: ビルド前に必要な処理。dockerレジストリへのログインとか、npmの依存関係をインストールとか。
  - `build`: ビルド作業そのものを記述。
  - `post_build`: ビルド後に必要な処理。dockerレジストリへのpushとか、jarファイルのパッケージ化とか。
* 残りの項目はoptional
  - `run-as`
  - `env`
  - `proxy`
  - `batch`
  - `reports`
  - `artifacts`
  - `cache`

### おもしろそうな機能

* Jenkinsプラグインを使ってJenkinsと統合することも可能（参考: [JenkinsとAWS CodeBuildおよびAWS CodeDeployとの連携によるCI/CDパイプラインの構築](https://aws.amazon.com/jp/blogs/news/setting-up-a-ci-cd-pipeline-by-integrating-jenkins-with-aws-codebuild-and-aws-codedeploy/)）
  - ビルド環境としてCodeBuildを利用できるっぽい
* Build Badge（GitHubとかに表示する、CIが通っていることを表示するアイコン画像）を提供
  - URLが生成されるので、READMEとかに貼ると最新のステータスが表示される
* `batch` でのビルド
  - 複数のタスクを逐次, 並列, matrixで実行可能
  - 今までこういうのはStepFunctionsなどにオフロードする必要があったけど、buildspec.yml内で書けるようになった
  - matrixは、たとえばimageはlinux, windowsで、環境変数をVAL1, VAL2の組み合わせ計4通り（linux+VAL1, linux+VAL2, win+VAL1, win+VAL2）で並列実行
* `reports`
  - コードカバレッジ, テストレポートなどを可視化してAWSコンソール上で見られる
  - コードカバレッジはClover XML, Cobertula XML, JaCoCoXML, SimpleCovJSONに対応
  - テストレポートはCucumber JSON, JUnitXML, NUnitXML, NUnit3 XML, TestNGXML, Visual Studio TRXに対応
* `cache`
  - ソースキャッシュ, Dockerレイヤーキャッシュ, カスタムのディレクトリキャッシュ
* ローカルでの実行
  - CodeBuildエージェントを利用してローカル環境でCodeBuildと同様のビルドが実行可能
* `codebuild-breakpoint` というコマンドをphasesに挟むと、ビルドが止まってデバッグ可能
  - ビルド環境にログインして `codebuild-resume` を実行すると再開する
  - ビルド環境へのログインはAWSコンソール内のセッションマネージャーから


## CodeDeploy

AWSにおけるCDの肝となるサービス。

※ 本配信では概要のみ説明

* フルマネージドなデプロイ自動化サービス
* デプロイ先としてEC2, オンプレミス, Lambda, ECSを選択可能
* Pull型のデプロイ
  - Push型はデプロイする人がデプロイ先のサーバを把握する必要がある
  - デプロイ自動化にはPull型が推奨される
* 様々なデプロイ方法を選択可能
  - In-Place
  - Blue/Green Deploy
  - Canary Deploy
  - Linear, All-at-once
* エラー時のロールバックも可能
* デプロイ設定を `appspec.yaml` に記載してデプロイするパッケージ内に入れたりリポジトリに配置したり
  - ミドルウェアのインストールなどの前後処理
  - 当該アプリケーションのデプロイ方法（EC2なら所定の場所にファイルを配置したり）
* `Application`, `Deployment Group`, `Revision` という概念（参考: [CodeDeployによるバージョン管理とステージング](https://dev.classmethod.jp/articles/versionig_and_staging_via_codedeploy/)）
* [CodeDeploy Agent](https://github.com/aws/aws-codedeploy-agent)というものをインストールすればオンプレミスへのデプロイも可能


## CodePipeline

ここまでのCI/CD一連の流れをパイプラインとしてつなげる。

※ 本配信では概要のみ説明

* Approvalステージを挟むことでContinuous Deliveryに対応
  - 複数のApprvalアクションを用意して、承認者のIAMポリシーを分けて付与することで承認者を複数設定することも可能。  
    （参考: [CodePipeline で複数名の承認を必要とするパイプラインの実装方法](https://dev.classmethod.jp/articles/two-person-rule-with-codepipeline/)）
* パイプラインのコード管理はAWS CLIで `get-pipeline` や `update-pipeline` を使って行う。


## 参考となるBlackbelt

CodeなんちゃらのBlackbeltが充実しているので、見るべし。

* [[AWS Black Belt Online Seminar] AWS CodeCommit & AWS CodeArtifact 資料及び QA 公開](https://aws.amazon.com/jp/blogs/news/webinar-bb-aws-codecommit_aws-codeartifact-2020/)
* [[AWS Black Belt Online Seminar] AWS CodeBuild 資料及び QA 公開](https://aws.amazon.com/jp/blogs/news/webinar-bb-aws-codebuild-2020/)
* [[AWS Black Belt Online Seminar] AWS CodeDeploy 資料及び QA 公開](https://aws.amazon.com/jp/blogs/news/webinar-bb-awscodedeploy-2021/)
* [[AWS Black Belt Online Seminar] AWS CodeStar & AWS CodePipeline 資料及び QA 公開](https://aws.amazon.com/jp/blogs/news/webinar-bb-awscodestar_awscodepipeline-2020/)
