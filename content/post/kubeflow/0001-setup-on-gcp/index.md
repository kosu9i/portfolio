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

## kfctl

Macだと[Githubのアーカイブ](https://github.com/kubeflow/kfctl/releases/tag/v1.0.2)からdarwin版を選んで以下で入れる。

```bash
$ wget https://github.com/kubeflow/kfctl/releases/download/v1.0.2/kfctl_v1.0.2-0-ga476281_darwin.tar.gz
$ tar -xvf kfctl_v1.0.2_<platform>.tar.gz
```

# Cloud IAPのセットアップ

GCPでKubeflowを使う時は[IAP](https://cloud.google.com/iap/docs/concepts-overview?hl=ja)の利用が推奨されている。  
使わなくてもイケるっぽいが、いくら検証目的でも認証なしは怖いのでやっておく。  
ちなみにBasic認証はKubeflow v1.0では[Deprecatedになってる](https://www.kubeflow.org/docs/gke/deploy/deploy-cli/#basic-authentication-deprecated)。

[Set up OAuth for Cloud IAP](https://www.kubeflow.org/docs/gke/deploy/oauth-setup/)を参考にセットアップする。


# デプロイ

## gcloudの設定

gcloudコマンドを最初に使うときにやっておく必要がある。  
要は使用するGCPプロジェクトのGoogleアカウント認証を済ませておく。

```bash
$ gcloud auth login
$ gcloud auth application-default login
```

## 環境変数など準備

デプロイ手順に必要な環境変数を定義しておく。もちろん実行時に直打ちでもOK。  
`CLIENT_ID`と`CLIENT_SECRET`は、GCPコンソールの`APIs & Services -> Credentials`から取得できる。

```bash
export CLIENT_ID=<設定したOAuthのクライアントID>
export CLIENT_SECRET=<設定したOAuthのクライアントシークレット>

export PROJECT=<使用するGCPプロジェクトID>
export ZONE=asia-east1-a # ここの手順だとK80が使えるゾーンを指定する必要がある模様

export KF_NAME="kf-test"
export BASE_DIR=<作業ディレクトリのパス>
export KF_DIR=${BASE_DIR}/${KF_NAME}
export PATH=$PATH:<kfctlをダウンロードしたディレクトリのパス>

export CONFIG_URI="https://raw.githubusercontent.com/kubeflow/manifests/v1.0-branch/kfdef/kfctl_gcp_iap.v1.0.2.yaml"
```

gcloudコマンドが見に行く先のPROJECTなどもセットしておく

```bash
$ gcloud config set project ${PROJECT}    
$ gcloud config set compute/zone ${ZONE}
```

## デプロイ作業

GCPの場合は[Deployment Manager](https://cloud.google.com/deployment-manager?hl=ja)（AWSのCloud Formationみたいなもの）を利用する。  
デプロイが途中でエラーになったとき、deploymentが残っていて再実行ができないときがあるので、その場合はdeploymentを削除してから再実行すると良い。

```bash
mkdir -p ${KF_DIR}
cd ${KF_DIR}
kfctl apply -V -f ${CONFIG_URI}
```

上記だけでOK。10分くらい待つ。  
成功すればGKE上にKubeflowがデプロイされている。

## いろいろ確認

### GKEのクラスタ

GKEの認証情報を取得。

```bash
$ gcloud container clusters get-credentials ${KF_NAME} --zone ${ZONE} --project ${PROJECT}
```

`kubeflow` というネームスペースのGKEクラスタをすべて取得。

```bash
$ kubectl -n kubeflow get all

NAME                                                               READY   STATUS      RESTARTS   AGE
pod/admission-webhook-bootstrap-stateful-set-0                     1/1     Running     0          6m55s
pod/admission-webhook-deployment-64cb96ddbf-2gp87                  1/1     Running     0          6m31s
pod/application-controller-stateful-set-0                          1/1     Running     0          7m56s
pod/argo-ui-778676df64-jrsgb                                       1/1     Running     0          6m58s
pod/centraldashboard-f8d4bdf96-d6dbc                               1/1     Running     0          6m57s
pod/cloud-endpoints-controller-7764d66f9b-hmwp7                    1/1     Running     0          6m

...以下略...
```

150行ぐらい出力される。まぁまぁ大きなマイクロサービス。

### KubeflowのUI

ブラウザから以下にアクセスすれば、KubeflowのダッシュボードUIにアクセスできるはず。  
SSLとDNSのプロビジョニングに時間がかかるようで、20分くらい待ってからアクセスするといいみたい。

```
https://<KF_NAME>.endpoints.<project-id>.cloud.goog/
```

ちなみに一旦デプロイされたKubeflowを削除し、再度同じ名前で上記デプロイを繰り返すと  
このUIへのアクセス時にDNS解決できない旨のエラー（`DNS_PROBE_FINISHED_NXDOMAIN`）が出た。  
根本的な解決方法は見つけられていない（同じドメインに対して異なるIPが割り当てられてコケている？）が、異なる`KF_NAME`で再実行するとうまくいった。


# 削除

デプロイしたKubeflowリソースを削除するには以下。  
参考: [Delete using CLI](https://www.kubeflow.org/docs/gke/deploy/delete-cli/)

```bash
$ export CONFIG_FILE=${KF_DIR}/kfctl_gcp_iap.v1.0.2.yaml
kfctl delete -f ${CONFIG_FILE} --delete_storage
```

上記はストレージリソースも削除するはずだが、自分がやったときはDeployment Managerでストレージが残ってしまっていた。
