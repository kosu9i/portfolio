---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#39 GCPでのETLいろいろ - Dataflow編"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "小杉が時事ネタ + GCP Dataflowなどについて話したよ。"
abstract: "小杉が時事ネタ + GCP Dataflowなどについて話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2021-02-11T10:20:00+09:00
#date_end: 2021-02-10T23:53:58+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2021-02-10T23:53:58+09:00

authors: []
tags: []

# Is this a featured talk? (true/false)
featured: false

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder. 
# Focal points: Smart, Center, TopLeft, Top, TopRight, Left, Right, BottomLeft, Bottom, BottomRight.
image:
  caption: ""
  focal_point: ""
  preview_only: false

# Custom links (optional).
#   Uncomment and edit lines below to show custom links.
# links:
# - name: Follow
#   url: https://twitter.com
#   icon_pack: fab
#   icon: twitter

# Optional filename of your slides within your talk's folder or a URL.
url_slides:

url_code:
url_pdf:
url_video:

# Markdown Slides (optional).
#   Associate this talk with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides = "example-slides"` references `content/slides/example-slides.md`.
#   Otherwise, set `slides = ""`.
slides: ""

# Projects (optional).
#   Associate this post with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `projects = ["internal-project"]` references `content/project/deep-learning/index.md`.
#   Otherwise, set `projects = []`.
projects: []
---

<iframe src="https://anchor.fm/mukiudo/embed/episodes/GCPETL---Dataflow-eq861c" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Notes

## [Email from Jeff Bezos to employees](https://www.aboutamazon.com/news/company-news/email-from-jeff-bezos-to-employees)

* AWSのCEO Andy JassyがAmazonのCEOに
* じゃあAWSのCEOは誰になるの？は未定。  
  TechCrunchの記事「[What Andy Jassy’s promotion to Amazon CEO could mean for AWS](https://techcrunch.com/2021/02/02/what-andy-jassys-promotion-to-amazon-ceo-could-mean-for-aws/)」によると、噂は
  - Peter DeSantis
    - グローバルインフラストラクチャ担当Vice President
    - re:Intent 2020でInfrastructure Keynoteやってた
  - Matt Garman
    - セールス・マーケティングVice President


## 本ネタ

自ブログの投稿「[GCP上でのETLいろいろ](https://mukiudo.dev/post/gcp/0002-etl-on-gcp/)」からGCP Dataflow, Data Fusion。


## [Dataform が Google Cloud の傘下に: BigQuery で SQL を使用してデータ変換をデプロイする](https://cloud.google.com/blog/ja/products/data-analytics/welcoming-dataform-to-bigquery)

いわゆるELTをBigQueryなどDWHで実施できるようになるDataformがGoogle Cloudによって買収。  
Dataform自体はRedshiftやSnowflakeでも使えるっぽい。

本ネタにちょっと関連するリリース（と言っても昨年の12月だけど）だったのでリンクのみ貼っておく。
