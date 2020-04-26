---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "GCP AI Platform概要"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-27T01:50:05+09:00
lastmod: 2020-04-27T01:50:05+09:00
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

# AI Platform（GCP）について

## 概要

* 機械学習プロジェクトの開発基盤
* 旧ML Engineというサービスがベースとなっている
    + notebook（jupyter lab）の利用
    + 学習, 推論ジョブの実行
    + モデルのデプロイ・管理
    + 推論APIの構築
    + モニタリング
* AI Platformは、GCPが提供している機械学習関連のサービスもろもろを  
  統合的に扱えるようにする、という概念的なものともいえる
* AI Hubというリポジトリもある


## 推しな点

* Trainingのマネージドなジョブ
    + GPUが使えて時間制限がない、っていうマネージドな環境は意外と他に無い
    + GPUの同時利用数が多い
    + TPUが使用できる
* 推論APIのホスティング
    + 自動スケーリングできる
* notebook上で他のサービスと連携可能
    + 特にBig Queryとの連携はうれしいかも


## 残念な点

* 各ML系サービスをシームレスに使えると言っているが  
  特別なメニューが用意されているわけではない。  
  認証はシームレスに使えるのでそれはありがたいが...
    + SageMaker Studioが一歩先をいった感

* MLの検証結果を可視化できるツールがあるわけではない。
    + モデル同士の結果を横串で見たりできるツールがあるわけではない。
    + SageMaker Experimentsが一歩先をいった感

* AutoMLとの連携は明示的にはうたっていない
    + SageMaker Autopilot, Processing

