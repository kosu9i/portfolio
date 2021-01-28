---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "GCP上でのETLいろいろ"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2021-01-13T01:39:53+09:00
lastmod: 2021-01-13T01:39:53+09:00
featured: false
draft: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

Courseraの「[Building Batch Data Pipelines on GCP](https://googlecourses.qwiklabs.com/course_templates/109)」を受講した上での整理。

# ETLとは？

Extract, Transform, Loadのこと。  
データソース（多くは各アプリケーションから蓄積しているDBやストレージ） => 変換処理 => 一元的なデータ置き場（DB, DWHなど）という流れになる。

ELT, ELもある。これらとの違いは変換処理の有無や順番。  
Transformが単純なSQLで書けない（もしくは書きづらい）ような複雑なものであったりTransformに時間がかかる場合はETL, そうでない場合はELT, TransformなしでいけるならELという感じ。

{{< figure src="ETLandELTRedshift1.png" title="ETL - ELT 引用: https://aws.amazon.com/jp/blogs/news/etl-and-elt-design-patterns-for-lake-house-architecture-using-amazon-redshift-part-1/" numbered="true" lightbox="true" >}}

有名でよくサンプルとして使われる、ファイル内の単語数を単語ごとに集計する[Word Count](https://beam.apache.org/get-started/wordcount-example/)というタスクがある。


# GCPにおけるETLの選択肢

欲しい機能・非機能要件によって色んな選択肢がある。

* Dataproc
* Data Fusion
* Dataprep
* Dataflow

AWSとの比較ドキュメントとして[「AWS プロフェッショナルのための Google Cloud: ビッグデータ」](https://cloud.google.com/docs/compare/aws/big-data)も公式に記載があるので興味がある場合見てみると良い。


## Dataproc

GCP上でマネージドにHadoop, Sparkなどの分散コンピューティングを利用できる。

* オンプレミス上でHadoopを利用する場合、ストレージとコンピューティングリソースの分離がしづらく、HDFSに永続化しておくためにクラスタを常時起動しておかないといけない、という困り事がある。
  - DataprocではGCSにデータを永続化しておくことが推奨されている。
  - GCSでも超高速（1Pbit/s）な内部ネットワーク（Jupiterネットワーク）で接続されている（[2分割帯域](https://postd.cc/how-google-invented-an-amazing-datacenter-network-only-they-could-create/)）ため遅延は少ない。（とはいえローカルSSDよりは低速）
  - これによりクラスタはいつでも起動・停止可能。
  - `hdfs://` を `gs://` に書き換えるだけ。
* コンピューティングリソースをいつでも拡張・縮小可能。
  - Auto Scalingもある（頻発する際はAuto Scalingが得意なDataflowへの置き換えが推奨されている）
* アイドル状態のクラスタを自動削除することも可能。


### ユースケース

* オンプレミスでHadoop, Sparkなどをすでに利用していてクラウド移行したい場合
  - 基本的にリフト＆シフトが可能（永続化にGCS利用する修正くらいはお手軽だし効果大なのでやったほうが良い）

### GCSではなくHDFSをストレージとして利用した方が良いケース

* メタデータ（パーティションやディレクトリなど）の更新が頻繁に行われる
* ファイルサイズが小さい
* ディレクトリのリネーム操作が多い時（GCSはディレクトリのリネームが遅い。というか全コピーが走る）
* append操作が多い
* パーティション分割した書き込みなど重い操作が多い
* 数ミリsecのレイテンシも許容できない

ただしこれらの場合でも中間データはHDFSを利用するとして、最初と最後（つまり永続化）にはGCSを利用すべき。  
また、HDFSにSSDではなくHDDを利用すると速度の恩恵はほとんどない。

### よりクラウド最適化するために

オンプレミスのHadoop, Sparkコードをリフト＆シフトで利用できるものの、元のコードの作りによってはクラウドの恩恵を最大化するために改善できることもある。

具体的には、処理がエフェメラルクラスタとなるよう工夫すべき。  
つまり永続化にはGCSなどHDFS以外を利用し、コンピューティングとストレージとの分離を図る。  
これによってクラスタリソースはいつでも破棄可能となり、クラスタリソースサイズの縮小、自動削除、プリエンプティブルVMの利用がしやすくなる。

例えば、Dataprocのクラスタ上でJupyter notebookなどを起動できるがいつもここから実行しているとクラスタを削除しづらい。（ついnotebookのローカルストレージに一時ファイルを保存しちゃうなど）  
Hadoop/Sparkの実行はスタンドアロンなスクリプトとして括りだしておき、クラスタ外部からジョブとして実行できるようにしておくと良い。（クラスタを単にコンピューティングリソースとしてだけ利用する）


### 使い方概要

1. Clusterを起動。
  * 冗長構成, マシンスペック, Hadoop/Sparkのバージョンとか選べる
  * 起動するとVMインスタンス, 作業用のGCSとかが勝手に作られる
  * Jupyter notebookとかも起動できる。
    - `gs://<自動的に作られるバケット>/notebooks/jupyter` 配下がmountされているのでこのGCSにアップロードすればDataproc内のJupyter notebookから参照可能。
    - このJupyter notebookにもDataprocのGCPコンソール上に表示されるリンクからシームレスに接続可能。
    - Jupyterはマスターノードで起動している様子。
2. ジョブを実行。
  * Hadoop/SparkのSDKを使って実行 or `gcloud dataproc` コマンドからジョブとして起動。
  * 前者はコンソール上に実行記録は残らないが、後者は記録が残る。
3. Clusterを停止。
  * この時点でほぼ課金（VMインスタンスが停止する）はストップになるはず。
  * HDFSに保存されたデータは残る。（メモリのみのデータは当然消える）
4. Clusterを削除。
  * クラスタに利用されていたVMインスタンスが削除される。
  * 上記の作業用のGCSも削除される...と思いきや残るっぽい。けど、念の為永続化用のGCSは自前で別に用意した方がよさそう。


## Data Fusion

{{< figure src="datafusion.png" title="Data Fusion概観" numbered="true" lightbox="true" >}}

* GUIでETLが組める。内部ではDataprocが走る。
  - Dataprocのクラスタは自動起動・削除される。
  - 既存のDataprocクラスタにプロビジョニングすることも可能。
* 将来的にはDataflowでの実行もサポートされる予定。
* パイプラインのテンプレート化も可能。
* 「データリネージ」の追跡が可能。
  - データの派生元, 変換した内容, メタデータなど。
* Data Fusion Studioを使ってGUI上でDAGを定義してパイプラインを構築していく。
  - 各ノードはあらかじめ処理が定義されていてコーディングは不要。
* スケジューリング実行機能もあり。
* バッチ処理のみ。ストリーミング処理はDataflowにて。

想定されるユースケースとしては「GUIでETLを組みたい」の一点に尽きると思う。   
手軽に試せるしexportもできるので資産管理もある程度可能、スケールもある程度やってくれる。ローコードでETLを実践したいときに便利。


## Dataflow（まだ書き途中）

GCPでのETL本命。

* フリマネージドなApache BEAM（Batch + strEAM）
* バッチとストリーミング両方に同じコードで対応可能

### Dataprocとの使い分け

基本的にGoogleはDataflow推しの様子。

* 既存のHadoop, Spark資産を使いまわしたかったらDataproc, それ以外はDataflow 
* サーバレスではなくクラスタ管理を自分たちで行いたい場合（DevOpsアプローチに慣れている場合）Dataproc, それ以外はDataflow

{{< figure src="dataflow1.png" title="DataprocとDataflow比較表" numbered="true" lightbox="true" >}}

{{< figure src="dataflow2.png" title="DataprocとDataflow使い分けフローチャート" numbered="true" lightbox="true" >}}

### バッチとストリーミング

* バッチは開始と終了がある有限のデータを処理する
  + 1940年代、パンチカードで処理していた。このパンチカードの塊をバッチと呼んでいた。
* ストリーミングは流動的な水の流れのような持続的なもの
  + 処理自体は細切れにされたマイクロバッチで処理されることが多い

{{< figure src="dataflow3.png" title="バッチとストリーム" numbered="true" lightbox="true" >}}

Dataflowでどちらも同じように処理可能としているのは以下の4つの概念。

* PTransforms: 処理
* PCollections: データ
  - データはすべてバイト列にシリアライズされて保持。これによりネットワーク転送時にデシリアライズする必要なし。
* Pipeline: ワークフロー
* Pipeline Runnners: 処理クラスタ

{{< figure src="dataflow4.png" title="Dataflowプログラミングモデル概要" numbered="true" lightbox="true" >}}

### Dataflowの特長

* 単にワークフローを構築するだけでなく、内部でグラフの最適化が行われる。
* ジョブ実行中に動的なオートスケーリング
* Apache Beam環境さえ構築できればどこでも動く
  - Pythonであればpip installで構築可能

