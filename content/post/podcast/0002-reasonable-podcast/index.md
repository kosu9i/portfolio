---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "低予算そこそこ音質で始めるpodcast"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-12-22T19:32:56+09:00
lastmod: 2020-12-22T19:32:56+09:00
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

この投稿は[ポッドキャスト配信について語る Advent Calendar 2020](https://adventar.org/calendars/5597)の24日目です。

いきなり余談ですが、本日12/24は自分たちのpodcast「[むきむきクラウド](https://anchor.fm/mukiudo)」を開始してちょうど1年となります。  
本投稿では**低予算そこそこ音質**をテーマに、1年前podcastを始めようと思った時に用意した機材などについて書きたいと思います。


# 音源サンプル

冒頭から宣伝ぽくて恐縮ですが、ここで書く内容で実践すれば、最低限↓くらいの音質では収録・配信が可能かと思います。（腕が良ければもっと良くなるはず）

<iframe src="https://anchor.fm/mukiudo/embed/episodes/reInvent-2020-eo3k7a" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>


# 背景

podcastを始めるにあたって自分は  
**音質にこだわるスキルも金もないけど、聴きづらいほど悪い音質は嫌だな**  
という思いがありました。

で、先人たちはどういう機材を使っているのかなと思い、ググると  
超偉大なテック系podcastである「[Rebuild.fm](https://rebuild.fm/)」の機材紹介記事「[Podcasting Guide 2017](https://weblog.bulknews.net/podcasting-guide-2017-2e88531a367d?gi=621556d37de5)」（ちょっと古いものだけど。最新版もあった気がしたけど見つからず...）が見つかり非常に勉強になったのですが...

**機材が高い...**

全部そろえると10万超えです。

そんな意見を見越したかのように、↑の記事には

> 項目の多さや、使用しているツールの価格など、「ここまでこだわることはないだろう」という印象を受ける人も多いかもしれない。もちろんそれは正しいのだが、言いたいことはむしろ逆である。良い機材やツールを利用すれば、その分、手間をかけずに、より聴きやすいエピソードを効率よく配信することができるようになる。

と書かれています。

分かる。100%同意するのだが...  
それでも貧乏根性の強い自分にとっては、最初から高額の投資をする勇気が湧かないのでした。

もしかして同じ考えの方も割といるのではないかと思い、今回「低予算そこそこ音質で始めるpodcast」というタイトルで投稿します。


# 目指すもの

自分たちのケースでは、以下のような目標がありました。

* 相方と2人でやりたいが、遠隔地にいるため**リモート収録**できるようにしたい
* **なるべく安価**（かかっても数千円程度）に済ましたい
* とはいえ、**なるべく良い音**で配信したい

自分たちがpodcastを始めたときはまだコロナ禍ではなかったのですが、そもそも2人が遠方に住んでいたためリモート収録が必須でした。  

当時は複数人収録の場合、対面で収録している人達が多かったように思います。（それはまた別のノウハウになるのですが、本投稿のスコープ外）  
もっとも、今このご時世ではリモート収録している人の方が多そうなので、本投稿の内容も少しは参考になる**かも**しれません。  


# 先に結論

なんか長くなりそうなので、先に結論として自分の録音環境を書いておきます。  
リモートにいる2人とも **Mac** を利用しているので、その環境を使っています。

* EarPods（昔のiPhoneに付属されてたイヤホンマイク）で音を収録。
* お互いのPC上でQuickTime Playerを使い音を別々に録音し、あとでGarageBandで重ねて1つの音源にする。
* GrageBandとAudacityで音を整える。
* Anchorで配信。

我々のようにMacやiPhoneを持っている~~敬虔なApple信者~~なら、このセットだと安価に（というか追加投資0円で）そこそこな音質・手軽な配信を行えるかと思います。  
Windowsの場合でも[無料のDAWがあるようなので](https://sakky.tokyo/free-daw/)それらを使うことで同様のコストでできるのではないかと思います。

EarPodsはAirPodsとは違います、念の為。有線のやつ。意外と音が優秀です。  
ひと昔のiPhoneには無料で付属していましたが、今は2,000円くらいで別売りです。

{{< figure src="Earpods.jpg" title="EarPods 引用: https://ja.wikipedia.org/wiki/EarPods" numbered="true" lightbox="true" width="30%">}}

では、個別にくわしく書いていきます。

# リモート収録

**Zoomにレコーディング機能があるのでそれでおｋ**

だけだとさすがに書き足りないので、もう少し違うことを書いてみます。

自分たちは↑のRebuild.fm記事で書かれている「ダブルエンダー」という方法を真似ています。  

Webミーティングツール自体で収録を行わない理由は以下です。

* ミーティングツールの仕様なのか、お互いの声がかぶったときなどに音声が打ち消されてしまう
* ネットワークトラブルに弱い
* お互いの声を別々に編集できない

なので、以降はダブルエンダーという方法を自分なりに記載しますが、ぶっちゃけZoomでのレコーディングも結構音は良いので「そこそこ音質」って意味ではZoom収録だけでも良いかもしれません。  
それでもダブルエンダーを使うことで多少音が良くなっていると思うので、そこは作業の面倒さと実際のZoom収録音を聴いてみたときの満足度を比べて判断すればいいと思います。

## ダブルエンダーについて

正直、[Rebuild.fmの解説記事](https://weblog.bulknews.net/podcasting-guide-2017-2e88531a367d)で十分なんですが、一応書きます。（Rebuild.fmの記事も読んでください）

ダブルエンダーという方法では、Webミーティングツールでお互いのコミュニケーションは図りつつ、それ自体では録音は行いません。  
録音はお互いのロケーションで個別に録音し、それらをあとで重ね合わせることで1つのpodcast音源とします。  
具体的には

1. ZoomなどのWebミーティングツールでリモート同士をつなぐ。  
  （Webミーティングツールはコミュニケーション用途だけど、後で重ね合わせるときの目印にするため録音もしておく。Zoomであればレコーディング機能を使える）
2. お互いの環境でQuickTime Playerを起動し、音声録音をする。
3. お互いの音源をGarageBandで重ね合わせる。

3をもう少し具体的に説明すると、

* 1, 2で収録した音声をすべてGarageBandに読み込む
* 波形を移動させて2の音声の位置を合わせる
* 1の音声はミュートして書き出す

という感じにすれば、2で別々に収録したQuickTime Player音源があたかも1つの収録音源かのように作成することができます。

コツとしては2でQuickTimePlayerを起動するタイミングをお互いで合わせることです。  
このとき「3, 2, 1, ポチ」などと声を出して起動することでそれが1の音声にも残り、位置を合わせやすくなります。（画像の青色部分）  
それで大体の位置を合わせて、今度は拡大して細かく3トラックの位置合わせをして完了です。（画像の赤色部分）

{{< figure src="garageband1.png" title="位置合わせ" numbered="true" lightbox="true" >}}

他にも「不要な前後をカットする」とか「相手の音が自分のマイクに入らないようにイヤホンの音量はなるべく小さくしておく」とか注意点はありますが、その辺も詳しく[Rebuild.fmの解説記事](https://weblog.bulknews.net/podcasting-guide-2017-2e88531a367d)に書いてあるので参照してください。（まるなげ）


# なるべく安価に済ます

先述の通り、Mac + iPhone使いであれば必要機材はすべてそろっているかと思います。

自分たちは

* Mac（1人はMacbook Pro, 1人はiMacだけどそこの差異は関係なし）
* EarPods（昔のiPhoneに無料で付属）
* Zoom（無料プラン）
* QuickTime Player（Macに無料で付属）
* GarageBand（Macに無料で付属）
* Audacity（フリーソフト）

という機材構成なので、元々持っていたという事情はあるものの追加投資なしでした。  
ただWindowsでも無料で録音できるソフトはあると思うので、同じようなレベルで低予算構成を組めると思います。

ここで一番言いたいのは**EarPodsが想像以上に優秀**ということです。

これ、ひと昔前のiPhoneでは無料で付属していたので、我々もそれを利用しているのですが、別途買うとしても2,000円くらいで売っています。

それでも侮るなかれ、これで収録した音声結構キレイなんです。  
podcast収録マイクではよく「指向性」が話題になりますが、EarPodsはそこまで尖ってないものの元々イヤホンマイクなのでそれなりに自分の声だけを拾おうとしてくれるようです。  

ぶっちゃけ「iPhoneに付いてたちゃっちいイヤホンマイク」というイメージあると思う（私もそうでした）んですが、
下手な安い外部マイクを買うよりいい音で録れると思うので、もしなるべく安価に始めたいのであれば私は迷わずEarPodsをオススメします。

{{< figure src="Earpods.jpg" title="EarPods 引用: https://ja.wikipedia.org/wiki/EarPods" numbered="true" lightbox="true" width="30%">}}


# なるべくいい音を目指す

ここまででとりあえずの機材はそろったので、あとはできる範囲で「なるべくいい音」にします。

ただ私は **「いい音」がよく分かりません。**

なので素人の主観ですが

* ノイズが少ない
* 言葉が聞き取りやすい

くらいを目指して、「なるべくいい音」に近づけます。

私がやっているのは

* ノイズが少ない => Audacityでノイズを低減
* 言葉が聞き取りやすい => GarageBandでコンプレッサーとEQ

だけです。本当はもっとやるべきことがある気がするのですが、それは今後勉強したいと思います...


## ノイズの低減

[Audacity](https://www.audacityteam.org/)はフリーの音声編集ソフトで、これを使っています。  
ノイズ低減の方法に参考になりそうなサイトをリンクしておきます（まるなげ）

* [5分でわかる！Audacityでノイズ除去する設定方法](https://pc-gadget.com/pc/sound/961/)
* [ノイズの除去](https://taira-komori.jpn.org/09noiseremoval.html)

基本的には↓の作業です。

1. しゃべっていない「ノイズだけ」の波形を選択
2. 「ノイズの低減」で「ノイズプロファイルの取得」を押して実行
3. 全波形を選択
4. 「ノイズの低減」で「OK」を押して実行

これで「サー」とかいうノイズが消えます。まだノイズが残っている場合は↑のサイトを参考にしながら設定値をいじると良いと思います。

1つポイントとしては、それぞれ別で収録した音をGarageBandで重ね合わせる作業の前にノイズ除去をすることをオススメします。  
重ね合わせた後でもいいのですが、それぞれの収録環境でノイズ音の成分が異なると思うので、個別に除去した方が無理なくキレイに除去することができます。  

{{< figure src="noise.png" title="Audacity ノイズの低減" numbered="true" lightbox="true" >}}


## コンプレッサー

私はGarageBandでやっていますが、Audacityでもできるようです。好きな方でやればいいと思います。

少し古めの記事かもしれませんが↓が参考になると思うのでリンクしておきます。（まるなげ）  
[GarageBand使い方講座トップ　＞　基本エフェクト：コンプレッサー](https://kaymusic-online.com/index.php?%E5%9F%BA%E6%9C%AC%E3%82%A8%E3%83%95%E3%82%A7%E3%82%AF%E3%83%88%EF%BC%9A%E3%82%B3%E3%83%B3%E3%83%97%E3%83%AC%E3%83%83%E3%82%B5%E3%83%BC)

コンプレッサーは雑に言うと小さい音と大きい音の差を少なくします。  
EarPodsの弱点として、突然笑ったときとかにそこの音だけ大きくなりがちです。  
そういう音量のバラツキを整える目的で使用しています。


## EQ

EQは高音をあげたり低音をさげたり、など周波数ごとの強弱を整えます。

podcastなど音声のみの場合は

* ローカットで低音をざっくり除去
* 1kHzあたりも少し抑える

が定石らしいです。GarageBandのEQでは音を聴きながら波形を見れるので、あとはモニタリングしながらお好みで色々変えてみると良いと思います。

私は~~面倒なので~~ざっくり↑をやってくれる「PopVocal」っていうプリセットをマスタートラック（すべての音源に適用される）にかけて、そのあと個別のトラックで特徴的な部分があればいじっています（例えば10kくらいで耳障りな音が入りがちだったら削る、声が野太かったらローをさらに削る、など）

{{< figure src="eq.png" title="GarageBandのEQ" numbered="true" lightbox="true" >}}


## その他

その他と言いつつ、一番重要なのは **ハキハキしゃべること** だと思います。これはかなり色んな配信者の方々も言われています。

心がけ次第でどうにかなる、という究極にローコストな方法ですが、かなり重要な要素なので、これは気をつけたいところです。

もう少し根拠を付け加えておくと、ハキハキしゃべることで聴き取りやすくなるのは当たり前のことですが、ノイズと音声の差をつけることで先述の「ノイズの低減」もより効果が出やすくなります。詳しくはS/N比などでググってみてください。


# 配信方法

本投稿は「そこそこ音質」に関するものが主旨なので、ここではサラッといきますが、配信元に特にこだわりないのであれば、[Anchor](https://anchor.fm/)を使うのが一番ラクです。  
いろんなプラットフォームに配信してくれてかつ無料なので、気軽さという面ではこれに勝るpodcast配信サービスは他にないと思います。

さらにスマホアプリもあって、まったく音質にこだわらないのであればスマホのみでpodcastを収録・配信することも十分可能です。  
こだわらないと言いつつBGMを入れたりもできるようなので、それなりにそれっぽいものが配信可能な強力なサービスです。


# 総括

ここまでで「低予算そこそこ音質」のやり方を紹介しました。  

ぶっちゃけ自分たちのpodcast音質に満足は全然できていないのですが、聴けないほど悪い音でもないかとは思っています。  
今後より精進して、良い音を目指したいと思います。  

そのときには今より高価な機材は揃えるかもしれませんが、本投稿では「まずpodcastを始めるとき」に「なるべく低予算」「でもなるべくいい音」でやりたい方の参考に少しでもなればと思い記載してみた次第です。


# お詫び

最後に...一つ嘘をついていたことをお詫びするのですが、私たちはEarPodsを長いこと使っていたのですが、最近は数千円のコンデンサマイクを使って収録しています。  

FIFINEのK670っていうやつで、[Yahooショッピングのセールとかだと4,000円くらい](https://store.shopping.yahoo.co.jp/dereshop/fifine-k670.html)で買えることもあります。（私は6,000円くらいでAmazonで買った...）  
このマイクもコスパよくて気に入っているのですが、正直EarPodsから劇的に変わったかと言うと微妙です...また、コンデンサマイクなので音量の調整とかも大変で、油断するとすぐに音が割れます。

というこで、私たちは気に入って使ってはいるものの、podcast始めるときのオススメはやはりEarPodsで変わりないです。嘘ついたことはすみませんでした。。  

参考までにEarPodsで収録した回と、FIFINE K670で収録した回のリンクを貼っておきます。

EarPodsで収録した回

<iframe src="https://anchor.fm/mukiudo/embed/episodes/GCPAI-Platform--AWS-SageMaker-ea492e" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

FIFINEのK670で収録した回

<iframe src="https://anchor.fm/mukiudo/embed/episodes/reInvent-2020-eo3k7a" height="102px" width="400px" frameborder="0" scrolling="no"></iframe>

やっぱあんま変わらん気がする...というかEarPodsの方が良い気すらする。  
無念だがEarPods優秀！精進いたします。
