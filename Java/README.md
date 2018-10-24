
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

# 비트연산자
### &
비트 AND 연산자로 양쪽 비트가 모두 1일 때만 결과가 1이 되고 그렇지 않으면 0이 됨
- ex)(4 & 5) -> 결과 : 4 , (4=100, 5=101)

### |
비트 OR 연산자로 양쪽 비트 중 어느 하나라도 1이면 결과가 1이 되고 모두 0일때만 0이 됨
- ex)(4 | 5) -> 결과 : 5

### ^
비트 EXCLUSIVE OR(또는 XOR) 연산자는 양쪽 비트가 서로 다를 때만 1, 같을 때는 0이 됨
- ex)(4 ^ 5) -> 결과 : 1

### ~
비트 NOT 연산자는 양쪽 비트 연산자와는 다르게 피연산자를 하나만 갖는 단항 연산자, 모든 비트값을 반대로 만든다 (0->1, 1->0)
- ex)(~5) -> 결과 : -6

# Char to int
### lowcase

```Java
String str = "abcdef";
char[] ch  = str.toCharArray();
for(char c : ch) {
    int temp = (int) c;
//    int temp_integer = 96;//output:123456
    int temp_integer = (int)'a';//output:012345
    if(temp <= 122 & temp >= 97) {//for lower case
        System.out.print(temp-temp_integer);
    }
}
```

### uppercase
```Java
String str = "ABCDEF";
char[] ch  = str.toCharArray();
for(char c : ch) {
    int temp = (int)c;
//    int temp_integer = 64;//output:123456
    int temp_integer = (int)'A';//output: 012345
    if(temp<=90 & temp>=65) {//for upper case
        System.out.print(temp-temp_integer);
    }
}
```

# String文字列結合のパフォーマンス


