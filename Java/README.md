
# Packageの命名ルール
https://stackoverflow.com/questions/3179216/what-is-the-convention-for-word-separator-in-java-package-names

# History of Java
```Java
//Java 1.2 
List list = new ArrayList();
list.add(1);
list.add(2);



//Java 1.5
List<Integer> list = new ArrayList<Integer>();
list.add(1);
list.add(2);



//Java 1.7 
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);



//Java 1.8
List<Integer> list = Stream.of(1,2).collect(Collectors.collectingAndThen(toList(), Collections::unmodifiableList));



//Java 9 
List<Integer> list = List.of(1,2);



//Java 10 
var list = List.of(1,2);
```