---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#23 VSCodeのAWS拡張, X as a Service, Bottlerecket, ML系クラウドサービス, etc"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "加藤がメインで最近の気になるクラウド系のサービスやニュースについて話したよ。<br/>今回、音声がひどいよ...ごめんなさい。"
abstract: "加藤がメインで最近の気になるクラウド系のサービスやニュースについて話したよ。<br/>今回、音声がひどいよ...ごめんなさい。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-09-07T01:05:00+09:00
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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/VSCodeAWS--X-as-a-Service--Bottlerecket--ML--etc-ej7b1l" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Note

## ピックアップニュース（加藤担当）

### [Amazon CloudWatch Logs の機能が AWS Toolkit for Visual Studio Code でご利用可能に](https://aws.amazon.com/jp/about-aws/whats-new/2020/08/amazon-cloudwatch-logs-features-available-aws-toolkit-visual-studio-code/)

* VSCode用の拡張機能の話
* CloudWatch Logsのリソースが扱えるようになった
* エディタ上でAWS CLIよりも直感的にフィルタリングとかができるのが嬉しい
* これでLambdaの実行→ログの確認がGUIで完結できるようになった

マシンリソースの効率性が上がる。マネコンを開きっぱにしているとすごいメモリ量になるので。特にLambda。  
個人的にはS3はCLIの方が慣れているし使いやすいかも。  
あと、マネコンの強みであるフロー、「このLambdaのロググループ」みたいな辿り方はできない。サジェストとかもマネコンが優秀。


### [Amazon WorkSpaces が AWS リソースグループタグエディタのサポートを開始](https://aws.amazon.com/jp/about-aws/whats-new/2020/08/amazon-workspaces-enables-aws-resource-groups-tag-editor/)

WorkSpacesがタグエディタのサポートを開始したという話。  
今回気になったのは英語版のWorkSpacesの説明文。

> Amazon WorkSpaces is a managed, secure Desktop-as-a-Service (DaaS) solution. 

DaaSである、と定義している。
前回MaaSの話があってXaaSって頭文字はレイヤーを示すものでは？って話したけど別にそれだけじゃないみたい

As a Service：例えば製造業などが販売じゃなくてサービスで提供する形式のビジネスモデル

>アズ・ア・サービスは、主に製造業が製品の販売から製品機能のサービスとしての提供へと提供する価値を変更し、顧客のコストダウンを図るとともに製品販売に関する競合との製品競争から離脱し、収益性の向上を目指すビジネスモデルです。
アズ・ア・サービスは、「サービスとして」という意味であり、従来の製品機能をサービスとして提供することを言います。

Pay as you Goでもある。  
スイッチコストが低いのが特徴的かな。所有権は事業者側になる。


### [AWS Summit Online 2020/9/8〜](https://aws.amazon.com/jp/summits/2020/)

好きなタイミングで動画を見れるのでブログ書きやすそう。  
修了証明書がもらえるらしいw

https://r25.jp/article/845167571721142074
（この人の話は注意して聞かないと行けないと思うけど）言ってることはちょっとわかる。これまでのオフラインイベントの効果ってエモの共有かもしれない


### [AWS、コンテナ実行に最適化したLinux OS「Bottlerocket」正式版リリース](https://www.publickey1.jp/blog/20/awslinux_osbottlerocket.html)

> Linuxカーネルとコンテナの実行に必要な最小限のソフトウェアで構成されるため、性能上のオーバーヘッドが小さくなっているだけでなく、セキュリティの脆弱性につながるような外部との境界面も小さくなっています。

→余計な機能が削がれているので、アップデートとかのメンテが比較的楽になりそうでは

### [Amazon Polly NTTS 音声の提供がシンガポール、東京、フランクフルト、ロンドンリージョンで開始](https://aws.amazon.com/jp/about-aws/whats-new/2020/09/amazon-polly-ntts-voices-available-london-tokyo-frankfurt-singapore-regions/)

東京リージョンでニューラルテキスト読み上げに対応した。  
ただし試してみたら言語は英語・ポルトガル語・スペイン語だけだった。

ニューラルテキスト読み上げとは、人間のように聞こえる音声を合成するテキスト読み上げのこと

>Amazon Polly を使用した日本語テキスト読み上げの最適化 | Amazon Web Services ブログ https://aws.amazon.com/jp/blogs/news/amazon-polly-japanese-text-optimization/
「日本語は、間にスペースを入れずに単語をつなぎ合わせるため、単語と単語の境界を予測するモデルが必要になります。」
同形異義語の問題

→「「行った」を「いった」と読むと、「ある場所に出かけたこと」を意味しますが、「おこなった」と読むと、「何かを実行したこと」を意味します。」
なので現状は使い方でカバーするしかない。

> https://azure.microsoft.com/ja-jp/services/cognitive-services/text-to-speech/

Azureではニューラルテキスト読み上げに対応してた。

> Text-to-Speech: 自然な音声合成  |  Google Cloud https://cloud.google.com/text-to-speech?hl=ja

GCPではWavenetに対応してた

個人的にはAzureが一番すごいと思った。音声のクリアさとダイナミックさがすごかった。


## ピックアップニュース（小杉担当）

### [AWS、コンテナ実行に最適化したLinux OS「Bottlerocket」正式版リリース（Pulickey）](https://www.publickey1.jp/blog/20/awslinux_osbottlerocket.html)

* コンテナ実行に特化したLinuxベースのコンテナホスト用OS。
* セキュリティが重視されている。ブート時の自己整合性チェックや、SELinuxのアクセス制御など。
* 現在はEKS, ECSで利用可能。
* [Githubにて公開中](https://github.com/bottlerocket-os)。

参考公式ブログ:
* [Bottlerocket – コンテナホスティング用オープンソース OS](https://aws.amazon.com/jp/blogs/news/bottlerocket-open-source-os-for-container-hosting/)
* [Bottlerocket: 特定目的のコンテナオペレーティングシステム](https://aws.amazon.com/jp/blogs/news/bottlerocket-a-special-purpose-container-operating-system/)


### [グーグル、「Cloud AI」を拡充--コンタクトセンターや文字認識、MLOps向け機能を強化（ZDNet）](https://japan.zdnet.com/article/35159135/)

Cloud AIが色々拡充。多分Cloud Next OnAirで発表もされている。

* [Contact Center AI](https://cloud.google.com/solutions/contact-center)
  - 対話のDialogflow
  - 音声認識や音声合成を組み合わせてコンタクトセンターを自動化
  - 関連: [Google Cloudで企業が独自の合成音声の作成が可能に](https://jp.techcrunch.com/2020/09/03/2020-09-01-google-cloud-lets-businesses-create-their-own-text-to-speech-voices/)
* [AI Platform](https://cloud.google.com/ai-platform)
  - MLOps向け機能を強化
  - Continuous Monitoring（モデルパフォーマンスの監視）を2020年末までに利用可能になる見込み
