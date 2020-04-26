---
# Documentation: https://sourcethemes.com/academic/docs/managing-content/

title: "Zplugin導入記"
subtitle: ""
summary: ""
authors: []
tags: []
categories: []
date: 2020-04-27T01:00:52+09:00
lastmod: 2020-04-27T01:00:52+09:00
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

# Zinit（旧Zplugin）

Zshのプラグインマネージャーとして、何も分からずoh-my-zshを使っていたが
Zpluginというのが速いらしいので、置き換えてみる。

Zpluginは2020/1月頃にZinitという名称に変わった。


# oh-my-zshのアンインストール

アンインストール用のコマンドが提供されている。親切。

```sh
$ uninstall_oh_my_zsh
Are you sure you want to remove Oh My Zsh? [y/N] y
Removing ~/.oh-my-zsh
Looking for original zsh config...
Thanks for trying out Oh My Zsh. It's been uninstalled.
Don't forget to restart your terminal!
```

あとは~/.zshrcから、oh-my-zsh関連の記述を消す。


# Zinitインストール

[公式Github](https://github.com/zdharma/zinit)

```
sh -c "$(curl -fsSL https://raw.githubusercontent.com/zdharma/zinit/master/doc/install.sh)"
```

下記が~/.zshrcに追記される。

```
### Added by Zinit's installer
if [[ ! -f $HOME/.zinit/bin/zinit.zsh ]]; then
    print -P "%F{33}▓▒░ %F{220}Installing DHARMA Initiative Plugin Manager (zdharma/zinit)…%f"
    command mkdir -p "$HOME/.zinit" && command chmod g-rwX "$HOME/.zinit"
    command git clone https://github.com/zdharma/zinit "$HOME/.zinit/bin" && \
        print -P "%F{33}▓▒░ %F{34}Installation successful.%f%b" || \
        print -P "%F{160}▓▒░ The clone has failed.%f%b"
fi

source "$HOME/.zinit/bin/zinit.zsh"
autoload -Uz _zinit
(( ${+_comps} )) && _comps[zinit]=_zinit

# Load a few important annexes, without Turbo
# (this is currently required for annexes)
zinit light-mode for \
    zinit-zsh/z-a-patch-dl \
    zinit-zsh/z-a-as-monitor \
    zinit-zsh/z-a-bin-gem-node

### End of Zinit's installer chunk
```

が、ここで `zinit-zsh/z-a-as-monitor` と `zinit-zsh/z-a-bin-gem-node` の2つがcloneできずエラーになる。
なんだそりゃ。

なので、削除する。

[ZinitのREADMEに書かれているExample](https://github.com/zdharma/zinit#example-usage)もいくつかcloneエラーになる。
あまりメンテナンスされていないのだろうか...

とりあえず使いそうな以下を~/.zshrcに追記

```
zinit light zsh-users/zsh-autosuggestions
zinit light zsh-users/zsh-syntax-highlighting
```

# Zinitの情報

日本語のブログだと初心者用に[ここ](https://blog.katio.net/page/zplugin)がまとまってる。



