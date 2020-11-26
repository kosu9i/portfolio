---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "CKAD体験記"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-11-23T00:20:13+09:00
lastmod: 2020-11-23T00:20:13+09:00
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

CKADを受けた体験記。

# CKADとは

CNCFが運営するkubernetesの資格。  
これには全部で3種類あって

* CKA（Certified Kubernetes Administrator）
* CKAD（Certified Kubernetes Application Developer）
* CKS（Certified Kubernetes Security Specialist）←最近できたやつ

がある。（3つの違い詳細は[公式ページ](https://docs.linuxfoundation.org/tc-docs/certification/faq-cka-ckad-cks)参照）
CKAとCKADは重複している範囲がかなり多く、CKAの方が範囲が少し広いらしい。  
よって、CKAを受かればそのままちょっと勉強を足してCKAD合格はしやすそう。

自分はアプリケーション開発者なのでCKADだけ受けた。


## CKAD-jpとの違い

[CKAD-jp](https://training.linuxfoundation.org/ja/certified-kubernetes-application-developer-ckad-jp/)っていうのもある。  
CKAD-jpは試験官とのやり取り（現在オンライン試験のみなのでチャットで試験前のやり取りをする必要がある）も日本語でできるということだと思う。

CKADでは試験前の試験官とのやり取りは英語（チャットのみ。音声会話はなし）で行う必要がある。  
CKADでも問題文は英語 or 日本語の選択を適宜切り替えられるが、  
問題文の日本語は機械翻訳感満載の微妙な訳なので、たまに問題が分からない。  
基本的に英語を見て問題は解き、詰まったら日本語訳を参照して進めるのが良い。


# おすすめ教材

## Udemy

* [CKAD受験対策コース](https://www.udemy.com/course/certified-kubernetes-application-developer/)がある。  
* 2万円以上するが、Udemyは ~~景品表示法大丈夫なん？ってくらい~~ よく90%オフセールをやっているので、そこで買うべし。
* 全部英語なので、最低限字幕を読めないとキツイ。  
  字幕も自動認識のセクションもあり、結構間違っている。


## kubernetes完全ガイド

* 体系的にまとまっており、理解しやすい良書だと思う。
* 自分は全部読んでないけど...  
  基本Udemyやって、わからないところはこの本で補強すれば試験対策としては十分と思う。
* 試験後も使える知識がある本で良いと思う。
* kindleもある。

## Githubの模擬試験

Githubに有志であがっている[模擬試験](https://github.com/dgkanatsios/CKAD-exercises)もおさえておくとかなり良い。  
特に `kubectl run`, `kubectl create`を押さえるのにおすすめ。  
時間の都合上、これらのコマンドを活用して解く必要あり。  
ドキュメントは試験中も参照できるが、全部コピペだと間に合わないので  
`run`, `create` でベースとなるyamlファイルを出力する方法を覚えておくと良い。

また、`create`と`run`は`-h`を打つとサブコマンドごとにサンプルが出力されるので、これがかなり役立つ。  
（試験問題と似たケースも表示してくれることが多い）


# 受験方法

年末ならLinux Foundationでサイバーマンデーセールを狙うのが良い。  
昨年はe-learningと受験バウチャー込みで、$180くらいで買えた。普段は受験だけで$300するので超お得。  
それぞれ期間は1年間あるので、いつか受験するつもりならサイバーマンデーは逃すなべし。

ただLinux Foundationのe-learningは試験対策としては微妙。

# 受験記

## オンライン試験での体験談

オンライン試験というのを初めて受けたが、Webカメラを通して机の上にカンニングできるものが置かれていないかなど  
かなり細かくチェックされる。結構大変で、自分の場合は準備に30分もかかった。

* 飲み物はラベルを剥がしたペットボトルなら置いて良いと言われた。  
  が、途中で机のうえのものを全部どけろと言われ、最終的にペットボトルは葬られた。
* IDは日本語の免許証だけではダメ。ローマ字の名前が入ったクレジットカードを2nd IDとして用意しておくこと。  
  パスポートがあればそっちを使ったほうがスムーズ。
* チャットがなかなかうざい
  - 細切れにドカドカとテンプレ送って来られて読みづらい
  - 途中でカメラから顔が見えなくなると怒られる
  - スマートウォッチとか付けてないか確認するから両手見せろと言われた
  - 画面がなかなか共有されないトラブルあり。  
    「Macですか？」と言われたのでyesと答えたらなぜか解決した。（サーバサイドで何かやってる？）
  - Ctrl + Alt + Deleteで他のプロセス全部停止しなさい、と言われる。さっきMacだって言っただろ。
* 残り時間が分からりづらい（プログレスバーのみ。正確な時間はチャットで送られるリマインドのみ）
  - 「あと17分です」って言われたけど中途半端で笑った
* 独り言もダメ

それ以外は滞りなく受験できた。

試験終了36時間以内に結果がメールで来る。自分は試験完了から34時間くらいで来た。（試験「開始」から36時間以内ということかも？）  


## 問題傾向

* 比較的短い問題が半分 + これらを2, 3個かけ合わせた問題（Deployment + Service, Pod + PV + PVCなど）が半分くらい。  
* いずれもそんなに難易度は高くなく、UdemyのMock Examくらい。（UdemyのChallenge Labより簡単）  
  Githubに有志であがっている[模擬試験](https://github.com/dgkanatsios/CKAD-exercises)もおさえておくと  
  試験時に使えるコマンドをかなり体験できる。
* 問題ごとにパーセンテージが書いてあるが、難易度と比例していない感じ。簡単でも高配点のものがあるのできちんと抑える。  
  逆に言うと難しそうで低配点のものは即スキップでもOK。
* 時間は結構キツキツなので、分からなかったらマークしてスキップが良い。
  - マークしても「手を付けてない」or「途中まで解いた」or「見直ししたい」などが  
    あとで分からなくなる（どこまでやったかk8sの環境を見直す羽目になる）。  
    これはメモを活用すると良かった。

# 総合的な所感

* 試験自体の難易度は高くない。↑のおすすめ教材をやっておけばほぼ大丈夫と思われ。  
  - 時間がなければUdemyが一番おすすめ。
* 合格したところでk8sできるようにはなったとは言えない。ホント入門の入門って感じ。  
* 試験勉強を通して習得できたことは、ただkubectlコマンドを実行できるようになっただけ、という感じ。  
  重要な観点と思われる、k8sのエコシステムやマイクロサービスアーキテクチャについては資格勉強だけではまったく身につかない。  
  その点、CKSは少し実用的な知識が得られるかも。
* 合格後、実際にアプリ開発しないとk8sできるようにならなさそうだが、個人開発でk8sってのも無理矢理感はある...どうしたものか。
* 普段使っている人が体系的に知識を復習するのは良いかもしれないが、別に不要とも思う。  
  自分のように業務でk8s使ってないけど、流行ってるし触っておきたい、という人が最初の取っ掛かりとして利用するのは良いかも。
