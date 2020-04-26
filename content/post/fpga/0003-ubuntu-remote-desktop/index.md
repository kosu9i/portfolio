---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Ubuntu Remote Desktop for FPGA"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-27T01:43:57+09:00
lastmod: 2020-04-27T01:43:57+09:00
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

# FPGA用Ubuntuの準備

FPGA用のUbuntuはそれなりにスペックが要求されるので  
ローカルのVirtualMachineじゃ厳しくなってきた。

そのため、GCP上にUbuntuをたててリモートデスクトップを試みる。


# GCPな理由

AWSだと月に1,000円しか無料枠がないため、ハイスペックだと超えそう。  
GCPは12ヶ月で30,000円無料枠を使える。1ヶ月で使い切ってもいいはず。  

n1-standard-4は4CPU, 15GBメモリで月に$150（1時間あたり$0.2）くらい。   
使うときだけ起動していればそこまで食わないはず。  


# Chrome Remote Desktop

1. ひとまずn1-standard-1で16.04LTSインスタンスを起動。（セットアップ後にスペックアップすればOK）
    * 後にインストールするVitisがディスクかなり食うので、ディスクサイズは200GBにしておく
    * 本当はSSDにしたかったが、無料枠ではSSDサイズは100GBが上限...
2. Ubuntu16.04にssh接続し、[公式ドキュメント](https://cloud.google.com/solutions/chrome-desktop-remote-on-compute-engine?hl=ja#configuring_and_starting_the_chrome_remote_desktop_service)にある通りセットアップしていく。
```
wget https://dl.google.com/linux/directchrome-remote-desktop_current_amd64.deb
sudo apt update
sudo dpkg --install chrome-remote-desktop_current_amd64.deb
sudo apt install --assume-yes --fix-broken

# 以下、Xfceを選択

sudo DEBIAN_FRONTEND=noninteractive \
    apt install --assume-yes xfce4 desktop-base
sudo bash -c 'echo "exec /etc/X11/Xsession /usr/bin/xfce4-session" > /etc/chrome-remote-desktop-session'
sudo apt install --assume-yes xscreensaver
sudo apt install --assume-yes task-xfce-desktop

sudo systemctl disable lightdm.service # エラーになるが無視
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb

sudo dpkg --install google-chrome-stable_current_amd64.deb
sudo apt install --assume-yes --fix-broken
```
3. 残りも公式ドキュメントの以下を実施すれば、ひとまずXfceのデスクトップには接続できた。
    + [Chrome リモート デスクトップ サービスの構成と開始](https://cloud.google.com/solutions/chrome-desktop-remote-on-compute-engine?hl=ja#configuring_and_starting_the_chrome_remote_desktop_service)
    + [VM インスタンスへの接続](https://cloud.google.com/solutions/chrome-desktop-remote-on-compute-engine?hl=ja#connecting_to_the_vm_instance)


## 結局...

目的のVitisはUbuntu18.04推奨のため、18.04でやりたかったが、  
18.04ではChrome Remote Desktopの設定がうまくいかなかった。  
そのため、Chrome Remote Desktopは諦めた。


# 通常のRDP

参考：[リモートデスクトップ環境をUbuntu 18.04 LTSで作成する](https://qiita.com/ryo-endo/items/00f3ec125917acf4cec7)

今度はXilinxのVitisが18.04.2までにしか対応しておらずマイナーバージョンが合わないが無理矢理進める。  
（一応、Vitisのインストールまではできた）


```
sudo apt-get update
sudo apt-get -y upgrade
sudo apt-get -y install ubuntu-desktop xrdp
sudo systemctl enable xrdp
sudo systemctl start xrdp

sudo apt-get -y install language-pack-ja
sudo localectl set-locale LANG=ja_JP.UTF-8 LANGUAGE="ja_JP:ja"
sudo timedatectl set-timezone Asia/Tokyo

sudo adduser kosugi
sudo gpasswd -a kosugi sudo

cat <<EOF | sudo tee /etc/polkit-1/localauthority/50-local.d/xrdp-color-manager.pkla  
[Netowrkmanager]  
Identity=unix-user:*  
Action=org.freedesktop.color-manager.create-device  
ResultAny=no  
ResultInactive=no  
ResultActive=yes  
EOF

```

[ここ](https://qiita.com/basaro_k/items/86811ed78397d2a3b4b1)を参考にし、Vitisの構築を進める。

ひとまず[Vitisのインストール](https://qiita.com/basaro_k/items/86811ed78397d2a3b4b1#vitis%E3%81%AE%E3%82%A4%E3%83%B3%E3%82%B9%E3%83%88%E3%83%BC%E3%83%AB)までは正常にできた。





