!SLIDE

# 次

* 暗黙の型変換
* 高階関数
* for

!SLIDE

### 出力のループ部分

```scala
// result : java.util.List<Tweet>

result.foreach { tweet =>
  // 表示する処理
}
```

!SLIDE
### **for**で書いても良かったが…
```scala
// result : java.util.List<Tweet>

result.foreach { tweet =>
  // 表示する処理
}

for(tweet <- result) {
  // 表示する処理
}
```

!SLIDE

```scala
result.foreach { tweet =>
  // 表示する処理
}
```


### *Ruby*だと…

```ruby
result.each do |tweet|
  # 表示する処理
end
```

!SLIDE

### 何か気づきませんか？

```scala
// result : java.util.List<Tweet>

result.foreach { tweet =>
  // 表示する処理
}
```


!SLIDE

// result : java.util.List&lt;Tweet&gt;

<br />

result.foreach *{ tweet =>*

　// 表示処理

*}*

<br />

### この部分も気になるが…

!SLIDE

// result : java.util.List&lt;Tweet&gt;

<br />

result.*foreach* { tweet =>

　// 表示処理

}

<br />

### Listにこんなメソッドあったっけ？



!SLIDE

## JavaのListには

## もちろん無い


!SLIDE

```scala
import twitter4j._
import scala.collection.JavaConversions._

val twitter =
    new TwitterFactory().getInstance
```

<br />

いったいどこから？

!SLIDE

import twitter4j._

import *scala.collection.*
　　　　　*JavaConversions._*

<br />

val twitter =

　　new TwitterFactory().getInstance

## ！

!SLIDE

```scala
implicit def asScalaBuffer[A](l : ju.List[A]):
	mutable.Buffer[A] = l match {
  case MutableBufferWrapper(wrapped) => wrapped
  case _ =>new JListWrapper(l)
}
```

こんなコードがあった

!SLIDE

### 暗黙の型変換(Implicit Conversion)

	必要に応じて他のクラスに
	自動で変換するための関数を定義できる

<br />

### 例：Intの場合

↓`scala.Predef` に定義

```scala
implicit def intWrapper(x: Int): RichInt =
	new RichInt(x)
```

!SLIDE

## 使用例

```
(-123).abs // => 123

1.to(10)
// => Range(1, 2, 3, 4, 5, 6, 7, 8, 9, 10)
// ↑あとで使う！
```
	
!SLIDE

```scala
// result : java.util.List<Tweet>

result.foreach { tweet =>
  // 表示する処理
}
```

`result` は *IterableLike* に変換された

!SLIDE

```scala
result.foreach { tweet =>
  println("-" * 20)
  println(tweet.getFromUser)
  println(tweet.getText)
}
```

### 関数型はじまるよー！

!SLIDE

### Scalaでは

# *関数* ∈ **値**

### と、考えて良い

!SLIDE

* 変数に関数を入れられる
* 関数の*引数*に関数をとれる
* 関数の*返り値*として関数を返せる

!SLIDE

* 変数に関数を入れられる
* **関数の引数に関数をとれる**←コレを説明
* 関数の*返り値*として関数を返せる

<br />

### コレクションの操作に便利！

!SLIDE

```scala
def foreach[U](f: A => U)
```

<br />

**foreach** は

「値を１つ取って何かする」関数をとる

!SLIDE

```scala
def puts(x: Int) {
    println(x)
}

List(1, 2, 3).foreach(puts)
```

<br />

### これでも良いが…

!SLIDE

```scala
List(1, 2, 3).foreach { (x: Int) =>
    println(x)
}
```

<br />

### やっぱり無名関数！

!SLIDE
### 例
[map]()(f: *A* => **B**)

1. *A*型の値を引数に取って
2. **B**型の値に変換する

という関数を引数に取る

<br />

```scala
List(1, 2, 3).map((x: Int) => 2 * x)
// => List(2, 4, 6)
```

!SLIDE
### 例
[filter]()(f: *A* => **Boolean**)

1. *A*型の値を引数に取って
2. 条件に合うか判定する

という関数を引数に取る

<br />

```scala
List(1, 2, 3).filter((x: Int) => x % 2 != 0)
// => List(1, 3)
```

!SLIDE
### 例
[exists]()(f: *A* => **Boolean**)

1. *A*型の値を引数に取って
2. 条件に合うか判定する

という関数を引数に取る

<br />

```scala
List(1, 2, 3).filter((x: Int) => x < 0)
// => false
```

!SLIDE

```scala
(x: Int) => 2 * x
```

→ **無名関数**

!SLIDE

* JavaScript

```js
function(n) {
	return 2 * n;
}
```

* Ruby

```ruby
{|x| 2 * x}
```


!SLIDE

* 引数が１個なのでカッコを外す

```scala
map(x: Int => 2 * x)
```

<br />

* 引数は型推論

```scala
map(x => 2 * x)
```

!SLIDE

* アンダースコアを使う（Perlの*$_*）

```scala
map(2 * _)
```

<br />

・ 2.* は引数を１個とる関数である

```scala
map(2 *)
```


!SLIDE

# for文の話

```scala
for(tweet <- result) {
  // 表示する処理
}
```

!SLIDE

## [Scala]()のfor文は
## *Java*で言う**foreach**

!SLIDE

## *Java*

<br />

```java
// list := List<Integer> { 1, 2, 3 }

for( int i : list ) {
    // なにかする
}
```

!SLIDE

## [Scala]()
<br />

```scala
// list := List[Int] ( 1, 2, 3 )

for( i <- list ) {
    // なにかする
}
```

!SLIDE

## 普通の繰り返し

<br />

```scala
for( i <- 1 to 10 ) {
    println(i)
}
```

<br />

`1 to 10` は 1.to(10)の略記法

暗黙の型変換でRangeオブジェクトができる

!SLIDE


```scala
for(i <- 1 to 10)
```

↓

```scala
for(i <- (new RichInt(1)).to(10))
```

↓

```scala
for(i <- Range.inclusive(1, 10))
```

!SLIDE

## でも、それだけじゃない

!SLIDE

```scala
val s = for( i <- List(1, 2, 3) )
	    yield i * 2

// s == List(2, 4, 6)
```

!SLIDE

## forの中にif

```scala
for {
  i <- List(3, 1, 4, 1, 5)
  if i <= 3
} println(i)
```

!SLIDE

## N重ループ

```scala
for {
  i <- 1 to 9
  j <- 1 to 9
} println(i * j)

// => 九九の表示
```

!SLIDE

### なんか似てない？

```scala
for( i <- List(2, 7, 1, 8) )
  println(i)
```

<br />

```scala
List(2, 7, 1, 8).foreach { i =>
  println(i)
}
```

!SLIDE

### なんか似てない？

```scala
val s = for( i <- List(1, 2, 3) )
	    yield i * 2
```

<br />

```scala
val s = List(1, 2, 3).map { i => i * 2 }
```

!SLIDE

### なんか似てない？

```scala
for {
  i <- List(2, 3, 5, 7)
  if i <= 3
} println(i)
```

<br />

```scala
List(2, 3, 5, 7)
  .filter { _ <= 3 }
  .foreach { println _ }
```

!SLIDE

Scalaの**for**は

* foreach
* map(flatMap)
* filter(withFilter)

に変換するシンタックス・シュガー

!SLIDE

![haskell](hello2/haskell.jpg)

某純粋関数型言語みたいなことが…