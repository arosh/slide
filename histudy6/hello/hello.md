!SLIDE

## お品書き

1. Scalaの現状
2. *特徴＆文法のはなし*
3. 開発環境について
4. Scalaのアツい分野

!SLIDE

1. *Java*のVM上で動作
2. **全て**がオブジェクト
3. シンタックス・シュガーが充実
4. [オブジェクト指向言語]()と*関数型言語*を統合
5. 静的（型システムが超強力）

!SLIDE

# *Java*のVM(JVM)で
# 動作する

!SLIDE

## JVM上で動く言語

* Java
* Groovy
* Jruby
* Jython
* Clojure
* *Scala*

ほかにもたくさん！

!SLIDE

## 何がうれしい？
* Javaのファイルがそのまま使える

	* Java用のライブラリ
	* 過去に書いたJavaのコード

<br />

* その逆も

	* JavaからScalaコードを呼び出し

!SLIDE

### ライブコーディングやります

## 今からやること

* Javaのライブラリを使いたいので、Twitter4Jを使います
* *\#histudy* タグの付いたツイートを拾ってみる


!SLIDE

# *Java*の場合

!SLIDE

```java
import twitter4j.*;
import java.util.List;

// main関数
Twitter twitter =
    new TwitterFactory().getInstance();

Query query = new Query();
query.setQuery("#histudy");
```

!SLIDE

```java
try {
  List<Tweet> result =
    twitter.search(query).getTweets();

  for(Tweet tweet : result) {
    System.out.println("--------------------");
    System.out.println(tweet.getFromUser());
    System.out.println(tweet.getText());
  }
} catch(TwitterException e) {
  e.printStackTrace();
}
		
```

!SLIDE

## 実行方法

* コンパイル → `scala` クラス名
* スクリプト形式 → `scala` ファイル名 ←*コレでやる*
* REPL（対話環境）

!SLIDE

# 実演

!SLIDE

# [Scala]()の場合

!SLIDE

```scala
import twitter4j._
import scala.collection.JavaConversions._

val twitter =
    new TwitterFactory().getInstance

val query = new Query()
query.setQuery("#histudy")
```

!SLIDE

```scala
val result =
    twitter.search(query).getTweets

result.foreach { tweet =>
  println("-" * 20)
  println(tweet.getFromUser)
  println(tweet.getText)
}
```

!SLIDE

### 見所が多すぎるので
* import文
* 型推論
* 例外処理
* for文
* 高階関数
* 暗黙の型変換

!SLIDE

### これだけにしてくださいorz
* import文
* *型推論*
* 例外処理
* *for文*
* *高階関数*
* *暗黙の型変換*

!SLIDE

# 比較

!SLIDE

```java
Twitter twitter =
    new TwitterFactory().getInstance();
```


<br />

　　↓

<br />


```scala
val twitter =
    new TwitterFactory().getInstance
```

!SLIDE

## 見どころ
* 変数の宣言
* 型推論
* いろいろ省略

!SLIDE

# 変数について

!SLIDE

* 型はコロンの後ろに

```java
int i;
```

<br />

　　↓

<br />

```scala
var i: Int
```

!SLIDE

* *var*は普通の変数
* **val**は再代入禁止（const, final）

<br />

```scala
var a: String = "foo"
a = "bar"

val b: String = "foo"
b = "bar" // →コンパイルエラー
```

!SLIDE

# 型推論
* 変数の型
* 関数の戻り値の型

### 書かなくても（だいたい）補完

!SLIDE

## Javaだと・・・
```java
ArrayList<Integer> list =
	new ArrayList<Integer>();
```

!SLIDE

## Java 7では
```java
ArrayList<Integer> list =
	new ArrayList<>();
```

!SLIDE

## Scalaでは

`val list`*: ArrayList[Int]* = `new ArrayList[Int]()`

<br />

　　↓

<br />

`val list = new ArrayList[Int]()`

!SLIDE

# 右辺から
# 左辺の型を
# 推測してくれる

!SLIDE

## *※注意※*
## 型を書いたほうが
## 分かりやすいことも多い

!SLIDE

### 「型が動的に変わる」
### 　というわけではない

```scala
// ↓Int型
var s = 123
// ↓String型
s = "foo" // => コンパイルエラー
```

!SLIDE

# 元の話に
# 戻ります

!SLIDE

```java
Twitter twitter =
    new TwitterFactory().getInstance();
```


<br />

　　↓

<br />


```scala
val twitter =
    new TwitterFactory().getInstance
```

!SLIDE

# セミコロンは
# 省略できる

```java
print(foo);
```

↓

```scala
print(foo)
```

!SLIDE

## 引数を取らない関数は
## カッコ要らない

```scala
val twitter =
    new TwitterFactory().getInstance()
```

　　↓

```scala
val twitter =
    new TwitterFactory.getInstance
```

!SLIDE
## ドットの省略

```scala
val twitter =
    new TwitterFactory.getInstance
```

　　↓

```scala
val twitter =
    new TwitterFactory getInstance
```

!SLIDE

## *※注意※*
* 境界が不明瞭だといろいろ面倒…
* 読みやすさとのバランスも大事

