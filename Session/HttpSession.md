# HttpSession Interface
### 新しいセッションの生成
```Java
HttpSession session = request.getSession();//既存にセッションが存在すればそれを返す、存在しなければ新しいセッションを生成し返す

or

HttpSession session = request.getSession(true);//いつも新しいセッションを生成して返す。
```

### 既存のセッションを取得する
```Java
HttpSession session = request.getSession(false);
```

### セッションの削除
```Java
session.invalidate();
```

