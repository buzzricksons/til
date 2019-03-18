# Document
- https://www.methods.co.nz/asciidoc/index.html
- https://asciidoctor.org/docs/asciidoc-syntax-quick-reference/
- https://qiita.com/xmeta/items/de667a8b8a0f982e123a

# Section title
```text
= Document Title (Level 0)

== Level 1 Section Title

=== Level 2 Section Title

==== Level 3 Section Title

===== Level 4 Section Title
```

# New Line
```
line1 +
line2
```

# Text
| text | print |
|:-:|:-:|
| `*bold*` | **bold** |
| `_italic_` | _italic_ |
| `` `monospace` `` | `monospace` |
| `X^2^` | X上2 |
| `X~2~` | X下2 |
| `[red]#赤色#` | <font color="red">赤色</font> |
| `[underline]#下線#` | __下線__ |
| `[line-through]#取り消し線#` | ~~取り消し線~~ |
| `//コメント` |  |

# Link
```text
http://asciidoctor.org/[リンク名]
```

## 行頭にリンクを書かない場合は、URLの前に空白文字またはlink:が必要
```text
ホニャララ http://asciidoctor.org/[Asciidoctor]
ホニャララlink:http://asciidoctor.org/[Asciidoctor]
```

# Image
```text
image::http://placehold.it/350x150[代替テキスト]
```

# List
## Disc
```text
* level 1
** level 2
*** level 3
**** level 4
***** level 5
* level 1
```

## Number
```text
. Step 1
. Step 2
.. Step 2a
.. Step 2b
. Step 3
```

# 라인개행표시
```text
CPU:: コンピューターの中心的な処理装置
RAM:: 読み書き可能な主記憶装置
SSD:: フラッシュメモリを使用した補助記憶装置
キーボード:: キーを押すことで信号を送信する入力装置
マウス:: コンピューターのポインティングデバイス
モニター:: 映像を表示する出力装置
```

# Code Block
```text
[source, rust]
----
fn main() {
    println!("Hello World!");
}
----
```

# 引用
```text
[quote, 'https://ja.wikipedia.org/wiki/%E8%BB%BD%E9%87%8F%E3%83%9E%E3%83%BC%E3%82%AF%E3%82%A2%E3%83%83%E3%83%97%E8%A8%80%E8%AA%9E[Wikipedia:軽量マークアップ言語]']
____
軽量マークアップ言語（けいりょうマークアップげんご、英語: lightweight markup language）は、人間がシンプルなテキストエディタを使っての入力が容易になるように設計された、簡潔な文法をもつマークアップ言語である。
____
```

# Table
```text
.テーブルタイトル
[options="header"]
|=======================
|Col 1|Col 2      |Col 3
|1    |Item 1     |a
|2    |Item 2     |b
|3    |Item 3     |c
|=======================
```

```text
[format="csv"]
|======
1,2,3,4
a,b,c,d
A,B,C,D
|======
```

# パススルー
```text
++++
<ruby>
  <rb>亜米利加</rb>
  <rp>（</rp>
  <rt> アメリカ</rt>
  <rp> ）</rp>
</ruby>
++++
```



