---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "SaaS Boost プレビュー版 雑記"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2021-02-22T12:12:40+09:00
lastmod: 2021-02-22T12:12:40+09:00
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

re:Invent 2020の基調講演でAWS SaaS Boostなるものが発表された。

{{< figure src="./aws_saas_boost_2021.png" title="SaaS Boost 引用: https://www.publickey1.jp/blog/20/awssaasaws_saas_boostisvsaasaws_reinvent_2020.html" numbered="true" lightbox="true" >}}

自分たちのソフトウェアをSaaSとして提供するために必要だけど面倒な諸々を助けてくれるもの。（雑）  
これのプレビュー版を申し込んだら承認されたので、使ってみた系の投稿。

SaaS Boost発表時の参考としてはこちら: [［速報］AWS、SaaS構築のフレームワーク「AWS SaaS Boost」発表。ISVがすぐにSaaSを提供可能。AWS re:Invent 2020](https://www.publickey1.jp/blog/20/awssaasaws_saas_boostisvsaasaws_reinvent_2020.html)


# SaaS Boost概要

* [プレビュー版申し込みページ](https://aws.amazon.com/jp/partners/saas-boost/)から申請可能
* 参考となるリンク
  - [AWS SaaS Boost を利用したモノリスアプリケーションの SaaS 移行](https://aws.amazon.com/jp/blogs/news/transforming-your-monolith-to-saas-with-aws-saas-boost/)
  - [AWS SaaS Factory プログラム](https://aws.amazon.com/jp/partners/saas-factory/)
    - ほとんど英語で動画も字幕なし...
  - [AWS SaaS Portal](https://aws.amazon.com/jp/partners/isv-saas-portal/)
    - 日本語コンテンツなので、ここから入ると良さそう。
    - [オンラインセミナー集](https://pages.awscloud.com/event_JAPAN_saas-dojo_ondemand-Confirmation-Page.html)


# そもそもSaaS運用の話

そもそもSaaSの特徴、運用方法として難しいことやその解決策など、AWSのSAが公開しているInnovateでのスライドがあった。  
参考: [事業のステージに応じたSaaSの悩みと解決案](https://d1.awsstatic.com/events/jp/2020/innovate/pdf/S-23_AWSInnovate_Online_Conference_2020_Spring_SaaS.pdf)

* パッケージ販売と比較して考える。
  - 導入時のコストを抑えられるが、安定運用がとても大事で下手するとここでコケる。
  - パッケージは導入時にユーザ個別に環境構築や導入コストがかかる。
* SaaS化のフェーズを踏んでいくと良い。
  - クラウドリフト
    - リフト&シフトするだけ。微妙。
  - シングルテナント（サイロ化モデル）
    - アプリケーションをWeb化する必要あり。
    - 顧客ごとに個別のインフラ(AWSならアカウント単位、インスタンス単位とか)を用意。そのため運用コストは大きい。
  - 一部をマルチテナント化（データ層を共通化）
    - データストアを共通化（プール化）したうえで、キーにテナントIDを付与することで分離
    - ユーザが増えることによる全体的なパフォーマンス劣化が生じるかも（特定ユーザによる過負荷に引きずられるなど）
  - すべてマルチテナント化（アプリ/データ層を共通化）
    - すべてをプール化するのではなく、特定顧客や負荷が大きい処理・ストレージ層をサイロ化して他ユーザの影響を受けないようにするアーキテクチャを目指す。
  - クラウド最適化（コンテナ化、サーバレス化）
    - スピードレイヤとバッチレイヤを分離など



# 利用手順

1. IAM作成
2. CLIを設定
3. SaaS Boostをインストールするインスタンスを用意
  - メモリ4GBが最小要件のためCloud Shellだと足りない。  
    ローカル環境を汚したくなければEC2が良いかも。例えばt2.largeでAmazon Linux, ストレージは適当に50GB。
  - リージョンはTokyoでもOK
4. 必要なパッケージをインストール（下記はAmazon Linuxでの例）
```sh
# Java (Coretto 11) https://docs.aws.amazon.com/corretto/latest/corretto-11-ug/downloads-list.html
$ curl -LO https://corretto.aws/downloads/latest/amazon-corretto-11-x86-linux-jdk.rpm
$ sudo yum -y install ld-linux.so.2
$ sudo rpm -ivh amazon-corretto-11-x86-linux-jdk.rpm
  
# Maven 3 https://maven.apache.org/install.html
$ curl -LO https://ftp.kddi-research.jp/infosystems/apache/maven/maven-3/3.6.3/binaries/apache-maven-3.6.3-bin.zip
$ unzip apache-maven-3.6.3-bin.zip
$ mkdir -p apache-maven-3.6.3/bin/
$ export PATH=$PATH:$PWD/apache-maven-3.6.3/bin

# AWS CLI v2 https://docs.aws.amazon.com/cli/latest/userguide/install-cliv2-linux.html
$ curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
$ unzip awscliv2.zip
$ sudo ./aws/install

# Node v14.15 https://nodejs.org/download/release/v14.15.1/
$ curl -LO https://nodejs.org/download/release/v14.15.1/node-v14.15.1-linux-x64.tar.gz
$ tar zxf node-v14.15.1-linux-x64.tar.gz
$ export PATH=$PATH:$PWD/node-v14.15.1-linux-x64/bin

# Yarn https://classic.yarnpkg.com/en/docs/install#mac-stable
$ npm install --global yarn
```
4. SaaS Boostをgit clone
5. SaaS Boostをinstall（30-40分くらいかかる）
```sh
$ cd ~/aws-saas-boost
$ bash install.sh
```
途中の選択肢は以下のようにした。
```
===========================================================
Welcome to the AWS SaaS Boost Installer
Installer Version: v0.9-11-gde666eb, Commit time: 2021-02-17T22:59:41+0000
Checking maven, yarn and AWS CLI...
Environment Checks for maven, yarn, and AWS CLI PASSED.
===========================================================
1. New AWS SaaS Boost install.
2. Install Metrics and Analytics in to existing AWS SaaS Boost deployment.
3. Update Web Application for existing AWS SaaS Boost deployment.
4. Update existing AWS SaaS Boost deployment.
5. Delete existing AWS SaaS Boost deployment.
6. Exit installer.
Please select an option to continue (1-6): 1
Directory path of saas-boost download (Press Enter for '/home/ec2-user/aws-saas-boost') :
Enter name of the AWS SaaS Boost environment to deploy (Ex. dev, test, uat, prod, etc.): dev
Enter the email address for your AWS SaaS Boost administrator: xxxxx@hoge.co.jp
Enter the email address address again to confirm: xxxxx@hoge.co.jp
Would you like to setup a domain in Route 53 as a Hosted Zone for the AWS SaaS Boost environment (y or n)? n
Would you like to install the metrics and analytics module of AWS SaaS Boost (y or n)? y
Would you like to setup Amazon Quicksight for Metrics and Analytics? You must have already registered for Quicksight in your account. (y or n)? : n

If your application requires a FSX for Windows Filesystem, an Active Directory is required.
Would you like to provision a Managed Active Directory to use with FSX for Windows Filesystem (y or n)? n
===========================================================

Would you like to continue the installation with the following options?
AWS SaaS Boost Environment Name: dev
Admin Email Address: xxxxx@hoge.co.jp
Route 53 Domain for AWS SaaS Boost environment:
Install Metrics and Analytics: y
Amazon Quicksight user for setup of Metrics and Analytics: n/a
Setup Active Directory for FSX for Windows: n
```
6. インストールが完了すると、上記で入力したアドレスにメールが届く。  
  そこにインストールしたSaaS BoostのURLと初期ID, passwordが記載されている。



