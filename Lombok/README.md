https://projectlombok.org/

# Feature
## @Data
@ToString, @EqualsAndHashCode, @Getter, @Setter,@RequiredArgsConstructorが含まれている

### コンパイル前
```Java
@Data
public class Luke {
    private String a;
    private String b;
    private String c;
}
```

### コンパイル後
```Java
public class Luke {
    private String a;
    private String b;
    private String c;

    public Luke() {
    }

    public String getA() {
        return this.a;
    }

    public String getB() {
        return this.b;
    }

    public String getC() {
        return this.c;
    }

    public void setA(String a) {
        this.a = a;
    }

    public void setB(String b) {
        this.b = b;
    }

    public void setC(String c) {
        this.c = c;
    }

    public boolean equals(Object o) {
        if (o == this) {
            return true;
        } else if (!(o instanceof Luke)) {
            return false;
        } else {
            Luke other = (Luke)o;
            if (!other.canEqual(this)) {
                return false;
            } else {
                label47: {
                    Object this$a = this.getA();
                    Object other$a = other.getA();
                    if (this$a == null) {
                        if (other$a == null) {
                            break label47;
                        }
                    } else if (this$a.equals(other$a)) {
                        break label47;
                    }

                    return false;
                }

                Object this$b = this.getB();
                Object other$b = other.getB();
                if (this$b == null) {
                    if (other$b != null) {
                        return false;
                    }
                } else if (!this$b.equals(other$b)) {
                    return false;
                }

                Object this$c = this.getC();
                Object other$c = other.getC();
                if (this$c == null) {
                    if (other$c != null) {
                        return false;
                    }
                } else if (!this$c.equals(other$c)) {
                    return false;
                }

                return true;
            }
        }
    }

    protected boolean canEqual(Object other) {
        return other instanceof Luke;
    }

    public int hashCode() {
        int PRIME = true;
        int result = 1;
        Object $a = this.getA();
        int result = result * 59 + ($a == null ? 43 : $a.hashCode());
        Object $b = this.getB();
        result = result * 59 + ($b == null ? 43 : $b.hashCode());
        Object $c = this.getC();
        result = result * 59 + ($c == null ? 43 : $c.hashCode());
        return result;
    }

    public String toString() {
        return "Luke(a=" + this.getA() + ", b=" + this.getB() + ", c=" + this.getC() + ")";
    }
}
```

# 注意点
## fieldの名前を変更する時、Builderで生成されたsetterの名前がうまく変更できない場合がある。

## @Dataは使用しない方が良い。
### @Dataのに含まれている@EqualsAndHashCodeの問題
```Java
public class Luke {
    @Data
    @Builder
    private static class Star {
        private String a;
    }
 
    public static void main(String[] args) {
        Set<Star> starSet = new HashSet<>();
        Star star = Star.builder().a("a").build();
        starSet.add(star);
 
        System.out.println(starSet.contains(star));//Trueを返す
 
        star.setA("b");//lombokによりHashcodeが自動で変わってしまう
 
        System.out.println(starSet.contains(star));//Falseを返す
    }
}
```

### @Dataのに含まれている@Setterの問題
field値がfinalではない場合、何回でも値の再設定ができてしまう。

### @Dataのに含まれている@RequiredArgsConstructorの問題
fieldの順番を変えるとコンストラクタの引数の順番ど自動で変わってしまう。同じタイプがのfieldだったらエラーが起きないため、見つけにくい。

```Java
public class Luke {
    @RequiredArgsConstructor(staticName = "of")
    @Getter
    private static class Star {
        @NonNull
        private String one;
        @NonNull
        private String two;
    }
 
    public static void main(String[] args) {
        Star star =Star.of("1", "2");
        System.out.println(star.getOne());//1を返す
        System.out.println(star.getTwo());//2を返す
    }
}
 
----------------------------------------------------------------------------------------
ここでfieldの順番を変えるとコンストラクタの引数の順番ど自動で変わってしまう。
----------------------------------------------------------------------------------------
 
public class Luke {
    @RequiredArgsConstructor(staticName = "of")
    @Getter
    private static class Star {
        //field値oneとtwoの順番を変える
        @NonNull
        private String two;
        @NonNull
        private String one;
    }
 
    public static void main(String[] args) {
        Star star =Star.of("1", "2");
        System.out.println(star.getOne());//1ではなく2を返す
        System.out.println(star.getTwo());//2ではなく1を返す
    }
}
```

# 解決(Yoda案)
@Dataの代わりに @Getterのみを使用。(@Setterは利用しないため、 @Builderの利用は必須になる)
equalsやhashcodeなどオーバーライドする必要がある場合はlombokではなく手動でoverrideする。
**結論は@Getterと@Builderの２つのアノテーション組み合わせのみ利用する。**
```Java
public class Luke {
    @Getter
    @Builder
    private static class Wars {
        private String a;
    }
 
    public static void main(String[] args) {
        Set<Wars> warsSet = new HashSet<>();
        Wars wars = Wars.builder().a("a").build();
        warsSet.add(wars);
 
        System.out.println(warsSet.contains(wars));//Trueを返す
 
        wars.setA("b");//setterが存在しないため、コンパイルエラー
 
        System.out.println(warsSet.contains(wars));
    }
}
```

# Constructor
https://blog.y-yuki.net/entry/2016/10/13/003000




