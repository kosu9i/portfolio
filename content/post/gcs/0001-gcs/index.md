---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "GCS概要"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-27T01:47:34+09:00
lastmod: 2020-04-27T01:47:34+09:00
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

# ストレージクラス

{{< figure src="gcp-storage-pricing.png" title="GCS料金表" numbered="true" lightbox="true" >}}

GCSでは「地理的冗長性」と「アクセス頻度」の2軸でストレージクラスを決定する。  
表を見ると分かりやすい体系になっている（個人的感想）

## 地理的冗長性

* Region
    + 単一リージョン
    + VMインスタンスと同じリージョンにすると低レイテンシとなる。
* Multi-region
    + 複数のリージョンで地理的に冗長化
    + `us` , `eu` , `asia` から選べる
    + VMインスタンスと同じリージョンにして低レイテンシとすることができない。
* Dual-region
    + ある特定の2リージョンに冗長化
        + `nam4` アイオワとサウスカロライナ
        + `eur4` オランダとフィンランド
    + 上記に要件が当てはまらない場合はまず使わない
    + VMインスタンスと同じ（もしくは近い）リージョンにすると低レイテンシとなる。
    + コストは一番高い

### そもそも地理的冗長性って

GCS, S3ともにイレブン9の耐久性があるはず。これはシングルリージョンでも変わらない。  
じゃあなんで地理的に冗長化する必要があるか。

そもそもイレブン9の算出には想定外の故障（災害など）は考慮されていないはず。  
極端な話、1つのリージョン全体が壊滅的な被害を受けた場合、
当然データは消失する。
これを避けたいのであればリージョン分散はすべき、という考え方。なはず。


## アクセス頻度

* Standard
* Nearline
* Coldline

昔はDRA（低可用性な代わりに低価格）っていうのもあった。今は非推奨。
（Standardの価格が下がって、DRAの意味がなくなった。今は低可用性でコスト抑えるならNearlineになる）


# データ取得

* S3 Glacierはテープバックアップを使用しているらしい。  
  なので、データ取り出しに時間がかかる。

* GCSのNearline, Coldlineはテープを使用していない。  
  低価格のストレージ機器を使っており、データ取り出しは数秒でOK。

# イレブン9

* イレブン9とは「耐久性」であり、可用性は99.99%（1年間で50分強はデータにアクセスできない状態がある）
* 10,000個のオブジェクトのうち1オブジェクトを失うのに1,000万年かかる。

# オブジェクトストレージとは

