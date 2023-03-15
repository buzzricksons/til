https://leetcode.com/

## Programming Language
### C++
```
vector<uint64_t> generate_fibonaccis(int n) {
    vector<uint64_t> fib(n);
    fib[0] = 1;
    fib[1] = 1;
    for (int i = 2; i < n; ++i) {
        fib[i] = fib[i - 2] + fib[i - 1];
    }
    return fib;
}

int main() {
    int n = 10;
    vector<uint64_t> fib = generate_fibonaccis(n);
    for (int i = 0; i < n; i++) {
        std::cout << fib[i] << " ";
    }
    return 0;
}
```

### Java
```
public class Main {
    public static long[] generateFibonaccis(int n) {
        long[] fib = new long[n];
        fib[0] = 1;
        fib[1] = 1;
        for (int i = 2; i < n; ++i) {
            fib[i] = fib[i - 2] + fib[i - 1];
        }
        return fib;
    }
    public static void main(String[] args) {
        int n = 10;
        long[] fib = generateFibonaccis(n);
        for (int i = 0; i < n; i++) {
            System.out.print(Long.toUnsignedString(fib[i]) + " ");
        }
    }
}
```

### Python
```
def fib():
    a, b = 1, 1
    while True:
        yield a
        a, b = b, a + b

for index, x in enumerate(fib()):
    if index == 10:
        break
    print("%s" % x),
```

### C
```
void generate_fibonaccis(int n, uint64_t *fib) {
    fib[0] = 1;
    fib[1] = 1;
    for (int i = 2; i < n; ++i) {
        fib[i] = fib[i - 2] + fib[i - 1];
    }
}

int main() {
    int n = 10;
    uint64_t fib[1000];
    generate_fibonaccis(n, fib);
    for (int i = 0; i < n; i++) {
        printf("%ju ", fib[i]);
    }
    return 0;
}
```

### C`#`
```
class HelloWorld {
    static ulong[] generateFibonaccis(int n) {
        ulong[] fib = new ulong[n];
        fib[0] = 1;
        fib[1] = 1;
        for (int i = 2; i < n; ++i) {
            fib[i] = fib[i - 2] + fib[i - 1];
        }
        return fib;
    }
    static void Main() {
        int n = 10;
        ulong[] fib = generateFibonaccis(n);
        for (int i = 0; i < n; i++) {
            System.Console.Write(fib[i] + " ");
        }
    }
}
```

### JavaScript
```
function generateFibonaccis(n) {
    var fib = [1, 1];
    for (var i = 2; i < n; i++) {
        fib[i] = fib[i - 2]+ fib[i - 1];
    }
    return fib;
}
var fib = generateFibonaccis(10);
console.log(fib.join(" "));
```

### Ruby
```
def generate_fibonaccis(n)
    fib = [1, 1]
    (2...n).each do |i|
        fib[i] = fib[i - 1] + fib[i - 2]
    end
    fib
end

fib = generate_fibonaccis(10)
puts fib.join(" ")
```

### Swift
```
func generateFibonaccis(_ n: Int) -> [Int] {
    var fib = Array(repeating: 1, count: n)
    for i in 2..<n {
        fib[i] = fib[i - 2] + fib[i - 1]
    }
    return fib
}

var fib = generateFibonaccis(10)
print(fib.map({"\($0)"}).joined(separator: " "))
```

### Go
```
package main

import "fmt"

// fib returns a function that returns
// successive Fibonacci numbers.
func generate_fibonaccis() func() uint64 {
    a, b := uint64(0), uint64(1)
	return func() uint64 {
		a, b = b, a+b
		return a
	}
}

func main() {
    fib := generate_fibonaccis()
	for j := 0; j < 10; j++ {
	    fmt.Printf("%v ", fib())
	}
}
```

## Result
```txt
C++
1 1 2 3 5 8 13 21 34 55 
Finished in 2 ms



Java
1 1 2 3 5 8 13 21 34 55 
Finished in 91 ms



Python
1 1 2 3 5 8 13 21 34 55
Finished in 34 ms



C
1 1 2 3 5 8 13 21 34 55 
Finished in 3 ms



C#
1 1 2 3 5 8 13 21 34 55 
Finished in 60 ms



JavaScript
1 1 2 3 5 8 13 21 34 55
Finished in 102 ms



Ruby
1 1 2 3 5 8 13 21 34 55
Finished in 83 ms



Swift
1 1 2 3 5 8 13 21 34 55
Finished in 34 ms



Go
1 1 2 3 5 8 13 21 34 55
Finished in 1 ms
```