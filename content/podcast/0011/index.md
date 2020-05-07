---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#11 【雑談回】リモートワーク2"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "前回に続き、加藤がリモートワークについて話したよ。<br/>分報の運用方法をメインで話し、VSCode Live Share、Virtual Officeについてもちょっと話したよ。"
abstract: "前回に続き、加藤がリモートワークについて話したよ。<br/>分報の運用方法をメインで話し、VSCode Live Share、Virtual Officeについてもちょっと話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-05-06T16:23:40+09:00
#date_end: 2020-05-06T16:19:40+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-05-06T16:19:40+09:00

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
<iframe src="https://anchor.fm/mukiudo/embed/episodes/2-edm8t4" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# 話したこと

## 分報

「分報」という習慣があるらしい。（下記リンク参照）

* [後から気づいたSlackでの分報がもたらすメリット](https://developer.ntt.com/ja/blog/d55e2be0-255d-4321-9d45-8608ce9d9726)
* [Slackで簡単に「日報」ならぬ「分報」をチームで実現する3ステップ〜Problemが10分で解決するチャットを作ろう](http://c16e.com/1511101558/)

加藤くんのところでは「社内Twitter」のような感覚で、各人がつぶやけるchannelをslackに開設（任意）して運用している。  
特にチーム内に「15分つまづいたら周りに訊け」というルールがあるらしく、そのつぶやき先として利用しやすいとのこと。  
例えばプログラミング言語専用のchannelとかだと個人的に気軽に質問するには少しハードルが高いような内容でも、自分の分報channelではつぶやく感覚で「この辺わかんねぇ」とできる。  
加藤くんはコロナ禍以前から、フルリモート勤務しているため、この分報channelは重要な役割を果たしており、うまく機能もしているとのこと。

個人的に

* 通知地獄にならない？
* 時間泥棒になりがちな気が。何か工夫されている？（通知OFF, 人数絞る, とか）
* 良いと感じる運用方法とかあれば（チームor個人ごとのtimesチャネル作る、無視してもOKという風潮を作る、など）

が聞いてみたかったので、その辺をpodcastで聞いてみた。


## VSCode Live Share

[VSCodeでリモートのペアプロ、モブプロができる拡張機能](https://visualstudio.microsoft.com/ja/services/live-share/)。

すごく良さそうだし、加藤くんもおすすめしている。  
最近はコロナ禍でリモート作業が増えているので、特に。

物理オフィスでは近くの人に「ここ動かないっす。どう思います？」とかできていたけど  
リモートだとそれができず、非効率になったりエンジニア同士のコミュニケーションが疎になっている感覚がある。  
Live Shareは、slackやWeb会議ツールなどと合わせて使うことでエンジニアの作業を助けてくれそうな良ツールなのでは。
（Live Share自体にも音声やチャット機能があるらしい）

セキュリティが気になる人もいるかもしれない。  
が、Microsoft純正のプラグイン（多分）であることもあって、きちんと[セキュリティに関するドキュメント](https://docs.microsoft.com/ja-jp/visualstudio/liveshare/reference/security)も用意されている。（しかも日本語もあり）

色々とさすが...という感じ。  
VSCodeを使わない理由がどんどん無くなっていきますな。


## Virtual Office

このご時世でヴァーチャルオフィスが注目されているっぽい。  
これは加藤くんも私も使ったことないので推測で話した。

多分[Remo](https://remo.co/virtual-office-space/)というサービスが人気。  
ただ、このタイミングで[料金体系が変更されたらしい](https://note.com/degumiu13/n/nd28c149babd8)。  
リンク先のブログの人が、検討中の他サービスも記載されているので、参考にされたし。


## その他podcast内で話せなかった質問リスト

質問者：小杉  
回答者：加藤くん  

* 自宅オフィス環境ってどんな感じ？
  + MBP13inch+モニタ1枚、EarPods、有線LAN接続

* 加藤くんはコロナ前からずっと在宅だけどコロナ後、何か変わった？  
  + とくに変わらず。

* モチベーションってどう保っている？
  + 普通の目標にプラスして無理だろ、ってくらい高い目標立ててみる（あくまで、思考用に）

* 1日のスケジュールはどんな感じ？
  + 9時開始、12時に昼食と運動、18時に終了をいつもだいたい同じ時間に。
  + AMはだいたい定例会、PMから自分の作業。

* ミーティングはどうしてる？
  + 全部meetかzoom
  + なるべく有線LAN接続
  + 伝わりづらいので、リアクションは大げさにするくらいで丁度いい。
  + 15分悩んだらSlackで相談するか分報でつぶやく→だいたいその後すぐmeetになる。

* 開発ってどう進めてる？
  + slackとかgithubとかbacklogとか活用。
  + チケットとかissueベースで担当し、VSCodeのLiveShareとかで自信がないところはペアプロしたり、meetで悩みを相談してます。

* 雑談がなくなったことで、メンバや会社の機微な情報が欠落してきた。どう対応している？
  + 私は積極的にSlackとかビデオ通話で雑談するようにしてます。
    分報で詰まってることとか面白そうなことを書いてます。
  + うちの会社で言えば毎週社長が朝礼で経営状況とかコロナ対策とかアップデートを話してくれるので、ざっくり経営状況の把握は週イチでできてます。
  + 興味あるプロジェクトには勝手にSlackのチャンネルに入って混ざりに行ったりしてます。
