# Stream
### takeWhile
```Java
        Stream.of("A is Java", "B is Groovy", "C is Kotlin", "D is Scala", "E is Python", "F is Go")
                .takeWhile(s -> !s.contains("Scala"))
                .forEach(System.out::println);//"A is Java", "B is Groovy", "C is Kotlin"


        Stream.of(1, 2, 3, 4, 5, 6)
                .takeWhile(i -> i < 3)
                .forEach(System.out::println);//1, 2
```

### dropWhile
```Java
        Stream.of("A is Java", "B is Groovy", "C is Kotlin", "D is Scala", "E is Python", "F is Go")
                .dropWhile(s -> !s.contains("Scala"))
                .forEach(System.out::println);//"D is Scala", "E is Python", "F is Go"


        Stream.of(1, 2, 3, 4, 5, 6)
                .dropWhile(i -> i < 3)
                .forEach(System.out::println);//3,4,5,6
```

> Scalaの場合

```Scala
    val x = (1 to 6).toArray
    x.takeWhile(_ < 3).foreach(println)//1,2
    x.dropWhile(_ < 3).foreach(println)//3,4,5,6
```