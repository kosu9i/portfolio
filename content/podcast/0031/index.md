---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#31 【番外編】AWS re:Invent 2020 Late Night Week1 'Mac Instance'について"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "re:Invent 2020の前夜祭的なイベントLate Night Week1で発表された'Mac Instance'について話したよ。<br/>お祭り感が冷めないうちにと急遽小杉1人でしゃべったよ。"
abstract: "re:Invent 2020の前夜祭的なイベントLate Night Week1で発表された'Mac Instance'について話したよ。<br/>お祭り感が冷めないうちにと急遽小杉1人でしゃべったよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-12-01T21:45:44+09:00
#date_end: 2020-12-01T21:45:44+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-12-01T21:45:44+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/AWS-reInvent-2020-Late-Night-Week1-Mac-Instance-en771s" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Notes

## Late Night Week1

### 概要

re:Invent 2020の前夜祭的なイベント。  
現地時間では夜だけど、日本時刻では13:00-14:00でLIVE配信された。

{{< figure src="late_night.jpeg" title="https://twitter.com/classmethod/status/1333633291145023488 より拝借" numbered="true" lightbox="true" >}}


最初はコンサートがあったり、re:Inventの概要を紹介されたり。（今年はCOVID-19の影響で云々カンヌン, etc）

{{< figure src="concert.jpeg" title="Zach Personというミュージシャンのコンサート" numbered="true" lightbox="true" >}}


### 言語

LIVEの字幕はどうやら自動の音声認識で出されている様子。  
途中字幕が追いつかなかったり、間違っていたりした。  
基本的に字幕を読んでも追っていけないので、頑張ってリスニングするしかなさそう。  
スライドがあるときは分かりやすいのだけど。


### Mac Instanceについて

唐突に発表されたEC2のMac Instance。  
TwitterのTLがMac Instanceの話で埋まった。

{{< figure src="tl.png" title="TLがMac Instanceで埋まる" numbered="true" lightbox="true" >}}

早速[公式ブログ記事](https://aws.amazon.com/jp/blogs/aws/new-use-mac-instances-to-build-test-macos-ios-ipados-tvos-and-watchos-apps/)も出ている。


#### Mac Instanceの内容

要は文字通り、EC2でMacが使える。

* 実態としてはMac miniがDedicated Hostで使うということ。
  - Dedicated HostなのでEC2インスタンスをシャットダウンしてもお金がかかる。
* 現在の提供リージョンは以下。
> US East (N. Virginia), US East (Ohio), US West (Oregon), Europe (Ireland), and Asia Pacific (Singapore) 
* [利用料金](https://aws.amazon.com/jp/ec2/dedicated-hosts/pricing/?nc1=h_ls)（「Dedicated Hostの料金」セクションを参照）はバージニア北部で$1.083/h, 自分が試したシンガポールでは$1.354/h。
* Mac Miniのスペックは下記のとおり。
> 8th generation, 6-core Intel Core i7 (Coffee Lake) processor running at 3.2 GHz, with Turbo Boost up to 4.6 GHz. There’s 32 GiB of memory
* ストレージとしてEBS, EFSなどがマウントできる。
  - EBSは最適化されており55,000IOPS
* 10Gbpsのスループットを持つENA networking
* 現在提供されているMac OSは10.14（Mojave）と10.15（Catalina）。Big Surはまだ。
* M1プロセッサもまだ。ただ2021年に対応予定とのこと。
 
上記公式ブログ記事の下部に記載されたCLI実行方法は若干間違っているので  
下記developers.io記事を参考にされたし。

[【速報】EC2がMac対応！ Amazon EC2 Mac Instancesがリリースされたので触ってみた #reinvent](https://dev.classmethod.jp/articles/amazon-ec2-mac-instance/)

クラスメソッドさん、さすがの速さです。


#### Mac Instance接続方法

シンガポールが近いのでリージョンはap-southeast-1を使う。

1. Dedicated Hostを`mac1.metal`インスタンスタイプで確保。（上記クラスメソッドのブログを参照）  
  [ベアメタルインスタンス](https://aws.amazon.com/jp/about-aws/whats-new/2019/02/introducing-five-new-amazon-ec2-bare-metal-instances/)という扱いみたい。
```
$ aws ec2 allocate-hosts --instance-type mac1.metal   --availability-zone ap-southeast-1a --auto-placement on   --quantity 1 --region ap-southeast-1
```
2. EC2インスタンスを上記のDedicated Host上で起動。
3. セキュリティグループで22を許可。
4. 作成したキーペアでsshで接続。

{{< figure src="ssh.png" title="ssh接続" numbered="true" lightbox="true" >}}

VNC接続する場合は

1. セキュリティグループで5900を許可。
2. デフォルトではVNCサーバが立ち上がっていないので、ssh接続先のMacでVNCサーバを起動。  
  参考) [Apple Remote Desktop で kickstart コマンドラインユーティリティを使う](https://support.apple.com/ja-jp/HT201710)
```
$ sudo /System/Library/CoreServices/RemoteManagement/ARDAgent.app/Contents/Resources/kickstart -activate -configure -access -on -restart -agent -privs -all
```
3. `ec2-user`にパスワードを設定。
```
$ sudo passwd ec2-user
```
4. VNCクライアントで`vnc://EC2外部IP:5900`を指定して接続。  
  参考) MacでのVNCクライアント利用方法は[こちら](http://mac-blog.arcist.net/?p=53)を参照。

{{< figure src="vnc1.png" title="VNC接続" numbered="true" lightbox="true" >}}
{{< figure src="vnc2.png" title="VNC接続 ログイン後" numbered="true" lightbox="true" >}}

**試したあとはDedicated Hostを必ずリリースすること！！EC2インスタンスを起動していなくても料金がかかるので。**


#### 何に使おう

* 公式が言っている通りMacOS, iOSなどの開発・検証環境として。
* developer以外だとすると、OSアップグレードしたときの簡易確認として。
* お遊び的な感覚で。


### Late Night Week1総括

* 冷静になってみるとMac Instanceはちょっと話題先行的な発表だった感じはするが  
  お祭り感は十分に楽しめた。前夜祭ということでツカミはがっちりというところ？
  + 実際に使うとなると結構利用料金は高い。（起動しっぱなしだと1ヶ月で10万円弱くらい）  
  + オンデマンドで試験環境的に使う感じか
* Late Nightを担当したMattさんのオススメセッションは以下だそう。
  + Harness the Power of Data with AWS Analysis （DEC 9 9:15-10:15 AM PST）
  + Replicate AWS DeepRacer Arichitecture to Conquer the Track with SageMaker（DEC 16 9:30-10:00 AM PST）
  + Amazon ECS: Roadmap & Vision（DEC 16 10:30-11:00 AM PST）
  + Architecture Trends & Topics for 2021（DEC 17 2:00-2:30PM PST）
* これ以上にたくさんのセッションがあるがとてもじゃないが全部見きれない。前夜祭だけで結構満腹感あった...
* このあと最初のKey Noteある（日本時間 深夜12:30より）  
  がんばっていこう

{{< figure src="recommend.png" title="Mattさんオススメセッション" numbered="true" lightbox="true" >}}
