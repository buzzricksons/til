
# I/O
### 標準入力
```Text
     int ch = System.in.read();
     System.out.print(ch);
```

### Buffer入力
```Text
     
     BufferedReader in= new BufferedReader(new InputStreamReader(System.in));
     int x = Integer.parseInt(in.readLine());
     System.out.println(x);
```

### スキャン入力
```Text
     Scanner scan = new Scanner(System.in); 
     int x = scan.nextInt();
     System.out.println(x);
```

# Thread
### 実現方法
- java.lang.Runnableをimplementする
- java.lang.Threadクラスを継承する

### Thread継承 vs Runnableのimplement
Runnableをimplementするのが良い場合がある。
- Javaは多重継承ができないためThreadクラスを継承すると他のクラスを継承することができない。だがRunnableをimplementする場合は他のクラスを継承することができる。
- Threadクラスを継承するのが負担感がある場合(Threadの全てを継承するため)はRunnableをimplementするほうが良い。

### Deadlock
下記の４つのことを全部満たす必要がある
1. `Mutual exclusion`: 一回に一つのプロセスのみ共有リソースを使用することができる。
2. `Hold and wait`: 共有リソースにアプローチできる権限を持っているプロセスがその権限を譲らない上で他のリソースに対するアプローチ権限を要求することができる。
3. `Preemption`: 一つのプロセスが他のプロセスのリソースアプローチ権限をキャンセルさせることができない。
4. `Circular wait`: ２つ以上のプロセスが他のプロセスからのリソースアプローチ権限を開放することを待っている。その間にcycleが存在する。

Deadlockを防ぐためには上記の中で一つを無くすべき。

# StringBuffer
全ての文字列の配列を作っておき、文字列オブジェクトへのコピーは必要な時だけ実行する。
```Text
String sentence = "";
for (String s : words) {
    sentence = sentence + w;
}
return sentence;

↓

StringBuffer sentence = new StringBuffer();
for (String s : words) {
    sentence.append(s);
}
return sentence.toString();
```

# java.lang.System.arraycopy() method
http://www.geeksforgeeks.org/java-lang-system-arraycopy-method/

java.lang.System class provides useful methods for standard input and output, for loading files and  
libraries or to access externally defined properties. The java.lang.System.arraycopy() method copies  
a source array from a specific beginning position to the destination array from the mentioned position.  
No. of arguments to be copied are decided by len argument.  
The components at source_Position to `source_Position + length – 1` are copied to destination array from destination_Position to `destination_Position + length – 1`

### Class Declaration
```
public final class System
   extends Object
```
![](https://lh3.google.com/u/1/d/0B2Yxg0Epe-6_MjJLdXBJZ3ZHdzA=w1920-h950-iv1)

### Syntax
```Text
public static void arraycopy(Object source_arr, int sourcePos,
                            Object dest_arr, int destPos, int len)

Parameters : 
source_arr : array to be copied from
sourcePos : starting position in source array from where to copy
dest_arr : array to be copied in
destPos : starting position in destination array, where to copy in
len : total no. of components to be copied.
```

### implementation
```Text
// Java program explaining System class method - arraycopy()
import java.lang.*;
public class NewClass
{
    public static void main(String[] args)
    {
        int s[] = { 10, 20, 30, 40, 50, 60, 70, 80, 90, 100};
        int d[] = { 15, 25, 35, 45, 55, 65, 75, 85, 95, 105};
 
        int source_arr[], sourcePos, dest_arr[], destPos, len;
        source_arr = s;
        sourcePos = 3;
        dest_arr = d;
        destPos = 5;
        len = 4;
 
        // Print elements of source
        System.out.print("source_array : ");
        for (int i = 0; i < s.length; i++)
            System.out.print(s[i] + " ");
        System.out.println("");
 
        System.out.println("sourcePos : " + sourcePos);
        
        // Print elements of source
        System.out.print("dest_array : ");
        for (int i = 0; i < d.length; i++)
            System.out.print(d[i] + " ");
        System.out.println("");
        
        System.out.println("destPos : " + destPos);
        
        System.out.println("len : " + len);
        
        // Use of arraycopy() method
        System.arraycopy(source_arr, sourcePos, dest_arr, 
                                            destPos, len);
        
        // Print elements of destination after
        System.out.print("final dest_array : ");
        for (int i = 0; i < d.length; i++)
            System.out.print(d[i] + " ");
    }
} 
```

### Output
```
source_array : 10 20 30 40 50 60 70 80 90 100 
sourcePos : 3
dest_array : 15 25 35 45 55 65 75 85 95 105 
destPos : 5
len : 4
final dest_array : 15 25 35 45 55 40 50 60 70 105 
```
