---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "機械学習基盤としてのクラウドサービス活用"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-27T01:51:39+09:00
lastmod: 2020-04-27T01:51:39+09:00
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

# クラウドでの機械学習

## 機械学習の学習ジョブをクラウドでやる場合の選択肢

マネージドなバッチ実行サービスは色々とあるが、機械学習用途に使えるのは意外と少ない気がする。  
以下の条件を満たす必要がある。

* 時間制限がない（学習に時間がどれくらいかかるか、最初はわからないことも多いため）
* 深層学習を使う場合は、多くはGPUが必要になる

多分、選択肢は以下になる。（AWS, GCPのみに絞った場合。Azureはごめんなさい、わかりません...）  
おすすめ順に記載する。

1. もともと機械学習基盤として売っているもの
    - SageMaker（AWS）
    - AI Platform（GCP）
    - そもそも機械学習向けに設計されてるので、使いやすいのは当たり前。
    - k8sとか自前で構築したくない・できない人向け。
2. Kubernetes関連でJobというWorkloadsを使う
    - GKE（GCP）
    - EKS（AWS）
    - 自前で基盤を開発したい・できる企業向け。  
      自社プロダクトの実行環境にk8sを導入している企業は増えてきていると思うので、  
      それとの親和性は高いと思う。
3. AWS Batch（AWS）
    - GPUが使える
    - ドキュメントにも「深層学習のジョブ実行環境として」という文言がある。
    - 構築がやや面倒かも。重厚長大なイメージ。
    - 他のジョブとのパイプラインを組みたいならありかも。
4. ECS Task
    - GPUは使えるっぽい
    - ECSクラスタをすでに持ってたらアリかもしれないけど、ECSクラスタを今から構築するのは微妙...？
5. 番外編：EC2やGCEなどVMインスタンスをアドホックに起動・停止

以下は、使えない。

* Cloud Run（GCP）
    - GPUは使えるっぽい
    - 時間制限がある（多分...確か最大15分までだったはず）
* Fargate（AWS）
    - GPUが使えない
* Lambda（AWS）、Cloud Function（GCP）
    - 時間制限あり

GPUが必要じゃない学習タスクの場合は、以下も選択肢になってきそう。

* Fargate（AWS）
    - 時間制限はない

### 学習ジョブのみで見たSageMaker vs AI Platform

総合的にはSageMakerだと思っているが、学習ジョブ実行環境としてのみ、だと  
どちらとも言えない。

* SageMaker
    + スポットインスタンスが使えるのはめっちゃいい
    + デフォルトだと同時に使えるGPU数が少ない
        - 1インスタンスに複数GPUがついてしまっているので、個別には使えない
* AI Platform
    + プリエンプティブルインスタンスが使えないのは痛い
        - GKEだとpreemptibleインスタンス使えるので、k8sユーザはGCPも良いかも
    + T4は意外と使いどころあるかも
    + デフォルトで使えるGPU数が多い
    + TPU使える

両者ともに言えることだが、すべての機能を使う必要はない。  
学習ジョブを実行する環境として使うだけ、でも割と恩恵は受けられると思うので  
GPUクラスタを自前で持てない場合はおすすめ。


### 余談

先日、社内のGPUクラスタが消費電力オーバーでいっせいに落ちた。  
クラウドに基盤を持っておくと色々うれしいこともある。

* 従量課金
* メンテナンス費用がいらない（電気代、土地代）
* 運用者の人件費がいらない（障害対応、新規マシンのセットアップなど）
* 最新のGPU機種がすぐに使える


## SageMaker, AI Platformでの推論API

どちらも推論用のAPIをサクッとたてられる。

### どうやってやるの？

AI PlatformだとTensorflowのSavedModelという形式で保存すると  
signature（入出力の情報）が埋め込まれる。  
なので、それで足りる場合はSavedModel形式のモデルをデプロイするだけでAPIが動作する。

ただ、入力データへの前処理、推論結果への後処理が必要なケースも多い。  
そういう場合は独自の関数を定義して、APIの実行前後に挟み込むことができる。

### 使いどころ

機械学習のプロダクトは、トライアンドエラーの繰り返し。  
そのため、手っ取り早くユーザ・開発者からのフィードバックを受けて、  
モデルを改善していく必要がある。

APIを簡単にたてられる人なら良いが、必ずしもデータサイエンティストのタスクではない。  
また、APIに必要なインフラの管理もめんどくさい。

なので、作ったモデルをすぐにAPIとしてデプロイし、誰かに使ってもらう、という  
用途に向いている。  
これによって機械学習プロダクトの開発サイクルを速めることができるはず。

k8sでそういう基盤がある人はそれを使えばいいが、ない場合は  
SageMaker, AI Platformでやっちゃえばいいと思う。

