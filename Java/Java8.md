# そのほか
## 素数(Prime Number)
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

