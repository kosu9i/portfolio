---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#25 AWS Amplify, GCPアップデート, AWS DevDay, etc"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "加藤がAWS Amplifyのアップデートと、関連してSPA、SSR、JAMStackとかについて話したよ。"
abstract: "加藤がAWS Amplifyのアップデートと、関連してSPA、SSR、JAMStackとかについて話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2020-10-04T14:39:28+09:00
#date_end: 2020-10-04T14:39:28+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2020-10-04T14:39:28+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/AWS-Amplify--GCP--AWS-DevDay--etc-ekj43j" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Note

## [AWS DevDay Online Japan](https://aws.amazon.com/jp/about-aws/events/2020/devday/)

* 開催日時：2020 年 10 月 20 日（火）～ 22 日（木）
  - 20 日: 10:00 ～ 18:05
  - 21 日: 10:00 ～ 18:00 
  - 22 日: 10:00 ～ 17:30
* 開催形態：オンラインにてライブ配信
* キーノートのゲストが豪華。（順不同・敬称略）
  - ジェームス・ゴスリン
  - 川口 耕助
  - 奥田 遼介
  - オードリー・タン
  - 真鍋 大度
  - 野田クリスタル

[ハンズオンセッション](https://aws.amazon.com/jp/about-aws/events/2020/devday/sessions/?aws-devdays-japan-cards.q=%E3%83%AF%E3%83%BC%E3%82%AF%E3%82%B7%E3%83%A7%E3%83%83%E3%83%97&aws-devdays-japan-cards.sort-by=item.additionalFields.sortOrder&aws-devdays-japan-cards.sort-order=asc&aws-devdays-japan-cards.q_operator=AND)もたくさんあったりで楽しそう。


## [Cloud Logging で新たにサポートされる正規表現の使用に関するヒントとアドバイス](https://cloud.google.com/blog/ja/products/management-tools/cloud-logging-gets-regular-expression-support)

GCPのCloud Loggingで正規表現検索が可能になった。（2020/9月くらいから）  
`textPayload =~ "^User.*Logged (In|Out)$"` みたいな感じで検索可能。


## [Cloudflareが「ステートフルなサーバーレス」を実現する「Durable Objects」を発表（Gigazine）](https://gigazine.net/news/20200930-cloudflare-workers-durable-objects/)

CloudflareはCDN事業社で「Cloudflare Workers」というサーバレスコンピューティングサービスも提供していた。  
今回「Durable Objects」というステートフルなサービスを実現する新機能をベータ版として提供開始。

どれくらいデータが永続化されるのか、とかは不明。


## [GCSでTokyo+Osakaのデュアルリージョン（asia1）が選択可能になった](https://cloud.google.com/storage/docs/release-notes#September_28_2020)

GCSには特定の地域でよしなにマルチリージョン, デュアルリージョンに冗長化する[オプションを選択できる](https://cloud.google.com/storage/docs/locations)。  
今回、このデュアルリージョン（高可用かつ定レイテンシ）にTokyo + Osakaが追加されるという[リリースノート](https://cloud.google.com/storage/docs/release-notes#September_28_2020)があった。  
（さっき見てみたが、新しい `asia` というデュアルリージョンは見当たらなかったが）

何らかの要件でデータ保管が国内のみに限定される場合など便利。


## いろんな障害

* 9/24 Google
  - [細かい障害レポートも出ている]((https://status.cloud.google.com/incident/zall/20010))
* 9/29 [「Microsoft 365」で障害発生（約5時間後に復旧）（ITMedia）](https://www.itmedia.co.jp/news/articles/2009/29/news065.html)
* 10/1 東証
  - [記者会見](https://youtu.be/ACFLlMXhlWg)が見事と絶賛されている。


## AWS Amplify SSR対応

[AWS Amplify](https://aws.amazon.com/jp/amplify/)のSSR対応について。

JAMstackについては、[JAMstackってなに？実践に学ぶ高速表示を実現するアーキテクチャの構成](https://employment.en-japan.com/engineerhub/entry/2019/12/10/103000)という記事が非常にわかりやすい。
