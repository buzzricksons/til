
## ストリームは一回のみ利用できる
```Text
List<String> title = Arrays.asList("Luke", "Yoda", "StarWars");
Stream<String> s = title.stream();
s.forEach(System.out::println);
s.forEach(System.out::println); //java.lang.IllegalStateException;が出てしまう
```

## distinct
ストリームで生成されたオブジェクトのhashCode, equalsで重複をfiltering
```Text
List<Integer> numbers = Arrays.asList(1, 2, 1, 3, 3, 2, 4);
numbers.stream()
       .filter(i -> i % 2 == 0)
       .distinct()
       .forEach(System.out::println);
```
結果は
```
System.out.println(2);
System.out.println(4);
```

## skip
skip(n)はn個の要素を抜いたストリームを返す。ストリームの長さより大きいnを呼び出すと空のストリームが返される。
```Text
List<Dish> dishes = menu.stream()
                        .skip(2) //0,1番目の要素を抜く
                        .collect(toList());
```

## map, flatMap

## reduce
二つのパラメータが存在する
- １番目は初期値
- 2番目はBinaryOperator<T>

```Text
int sum = numbers.stream().reduce(0, (a, b) -> a + b);
int sum = numbers.stream().reduce(1, (a, b) -> a * b);
int sum = numbers.stream().reduce(0, Integer::sum);
```

### 最大値と最小値(max, min)
```Text
Optional<Integer> max = numbers.stream().reduce(Integer::max);
Optional<Integer> min = numbers.stream().reduce(Integer::min);
```

```Text
Optional<Transaction> smallestTransaction = transactions.stream()
						.min(comparing(Transaction::getValue));
```

#### Comparatorによる最大値と最小値
```Text
Comparator<Dish> dishCaloriesComparator = Comparator.comparingInt(Dish::getCalories);
Optional<Dish> mostCalorieDish = menu.stream()
                                    .collect(maxBy(dishCaloriesComparator));
```

### 予約演算
Collectors.summingInt
```Text
int totalCalories = menu.stream().collect(summingInt(Dish::getCalories));
```


### map-reduceパータン
```Text
int count = menu.stream()
		.map(d -> 1)
		.reduce(0, (a,b) -> a+b);


↓並列化

int count = menu.parallelStream()
		.map(d -> 1)
		.reduce(0, (a,b) -> a+b);
```
※reduceに渡されたlambdaの状態(インスタンス変数など)が変わらない必要があり、演算順番が変わっても結果が変わらないべき。


### joining
```Text
String traderStr = transactions.stream()
			.map(transaction -> transaction.getTrader().getName())
         		.distinct()
			.sorted()
			.reduce("", (n1, n2) -> n1 + n2);

↓

String traderStr = transactions.stream()
			.map(transaction -> transaction.getTrader().getName())
	        	.distinct()
			.sorted()
			.collect(joining());
```
※joiningは裏側でStringBuilderを使用する

#### separatorを指定
```Text
String shortMenu = menu.stream().map(Dish::getName).collect(joining(", "));
↓結果

pork, beef, chicken, french fries, rice, season fruit, pizza, prawns, salmon
```

#### joiningとreducing
```Text
String shortMenu = menu.stream().map(Dish::getName).collect(joining());
                 = menu.stream().map(Dish::getName).collect(reducing(s1, s2) -> s1 + s2)).get();//Optionalのため.get()を使用
                 = menu.stream().collect(reducing("", Dish::getName, (s1, s2) -> s1 + s2));//1番めの引数は初期値。というわけでOptionalは使用しない
```

## 基本形特化ストリーム
ボクシングの効率性だけに関係がある。その他の追加された機能はない。

### mapToInt, mapToDouble, mapToLong
```Text
int calories = menu.stream()
		.map(Dish::getCalories)
		.reduce(0, Integer::sum);
```
上記のソースは無駄な`int -> Integer -> 結果のint`Boxing処理が含まれている。  
これを防ぐために下記のように作成する
```Text
int calories = menu.stream()
		.map(Dish::getCalories)
		.sum();
```
でもこれはmapメソッドがStream<T>を生成するため実行できない。  
これを下記の数字ストリームで解決できる。

