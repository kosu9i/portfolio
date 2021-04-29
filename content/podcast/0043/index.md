---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#43 AWSでのCI/CD Codeなんちゃら系のサービスまとめ [後編]"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "小杉がAWSでのCi/CD系サービスについて話したよ。前回に続き、Codeなんちゃら系の話だよ。"
abstract:

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2021-04-28T21:39:51+09:00
#date_end: 2021-04-30T21:39:51+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2021-04-28T21:39:51+09:00

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

AWS上でCI/CDを行うサービスを整理。後編。

## 前回のおさらい

[前回の配信](https://mukiudo.dev/podcast/0042/)ではAWS上のCI/CD系サービスとして主にCodeCommit, CodeBuild周りを話した。

今回はCodeDeploy, CodePipelineあたりを中心に。

## CodeDeploy

{{< figure src="codedeploy.png" title="CodeDeploy 引用: https://docs.aws.amazon.com/ja_jp/codedeploy/latest/userguide/welcome.html" numbered="true" lightbox="true" >}}

AWSにおけるCDの肝となるサービス。

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
* [CodeDeploy Agent](https://github.com/aws/aws-codedeploy-agent)というものをインストールすればオンプレミスへのデプロイも可能
* EC2, Lambda, ECSへのデプロイには課金なし
  - オンプレミスは1つのインスタンスあたり$0.02。

## CodePipeline

{{< figure src="CodePipeline.png" title="CodePipeline 引用: https://docs.aws.amazon.com/ja_jp/codepipeline/latest/userguide/welcome-introducing.html" numbered="true" lightbox="true" >}}

ここまでのCI/CD一連の流れをパイプラインとしてつなげて自動化する。  
リリースプロセスをワークフローとして定義する。

* Approvalステージを挟むことでContinuous Deliveryに対応
  - 複数のApprvalアクションを用意して、承認者のIAMポリシーを分けて付与することで承認者を複数設定することも可能。  
    （参考: [CodePipeline で複数名の承認を必要とするパイプラインの実装方法](https://dev.classmethod.jp/articles/two-person-rule-with-codepipeline/)）
* CodeBuild, CodeDeployなどだけではなく様々なプロバイダと連携が可能
  - CloudFormation, AppConfigなどその他のAWSサービス
  - GitHub, Jenkinsなどサードパーティ
  - Lambda, StepFunctionsと連携するCustomアクション
* Build, Deployを並列で実行することも可能
* 通知機能はSNS経由
* パイプラインのコード管理はAWS CLIで `get-pipeline` や `update-pipeline` を使って行う。
* 例えば
  1. GitHubのmergeからトリガ
  2. CodeBuildでbuild
  3. CodeBuildでUnit Test
  4. Staging環境にデプロイ
  5. Staging環境でIntegration Testや人手の確認
  6. リリース承認者に通知
  7. 承認者によるApproval
  8. 本番環境にデプロイ
* 費用はアクティブパイプライン（30日以上存在していて、月に1回以上実行されたパイプライン）につき$1.00/月

## 結局どう使っていくか

個人的な意見なので参考までに、だけど↓

1. CodePipeline, CodeBuildはあらゆるケースに対応できそうなので導入してみると良いかも
  - デプロイにもCodeDeploy使わず、CodeBuildでやれちゃう or せざるを得ないケースは多そう
2. EC2, Lambda, ECS, オンプレミスへのdeployを高度化したいときにはCodeDeployの導入を検討し、マッチしそうであれば導入する
  - 特に対象サービスでBlue/GreenやCanary Deploy, ロールバックを導入しやすいのはメリット


個人的にはCIよりCDの方が難易度が高い気がする。最初に適切なツールでしっかり設計すべし。  
CDは構成管理がきちんとできているか、デプロイ先の環境が意図せず変更されていないか、ロールバックはきちんとできるか、Blue/GreenやCanaryのモニタリングはきちんとできているか...など考えることいっぱい。  
でも開発スピードやアジリティを高めるためには必要なことなのでしっかり検討すべし。

## 参考となるBlackbelt

CodeなんちゃらのBlackbeltが充実しているので、見るべし。

* [[AWS Black Belt Online Seminar] AWS CodeCommit & AWS CodeArtifact 資料及び QA 公開](https://aws.amazon.com/jp/blogs/news/webinar-bb-aws-codecommit_aws-codeartifact-2020/)
* [[AWS Black Belt Online Seminar] AWS CodeBuild 資料及び QA 公開](https://aws.amazon.com/jp/blogs/news/webinar-bb-aws-codebuild-2020/)
* [[AWS Black Belt Online Seminar] AWS CodeDeploy 資料及び QA 公開](https://aws.amazon.com/jp/blogs/news/webinar-bb-awscodedeploy-2021/)
* [[AWS Black Belt Online Seminar] AWS CodeStar & AWS CodePipeline 資料及び QA 公開](https://aws.amazon.com/jp/blogs/news/webinar-bb-awscodestar_awscodepipeline-2020/)
