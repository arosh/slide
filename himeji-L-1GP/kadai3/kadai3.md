!SLIDE

## 課題3. tail -n 5

### 難しいところ

* 全部読み込んで、後ろから5行 → メモリが…
* 後ろから読み込む → 難しい(特にScalaでは)
* 前から読み込んで、ゴミは捨てる、という処理を書く
	* Haskellでは良い感じに取り計らってくれるが…
* 5行未満のファイルを読み込ませた時の処理

!SLIDE

## 私の解法

### → Queueに放り込む

* データを1つ入れる (push, enqueue)
* データを1つ取り出す (pop, dequeue)
* 先に入れたものが先に出る (*FIFO*)

<br>

* 前の行から順にpushして、

	サイズが5を超えたらpopして前のデータを捨てる

!SLIDE

## **const教**再び

* データを入れる、取り出すという操作は、Queueの*状態を変更する* → mutableなオブジェクト

* const教徒としてはコレはマズい

* Queueの状態を変更せずにデータの出し入れを行う方法もある → [@kakkun61](https://twitter.com/kakkun61) に聞いて下さい

* 今回はちょっと逃げてみよう

!SLIDE

## 前から順に読み込む

*Java*の**BufferdReader**はさすがにダサい

```java
while (( line = reader.readLine() ) != null) { /* */ }
```

<br>

[Scala]()の*Iterator*が便利！

```scala
for ( line <- reader ) { /* */ }
```

<br>

→ 読み込んだ後のデータは捨てる


!SLIDE

```scala
import java.io.File

import scala.collection.mutable
import scala.io.Source

val PARAM_N = 5

if (args.size == 0) {
  println("usage: scala tail.scala fileName")
  sys.exit(1)
}

val fileName = args(0)
```

!SLIDE

```scala
val handle = new File(fileName)

if (handle.exists == false) {
  println(fileName + ": No such file or directory")
  sys.exit(1)
}

val stream = Source.fromFile(handle)
val lineIter = stream.getLines

val queue = mutable.Queue.empty[String]
```

!SLIDE

```scala
for (line <- lineIter) {
  queue.enqueue(line)

  if (queue.size > PARAM_N) {
    queue.dequeue()
  }
}

stream.close()

for (line <- queue) {
  println(line)
}
```
