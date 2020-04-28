---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Netlify + Academicで'Last Updated On'となってしまうのを修正"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-28T13:45:56+09:00
lastmod: 2020-04-28T13:45:56+09:00
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

ローカルのhugo serverで起動したら、各記事の先頭に書いたメタデータが反映されて  
下記赤枠ように記事の時刻が表示される。

{{< figure src="metadata_date.png" title="メタデータの時刻が表示されてる" numbered="true" lightbox="true" >}}


しかし、Netlifyにデプロイすると、デプロイした（gitの最終updateタイムスタンプ？かも）時刻で  
表示されてしまう。  
これだとせっかく過去の記事を、そのときのタイムスタンプに書き換えてデプロイしたのに意味がない。

{{< figure src="netlify_date.png" title="NetlifyにデプロイするとタイムスタンプがLast updatedになってしまう" numbered="true" lightbox="true" >}}

これはNetlifyの仕様とのこと。  
これをローカルでの挙動と合わせて、各記事のメタデータに合わせるようにするには  
`netlify.toml` の以下を書き換えると良い。

```toml
[build.environment]
  HUGO_VERSION = "0.68.3"
  HUGO_ENABLEGITINFO = "false" # ここをfalseにする
  #HUGO_ENABLEGITINFO = "true"
```

[GitHubにissue](https://github.com/gcushen/hugo-academic/issues/1346)があがってた。（バグではない）  
そこで↑のやり方が回答されてる。
