# インストール
```Text
brew update
brew install scala
brew install sbt
```

# Javaとの比較
## Java
```Java
public class YodaJava {
    static BiFunction<Integer, Integer, Integer> go = (n, acc) -> n <= 0 ? acc : YodaJava.go.apply(n - 1, n * acc);
    static Function<Integer, Integer> factorial = i -> go.apply(i, 1);
 
    public static String formatResult(String name, int n, Function<Integer, Integer> f) {
        final String msg = "The %s of %d is %d.";
        return String.format(msg, name, n, f.apply(n));
    }
 
    public static void main(String[]args) {
        System.out.println(formatResult("factorial", 7, factorial));
    }
}
```

## Scala
```Java
object YodaScala {
  def factorial(n: Int): Int = {
    def go(n: Int, acc: Int): Int =
      if (n <= 0) acc
      else go(n-1, n*acc)
 
    go(n, 1)
  }
 
  def formatResult(name: String, n: Int, f:Int => Int) = {
    val msg = "The %s of %d is %d."
    msg.format(name, n, f(n))
  }
 
  def main(args: Array[String]): Unit = {
    println(formatResult("factorial", 7, factorial))
  }
}
```

# 参考
- http://skyul.tistory.com/335
- https://ppassa.wordpress.com/2012/05/23/scala_for_java_programmer/
- https://www.slideshare.net/jongwookkim/scala-for-java-gurus
- https://www.slideshare.net/danieltedkim/scala-43612706
- https://docs.scala-lang.org/ko/tutorials/scala-for-java-programmers.html

