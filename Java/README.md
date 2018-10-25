
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
### Performance when Concatenating Two Individual Strings (higher is better)
![](https://github.com/buzzricksons/til/blob/master/_Image/Java/string_join_result_1.png)

### Performance when Concatenating Ten Individual Strings (higher is better)
![](https://github.com/buzzricksons/til/blob/master/_Image/Java/string_join_result_2.png)

### Performance when Concatenating a List of 100 Strings (higher is better)
![](https://github.com/buzzricksons/til/blob/master/_Image/Java/string_join_result_3.png)

# Singleton
- https://medium.com/exploring-code/digesting-singleton-design-pattern-in-java-5d434f4f322

## Pattern
### Default (not thread safe)
#### example
```Java
/**
 * Basic pattern. (not thread safe)
 */
public class Singleton00 {
    private static Singleton00 singleton;
    private Singleton00() {
    }
    public static Singleton00 getInstance() {
        if (singleton == null) {
            singleton = new Singleton00();
        }
        return singleton;
    }

    public static void main(String[] args) throws ExecutionException, InterruptedException {
        singletonThreadSafeTest();
    }

    public static void singletonThreadSafeTest() throws ExecutionException, InterruptedException {
        Callable<Singleton00> c = new Callable<Singleton00>() {
            @Override
            public Singleton00 call() throws Exception {
                return Singleton00.getInstance();
            }
        };
        ExecutorService ex = Executors.newFixedThreadPool(2);
        for(;;) {
            Future<Singleton00> f1 = ex.submit(c);
            Future<Singleton00> f2 = ex.submit(c);
            if (f1.get() != f2.get()) {
                System.out.println("Not Singleton instance.[instance1: "+f1.get().hashCode()+"],[instance1: "+f2.get().hashCode()+"]");
            } else {
//                System.out.println("Singleton instance.[instance1: "+f1.get().hashCode()+"],[instance1: "+f2.get().hashCode()+"]");
            }
            singleton = null;//reset
        }
    }
}
```

### Enum Singleton (thread safe and lazy)
```Java
public enum SingletonEnum {
    INSTANCE;
    int value;
    public int getValue() {
        return value;
    }
    public void setValue(int value) {
        this.value = value;
    }
}



public class EnumDemo {
    public static void main(String[] args) {
        SingletonEnum singleton = SingletonEnum.INSTANCE;
        System.out.println(singleton.getValue());
        singleton.setValue(2);
        System.out.println(singleton.getValue());
    }
}
```

#### example
```Java
/**
 * Enum pattern.(thread safe and lazy)
 */
public class Singleton01 {
    public static void main(String[] args) throws ExecutionException, InterruptedException {
        threadTest();//        RESULT↓
//        Here → Because of lazy.
//        Instance 1 hash: 807683689
//        Instance 2 hash: 807683689


    }
    public enum MySingleton {
        INSTANCE;
        private MySingleton() {
            System.out.println("Here");
        }
    }


    public static void threadTest() {
        //Thread 1
        Thread t1 = new Thread(new Runnable() {
            @Override
            public void run() {
                MySingleton instance1 = MySingleton.INSTANCE;
                System.out.println("Instance 1 hash: " + instance1.hashCode());
            }
        });

        //Thread 2
        Thread t2 = new Thread(new Runnable() {
            @Override
            public void run() {
                MySingleton instance2 = MySingleton.INSTANCE;
                System.out.println("Instance 2 hash: " + instance2.hashCode());
            }
        });

        //start both the threads
        t1.start();
        t2.start();
    }
}
```

### Bill Pugh Singleton(thread safe and lazy)
```Java
public class Logger {
	private Logger() {
		// private constructor
	}
        
        // static inner class - inner classes are not loaded until they are
        // referenced.
	private static class LoggerHolder {
		private static Logger logger = new Logger();
	}
        // global access point
	public static Logger getInstance() {
		return LoggerHolder.logger;
	}
 
	//Other methods
}
```
When the singleton class is loaded, inner class is not loaded and hence doesn’t create object when loading the class. Inner class is created only when getInstance() method is called. So it may seem like eager initialization but it is lazy initialization.
This is the most widely used approach as it doesn’t use synchronization.

#### example
```Java
/**
 * Bill Pugh Singleton pattern(thread safe and lazy)
 */
public class Singleton02 {
    private Singleton02() {
        System.out.println("Here");
    }

    // static inner class - inner classes are not loaded until they are referenced.
    private static class Singleton03Holder {
        private static Singleton02 logger = new Singleton02();
    }
    // global access point
    public static Singleton02 getInstance() {
        return Singleton03Holder.logger;
    }



    public static void main(String[] args) throws ExecutionException, InterruptedException {
        Singleton02 instance1 = Singleton02.getInstance();
        Singleton02 instance2 = Singleton02.getInstance();
        System.out.println("instance1 hash: "+instance1.hashCode());
        System.out.println("instance2 hash: "+instance2.hashCode());// RESULT ↓
//        Here → Because of lazy
//        instance1 hash: 401424608
//        instance2 hash: 401424608


//        singletonThreadSafeTest();
    }

    public static void singletonThreadSafeTest() throws ExecutionException, InterruptedException {
        Callable<Singleton02> c = new Callable<Singleton02>() {
            @Override
            public Singleton02 call() throws Exception {
                return Singleton02.getInstance();
            }
        };
        ExecutorService ex = Executors.newFixedThreadPool(2);
        for(;;) {
            Future<Singleton02> f1 = ex.submit(c);
            Future<Singleton02> f2 = ex.submit(c);
            if (f1.get() != f2.get()) {
                System.out.println("Not Singleton instance.[instance1: "+f1.get().hashCode()+"],[instance1: "+f2.get().hashCode()+"]");
            } else {
//                System.out.println("Singleton instance.[instance1: "+f1.get().hashCode()+"],[instance1: "+f2.get().hashCode()+"]");
            }
            Singleton03Holder.logger = null;//reset
        }
    }

}
```

#### ※Reflectionを使う場合は問題あり
```Java
public class LoggerReflection {

    public static void main(String[] args) {
        Logger instance1 = Logger.getInstance();
        Logger instance2 = null;
        try {
            Constructor[] cstr 
             = Logger.class.getDeclaredConstructors();
            for (Constructor constructor : cstr) {
               //Setting constructor accessible
                constructor.setAccessible(true);
                instance2 
                   = (Logger) constructor.newInstance();
                break;
            }
        } catch (Exception e) {
             System.out.println(e);
        }
        System.out.println(instance1.hashCode());
        System.out.println(instance2.hashCode());
        //hashcodeが異なる
    }
```

## Thread safe test
```Java
    public static void singletonThreadSafeTest() throws ExecutionException, InterruptedException {
        Callable<Singleton00> c = new Callable<Singleton00>() {
            @Override
            public Singleton00 call() throws Exception {
                return Singleton00.getInstance();
            }
        };
        ExecutorService ex = Executors.newFixedThreadPool(2);
        for(;;) {
            Future<Singleton00> f1 = ex.submit(c);
            Future<Singleton00> f2 = ex.submit(c);
            if (f1.get() != f2.get()) {
                System.out.println("Not Singleton instance.[instance1: "+f1.get().hashCode()+"],[instance1: "+f2.get().hashCode()+"]");
            } else {
//                System.out.println("Singleton instance.[instance1: "+f1.get().hashCode()+"],[instance1: "+f2.get().hashCode()+"]");
            }
            singleton = null;//reset
        }
    }
```
