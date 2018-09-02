
# for loopでのindex使用
- The current iteration index, starting with 0. This is the `index` property.
- The current iteration index, starting with 1. This is the `count` property.
- The total amount of elements in the iterated variable. This is the `size` property.
- The iter variable for each iteration. This is the `current` property.
- Whether the current iteration is even or odd. These are the `even`/`odd` boolean properties.
- Whether the current iteration is the first one. This is the `first` boolean property.
- Whether the current iteration is the last one. This is the `last` boolean property.

```Text
例：
  <tr th:each="prod,iter : ${prods}" th:class="${iter.odd}? 'odd'">
    <td th:text="${iter.index}">starting with 0. This is the index property.</td>
    <td th:text="${iter.count}">starting with 1. This is the count property.</td>
    <td th:text="${prod.inStock}? #{true} : #{false}">yes</td>
  </tr>
```

# Custom attribute
```Text
<div th:attr="data-el_id=${element.getId()}">
<div th:attr="data-id=${element.getId()},data-name=${element.getN‌​ame()}"> 
```

# Javascript関数にThymeleafの値を引数で渡す
### 一つの引数を渡す場合
```Text
<span th:onclick="'javascript:function(\'' + ${args} + '\');'">Test</span>
```

### 複数の引数を渡す場合
```Text
<span th:onclick="'javascript:function(\'' + ${args1} + '\',\'' + ${args2} + '\');'">Test</span>
```

### ||を利用する
```Text
<span th:href="|javascript:document.ph01.src = '${imageUrlOsize}'; void(0);|">Test</span>
```

# 動的にattrを追加
### conditionalなクラス追加
```Text
<img class="swiper-slide__img" th:classappend="${isFirst} ? 'active':''" ..........>

↓

1)isFirstの場合
<img class="swiper-slide__img active"............>
 
 
2)isFirstではない場合
<img class="swiper-slide__img" .............>
```

```Text
<div class="swiper-slide" th:attr="id=${isFirst} ? 'box' : null">

↓
 
1)isFirstの場合
<div class="swiper-slide" id="box">
 
 
2)isFirstではない場合
<div class="swiper-slide">
```

# includeに引数を渡す方法
### 呼び出し元
```Html
<!--/*/ <th:block th:replace="include_common :: coordinate(${contentsKey})" /> /*/-->
```

### includeファイル
include_common.html
```Html
<th:block th:fragment="coordinate(contentsKey)">
    <!--STAFFSTART Contents START -->
    <div class="AAA" th:attr="key=${contentsKey}"></div>
    <!--STAFFSTART Contents END -->
</th:block>```