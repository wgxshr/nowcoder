# nowcoder
2022刷题总结

## 华为机试题

#### 1. 字符串最后一个单词的长度

   ######   输入描述:

   ```
   输入一行，代表要计算的字符串，非空，长度小于5000。
   ```

   ###### 输出描述:

   ```
   输出一个整数，表示输入字符串最后一个单词的长度。
   ```

   示例1

   ###### 输入

   ```
   hello nowcoder
   ```

   ###### 输出

   ```
   8
   ```

###### 思路

> 先使用trim将左右空格删除，遍历字符串，遇到空格的时候将结果置0，否则结果加1。

```
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String str = sc.nextLine();
        str = str.trim();
        System.out.println(Solution(str));
    }
    
    public static int Solution(String str) {
        if(str == null || str.length() == 0) {
            return 0;
        }
        int ans = 0;
        for(int i = 0; i < str.length(); ++i) {
            if(str.charAt(i) == ' ') {
                ans = 0;
            } else {
                ++ans;
            }
        }
        return ans;
    }
}
```

#### 2.计算某字母出现的次数

###### 输入描述:

```
第一行输入一个由字母和数字以及空格组成的字符串，第二行输入一个字母。
```

###### 输出描述:

```
输出输入字符串中含有该字符的个数。
```

示例1

###### 输入

```
ABCabc
A
```

###### 输出

```
2
```

> 先将输入的字符c转为小写，遍历字符串，将每个字符串转为小写，和c相等则结果加一

```
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String str = sc.nextLine();
        char c = sc.nextLine().charAt(0);
        System.out.println(solution(str, c));
    }

    public static int solution(String str, char c) {
        int ans = 0;
        c = Character.toLowerCase(c);
        for(int i = 0; i < str.length(); ++i) {
            if(Character.toLowerCase(str.charAt(i)) == c) {
                ++ans;
            }
        }
        return ans;
    }
}
```

#### 3.明明的随机数

###### 输入描述:

```
注意：输入可能有多组数据(用于不同的调查)。每组数据都包括多行，第一行先输入随机整数的个数N，接下来的N行再输入相应个数的整数。具体格式请看下面的"示例"。
```

######## 输出描述:

```
返回多行，处理后的结果
```

示例1

###### 输入

[复制](javascript:void(0);)

```
3
2
2
1
11
10
20
40
32
67
40
20
89
300
400
15
```

###### 输出

[复制](javascript:void(0);)

```
1
2
10
15
20
32
40
67
89
300
400
```

###### 说明

```
样例输入解释：
样例有两组测试
第一组是3个数字，分别是：2，2，1。
第二组是11个数字，分别是：10，20，40，32，67，40，20，89，300，400，15。  
```
> 本题主要考察对scanner函数的熟练程度，题目要求结果有序且无重复，可以将每一个输入放到TreeSet中，读完输入后，直接顺序打印set即可

```
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while(sc.hasNext()) {
            TreeSet<Integer> set = new TreeSet<>(); 
            int n = sc.nextInt();
            int[] arr = new int[n];
            if(n > 0) {
                for(int i = 0; i < n; ++i) {
                    set.add(sc.nextInt());
                }
            }
            for(Integer i : set) {
                System.out.println(i);
            }
        }
    }
}
```

#### 4.字符串分割

###### 输入描述:

```
连续输入字符串(输入多次,每个字符串长度小于100)
```

###### 输出描述:

```
输出到长度为8的新字符串数组
```

示例1

###### 输入

```
abc
123456789
```

###### 输出

```
abc00000
12345678
90000000
```
> 先将长度不能被8整除的字符串补”00000000“，然后当字符串长度大于8时，每次将字符串的前8个加入到结果中，然后取字符串从第九个字符开始的子串

```
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while(sc.hasNext()) {
            String s = sc.nextLine();
            if(s.length() % 8 != 0) {
                s = s + "00000000";
            }
            while(s.length() >= 8) {
                System.out.println(s.substring(0, 8));
                s = s.substring(8);
            }
        }
    }
}
```