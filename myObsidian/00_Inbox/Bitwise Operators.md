字节OA 的面试题， 答案BCD
![](https://raw.githubusercontent.com/PANhuihuihuihui/PicBed/main/202210051930318.png)

1.  The **& (bitwise AND)** in C or C++ takes two numbers as operands and does AND on every bit of two numbers. The result of AND is 1 only if both bits are 1.  
2.  The **| (bitwise OR)** in C or C++ takes two numbers as operands and does OR on every bit of two numbers. The result of OR is 1 if any of the two bits is 1. 
3.  The **^ (bitwise XOR)** in C or C++ takes two numbers as operands and does XOR on every bit of two numbers. The result of XOR is 1 if the two bits are different. 
4.  The **<< (left shift)** in C or C++ takes two numbers, left shifts the bits of the first operand, the second operand decides the number of places to shift. 
5.  The **>> (right shift)** in C or C++ takes two numbers, right shifts the bits of the first operand, the second operand decides the number of places to shift. 
6.  The **~ (bitwise NOT)** in C or C++ takes one number and inverts all bits of it.

```java
    public static boolean transformArray(int[] a,int[] b) {
        // use TreeSet to slove
        Arrays.sort(a);
        Arrays.sort(b);
        for (int i = 0; i < b.length; i++) {
            if (a[i]!=b[i] && a[i]+1 != b[i]){
                return false;
            }
        }
        return true;

    }
    public static void main(String[] args) {
        int[] a = {4,2,3,4,10};
        int[] b = {1,2,3,4,5};
        System.out.println(transformArray(a,b));
    
    }
```

