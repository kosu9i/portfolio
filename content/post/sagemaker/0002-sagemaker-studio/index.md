---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "SageMaker Studio（準備編）"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-05-01T15:34:53+09:00
lastmod: 2020-05-01T15:34:53+09:00
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

# SageMaker Studio

* 2019年末に公開されたSageMakerの新機能。
* 要はマネージドなJupyter Lab。
* 同じく2019年末に発表された新しい機能（Experiments, Autopilotなど）もJupyter Lab上で使える。
* 使えるリージョンは現在限定されているらしい。（下記、developer guideから抜粋）
  + 米国東部 (オハイオ)、us-east-2
  + 米国東部 (バージニア北部)、us-east-1
  + 米国西部 (オレゴン北部)、us-west-2
  + 欧州 (アイルランド)、eu-west-1
* 2020/05/01現在はプレビュー版。商用利用はまだ避けたほうが良い。

最近、日本語版の[SageMaker developer guide](https://docs.aws.amazon.com/ja_jp/sagemaker/latest/dg/whatis.html)もStudio対応している様子。

# SageMaker Studioをオンボード

Studioを使える状態にすることを「オンボードする」と呼んでるっぽい。

1. `Amazon SageMaker Studio` のボタンを押下。
  {{< figure src="start-1.png" title="SageMakerStudio有効化" numbered="true" lightbox="true" >}}

2. デフォルト設定でよければ `Quick start` で `User name` と `Execution role` を選択。  
  `Standard setup` を選択すると、ネットワーク（VPC内にする、とか。ちなみにデフォルトは非VPC）の設定ができたり、タグを付けたりできる。  
  Standardでは、[AWS SSO](https://aws.amazon.com/jp/single-sign-on/)を使えるようになるのもメリットになり得るけど、AWS SSOよく分からん。
  {{< figure src="start-2.png" title="Get started" numbered="true" lightbox="true" >}}

3. `新しいロールの作成` を選択すると、`AmazonSageMakerFullAccess` （SageMakerに必要な機能へのアクセス全部盛り）でIAMロールが作成できる。あらかじめアクセスできるS3の制限もこの時点で記載可能。
  {{< figure src="start-3.png" title="Create IAM role" numbered="true" lightbox="true" >}}

4. `送信` を押すとSageMaker Studioの初期化が走る。（数分待つ）

この時点（オンボードしただけ）では、料金はかからないとのこと。

# SageMaker Studio Notebooksを使う

作成したユーザ名の右端にある `Open Studio` をクリックすると、SageMaker Studio（つまりJupyter Lab）が起動する。  
このJupyter Labは[使用するインスタンスタイプに応じてお金がかかる](https://aws.amazon.com/jp/sagemaker/pricing/)。  

{{< figure src="onboard.png" title="On Board" numbered="true" lightbox="true" >}}

## インスタンスタイプの変更

デフォルトでは `ml.t3.medium`（vCPU * 2, Memory 4GB, GPUなし）が選択されている。
インスタンスタイプは、notebookごと（つまり*.ipynbのファイルごと）に変えられる。  

{{< figure src="instance-type.png" title="Change instance type" numbered="true" lightbox="true" >}}

ただ、[同じインスタンスタイプを使っている複数notebookでは、インスタンスが共有されるらしい](https://docs.aws.amazon.com/ja_jp/sagemaker/latest/dg/notebooks-usage-metering.html)。

上記リンクから引用した計測例。

> ノートブック #1 を開きました。Studio では ml.t3.medium インスタンスタイプでこれを開きます。  
> 1 時間後に、ノート #2 を開きました。このノートブックは、ノートブック #1 と同じインスタンス (ml.t3.medium インスタンスタイプ) で実行されます。  
> 1 時間後に、ノートブック #3 を開き、すぐに ml.m5.large インスタンスタイプに切り替えました。  
> さらに 1 時間後、すべてのインスタンスタイプでカーネルをシャットダウンします。
> 
> ノートブックが実行された時間は次のようになります。
> * ノートブック #1: 3 時間
> * ノートブック #2: 2時間
> * ノートブック #3: 1 時間
> 
> お客様には、以下の使用について請求されます。
> 
> 3 hours at the ml.t3.medium rate +  
> 1 hour at the ml.m5.large rate  
>
> 2 時間目と 3 時間目の間に、ノートブック #1 とノートブック #2 が同じ ml.t3.medium インスタンスで実行されました。

notebookのインスタンスでGPU付きも選択できるが、そもそも学習などリソースを使う作業はnotebookのインスタンスでは行わず、別途[トレーニングジョブ](https://docs.aws.amazon.com/ja_jp/sagemaker/latest/dg/how-it-works-training.html)を発行すべき。  
notebookはEDAなどの作業で使うのが良かろうと思われる。

## データの準備

SageMakerで利用するデータはS3に置くのが基本。  
最初に指定したIAMロールであればS3のバケット作成や、`[Ss]age[Mm]aker`という名のバケット配下にあるオブジェクトのGet, Put, Deletなどが可能。
下記、`arn:aws:iam::aws:policy/AmazonSageMakerFullAccess`に付与されているポリシーの一部。

```json
...略...
{
    "Effect": "Allow",
    "Action": [
        "s3:GetObject",
        "s3:PutObject",
        "s3:DeleteObject",
        "s3:AbortMultipartUpload"
    ],
    "Resource": [
        "arn:aws:s3:::*SageMaker*",
        "arn:aws:s3:::*Sagemaker*",
        "arn:aws:s3:::*sagemaker*",
        "arn:aws:s3:::*aws-glue*"
    ]
},
{
    "Effect": "Allow",
    "Action": [
        "s3:GetObject"
    ],
    "Resource": "*",
    "Condition": {
        "StringEqualsIgnoreCase": {
            "s3:ExistingObjectTag/SageMaker": "true"
        }
    }
},
{
    "Effect": "Allow",
    "Action": [
        "s3:CreateBucket",
        "s3:GetBucketLocation",
        "s3:ListBucket",
        "s3:ListAllMyBuckets",
        "s3:GetBucketCors",
        "s3:PutBucketCors"
    ],
    "Resource": "*"
},
...略...
```


## シャットダウン

notebookのタブを閉じてもシャットダウンされない...？（**未確認**）

[kernel自体のシャットダウン](https://docs.aws.amazon.com/ja_jp/sagemaker/latest/dg/notebooks-run-and-manage-shut-down.html)を別途行う必要があるとすれば、結構不親切なのでは...  
未シャットダウンのインスタンスで料金が発生してしまうと嫌だな。

