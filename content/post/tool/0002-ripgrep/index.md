---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "ripgrep導入"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-27T01:35:58+09:00
lastmod: 2020-04-27T01:35:58+09:00
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

# ripgrep

正規表現でディレクトリを再帰的に検索できるツール。  
毎度あほみたいに `find . -name "*.py" | xargs grep "hoge"` とかやってたのを  
`rg -t py hoge` でやってくれるうえに、爆速。


# なんで速いか

* 検索する必要がなさそうなファイル（隠しファイル, バイナリファイル）を無視
* そもそも使用している検索アルゴリズム自体が高速


# インストール

```
brew update
brew install ripgrep
```


# 基本的な使い方

カレントディレクトリ以下を全部検索

```
rg 検索文字列
```

特定のディレクトリ以下を検索

```
rg 検索文字列 ディレクトリ
```

特定の拡張子のファイルのみを検索対象とする

```
rg -t 拡張子 検索文字列
```

特定の正規表現にマッチしたファイルのみを検索対象とする

```
rg -g '*正規表現*' 検索文字列
```

検索文字列には正規表現が使える

```
rg '_.+hoge'
```