## 参考
* [ストレージ オブジェクトストレージとは - 富士通](https://www.fujitsu.com/jp/products/computing/storage/lib-f/tech/beginner/object-storage/)
* [5分で絶対に分かるオブジェクトストレージ (3/5) - IT](https://www.atmarkit.co.jp/ait/articles/1705/29/news014_3.html)

## vs ファイルストレージ
* 保存期間, コピー回数など多くのメタデータを保持できる
* ディレクトリのような階層構造はない（S3やGCSでスラッシュ区切りになっているのは、オブジェクトパス名に `/` が入っているというだけ）
* 一般的には汎用ストレージを並列構築しており、スケーラビリティに優れている。
    + フラットな構造でデータを保存するので、データを分散して保持しやすい。
    + ファイルストレージでは、階層構造を持っているのでここの階層はこっちのストレージサーバ、など
      細かく構築してあげないといけない。
* 更新が少ない大容量データに向いている。
    + S3では1ファイルサイズの上限は5TB（1PUT上限は5GBなのでMultipartUploadで分割アップロードする必要はあり）
    + GCSも5TB。1PUTの上限も5TB。
* データ操作にREST APIが必要

## vs ブロックストレージ
* ブロックストーレジは、1ファイルを複数ブロックに分けて保持。
    + 低レイテンシも実現できる。
    + 一般的に高価。
    + そもそもファイルストレージとはレイヤーが違う。
      ブロックストレージをファイルストレージとして利用する、など。
* EBSはブロックストレージ
* ブロックストレージは部分更新が可能。
    + オブジェクトストレージはオブジェクト単位でatomic。つまり部分的な更新だとしてもオブジェクトをまるごと更新する。

# S3との比較

## リージョン

リージョンはS3と同様に選択可能。
Multi-regionというのもあり、特定のざっくりした地域（`us` , `eu` , `asia`）に勝手に冗長化してくれる。


## アベイラビリティゾーン

特に選択できない。S3の標準も勝手にマルチAZになるはず。
S3には `1ゾーン` っていうシングルAZで低コスト、というオプションも選べる。これはGCSには見当たらなかった。

## ファイル構造

S3と同じくバケット > オブジェクト、という構造。
一般的なオブジェクトストレージと同義。


## ストレージクラス

S3ほど細かくはなっていないが、オブジェクトごとに設定可能。
GCSではgsutilコマンドを使う必要あり。S3はブラウザで色々設定変更できて楽だなと思う。

## ライフサイクル

S3と同様、一定時間が経過したら「削除」したり「ストレージクラスを変更」というルールを書ける。

## アクセスコントロール

### GCSのアクセスコントロール

* Bucket単位での権限付与（[バケットポリシー](https://cloud.google.com/storage/docs/bucket-policy-only?hl=ja)）
    + バケット単位でざっくり権限付与。S3の「バケットポリシー」とは大分意味が違う！
    + Cloud IAM（GCPプロジェクトごとに「オブジェクトの削除・更新」とかの権限が設定される）でのアクセスコントロールになる。
    + ACLは無効になる
    + 現在β版
    + オブジェクト単位での一般公開（Webホスティング）ができなくなる。
* オブジェクト単位での権限付与（[アクセス制御リスト](https://cloud.google.com/storage/docs/access-control/lists?hl=ja)）
    + Default ACLを設定できる。（ただしgcloudコマンド必要）
    + Cloud IAMでのざっくり設定が推奨されている。ただしオブジェクトごとに権限を付与したかったらACLを使うしかない。

### S3で出来て、GCSでできないこと

* IP制限
    + [VPC Service Controls](https://medium.com/google-cloud-jp/gcp-secure-protection-with-vpc-service-controls-part-1-85643fbfb674)というのを別途使えばできる。
* prefixでの制限
    + `s3://bucket1/dir1/*` みたいな書き方はできない

### 注意点

* S3と似たようで、内容が非なる用語がたくさんあり、かなり混乱すると思う。  
  S3に慣れている場合は注意。（逆もまた然り）
* GCSの中でも「レガシーバケットポリシー」とか最新のポリシーとかあって、混乱する。  
  ドキュメントを見ながら、実際に構築して慣れるのが良い。
* S3, GCSともに、こういう権限系は手動でやることなかれ。  
  少なくとも本格運用時には、必ずJSONなり権限を定義したファイルを用意してそれをメンテナンスしていくべし。

## 暗号化

GCSでも可能。以下の選択が可能。
* GCP側で全部やってくれる
* GCP KMSでクラウド上にそれぞれの鍵で管理
* オンプレ上のそれぞれの鍵で管理

S3のようにオブジェクトごとに暗号化オプションを選択するには [gsutilコマンドを使う](https://cloud.google.com/storage/docs/encryption/using-customer-managed-keys?hl=ja#add-object-key) 。

## WEBホスティング

S3と同様、権限をpublicにすることで静的ファイルをホスティングすることが可能。

* 独自ドメインも設定可能（CNAMEでGCSの発行したドメインに紐付ける）
* デフォルトでHTTPS
* デフォルトページ（ディレクトリアクセスしたときのindex.html的な）やエラーページも指定できる。
* AWS Cloud Frontのキャッシュを介したアクセスはちょっと特殊。  
  メタデータに `Cache-Control: public,max-age=3` などと書くとGoogleのエッジキャッシュというのが有効になるらしい。
    + [GCP エッジキャッシュ](https://qiita.com/sinmetal/items/37c105a098174fb6bf77)。
    + [Cloud Storage のベスト プラクティス](https://cloud.google.com/storage/docs/best-practices?hl=ja#traffic)


## ロギング

ロギングを有効にできる。Stack Driver（Cloud WatchのGCP版）に保存できたり。  
ただしgcloudコマンドで設定する必要あり。  
Cloud Audit Logging（監査ログ）ってのもある。

## セキュリティ対策

上述の「Cloud Audit Logging」ってのがある。（Cloud TrailのGCP版）
アラートも設定可能。

## API

上述の通り、GCPコンソール（ブラウザ）で設定できる項目が結構少ない。
gcloudコマンドを多用することになる。

