---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "MacでUbuntuの起動ディスクを作成"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-10-15T15:36:07+09:00
lastmod: 2020-10-15T15:36:07+09:00
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

毎回手順を忘れるのでメモ。

1. [isoイメージ](https://releases.ubuntu.com/18.04/)をダウンロード。
2. USBをフォーマット。
```shell
# USBのデバイスを確認（USB挿入前後で増えたやつがそれ。ここでは/dev/disk6と仮定する）
$ diskutil list

# アンマウント
$ diskutil unmountDisk /dev/disk6

# 消去
diskutil eraseDisk HFS+ Untitled /dev/disk6

```
3. UTBにイメージを書き込み
```shell
# アンマウント
$ diskutil unmountDisk /dev/disk6

# 書き込み
$ sudo dd if=ubuntu-18.04.5-live-server-amd64.iso of=/dev/rdisk6 bs=1m
```
