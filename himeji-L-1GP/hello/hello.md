!SLIDE 

## まとめ

* Scalaの構文には[隠された力]()が秘められている
* **コーカイカンスー**は関数型プログラミングの必殺技
* better Javaとしても使える
* const教では一緒に*const*を付けてくれる仲間を募集しています

!SLIDE

## おまけ@FizzBuzz

```scala
import scalaz._, Scalaz._, effects._

val fizzbuzz: Int => String = { n: Int =>
  ((n % 3 === 0 option "Fizz") |+|
  (n % 5 === 0 option "Buzz")) | n.shows
}

val runc: IO[Unit] =
  (1 to 100).map(fizzbuzz >>> putStrLn).sumr

def main(args: Array[String]): Unit =
  runc.unsafePerformIO
```

!SLIDE

## おまけ@tail -n 5

```scala
import scala.sys.process._

val fileName = args(0)

("tail -n 5 %s" format fileName) !
```
