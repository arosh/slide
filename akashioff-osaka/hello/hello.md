!SLIDE

# オレの**.zshrc**

<br>

### #akashioff in Osaka

!SLIDE

## 自己紹介

* [@shora_kujira16](http://twttr.com/shora_kujira16)
* 大学1年生
* *TopCoder*: **arosh** レーティング3ケタ
* 興味があるもの: Scala / 組み込み
* いい加減に免許取れ

!SLIDE

## **.zshrc**ってなに？

* Unix向けのコマンドラインシェル *zsh* の設定ファイル
* コピペでもかなり幸せになれる

参考：[漢のzsh(24)グッバイ野郎ども! コピペではじめるzshファイナル](http://news.mynavi.jp/column/zsh/024/index.html)

* みんなで設定して幸せになろうぜっ！！！

!SLIDE

## お品書き

zshを半年間使って手放せなくなった*怠惰な設定*を紹介

* 大文字小文字を無視
* 補完候補をリストから選択
* ヒストリ検索
* cd ..
* お手軽解凍コマンド
* clipコマンド


!SLIDE

## お知らせ

* 現在使っている **.zshrc** は *Github* に上げています

http://github.com/arosh/dotfiles

* このスライドも上げる予定

<br>

* だいたいの設定は他のシェルでもできるはず

!SLIDE

## 大文字小文字を無視

zstyle ':completion:*' matcher-list 'm:{a-z}={A-Z}'

<br>

* **小文字**を入力している間は無視
* *大文字*が入力されたら区別する
* vimで言えば ignorecase + smartcase

<br>


* bashでは組み込み (set completion-ignore-case on)
* ただし、無視するだけ

!SLIDE

## 補完候補をリストから選択
zstyle ':completion:*:default' menu select=2

<br>

* *Tab連打*生活が捗りすぎてヤバイ
* 日本語の入ったファイルを選ぶときに便利

!SLIDE

## ヒストリ検索 (1/2)

<br>

```
autoload history-search-end
zle -N history-beginning-search-backward-end history-search-end
zle -N history-beginning-search-forward-end history-search-end
bindkey "^P" history-beginning-search-backward-end
bindkey "^N" history-beginning-search-forward-end
```

<br>

コピペしましょう

!SLIDE

## ヒストリ検索 (2/2)

$ vim ← ここで *Ctrl+P* or **Ctrl+N**

* 今までの履歴から vim で始まるものを順に補完
* Ctrl+R よりも便利だと思う (個人的印象)
* あまり使わないコマンドにも威力を発揮

!SLIDE

## cd .. (1/3)

<br>

```
function cdup() {
        echo
        cd ..
        zle reset-prompt
}
zle -N cdup
bindkey '^\^' cdup
```

<br>

設定の細かい意味は知りません（Ｕ＾ω＾）

!SLIDE

## cd .. (2/3)

<br>

*Ctrl-^* で cd ..

cd .. を使わなすぎてヤバイ

!SLIDE

## cd .. (3/3)

効果を検証しましょう

→ キーバインドを使った回数は分からないのでゴメンナサイ

<br>

`grep -Ec "^cd" ~/.zsh_history`

→ 1355行


<br>

`grep -Ec "^cd \.\." ~/.zsh_history`

→ 3行

!SLIDE

## お手軽解凍コマンド

!SLIDE

* *tar.gz*

→ tar zxvf foo.tar.gz

<br>

* **tar.bz2**

→ tar xvjf foo.tar.bz2

<br>

* [zip]()

→ unzip foo.zip -d foo

だいたい決まってるよねー

!SLIDE

```
extract () {
if [ -f $1 ] ; then
    case $1 in
        *.tar.bz2)   tar xvjf $1    ;;
        *.tar.gz)    tar xvzf $1    ;;
        *.tar.xz)    tar xvJf $1    ;;
        *.bz2)       bunzip2 $1     ;;
        *.rar)       unrar x $1     ;;
        (略)

alias ex='extract'
```

!SLIDE

* *tar.gz*

→ ex foo.tar.gz

<br>

* **tar.bz2**

→ ex foo.tar.bz2

<br>

* [zip]()

→ ex foo.zip

!SLIDE

## clipコマンド

!SLIDE

```
func_clip() {
  if which pbcopy >/dev/null 2>&1 ; then
    # Mac
    cat $1 | pbcopy
  elif which xsel >/dev/null 2>&1 ; then
    # Linux
    cat $1 | xsel --input --clipboard
  elif which putclip >/dev/null 2>&1 ; then
    # Cygwin
    cat $1 | putclip
  fi
}
alias clip=func_clip
```


!SLIDE

## 競技プログラマ御用達のコマンド

* 問題を見る
* Vimで問題を解く
* clipコマンドでソースをコピー

**clip** a.cpp

* 提出フォームに貼り付ける

!SLIDE

`grep -Ec "^clip" ~/.zsh_history`

結果：279行

!SLIDE

## 質問ありますか？