```Text
int calories = menu.stream()
		.mapToInt(Dish::getCalories)
		.sum();
```

#### boxing
```Java
int[] data = {1,2,3,4,5,6,7,8,9,10};

// To boxed array
Integer[] what = Arrays.stream( data ).boxed().toArray( Integer[]::new );
Integer[] ever = IntStream.of( data ).boxed().toArray( Integer[]::new );

// To boxed list
List<Integer> you  = Arrays.stream( data ).boxed().collect( Collectors.toList() );
List<Integer> like = IntStream.of( data ).boxed().collect( Collectors.toList() );
```

### オブジェクトstreamに復元する方法
```Text
IntStream intStream = menu.stream().mapToInt(Dish::getCalories);
Stream<Integer> stream = intStream.boxed();
```

### デフォルト値の指定
```Text
OptionalInt maxCalories = menu.stream()
                            .mapToInt(Dish::getCalories)
                            .max();
int max = maxCalories.orElse(1);
```

### 数字の範囲
http://www.deadcoderising.com/2015-05-19-java-8-replace-traditional-for-loops-with-intstreams/

#### 初期値と終了値を含む
```Text
IntStream evenNumbers = IntStream.rangeClosed(1, 100) //1以上、100以下
                                .fileter(n -> n % 2 == 0);//偶数
System.out.println(evenNumbers.count());
```

#### 初期値と終了値を含まない
```Text
IntStream evenNumbers = IntStream.range(1, 100) //1超過、100未満
                                .fileter(n -> n % 2 == 0);
System.out.println(evenNumbers.count());
```

## フィボナッチの数列
```Text
Stream.iterate(new int[]{0,1},
                t -> new int[]{t[1], t[0]+t[1]})
        .limit(10)
        .map(t -> t[0])
        .forEach(System.out::println);
```

```Text
IntSupplier fib = new IntSupplier() {
    private int previous = 0;
    private int current = 1;
    public int getAsInt() {
        int oldPrevious = this.previous;
        int nextValue = this.previous + this.current;
        this.previous = this.current;
        this.current = nextValue;
        return oldPrevious;
    }
};

IntStream.generate(fib).limit(10).forEach(System.out::println);
```



## グルーピング
```Text
Map<Dish.Type, List<Dish>> dishesByType = menu.stream().collect(groupingBy(Dish::getType));

↓結果
{FISH=[prawns, salmon], OTHER=[french fries, rice, season fruit, pizza], MEAT=[pork, beef, chicken]}

```
### 条件ごとの分類を適用
```Text
Map<CaloricLevel, List<Dish>> dishesByCaloricLevel = menu.stream().collect(
			groupingBy(dish -> {
				if (dish.getCalories() <= 400) {
					return CaloricLevel.DIET;
				} else if (dish.getCalories() <= 700) {
					return CaloricLevel.NORMAL;
				} else {
					return CaloricLevel.FAT;
				}
			})
);
```

#### keyを指定した条件ごとの分類を適用
```Text
Map<Dish.Type, Map<CaloricLevel, List<Dish>>> dishesByCaloricLevel = menu.stream().collect(
		groupingBy(Dish::getType,
			groupingBy(dish -> {
				if (dish.getCalories() <= 400) {
					return CaloricLevel.DIET;
				} else if (dish.getCalories() <= 700) {
					return CaloricLevel.NORMAL;
				} else {
					return CaloricLevel.FAT;
				}
			})
		)
);
```

### 条件(collector)による収集
```Text
Map<Dish.Type, Optional<Dish>> mostCaloricByType = menu.stream()
		.collect(groupingBy(Dish::getType,
					maxBy(comparingInt(Dish::getCalories))
		)
);

↓結果(valueはOptional<Dish>でラッピングされる)

{FISH=Optional[salmon], OTHER=Optional[pizza], MEAT=Optional[pork]}
```

#### valueからOptionalを外す
```Text
Map<Dish.Type, Dish> mostCaloricByType = menu.stream()
		.collect(groupingBy(Dish::getType,
			collectingAndThen(
						maxBy(comparingInt(Dish::getCalories)),
							Optional::get)
				)
		);

↓結果

{FISH=salmon, OTHER=pizza, MEAT=pork}
```

