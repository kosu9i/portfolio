---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "#40 Amazon CloudFront"
event:
event_url:
location:
address:
  street:
  city:
  region:
  postcode:
  country:
summary: "加藤がSAPの勉強中。その中からCloudFrontをネタに取り上げて話したよ。"
abstract: "加藤がSAPの勉強中。その中からCloudFrontをネタに取り上げて話したよ。"

# Talk start and end times.
#   End time can optionally be hidden by prefixing the line with `#`.
date: 2021-02-22T10:48:49+09:00
#date_end: 2021-02-22T10:48:49+09:00
all_day: false

# Schedule page publish date (NOT talk date).
publishDate: 2021-02-22T10:48:49+09:00

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

<iframe src="https://anchor.fm/mukiudo/embed/episodes/Amazon-CloudFront-eqo83r" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

# Show Notes

## Amazon CloudFront

- Amazon CloudFrontとはCDNサービスである
- CDNとは、同一のコンテンツをより素早く効率的に配信するためのネットワークである
​
- S3やEC2等を利用すると、簡単に世界中のユーザからコンテンツにアクセス可能にできる
- ただし、以下のような課題がある
    - 大量のアクセスがある場合、アクセス数分の負荷に耐えなければならない
    - ユーザから遠いロケーションに配置されたコンテンツの取得には時間がかかる
    - XSSやDDoSのリスクがある
    - ・・・等。
​
- CloudFrontディストリビューションを作成して、コンテンツを効率的に配信可能
- ディストリビューションとは、ドメイン単位で割り当てられるCloudFrontの設定の事
- オリジンサーバをキャッシュし、エッジロケーションにプロビジョニングする
    - オリジンの負荷がオフロードされる
    - ユーザから近いエッジロケーションからコンテンツを取得させる
​
- 設定で様々なケースに対応可能
    - セキュアに通信をしたければHTTPSを利用する
        - デフォルト証明書、独自SSL証明書が使える
            - 独自SSL証明書はSNI、専用IPアドレスSSL証明書が使える
    - 通信方式の制御も可能（TLS1.2や1.1等）
    - XSSやDDoS等の対策も可能
        - AWS WAFをディストリビューションにセットできる
        - AWS Shieldがデフォルトで組み込まれている
    - アクセス制御をするにはRestricted Viewer Accessを利用
        - 署名付きURLや署名付きCookieを利用する
            - 複数のファイルを制御するなら署名付きCookieを利用
        - S3ならさらにOrigin Access IdentityでS3でアクセスコントロールできる
            - 必ずCloudFrontを経由する仕組みが実現できる
    - 接続地域を制限したいならGeo-Restrictionsを利用
    - POSTリクエストの特定のフィールドだけアクセスできるようにもできる
        - フィールドレベル暗号化を利用
    - キャッシュの制御もできる
        - TTLを設定できる
        - Invalidationでキャッシュの削除もできる
    - コンテンツやヘッダーの加工もできる
        - ビューワーリクエスト→オリジンリクエスト→オリジンレスポンス→ビューワーレスポンスという4つの区間に分けて加工できる
        - ヘッダーを追加したり上書きできる
        - エラーページを設定できる
        - Lambda@Edgeをトリガできる
            - Lambda@Edge内でコンテンツやヘッダを加工できる
                - Header、URL、クエリ文字列の読み書き等が可能
    - ここまでの設定をパス毎に設定できる（パス毎の単位をBehavierという）
    - セカンダリオリジンを設定して、フェイルオーバーの設定もできる
- CloudWatchと連携して各種ログの確認ができる

