---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "GCPの新資格 \"Professional Machine Learning Engineer BETA\" を受けてきた"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-08-22T10:52:34+09:00
lastmod: 2020-08-22T10:52:34+09:00
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

2020/7月頃にリリースされたベータ版の試験[Professional Machine Learning Engineer](https://cloud.google.com/certification/machine-learning-engineer)を受験してきたのでその備忘録。  
と言っても、秘密保持があるため試験問題の詳細については触れない。


# ベータ版の試験とは？

[https://cloud.google.com/certification/faqs/?hl=ja](https://cloud.google.com/certification/faqs/?hl=ja)の「ベータ版認定資格」にFAQがまとめられている。  
新しい資格がリリースされる際に、正式版に先立ってベータ版が試しに公開される。  
この統計情報をもとに、最終的な正式版の問題や合格基準が決定されるとのこと。

主な特徴は以下。

* ベータ版の公開は期間限定。（今回のML Engineer試験は2020/7〜2020/8で公開されていた）
  - 1度しか受けられない。
* 安く受けられる。（MLEは30% OFFだった）
* 試験時間が長い。（MLEは4時間...！）
* 試験問題が多い。（MLEは120問だった）
* 試験問題は全部英語。
* ベータ版に合格すると、正式版と同じ認定扱いになる。
* すぐには合否が出ない。（普通の試験だと、試験終了時に即時結果が画面に表示される）  
  「正式版のリリース前までのいつか」にメール通知されるとのこと。


# Professional Machine Learning Engineer BETAの試験範囲

[公式ページの試験ガイド](https://cloud.google.com/certification/guides/machine-learning-engineer)に載っている。


# どんな人が対象か？

上記の試験ガイドを見るとなんとなく分かるが、実際に受けた際の所感を含め書く。  
（あくまでベータ版での内容のため、正式版では変わる可能性あり）

MLエンジニアの定義は明確ではないと思うが、一般的に「MLエンジニア」として仕事をしている人たちに近い内容になってると感じる。  
要はモデルの構築だけではなく、それをデプロイして利用するところまでを独力でこなせる人たち、という感じ。  
完全に主観だが「ML:クラウドエンジニアリング」の比重が3:7〜4:6くらいの感じがした。  
ただGCP資格なので「環境はGCP」「フレームワークはTensorflow」が前提になる。

以下のスキルが必要とされていた印象。

* Tensorflowの実装経験（特にtf.dataやEstimatorなどを活用した資源効率化の工夫）
* 機械学習モデル評価と改善方法の基礎知識
  - 不均衡データの扱い、trainとtestで評価値が異なるときの対処、など
* GCPを用いたモデル構築（前処理、モデリングなど）や推論時の速度向上、コスト削減、スケーラビリティの考慮
  - 特にAI Platform, Dataflow, BigQuery MLあたりは重要
  - 次にDataproc, GCS, BigQueryとの連携, 各種ML系SaaS（Vision APIなど）あたり

あと、ベータ版限定の話だが英語がある程度読めないと厳しい。  
問題文が結構長い（「あなたはxxな企業で働いていて...xxなMLモデルを構築する。適切なアプローチのはどれか？」みたいな問題が多い）ので  
英語に詰まると解けない & 時間が溶ける。（自分は英語力底辺なので、4時間ぜんぶ使っても全問解けなかった...）

「コストを下げるには、どのアプローチがいいか」「コストは許容するからとにかく速くしたいときは」という観点は多くの問題で重要視されていたので  
その辺りをGCP, Tensorflowを用いてどう解決するかを問われる感じ。


# Professional Data Engineerとの違い

似た資格に[Professional Data Engineer](https://cloud.google.com/certification/data-engineer?hl=ja)というのがある。

これも主観だが、Data Engineerの方は「GCPを使ったデータの管理・加工方法」や「BigQueryそのもの（クエリとか）」についての問題が多いが、ML Engineerの方は「GCPやTensorflowを使ったMLモデルの構築方法」や「BigQuery ML, 」についての問題が多かった印象。 
まぁ文字通りと言ったところ。

ただ、やはりかぶる領域も多いのでData Engineerをすでに持っている人などはML Engineerも受かりやすいと思われる。


# 試験対策

これといってドンピシャな試験対策方法はないが、[ここ](https://cloud.google.com/certification/machine-learning-engineer)の「Step 3: Round out your skills with training」に書かれているもので経験不足そうなところがあれば、やっておくと良いと思う。  
自分はやってないが、やっておけばよかったと後悔...やっぱり公式のガイダンスは結構試験に当てはまってるな、と実感。
  
あとは[Data Engineerの模擬試験](https://cloud.google.com/certification/practice-exam/data-engineer?hl=ja)もおすすめ。


# その他の所感

* 4時間はキツイ。  
  自分が受けた試験会場は途中トイレとかに行くのは許可されていたけど、すべての会場でそうなのか、  
  自宅で遠隔受験したときはどうか、などは不明。
* 英語で死んだ。多分ボーダー付近で落ちる気がする。
  - 問題と選択肢の細かいニュアンスが分からず、大体2択で迷った。時間もロスした。
  - 日本語だったら受かったのになー！（多分落ちる）
