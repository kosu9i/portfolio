---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#37 【AWS】Auto Scalingについて復習"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "加藤がAuto Scalingについて話したよ。"
abstract: "加藤がAuto Scalingについて話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2021-01-12T09:53:53+09:00
#date_end: 2021-01-12T09:53:53+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2021-01-12T09:53:53+09:00

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

# Show Notes

## AWS Auto ScalingのBlackBelt要約

参考にしたBlack Belt: [Amazon EC2 Auto Scaling and AWS Auto Scaling](https://www.youtube.com/watch?reload=9&v=o01IOnVvRxM)

AWS Auto ScalingのBlackBeltで話していたことは以下の5つ（アジェンダから抜粋）

1. Auto Scalingサービスのコンセプト
2. Auto Scalingの基礎知識
3. 主要機能：スケーリングの整理
4. Auto Scalingを使ってみる
5. こんなときどうする？ - 各種機能の紹介

今回は1-3についてお伝えする。


AWS Auto Scalingとは、インスタンスやクラスタ等のキャパシティをいい感じに保ってくれるサービス

こちらで設定するのは一つだけ。「希望容量」を設定すること

AWS Auto Scalingがやってくれることは3つだけ  
「希望容量と現実容量の差分監視」「スケールアウト」「スケールイン」  

「希望容量と現実容量の差分監視」の動作定義を「スケーリングオプション」という。  
「スケーリングオプション」は3種類ある。  
動的スケーリング、予測スケーリング、スケジュールスケーリング。  

動的スケーリングの設定方法は2種類ある。  
しきい値か目標値。  
しきい値を超えたらスケールアウトするか、目標値に達するまでスケールアウトし続けるか、といった違い。  
例えば、前者は「CPU使用率が50を超えたら1台追加」後者は「CPU使用率を40に維持するのに必要なら1台追加」  

予測スケーリングの設定方法は1つだけ。  
2周間分のメトリクスを分析し、次の2日の需要を予測し、予測した結果でスケジュールして台数を増減する  

スケジュールスケーリングの設定方法は2つある。  
一回だけ、定期的な設定。cronみたいなもん。  
MinCapacityかMaxCapacityか両方を指定して、それに応じて指定タイミングでスケールイン・スケールアウトする。  

で、できることはわかったけどどれにすればいいの？という話しについて。  
予測スケーリングと動的スケーリングをセットで使うのがおすすめ。  
大まかなキャパシティ増減は予測スケーリングで対応できる。そのうえで実際の不可に対して不足した分を目標値設定で補充する。つまり、「予測の通り動かす」「ただしCPU利用率を40%に維持するのに必要なら1台追加」8割位は予測でカバーできそう。  
ただ、これはEC2にしか使えない。予測スケーリングがEC2でしか使えないので。  
EC2以外なら動的スケーリングだけを使う。  
