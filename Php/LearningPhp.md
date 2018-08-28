### define과 defined의 차이
- define(): 상수를 정의. 상수이름과 상수값을 인수로 넣어줌.

```Php
<?php define("상수 이름", "상수값");?>

```

- defined(): 상수가 정의되어 있는지 검사.

### isset
변수의 유무 체크
```Php
<?php

$val = 'value';

if (isset($val)) {
    echo '$val은 값이 존재';
}
```


### 오브젝트 출력
```
var_dump(情報を出力する変数)
```

### 널 병합 연산자
PHP7부터

```Php
product_id: <?php print $_POST['product_id'] ?? '' ?>
```

- PHP7이전의 경우
```Php
if (isset($_POST['product_id'])) {
    print $_POST['product_id'];
}
```

### 다중값을 지닌 폼 요소
- 다중값

```Php
<form method="POST" action="eat.php">
<select name="lunch[]" multiple>
<option value ...
.
.
.
```

- 접근

```Php
<?php
if (isset($_POST['lunch'])) {
    foreach($_POST['lunch'] as $choice) {
        print "$choice 번을 골랐습니다.</br>";
    }
}
?>
```

### 이메일 주소 검증
```Php
$input['email'] = filter_input(INPUT_POST, 'email', FILTER_VALIDATE_EMAIL);
if(!$input['email']) {
    $errors[] = '올바른 이메일 주소를 입력해주세요.';
}
```

### 문자열에서 HTML태그 제거 or 인코딩하기
```Php
// 댓글에서 HTML제거하는 방법
$comments = strip_tags($_POST['comments']);
print $comments;

// 댓글에서 HTML인코딩 하는 방법(추천)
$comments = htmlentities($_POST['comments']);
```

### Prepared Statement
```Php
$stmt = $db -> prepare('INSERT INTO dishes (dish_name, price, is_spicy) VALUES (?,?,?)');
$stmt->execute(array($_POST['new_dish_name'], $_POST['new_price'], $_POST['is_spicy']));
```

### file
```Php
// 앞선 예제의 템플릿 파일 불러오기
$page = file_get_contents('page-template.html');


// 결과를 저장
file_put_contents('page.html', $page);


// 한 번에 한 줄씩 읽기
$fh = fopen('people.txt', 'rb');
while((!feof($fh)) && ($line = fgets($fh))) {
    $line = trim($line);
    $info = explode('|', $line);
    print '<lil><a href="mailto:' .$info[0] . '">' . $info[1] ."</li>\n";
}
fclose($fh);
```

### realpath()
```
realpath('/usr/local/data/../../../etc/passwd') 실행↓

/etc/passwd 반환
```

### 쿠키
```
setcookie('userid', 'ralph');

↓

print 'Hello, ' .$_COOKIE['userid'];
```

```
setcookie('short-userid','ralph',0,'/');
setcookie('short-userid','ralph',0,'/~alice/');
```






