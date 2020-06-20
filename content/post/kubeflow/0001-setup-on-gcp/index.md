---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "GCPでのKubeflowセットアップ"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-06-19T12:32:51+09:00
lastmod: 2020-06-19T12:32:51+09:00
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

KubeflowをGCP上でセットアップしていく。  
[公式ドキュメント](https://www.kubeflow.org/docs/gke/)が充実しているので、それに沿っていく。

# 基本的な流れ

1. GCPプロジェクトの準備
2. 作業に必要なCLIツールなどの準備
3. Cloud IAPのセットアップ
4. Kubeflowのデプロイ


# GCPプロジェクトの準備

GCPを扱う上で基本的な作業なのでここでは割愛。  
一応公式ドキュメントにも[説明されたページ](https://www.kubeflow.org/docs/gke/deploy/project-setup/)があるので、必要に応じて参照。

重要なのは

* 上記ドキュメントに列挙されているAPIを有効化しておく
* 無料枠ではKubeflowはできないので、有料アカウントでやる

くらいか。


# 作業に必要なCLIツールなどの準備

[Kubeflowが用意しているUI](https://deploy.kubeflow.cloud/#/)から[ポチポチしながらKubeflowを構築する手順](https://www.kubeflow.org/docs/gke/deploy/deploy-ui/)もあるが  
手でポチポチするのは面倒なので、[CLIを用いた構築手順](https://www.kubeflow.org/docs/gke/deploy/deploy-cli/)をやっていく。

## kubectl

Macではバイナリをcurlでダウンロードするか、Homebrewで入れられる。  
どちらの方法でもOK。最新版を入れておく。  
参考: [macOSへkubectlをインストールする](https://kubernetes.io/ja/docs/tasks/tools/install-kubectl/#install-kubectl-on-macos)

## gcloud

gcloudコマンドは最新にしておく。

```bash
$ gcloud components update
````

# Cloud IAPのセットアップ

GCPでKubeflowを使う時は[IAP](https://cloud.google.com/iap/docs/concepts-overview?hl=ja)の利用が推奨されている。  
使わなくてもイケるっぽいが、いくら検証目的でも認証なしは怖いのでやっておく。  
ちなみにBasic認証はKubeflow v1.0では[Deprecatedになってる](https://www.kubeflow.org/docs/gke/deploy/deploy-cli/#basic-authentication-deprecated)。

参考: [Set up OAuth for Cloud IAP](https://www.kubeflow.org/docs/gke/deploy/oauth-setup/)



# デプロイ

Deployment managerを利用する。  
エラーになったとき、deploymentが残っていて再実行ができないときがあるので削除する。

