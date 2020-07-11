---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#17 【GCP】Cloud Run"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "小杉がCloud Runについて話したよ。"
abstract: "小杉がCloud Runについて話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-07-12T01:18:00+09:00
#date_end: 2020-07-11T21:12:17+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-07-11T21:12:17+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/GCPCloud-Run-egjq7m" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# 話したこと

## 雑談

### GoogleがIsolated Regionから撤退

[ZDNetとかで見た記事](https://japan.zdnet.com/article/35156570/)。  
オリジナルは[Bloombergの記事](https://www.bloomberg.com/news/articles/2020-07-08/google-scrapped-cloud-initiative-in-china-sensitive-markets)

ていうかIsolated Regionって何よ...。  
ググっても出てこない。

ZDNetによると「データを国内で管理したいという国々の要望に応えるために開発していた」**なにか**ということになるが、結局なんだったのかよく分からず。

国内のデータを国内で保護したい、というモチベーションの背景には  
[CLOUD法](https://aws.amazon.com/jp/compliance/cloud-act/)というのも関係しているらしい。

CLOUD法って何よ...。  
という人（私だ）は要勉強。  
超絶ざっくり言うとアメリカが国外のデータセンターにあるデータでも、米国企業のデータなら令状なしに政府が開示を要求できるというもの。（多分）  
The Clarifying Lawful Overseas Use of Data Actの略。

ぱっと聞くとヤバそうな法律だけど、Google, Apple, Microsoftなど名だたる企業はこの法律を支持している（おそらくデータ保護に関する法整備が進んできたというポジティブな反応なのだと思われる）らしいし、単純な話ではなさそうなことが分かる。  

「あ、これ知っとかないとダメなやつやん...」と思ったのだった。

### Google Cloud Next OnAir 2020

Cloud Nextのオンライン版が7/15から9週間（！！）開催される。  
毎週テーマごとにコンテンツが追加されていくらしい。（日本時間の深夜1時）

とりあえず[日本版のサイト](https://cloud.withgoogle.com/next/sf/japan)から申し込んでみた。  
こちらの日本版には「Next OnAir Japan」というタイトルが付いている。  


基本的に[グローバルな方のイベント](https://cloud.withgoogle.com/next/sf/)の方がメイン。  
セッション一覧で「Japan」のfilterをかますと、コンテンツが1/10くらいになる...。  
JapanコンテンツはRecapも多い。


### AWS Summit Online Japan

[AWS Summit Online 初開催決定](https://aws.amazon.com/jp/summits/2020/)

日程： 2020年9月8日(火)～2020年9月30日(水)

> クラウドの最新技術を "実際に手を動かして楽しみながら学ぶ" 23日間

ということ。

### AWS Startup Architecture of the Year Japan 2020

[AWS Startup Architecture of the Year Japan 2020](https://awssaoyjapan2020.splashthat.com/)というのが開催されるらしい。

アーキテクチャのコンペティション。詳細は不明。  
優勝したら、ラスベガスでのre:Invent 2020決勝戦への参加権が与えられる。

> ◆ 評価基準: 
> 1) AWS Well-Architected Frameworkの基準（スケーラビリティー、可用性、パフォーマンス、コスト効率、セキュリティ）に適合し、主要かつ戦略的ソリューション（コンテナ、AI/ML、ビッグデータ、IoT、サーバーレス、AR/VR）を使用する独自の設計を持つ:  50%
> 2) 明確なビジネスインパクトを持つソリューションがある: 50%


## 本題

### Cloud Run

GCPのコンテナサービスCloud Runについて[こちらのブログ](https://mukiudo.dev/post/cloudrun/0001-get-started/)に書いた内容を中心に話した。

結構違いはあるものの、位置づけ的にはAWSのFargateみたいなもの。
