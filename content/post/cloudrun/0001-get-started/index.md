---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Cloud Run ことはじめ"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-07-06T01:37:35+09:00
lastmod: 2020-07-06T01:37:35+09:00
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

# 概要

Cloud Runって？

* フルマネージドのコンテナ向けサーバレス
  - 使っていない時はゼロまでスケールインする。
* AWSのFargateに近いが、時間制限によってLambdaとFargateの中間、みたいな使い勝手に個人的には感じる。
* 処理時間に応じて課金（100ms単位）
  - かなり安い（1vCPU秒あたり$0.000024, メモリ1GiB/秒あたり$0.000025, 100万リクエストあたり$0.40）。
  - Always Free（有料アカウントでも使える無料枠）もある。
* Knative（後述）をベースにしている。
* 実行時間の制限あり。（デフォルト5分、最大15分）
  - イメージのデプロイ時に設定可能。（参考: [公式: リクエスト タイムアウトの設定](https://cloud.google.com/run/docs/configuring/request-timeout?hl=ja)）
  - AWS Fargateは時間なしだったような。
* GPUは使えない。
  - Cloud Run for Anthosでは[GPU使えるけど、15分制限は同じ](https://cloud.google.com/serverless-options?hl=ja#%E3%83%97%E3%83%AD%E3%83%80%E3%82%AF%E3%83%88%E3%81%AE%E6%AF%94%E8%BC%83)。


# ユースケース

k8sを使うほどではないマイクロサービスに向いているとのこと。  
参考: [GKE と Cloud Run、どう使い分けるべきか](https://cloud.google.com/blog/ja/products/containers-kubernetes/when-to-use-google-kubernetes-engine-vs-cloud-run-for-containers)

公式ドキュメントに記載されているもので個人的にしっくりきたものを以下に抜粋。

* シンプルな構成のAPIやWebサイト
* GSuiteと連携するバックエンドアプリケーション
* 短時間で終わるデータ処理でコンテナ使いたいとき

参考: [Cloud Run公式ドキュメント ユースケース](https://cloud.google.com/run?hl=ja#section-5)

基本的には**シンプルな構成**のアプリケーションで**コンテナを使いたい場合**、になると思う。  
また、制限時間があるので1つのコンテナ処理時間が短いもの。


# 基本的な使い方

1. GCRにDockerイメージをpush
2. Cloud Runをデプロイ

これだけ。

デプロイすると、ダッシュボード上で簡単なメトリクスが見れたり。

{{< figure src="./cloudrun-1.png" title="Cloud Run ダッシュボード" numbered="true" lightbox="true" >}}

StackDriverのログが見れたり。

{{< figure src="./cloudrun-2.png" title="Cloud Run ログ" numbered="true" lightbox="true" >}}

デプロイしたコンテナごとに固有のHTTPSエンドポイントが付与される。  
（[カスタムドメインのマッピングも出来るけどベータっぽい。](https://cloud.google.com/run/docs/mapping-custom-domains?hl=ja)）  
このエンドポイントにリクエストを送ることで、コンテナ内のアプリケーションが実行される。

コンテナ内のコードは
> PORT 環境変数で定義されたポートで HTTP リクエストをリッスンする必要があります。

参照: [コンテナをビルドする](https://cloud.google.com/run/docs/building/containers?hl=ja)

つまりバッチ処理だろうが、Flask的なHTTPサーバをコンテナ内に用意しなければならない。  
この理由からバッチ処理よりは、REST APIやWebアプリケーションに向いてそう。


# Knative

k8s上でサーバレスワークロードを開発・管理するためのプラットフォーム。  
Knativeとは？をやり出すと膨大になるので割愛（~~というか知識不足で説明できない~~）  
参考: [公式ドキュメント](https://cloud.google.com/knative?hl=ja)  
ちなみにKubeflowのサービング（[KFServing](https://github.com/kubeflow/kfserving#kfserving)）にもKnativeが使われている。

デプロイ、サービング、オートスケールなど、コンテナアプリケーションの構築で面倒なところを助けてくれる。

Cloud RunはKnativeをベースにすることで、Kubenetes, Cloud Run, Cloud Run for Anthos間の移行がスムーズになっているとのこと。


# 起動時間

ゼロにスケールする、ということはゼロから新規起動時には遅そう。  
公式ドキュメントにも、コールドスタートが発生するとあるらしい。

よく検証されているブログがあったのでリンクを貼っておく。  
[Cloud Runをコールドスタートからレスポンスタイムが安定化されるまでどのぐらいかかるか](https://medium.com/google-cloud-jp/cloud-run%E3%82%92%E3%82%B3%E3%83%BC%E3%83%AB%E3%83%89%E3%82%B9%E3%82%BF%E3%83%BC%E3%83%88%E3%81%8B%E3%82%89%E3%83%AC%E3%82%B9%E3%83%9D%E3%83%B3%E3%82%B9%E3%82%BF%E3%82%A4%E3%83%A0%E3%81%8C%E5%AE%89%E5%AE%9A%E5%8C%96%E3%81%95%E3%82%8C%E3%82%8B%E3%81%BE%E3%81%A7%E3%81%A9%E3%81%AE%E3%81%90%E3%82%89%E3%81%84%E3%81%8B%E3%81%8B%E3%82%8B%E3%81%8B-abdb9bbc84bf)

コールドスタートの発生を防ぐために、一部のインスタンスをアイドル状態にすることがあるらしい。（[公式ドキュメント: インスタンスをアイドル状態にしてコールド スタートを最小限に抑える](https://cloud.google.com/run/docs/about-instance-autoscaling?hl=ja#idle-instance)）  
多分、アイドル状態時に課金はされないはず。（されないでくれ）

Cloud Schedulerなどで定期的にリクエストをCloud Runに投げる、など工夫も可能。
[参考: [Cloud OnAir] Cloud Run Deep Dive ~ GCP で実践するモダンなサーバーレス アプリケーション開発 ~ 2019年9月12日 放送
](https://www.slideshare.net/GoogleCloudPlatformJP/cloud-onair-cloud-run-deep-dive-gcp-2019912)


# 一緒に使いそうなサービス

## Cloud Build

GCPのCIサービス。Cloud Buildのコンテナ内でビルドしたDockerイメージをGCRにpushできる。  
Cloud Runのデプロイ時に、GCRにあげたイメージ名を指定する。  
（Cloud Buildを使わなくても、ローカルでdocker buildしてGCRにpushしてもOK）

## Cloud Tasks

マネージドなキュー。非同期実行したいときに使う。  

## Cloud Pub/Sub

マネージドなPub/Sub。同じく非同期実行したいときに使う。
