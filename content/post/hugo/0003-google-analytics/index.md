---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Google AnalyticsをHugo Academicテーマに導入する"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-05-12T00:25:27+09:00
lastmod: 2020-05-12T00:25:27+09:00
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

せっかくなのでこのブログにGA（Google Analytics）を導入してみようと思った。

# Google Analytics

GoogleアカウントがあればOK。  
[Google Analyticsのページ](https://analytics.google.com)に行ってGA用のアカウントを作成。

{{< figure src="ga_top.png" title="Google Analyticsトップ" numbered="true" lightbox="true" >}}

「アカウント名」には適当な名前を入れる。  
「アカウントのデータ共有設定」はデフォルト（全部ON）でOK。

{{< figure src="ga_create_account.png" title="アカウント作成" numbered="true" lightbox="true" >}}

測定の対象はこのブログなので`ウェブ`のままでOK。

{{< figure src="ga_target_type.png" title="測定の対象" numbered="true" lightbox="true" >}}

プロパティは以下の感じ。

{{< figure src="ga_account_property.png" title="プロパティの設定" numbered="true" lightbox="true" >}}

「作成」を押すと利用規約が表示されるので、`日本`を選んで同意する。

{{< figure src="ga_terms.png" title="利用規約" numbered="true" lightbox="true" >}}

アカウントが作成され、トラッキングID（`UA-`から始まる文字列）というのが付与されるはず。


# Hugo AcademicでGoogle Analyticsを有効化

めっちゃ簡単。  
`config/_default/params.toml` に以下の記述があるので `google_analytics` のところにトラッキングIDを書けばいいだけ。

```toml
############################
## Marketing
############################
[marketing]
  google_analytics = ""
  google_tag_manager = ""
```

あとはNetlifyにデプロイするだけ。


## 確認

うまく設定できているかは、GAの「管理」=>「トラッキング情報」=>「トラッキング コード」=>「テストトラフィックを送信」で確認できる。

{{< figure src="ga_admin.png" title="管理画面" numbered="true" lightbox="true" >}}

「テストトラフィックを送信」してしばらく待つと、`現在のアクティブ ユーザー数です（テスト トラフィックからの n 人を含む）`という表示がされるはず。ここの`n`が1以上になっていればテストOKでちゃんと設定できていると分かる。

{{< figure src="ga_test_traffic.png" title="テストトラフィックを送信" numbered="true" lightbox="true" >}}


## 補足

Hugo serverをlocalで立ち上げても、GAの反映はされていない（HTMLファイルに`gtag`のJavaScriptが埋め込まれない）と思う。  
これはAcademicが `HUGO_ENV = "production"` である場合のみ、GAを有効化するようになっているから。（確かにその方が良い）

`HUGO_ENV = "production"`は`netlify.toml`で定義されているので、NetlifyにデプロイしたときだけGAのコードが有効化されるというわけだった。

参考：[Google Analytics seems not working #1368](https://github.com/gcushen/hugo-academic/issues/1368)


