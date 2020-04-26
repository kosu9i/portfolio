---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "ghqの導入"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-27T01:32:42+09:00
lastmod: 2020-04-27T01:32:42+09:00
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

# ghq関連の導入

参考：[ghq, peco, hubで快適Gitライフを手に入れよう！](https://qiita.com/itkrt2y/items/0671d1f48e66f21241e2)


## インストール

```
$ brew install ghq
$ brew install peco
$ brew install hub
```

## セットアップ

### ghq

* `ghq look` は廃止され、 `ghq get --look` になったらしい。  
  ただ、サブシェルが起動されてしまうため、基本的には素直にcdした方が良いとのこと。  
  https://songmu.jp/riji/ 

### alias

~/.zshrc に以下を追記

```
alias g='cd $(ghq root)/$(ghq list | peco)'
alias gh='hub browse $(ghq list | peco | cut -d "/" -f 2,3)'
```
