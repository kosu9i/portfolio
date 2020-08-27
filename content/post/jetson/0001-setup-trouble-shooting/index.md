---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Jetson AGX Xavierセットアップ トラブルシューティング"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-08-28T01:30:38+09:00
lastmod: 2020-08-28T01:30:38+09:00
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

[Jetson AGX Xavier](https://www.nvidia.com/ja-jp/autonomous-machines/embedded-systems/jetson-agx-xavier/)のセットアップ関連でつまづいたところを自分用にメモしておく。

# JetPackのアップグレード

Jetsonの新規インストール手順などは色んな所に書いてるので下記などを参照。  
ホストマシンとの接続方法や、Force recoveryモードでのJetson起動方法（電源ボタンの押し方）などはこれらと同じ。  
ただ、アップグレードの場合は最初のJetson側のUbuntuインストールがない。これをどうにかする必要がある。

* [本家インストールマニュアル](https://docs.nvidia.com/sdk-manager/install-with-sdkm-jetson/index.html#install-with-sdkm-jetson)
* [「Jetson AGX Xavier」レビュー(2) セットアップ＆ベンチマーク編 エッジを知能化する超小型AIコンピュータの実力は本物か?](https://robotstart.info/2019/03/04/jetson-xavier-review-02.html)
* [【物体検出】vol.9 ：YOLOv3をNVIDIA Jetson AGX Xavierで動かす] (https://www.nakasha.co.jp/future/ai/vol9_yolov3nvidia_jetson_agx_xavier.html)
* [NVIDIA AGX Xavierのセットアップ](http://www1.meijo-u.ac.jp/~kohara/cms/technicalreport/nvidia-agx-xavier-setup)

JetPack 4.4以前から新しいバージョンのJetPackにアップグレードしたい場合は、基本的にクリーンインストールしかない。
[4.4以降はupgradeできるようになるよ、と本家ドキュメントにはある](https://docs.nvidia.com/jetson/jetpack/install-jetpack/index.html#upgrade-jetpack)が定かではない。期待せずに待つことにする。


## JetPackのバージョン確認

そもそも今入っているJetPackのバージョン確認をするための便利ツールがある。  
参考: [Jetson NanoでDeepStreamを使う](https://www.usagi1975.com/202001120052/)

```sh
$ git clone https://github.com/jetsonhacks/jetsonUtilities
$ cd jetsonUtilities
$ python jetsonInfo.py

 NVIDIA Jetson TX1
 L4T 32.2.0 [ JetPack 4.2.1 ]
 Ubuntu 18.04.3 LTS
 Kernel Version: 4.9.140-tegra
 CUDA 10.0.326
```


## Ubuntu 18.04マシンの準備

Jetsonと接続してインストールするために、ホストOSとしてUbuntu 18.04が動く物理マシンが必要。  
仮想マシンではダメらしい。[Mac + VirtualBoxでやっている人も見かけた](https://qiita.com/baba5246/items/c86a25678a0d85a204f3)が、物理マシンを用意できるならそれが無難。（JetPackのエラーは分かりづらいので変なところでつまづくとワケ分からなくなる）

ホストのマシンが準備できたら、アップグレードしたいJetPackのバージョンをインストールできる[NVIDIA SDK Manager](https://developer.nvidia.com/nvidia-sdk-manager)をUbuntuにインストールする。  
このとき、GUIのパッケージマネージャーからインストールすると固まることがあるので、`dpkg` コマンドでインストールすると良い。

ちなみに他の小さなJetson Xavier NXとかNanoとかだとSD Cardにイメージを焼いてセットアップするらしい。


## NVIDIA SDK ManagerからJetsonを再セットアップ

上記の新規インストール手順と同様に、NVIDIA SDK Managerからインストールを進めればOK。  

で、ここからがつまづいたところ。


### ネット回線

数GBのダウンロードが走るので、ネット回線は安定していて太いものがあると良い。  
細いと途中でエラーになる。


### Connection refused connecting via SSH

NVIDIA SDK Managerからのセットアップがある程度すすむと、sshでJetsonに接続するプロンプトが出る。（下記、公式ドキュメントから画像転用）

{{< figure src="sdkm-3-post-flash-dialog-jetson.02.png" title="JetsonとのSSH接続（公式ドキュメントから転用）" numbered="true" lightbox="true" >}}

このssh接続はUSBケーブルでホストOSとJetsonをつないで行う。  
Jetson側のIPアドレスは固定で `192.168.55.1` になっている。（ちなみにホストOS側は `192.168.55.100` になるはず）

が、このssh接続で「Connection refused connecting via SSH」が出て進まなくなる。

これはNVIDIA SDK Managerが

1. JetsonのOSを再インストールし始める
2. OSの再インストール中にssh接続しようとする
3. OSの再インストールを完了する

という流れで動いているからのように見える。つまりJetsonのOSがセットアップされていないからssh接続できない。

そのため、一旦このSSH接続はSkipして諦める。

その後、Jetson側のOSの再インストールが終わるのでSDK Managerを終了する。

で、今度は **しばらく待ってから（10分くらい）** Jetsonを再起動し、Jetson側にHDMIケーブルをつないでディスプレイで起動を確認する。  
この **しばらく待ってから** が重要だったみたいで、待たずに再起動するとOSのインストールが完了する前に電源が落ちてシステムが壊れたことがあった。

無事OSのインストールが終わったら、Jetsonの画面でUbuntuのGUIが立ち上がり、初期セットアップになる。  
ここでJetson側のUbuntuユーザをセットアップできるので、ユーザ名に `nvidia` , パスワードに `nvidia` とか適当なジョーアカウントで良いので設定しておく。

これを終わらせた後、再度ホストOSとJetsonをUSB接続し、改めてNVIDIA SDK Managerを起動する。  
今度は **「Jetson OS」という項目のチェックを外して** セットアップを進める。  
これをしないとまたOSが上書きされて、SSH接続できない、の繰り返し。

{{< figure src="sdkm-3-install-details-jetpack.02.png" title="残りのセットアップ（公式ドキュメントから転用）" numbered="true" lightbox="true" >}}

これが終われば、無事CUDAやdockerなど必要なツール類もインストールされてJetPackのアップグレード（と言っても上書きインストールだが）が完了する。


# その他

## jtopのインストール

htopのJetson版みたいなツール。入れておくと良い。

```sh
$ pip install jetson-stats
```

