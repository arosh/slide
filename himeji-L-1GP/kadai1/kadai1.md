!SLIDE

## 課題1. fizzbuzz

```scala
for (i <- 1 to 100) {
  if (i % 3 == 0 && i % 5 == 0)
    println("FizzBuzz")
  else if (i % 3 == 0)
    println("Fizz")
  else if (i % 5 == 0)
    println("Buzz")
  else
    println(i)
}
```

!SLIDE

## for式

```scala
for (i <- 1 to 100)
```

<br>

* Scalaには `for (…; …; …) {}` のような構文は無い
* Javaの*拡張for文*ならある

<br>

```java
for (int i : list) // Java
```

```ruby
for i in 1..100 // Ruby
```

```php
foreach (range(1, 100) as $i) // PHP
```

```python
for i in range(1,101) // Python
```

!SLIDE

## その他

* 文法の*見た目*はJavaの文法を踏襲

```scala
if (i % 3 == 0 && i % 5 == 0)
```

* ただし*隠された力*を持っていたりする
	* 「forはモナドを扱うための…
	* 「ifは三項演算子…
* はじめのうちは**better Java**として使えば良いのでは


!SLIDE

## 課題1. fizzbuzz (再掲)

```scala
for (i <- 1 to 100) {
  if (i % 3 == 0 && i % 5 == 0)
    println("FizzBuzz")
  else if (i % 3 == 0)
    println("Fizz")
  else if (i % 5 == 0)
    println("Buzz")
  else
    println(i)
}
```

