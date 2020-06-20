---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#16 【GCP？】Kubeflow超概要"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "小杉がk8s上で動く機械学習ワークフロー開発ツールKubeflowの超概要について話したよ。<br/>かろうじてGCP？としたけどOSSだよ。（詳しくは本編にて）"
abstract: "小杉がk8s上で動く機械学習ワークフロー開発ツールKubeflowの超概要について話したよ。<br/>かろうじてGCP？としたけどOSSだよ。（詳しくは本編にて）"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-06-21T00:48:00+09:00
#date_end: 2020-06-20T17:28:19+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-06-20T17:28:19+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/GCPKubeflow-efmh8l" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# 話したこと

Kubeflowの**超概要**  
まだ検証中なので、間違ってたりするかもしれない...  
今後もっと検証を進めたら続編をpodcastでも話す。


## Kubeflow概要

* [Kubeflow](https://www.kubeflow.org/docs/about/kubeflow/)とは、k8s上で動くOSSの機械学習のワークフロー開発ツール。
* Googleが筆頭で開発。
* Apache 2.0 License
* 2020/3月にv1.0がリリースされた。
* 読み方は「キューブフロー」（Youtubeとかで現地の人の発音を聞いた限り、多分）

CI/CDに加え、機械学習ではCT（Continuous Training）というのがある、と[Googleが言っている](https://cloud.google.com/solutions/machine-learning/architecture-for-mlops-using-tfx-kubeflow-pipelines-and-cloud-build?hl=ja#cicd_pipeline_compared_to_ct_pipeline)。  
いわゆるMLOpsということになると思うが、このMLOpsを支援するのがKubeflowと言えそう。

ちなみに[公式ドキュメント](https://www.kubeflow.org/docs/)は英語だけど、とても良くまとまっており分かりやすい。


## 歴史

もともとは[Tensorflow Extended（TFX）](https://www.tensorflow.org/tfx/)として開発されていたものが  
より汎用化するためにKubeflowとして独立したらしい。（参考: [Kubeflowとは](https://ymym3412.hatenablog.com/entry/2020/01/07/051653#Kubeflow%E3%81%A8%E3%81%AF)）

以前は結構バグが多かったみたいだけど、最近v1.0がリリースされ使ってる人の記事もちらほら見かけるようになった。


### TFXとの違い

先述のTFXも依然として開発は進んでおり、さらにKubeflowの中にTFXのpipelineを呼び出す機能もあったりしてややこしい。  
名前からしてTFXはTensoflowに特化している？とも思ったけど、TFXが他のMLフレームワークも扱えるのか不明...  
正直使い分けがよく分かってないので、後日ちゃんと理解したい。


### AI Platformとの違い

AI Platformともかぶる。  
こちらもKubeflowからAI Platformのジョブを呼び出せたり、AI Platformのいち機能として「[AI Platform Pipelines](https://cloud.google.com/blog/ja/products/ai-machine-learning/introducing-cloud-ai-platform-pipelines)」というものが提供されておりこの実態はKubeflowだったりして、さらにややこしい。  

ただ違いとしてはざっくり「AI PlatformはGCPのマネージドサービス」「KubeflowはOSS」と分けて考えても  
選択基準としては差し支えないのではないかと感じる。  
マネージドで楽したい、あまり細かい管理は要らない、というのであればSaaSであるAI Platform（もしくはAI Platform Pipelines）を使えば良いし  
それじゃ足りなくなってきたり、よりカスタマイズした環境・機能を利用したいのであればKubeflow、というくらいの抑え方でも問題ないのでは、と思う。  
（もちろん機能的な面でも違いはあるが）


## 機能

公式ドキュメントに[Components of Kubeflow](https://www.kubeflow.org/docs/components/)というものがあるのでそこから抜粋。

概要レベルだけど、Kubeflowの提供機能（というかコンポーネント）は以下。

* Central Dashboard
  + ダッシュボードUI
* Metadata
  + Kubeflow上で実行されたワークフローのメタデータを管理
  + 実験結果とかモデルのバージョニングとかかな（多分）
* Jupyter Notebooks
  + そのまんま
* Frameworks for Training
  + 学習フレームワーク。多分、分散学習とかもやりやすくなってる。
* Hyperparameter Tuning
  + そのまんまハイパーパラメータの自動チューニングの機能があると思われる。
* Pipelines
  + MLワークフローをDAGで定義できる。結構肝の機能。
* Tools for Serving
  + 推論APIの構築や、推論バッチ実行ができるものと思われる。
* Multi-Tenancy in Kubeflow
  + 認証系と思われるが、この辺はまだ弱いかも？
* Miscellaneous
  + その他

ぱっと見、SageMakerやAI Platformとかぶりそう。
先述の通り、マネージドかOSSで選択すれば良いと思う。

ただ、目玉のPipelinesとかはSageMakerやAI Platform単体ではそこまでうまく出来なさそうなので  
最初からそこを使いたい場合はKubeflow、もしくはAI Platform Pipelinesが選択肢に入ってきそう。


## 特徴

[公式](https://www.kubeflow.org/docs/about/kubeflow/#the-kubeflow-mission)には以下のようにある。

> * Easy, repeatable, portable deployments on a diverse infrastructure (for example, experimenting on a laptop, then moving to an on-premises cluster or to the cloud)
> * Deploying and managing loosely-coupled microservices
> * Scaling based on demand

中でも「portable」というところが一番のメリットだと、個人的には感じている。  

### メリット

* OSSなので自由が効く。
* portable

### デメリット

* 学習・構築コスト

### 期待していること

portableということで、ベンダーロックインしないように構築可能（多分）

SageMakerやAI Platformは処理自体はコンテナ化することができるが  
結局ジョブを呼び出す部分の処理や、ファイルIOの部分でベンダーロックインするところがある。

KubeflowはGCPのGKEをはじめ、EKS, AKS, オンプレミスで同じように動作するため  
構築する部分はそれぞれ用意する必要があるが、ワークフロー自体は同様に処理できる。はず。  
という期待を持って検証中。

## 参考になりそうなリンク（主に日本語）

* [TFX、Kubeflow Pipelines、Cloud Build を使用した MLOps のアーキテクチャ](https://cloud.google.com/solutions/machine-learning/architecture-for-mlops-using-tfx-kubeflow-pipelines-and-cloud-build?hl=ja#cicd_pipeline_compared_to_ct_pipeline)
  + GCPのドキュメント
* [AI Hub と Kubeflow Pipelines を発表 -- AI をよりシンプル、高速、便利なものに](kubeflow.org/docs/gke/deploy/deploy-cli/)
  + GCPのブログ
* [Kubeflow Pipelinesで日本語テキスト分類の実験管理](https://ymym3412.hatenablog.com/entry/2020/01/07/051653)
  + [@ymym3412](https://twitter.com/ymym3412)さんという方のブログ
* [KARTEにおけるKubeflow Pipelineの活用](https://tech.plaid.co.jp/kubeflow-pipeline-first-step/)
  + PLAID社のブログ
* [Kubeflow Pipelines with AI Platform](https://www.qwiklabs.com/focuses/10948?catalog_rank=%7B%22rank%22%3A2%2C%22num_filters%22%3A0%2C%22has_search%22%3Atrue%7D&parent=catalog&search_id=5957785)
  + Kubeflowっていうか、AI Platform Pipelinesのqwiklabsハンズオン
  + 英語

英語だけど分かりやすいし、[公式ドキュメント](https://www.kubeflow.org/docs/)は必ず見るべし。


# おまけで話したこと

* [Google Cloud Day: Digital Archives](https://cloudonair.withgoogle.com/events/google-cloud-day-digital)
  + 2020/6月末までアーカイブ公開
* [Qwiklabsの1ヶ月無料キャンペーンページ](https://inthecloud.withgoogle.com/training-discount-jp-q2-20/register.html)
  + 2020/7月末まで申し込み可能

