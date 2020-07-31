---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Dockerfileで思考停止的にENV DEBIAN_FRONTEND noninteractiveを書いてはいかん"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-07-31T17:48:01+09:00
lastmod: 2020-07-31T17:48:01+09:00
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

タイトルどおり、私は今までUbuntu系のイメージを作成するときに  
`ENV DEBIAN_FRONTEND noninteractive` をおまじない的に書いてしまっていたが良くない。

[公式ドキュメント](http://docs.docker.jp/engine/faq.html#dockerfile-debian-frontend-noninteractive)でも非推奨と書いてある。

そもそもこのおまじないを書くのは、apt installするときにダイアログボックスを開こうとするパッケージがあって  
そのインストール時に失敗するから。

Dockerfile内で `ENV DEBIAN_FRONTEND noninteractive` としてしまうと  
そのDocker imageを使っているときに、何も知らないユーザがコンテナ内で追加でapt installしようとする（その良し悪しは置いといて）と  
環境変数が継承されたままなので、悪影響を及ぼす可能性がある。

そのため、公式では`DEBIAN_FRONTEND`環境変数を最終的にはデフォルト値（多分`newt`かな）に戻せとある。

私はデフォルト値が`newt`なのか確信がないので、Dockerfile内ではapt installするときに  
```
RUN apt-get update && DEBIAN_FRONTEND=noninteractive apt-get install -y \
  git \
  ...
```
のようにapt実行時にだけ適用することにし、再び思考停止した。