#### その他
```Text
Map<Dish.Type, Integer> totalCaloriesByType = 
    menu.stream()
        .collect(groupingBy(Dish::getType, summingInt(Dish::getCalories)));
```

```Text
Map<Dish.Type, Set<CaloricLevel>> caloricLevelsByType = 
    menu.stream()
        .collect(
            groupingBy(Dish::getType
                        , mapping(dish -> {
                            if (dish.getCalories() <= 400) {
                                return CaloricLevel.DIET;
                            } else if () {
                                return CaloricLevel.NORMAL;
                            } else {
                                return CaloricLevel.FAT;
                            }
                          }
                            , toSet() //toCollection(HashSet::new)にしても同じ
                          )
                      )
                );

↓結果

{OTHER=[DIET, NORMAL], MEAT=[DIET, NORMAL, FAT], FISH=[DIET, NORMAL]}
```

### 分割
```Text
Map<Boolean, List<Dish>> partitionedMenu = 
    menu.stream()
        .collect(partitioningBy(Dish::isVegetarian));

↓結果

{false=[pork, beef, chicken, prawns, salmon],
    true=[french fries, rice, season fruit, pizza]}
```

#### groupingByとの組み合わせ
```Text
Map<Boolean, Map<Dish.Type, List<Dish>>> vegetarianDishedByType =
    menu.stream()
        .collect(partitioningBy(Dish::isVegetarian,
                                    groupingBy(Dish::getType)));

↓結果

{false={FISH=[prawns, salmon], MEAT=[pork, beef, chicken]},
    true={OTHER=[french fries, rice, season fruit, pizza]}}
```

### 素数(Prime Number)
```Java
public boolean isPrime(int candidate) {
    return IntStream.range(2, candidate)
                    .noneMatch(i -> candidate % i == 0);


public Map<Boolean, List<Integer>> partitionPrimes(int n) {
    return IntStream.rangeClosed(2, n)
                    .boxed()
                    .collect(partitionBy(candidate -> isPrime(candidate)));
}
```

※제곱근 이하로 대상 숫자범위를 제한할 경우
```Java
int candidateRoot = (int)Math.sqrt((double) candidate);
```

## Collectorsクラスのstaticメソッド
| メソッド | 説明 | 例 |
| ------------- |:-------------:| -----:|
| toCollection | ストリームのすべての項目を引数のコレクションでまとめる | Collection<Dish> dishes = menuStream.collect(toCollection(), ArrayList::new); |
| counting | ストリームの項目数を計算 | long howManyDishes = menuStream.collect(counting()); |
| summingInt | ストリームの項目からintのプロパティを計算 | int totalCalories = mentStream.collect(summingInt(Dish::getCalories)); |
| averagingInt | ストリームの項目のintプロパティの平均値を計算 | double avgCalories = mentStream.collect(averagingInt(Dish::getCalories)); |
| joining | ストリームの各項目にtoStringメソッドの結果を結ぶ | String shortMenu = mentStream.map(Dish::getName).collect(joining(",")); |
| maxBy | 引数の利用してストリームの最大のプロパティをOptionalでラッピングして返す。存在しない場合はOption.empty()を返す | Option<Dish> fattest = mentStream.collect(maxBy(comparingInt(Dish::getCalories))); |
| minBy | maxByと逆 |  |
| reducing | 0に初期化してBinaryOperatorでストリームの各プロパティを繰り返してプラスして一つの値にreducing | int totalCalories = menuStream.collect(reducing(0, Dish::getCalories, Integer::sum)); |
| collectingAndThen | collectorをラッピングしその結果に引数のメソッドを適用 | int howManyDishes = menuStream.collect(collectingAndThen(toList(), List::size)); |
| groupingBy | 一つのプロパティ値をもとにストリームの項目をグルーピングし、もとになったプロパティの値を返すMapのキーとして使用 | Map<Dish.Type, List<Dish>> dishesByType = menuStream.collect(groupingBy(Dish::getType)); |
| partitioningBy | predicateをストリームの各項目に適用した結果で分割する | Map<Boolean, List<Dish>> vegetarianDishes = menuStream.collect(partitioningBy(Dish::isVegetarian)); |




226pageまでのまとめ