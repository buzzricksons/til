
# Method Reference式で書くのが効率的
```java
Shop::load //Method Reference
(serial) -> Shop.load(serial) //Basic Lambda

↓↓loadメソッドの引数が増えた時

Shop::load //修正する必要なし
(serial, 引数) -> Shop.load(serial, 引数) //引数追加の修正が必要
```

# イミュータブルリスト
### Java 8以前
```
List<YodaObj> list1 = new ArrayList<>();
for (YodaObj luke : originList) {
    if (yoda.priority().equals(Numeric.valueOf(Integer.MAX_VALUE))) continue;
    list1.add(yoda);
}

Collections.sort(list1, comparator(YodaObjComparator.BY_PRIORITY, YodaObjComparator.BY_CODE));
return Collections.unmodifiableList(list1);

```

### Java 8

```Text
return originList.stream()
                .filter(yoda -> !yoda.priority().equals(Numeric.valueOf(Integer.MAX_VALUE)))
                .sorted(BY_PRIORITY.thenComparing(BY_CODE))
                .collect(Collectors.collectingAndThen(Collectors.toList(), Collections::unmodifiableList));
```


# Comparator
## Multiple comparator
### Java 8以前
```
public static Comparator<YodaObj> comparator(final YodaObjComparator... multipleOptions) {
    return new Comparator<YodaObj>() {
        public int compare(YodaObj e1, YodaObj e2) {
            for (YodaObjComparator option : multipleOptions) {
                int result = option.compare(e1, e2);
                if (result != 0) {
                    return result;
                }
            }
            return 0;
        }
    };
}
    
public enum YodaObjComparator implements Comparator<YodaObj> {
    BY_PRIORITY {
        public int compare(YodaObj o1, YodaObj o2) {
            return o1.priority().compareTo(o2.priority());
        }
    },
    BY_CODE {
        public int compare(YodaObj o1, YodaObj o2) {
            return o1.code().compareTo(o2.code());
        }
    };
}

Collections.sort(originalList, comparator(YodaObjComparator.BY_PRIORITY, YodaObjComparator.BY_CODE));
return originalList;

```

### Java 8
```Text
Comparator<YodaObj> BY_PRIORITY = (e1, e2) -> e1.priority().compareTo(e2.priority());
Comparator<YodaObj> BY_CODE = (e1, e2) -> e1.code().compareTo(e2.code());

return originalList.stream().sorted(BY_PRIORITY.thenComparing(BY_CODE)).collect(Collectors.toList());

```

## Sort
```Text
inventory.sort((Apple a1, Apple a2) -> a1.getWeight().compareTo(a2.getWeight()));
↓
inventory.sort((a1, a2) -> a1.getWeight().compareTo(a2.getWeight()));
↓
inventory.sort(comparing((a) -> a.getWeight()));
↓
inventory.sort(comparing(Apple::getWeight));

```

### reversed
```Text
inventory.sort(comparing(Apple::getWeight).reversed());
```

### マルチComparator
```Text
inventory.sort(comparing(Apple::getWeight)
         .reversed()
         .thenComparing(Apple::getCountry));
```

# Predicate
## and, or
```Text
Predicate<Apple> redAndHeavyAppleOrGreen =
    redApple.and(a -> a.getWeight() > 150)
            .or(a -> "green".equals(a.getColor()));
```
※`a.or(b).and(c)`は`(a || b) && c` と同じ

## match
結果はbooleanで最終演算。
### anyMatch
### allMatchとnoneMatch
```Text
boolean isHealthy = menu.stream()
                        .allMatch(d -> d.getCalories() < 1000);
```

上記は下記と同じ


```Text
boolean isHealthy = menu.stream()
                        .noneMatch(d -> d.getCalories() >= 100);
```


# ショートサーキット
ストリーム全体をチェックせずに満足すれば途中で終了するため効率的。
### allMatch
### noneMatch
### findFirst
### findAny
### limit

# findFirstとfindAnyはいつ使うの？
parallel(並列)では一番目の要素を調べにくい。
順番が関係ない場合、parallelではfindAnyがおすすめ

# Function
https://docs.oracle.com/javase/jp/8/docs/api/java/util/function/package-summary.html
### andThen
```Text
Function<Integer, Integer> f = x -> x + 1;
Function<Integer, Integer> g = x -> x * 2;
Function<Integer, Integer> h = f.andThen(g);
int result = h.apply(1);
```
resultは`4`。つまりg(f(x))

### compose
```Text
Function<Integer, Integer> f = x -> x + 1;
Function<Integer, Integer> g = x -> x * 2;
Function<Integer, Integer> h = f.compose(g);
int result = h.apply(1);
```
resultは`3`。つまりf(g(x))
※composeメソッドは引数で渡されたメソッドを先に実行し、その結果を呼び出し元に引数として返す。

# パイプライン
```Text
Function<String, String> addHeader = Letter::addHeader;
Function<String, String> transformationPipeline = 
    addHeader.andThen(Letter::checkSpelling)
             .andThen(Letter::addFooter);
```
