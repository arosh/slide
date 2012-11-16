!SLIDE

## 課題2. GPA(Grade Point Average)

<br>

### 方針

1. 評価(A,B,C,D,F)を点数に換算
2. その合計を変数 sum に入れる
3. 単位の個数 N で割る

<br>

<span style="color: gray;">余談: 発表者は振動波動論 (通称「しんぱ」) の単位にｇｋｂｒ中</span>

!SLIDE

## 愚直に書いてみた

```scala
var N = readInt // 1行読み込んで整数に
var r = readLine // 1行読み込む
var sum = 0

for (c <- r) {
  if      (c == 'A') sum += 4
  else if (c == 'B') sum += 3
  else if (c == 'C') sum += 2
  else if (c == 'D') sum += 1
  else if (c == 'F') sum += 0
}
var gpa = sum.toDouble / N
println(gpa)
```

!SLIDE

## パターンマッチ

→ Switch-Case文に相当するもの

例によって*隠された力*も持っている


```scala
var sum = 0
for (c <- r) {
  c match {
    case 'A' => sum += 4
    case 'B' => sum += 3
    case 'C' => sum += 2
    case 'D' => sum += 1
    case 'F' => sum += 0
  }
}
```

!SLIDE

## 隠された力その１

パターンマッチは*値を返す*


```scala
var sum = 0
for (c <- r) {
  var k = (c match {
    case 'A' => 4
    case 'B' => 3
    case 'C' => 2
    case 'D' => 1
    case 'F' => 0
  })
  sum += k
}
```

!SLIDE

# とりあえず動くコードは完成

!SLIDE

# ところで、みなさん

<br>

# *const教* って御存知ですか？

!SLIDE

## constとは

→ 変数を*読み取り専用*にする修飾子。Javaでは final とも

```cpp

int hoge;

void foo() { /* hogeを利用する処理 */ }
void bar() { /* hogeを利用する処理 */ }

hoge = 123;
foo();
bar();
```

→ foo() の中で hoge を**誤って書き換える**と bar() も*バグる*

!SLIDE

## 対処法

1. 必要な情報は**引数で渡す**
2. hogeを*書き換えられないように*する

<br>

→ 2の場合はconstを付けることで解決

bar()の中で[書き換えていないかどうか]()ということに対して*安心感がある*

!SLIDE

## const教の活動について

* 主にC++界隈に生息？
* constを付けるべき変数にconstを付ける
* constを付けるために*処理を書き換える*

<br>

## Scalaとconst教との関係

### → 変数の宣言**var**を*val*に変えるだけで*const*になる

!SLIDE

## 現在のコード

```scala
var N = readInt
var r = readLine
var sum = 0
for (c <- r) {
  var k = (c match {
    case 'A' => 4
    /* 略 */
  })
  sum += k
}
var gpa = sum.toDouble / N
println(gpa)
```

!SLIDE

## 可能なところだけ書き換え

```scala
val N = readInt
val r = readLine
var sum = 0
for (c <- r) {
  val k = (c match {
    case 'A' => sum += 4
    /* 略 */
  })
  sum += k
}
val gpa = sum.toDouble / N
println(gpa)
```

!SLIDE

# *var* sum を消し去りたい！！

!SLIDE

## ところで

→ リストにはsumというメソッドがある

```scala
List(1, 2, 3).sum // => 6
```

<br>

点数に変換したリスト `scoreList` を作れば

```scala
val r = "BAF"
val scoreList = (3, 4, 0)
val sum = scoreList.sum
```

*var*を消せる！

!SLIDE

## 無理やり変換してみた

```scala
var scoreList = List.empty[Int]
for (c <- r) {
  val k = (c match {
    case 'A' => 4
    case 'B' => 3
    case 'C' => 2
    case 'D' => 1
    case 'F' => 0
  })
  scoreList :+= k // 後ろに追加する
}
val sum = scoreList.sum
```

!SLIDE

# もっと簡単にやりたい

# scoreListの*var*を消したい

!SLIDE

## 関数型言語の必殺技

→ 高階関数

### *map*: 「要素を変換する関数」を使ってリストを変換

<br>

```scala
val double = { a: Int => 2 * a } // 変換する関数
List(1, 2, 3).map(double)
// => List(double(1), double(2), double(3))
// => List(2, 4, 6)

// 略記法 (無名関数)
List(1, 2, 3).map( a => 2 * a )
```

!SLIDE

## 必殺技を使ってみる

```scala
val N = readInt
val r = readLine

val scoreList = r.map {
  case 'A' => 4
  case 'B' => 3
  case 'C' => 2
  case 'D' => 1
  case 'F' => 0
}
val sum = scoreList.sum
val gpa = sum.toDouble / N
println(gpa)
```

