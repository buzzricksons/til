http://www.ne.jp/asahi/hishidama/home/tech/java/reflection.htmlより
メソッド呼び出し
Javaでは、メソッドを保持するためにMethodというクラスが用意されている。

import java.lang.reflect.Method;
Methodは、Class#getMethod()やgetDeclaredMethod()を使って取得できる。
メソッド呼び出しにはMethod#invoke()を使用する。
戻り値はObject型として返るが、内容は当然元のメソッドが返す型となる。プリミティブ型（int等）の場合、ラッパークラス（Integer等）として返る。またvoidの場合はnullが返る。
（何の型が返るのかはMethod#getReturnType()で調べる）

引数なしstaticメソッド実行
	Method method;
	try {
		method = clazz.getMethod("メソッド名", null);
	} catch (SecurityException e) {
		throw new RuntimeException(e);
	} catch (NoSuchMethodException e) {
		throw new RuntimeException(e);
	}

	Object ret; //戻り値
	try {
		ret = method.invoke(null, null);
		//  = クラス名.メソッド名(); と同じ
	} catch (IllegalArgumentException e) {
		throw new RuntimeException(e);
	} catch (IllegalAccessException e) {
		throw new RuntimeException(e);
	} catch (InvocationTargetException e) {
		throw new RuntimeException(e);
	}
引数なしのインスタンスメソッド実行
	Method method;
	try {
		method = object.getClass().getMethod("メソッド名", null);
	} catch (SecurityException e) {
		throw new RuntimeException(e);
	} catch (NoSuchMethodException e) {
		throw new RuntimeException(e);
	}

	Object ret; //戻り値
	try {
		ret = method.invoke(object, null);
		//  = object.メソッド名(); と同じ
	} catch (IllegalArgumentException e) {
		throw new RuntimeException(e);
	} catch (IllegalAccessException e) {
		throw new RuntimeException(e);
	} catch (InvocationTargetException e) {
		throw new RuntimeException(e);
	}
引数ありのインスタンスメソッド実行
	Method method;
	try {
		method = object.getClass().getMethod("メソッド名", new Class[]{ int.class });
	} catch (SecurityException e) {
		throw new RuntimeException(e);
	} catch (NoSuchMethodException e) {
		throw new RuntimeException(e);
	}

	Object ret; //戻り値
	try {
		ret = method.invoke(object, new Object[]{ new Integer(1) });
		//  = object.メソッド((int)1); と同じ
	} catch (IllegalArgumentException e) {
		throw new RuntimeException(e);
	} catch (IllegalAccessException e) {
		throw new RuntimeException(e);
	} catch (InvocationTargetException e) {
		throw new RuntimeException(e);
	}
すなわち、invoke()の第1引数が有ればそのインスタンスに対して実行、無ければ（nullならば）staticメソッドとして実行する。
第2引数でメソッド自身の引数を指定する。引数が無い場合、空の配列かnullを渡す。引数の扱い方については、コンストラクターの場合と同様。

呼び出したメソッドが返す例外は、invoke()の中でInvocationTargetExceptionに入れられる。

JDK1.5では、インスタンス生成と同様に、メソッドの呼び出しも可変長引数になって便利になった。[2007-11-13]

	public Object メソッド名(int arg1, int arg2) { ～ }
	public Object 引数無しメソッド() { ～ }
	Object ret, ret2;
	try {
		Method m = clazz.getMethod("メソッド名", int.class, int.class);
		ret = m.invoke(object, 123, 456); //自動ボクシングも使用

		Method m2 = clazz.getMethod("引数無しメソッド");
		ret2 = m2.invoke(object);
	} catch (Exception e) {
		throw new RuntimeException(e);
	}
ただし、「引数なし」を意味するnullを指定していた場合は注意。[2008-07-03]

可変長引数ありのメソッド
可変長引数を持つメソッドをgetMethod()で取得したい場合、引数の型には配列を指定する。[2008-02-10]

	// リフレクションで取得したい可変長引数メソッド
	public void メソッド名(クラス... args) { ～ }
		Method m = clazz.getMethod("メソッド名", クラス[].class);

		m.invoke(オブジェクト, new Object[]{ new クラス[]{ 値,値,… }});
//×		m.invoke(オブジェクト, 値,値,…);
invoke()の引数に（配列を使わずに）実引数を並べるような書き方は出来ない。
要するに普通に配列を扱うのと同様にコーディングする。

具体例 [2015-04-26]
可変長引数以外の引数が無い	可変長引数以外の引数が有る
取得したいメソッド	public String example1(String... ss) {
  ～
}	public String example2(String s,	String... ss) {
  ～
}
取得方法	Method m = clazz.getDeclaredMethod("example1", String[].class);	Method m = clazz.getDeclaredMethod("example2", String.class, String[].class);
呼び出し方法
（invokeに配列を渡す）	Object[] args = { new String[]{ "abc", "def" } };
Object r = m.invoke(object, args);	Object[] args = { "123", new String[]{ "abc", "def" } };
Object r = m.invoke(object, args);
呼び出し方法
（invokeの可変長引数を利用）	以下の書き方では実行時に例外発生。
Object r = m.invoke(object, "abc", "def");	以下の書き方では実行時に例外発生。
Object r = m.invoke(object, "123", "abc", "def");
以下の書き方ではコンパイル時に警告、実行時に例外発生。
Object r = m.invoke(object, new String[]{ "abc", "def" });	Object r = m.invoke(object, "123", new String[]{ "abc", "def" });
以下の書き方ならOK。
Object r = m.invoke(object, (Object)new String[]{ "abc", "def" });	Object r = m.invoke(object, (Object)"123", (Object)new String[]{ "abc", "def" });
「可変長引数しか持たないメソッド」を呼び出す際にinvokeの可変長引数を利用した書き方が出来ない理由は、以下のように解釈されるから。[2015-04-26]

例	m.invoke(object, "abc", "def")	m.invoke(object, new String[]{ "abc", "def" })	m.invoke(object, (Object)new String[]{ "abc", "def" })
解釈	1個目の引数の型はString、値は"abc"
2個目の引数の型はString、値は"def"
しかし呼び出したいメソッドの引数は1個のみで、型はString[]
なので一致しない。	invokeの引数の型はObject...であり、実体はObject[]。
Javaの配列は共変なので、String[]はObject[]に代入可能。
したがってm.invoke(object, new Object[]{ "abc", "def" })と解釈される。（ただし警告が出る）
これは左記のm.invoke(object, "abc", "def")と同じ。	String[]をObjectにキャストしているので、
invoke側から見ると、1個の引数という扱い。
要するに、invokeに配列を渡すと、その配列が「invokeの引数Object[]そのもの」なのか「Object[0]に配列を入れた」のか区別が付かない（というか前者として解釈される）のが問題。
なので、呼び出したいメソッドに可変長引数以外の引数が1つでもあれば、「invokeのObject[]」と「呼び出したいメソッドの引数」との区別が付く。

ちなみに、あるメソッドが可変引数を持つかどうかはMethod#isVarArgs()で判断できる。