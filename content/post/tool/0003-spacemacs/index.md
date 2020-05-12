---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Spacemacs使い始めてみる"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-05-11T12:32:28+09:00
lastmod: 2020-05-11T12:32:28+09:00
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

# 背景

* TODO管理用にEmacsのOrg-modeを使いたいと常々思っていた。
* 普段使っているエディタはNeoVimで、Emacsに本格移行するつもりはあまりない。

という状態だった。  
Org-modeのためだけにEmacsを導入しようと思って色々調べていたら、  
何やら[Spacemacs](https://www.spacemacs.org/)なるものがあるらしい。

元々はVimからEmacsに移行しやすくするために作られたとのこと。  
今となっては `The best editor is neither Emacs nor Vim, it's Emacs and Vim!` と公式でも謳われており  
つまり`Vim+Emacs`が最強のエディタと言いたいみたい。

これ良いんじゃないかと思い、使ってみることに。


# インストール

[GitHubのREADME](https://github.com/syl20bnr/spacemacs)を元にやっていく。（環境はMac）

## Emacs

まずはEmacsをインストール。最新版を入れたいのでHomebrewを使う。

```sh
$ brew tap d12frosted/emacs-plus
$ brew install emacs-plus
$ brew linkapps emacs-plus
```

`emacs-plus`というのは、GNU Emacsに加えて色々サポートが追加されているらしく、spacemacsには都合が良いみたい。

最後の`linkapps`コマンドはbrewでdeprecatedになっているのでエラーになる。  
代わりに自力で `$ ln -s /usr/local/opt/emacs-plus/Emacs.app /Applications` を実行する。

`emacs` コマンドも、Xcodeでバンドルされているもの（ver 22.1と古い）からHomebrew版を見るようにしておく。  
以下を`~/.zshrc`に追記。

```sh
alias emacs='/usr/local/opt/emacs-plus/bin/emacs -nw'
alias e='emacs'
```

`-nw`はターミナル内でEmacsを開くoption。これをつけないと別途GUIアプリが起動する。  
私はターミナル内でCLIとして`emacs`を起動したときは`-nw`付き、  
GUIを起動したいときはAlfredのランチャ起動するようにしたかったので、このようにした。


## Spacemacs

要はSpacemacsは色々入っている`.emacs.d`みたい。  
なので、元から`~/.emacs.d/`がある場合は、バックアップしておくと良い。

```sh
$ mv ~/.emacs.d ~/.emacs.bak
```

Spacemacsのインストール。  
[公式サイトのトップ](https://www.spacemacs.org/)にあるコマンドをコピペするだけ。

```sh
$ git clone https://github.com/syl20bnr/spacemacs ~/.emacs.d
```

`Emacs.app`を起動すると、下部に`Dotfile wizard installer`というのが表示される。  
これに従って初期セットアップが可能。

{{< figure src="init.png" title="Dotfile wizard installer" numbered="true" lightbox="true" >}}

私は以下のようにした。

```
What is your preferred editing style?
-> Among the stars aboard the Evil flagship (vim)

What distribution of spacemacs would you like to start with?
-> The standard distribution, recommended (spacemacs)

What type of completion framework do you want?
-> A lighter one but still very powerful (ivy)
```

`ivy`は補完ツール。`helm`より速いとのことでこっちにした。  
あとはデフォルト。

しばらくインストールが勝手に走るので待つ。

## org-mode（org-layer）の設定

Spacemacsにはレイヤーという概念がある。  
パッケージの上位層で、色んなパッケージがまとめられているとのこと。  
例えば、pythonレイヤーの下にはpython用のパッケージをまとめて整理できる、のような。（多分）

org-modeもorg-layerとして管理されているようである。  
デフォルトの`~/.spacemacs`ファイルでは以下のようにコメントアウトされているので`org`のコメントアウトを外すだけ。

```
dotspacemacs-configuration-layers
   '(
     markdown
     ;; ----------------------------------------------------------------
     ;; Example of useful layers you may want to use right away.
     ;; Uncomment some layer names and press <SPC f e R> (Vim style) or
     ;; <M-m f e R> (Emacs style) to install them.
     ;; ----------------------------------------------------------------
     ivy
     ;; auto-completion
     ;; better-defaults
     emacs-lisp
     ;; git
     ;; markdown
     ;; org  ;; ここのコメントアウトを外す
     ;; (shell :variables
     ;;        shell-default-height 30
     ;;        shell-default-position 'bottom)
     ;; spell-checking
     ;; syntax-checking
     ;; version-control
     )
```

Spacemacsを再起動するとorg-layerに必要なものがインストールされるので待つ。

これで適当に`*.org`という拡張子のファイルを開くとorg-layerが有効になる。  

と、導入できたっぽいのは良いが、org-modeの使い方が分からず、それはまた次回...

