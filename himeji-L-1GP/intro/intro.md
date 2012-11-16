!SLIDE

## 「もし健全な学生が

## **関数型プログラミング言語**の

## 『*Scala*』に取り憑かれたら」

<br>

### 第0回 姫路L-1グランプリ
### @[姫路IT系勉強会](https://sites.google.com/site/himejiitstudy/) Vol.11

!SLIDE

## おまえ誰よ

* 本名: いいづか しょう
* [@shora_kujira16](http://twttr.com/shora_kujira16)
* 大学生 (市内在住)

* 今読んでる本

	→ すごい*Haske*…うわなにをするやめｒ

* 信仰

	→ Vim / Zsh / *Ruby* on Rails

!SLIDE

## Scalaとは

* 創始者: Martin Odersky (通称『*小田好先生*』)
* 2003年ごろ開発開始
* [Twitter]()とか**tumblr**でも使われてるらしいよ

<br>

* JVM上の言語
* 関数型プログラミング*"も"*できる

<br>

* ポストJavaになったらいいなー


!SLIDE

## JVM上の言語？

「Javaファミリー」とか「JVMファミリー」とか呼ばれる

* Java
* Groovy
* Jruby
* Jython
* Clojure
* Scala

などなど


!SLIDE

## 利点

* *Java*のコードを[Scala]()から呼べる
* [Scala]()のコードを*Java*から呼べる

<br>

### → Javaの膨大な資産が利用できる

<br>

* <span style="color: gray;">余談: Scala for .NET とは何だったのか</span>

!SLIDE

## 関数型プログラミング言語って何？

→ 関数を値として扱える

<br>

* 関数を変数に入れる
* 引数に関数を取る関数

	→ いわゆる「*高階関数*」 (コーカイカンスー)

* 関数を返す関数

<br>

### ※今回は1回だけ使いました


!SLIDE

## 最近のScala動向

* 2012/8/27

[Scala 2.10.0 Milestone 7](http://www.scala-lang.org/node/12797)

<br>

* 2012/10/19

[Scala 2.10.0 RC1](http://www.scala-lang.org/node/13096)

<br>

* 2012/11/9

[Scala 2.10.0 RC2](http://www.scala-lang.org/node/16606)


!SLIDE

## 私とScalaとの関係 (1/2)

* 2011年上半期

存在を知る。いろいろ理解できず挫折

* 2011年9月

関数脳本を買う。 関数型言語の何たるかを知る

* 2011年12月

日本Scalaユーザーズグループができる

!SLIDE

## 私とScalaとの関係 (2/2)

* 2012年2月

某サイトのAPIのラッパーを作ってみたりとか

* 2012年6月

\#histudy vol.6 で Scalaを布教

* 最近

Scalaz (黒魔術を収めたライブラリ) に手を出し始める

<span style="color: gray;">┌（┌ ＾o＾）┐モナドォ…</span>




!SLIDE

## まずはHelloWorld

<br>

実行する方法は複数ある

* コンパイルする
* スクリプト形式
* 対話環境 (REPL)

!SLIDE

## コンパイルする場合

```scala
// Hello.scala
object Hello {
  def main(args: Array[String]) {
    println("Hello, world!")
  }
}
```

<br>

```
$ scalac Hello.scala
$ scala Hello
→ Hello, world!
```

!SLIDE

## スクリプト形式

```scala
// hello.scala
println("Hello, world!")
```

<br>

```
$ scala hello.scala
→ Hello, world!
```

<br>

数十行程度のコードを書くときに便利

!SLIDE

## REPL形式

```
$ scala
Welcome to Scala version 2.9.2 (Java HotSpot(TM) 64-Bit Server VM, Java 1.6.0_37).
Type in expressions to have them evaluated.
Type :help for more information.

scala> println("Hello, world!")
→ Hello, world!
```

<br>

テスト、実験などで大活躍
