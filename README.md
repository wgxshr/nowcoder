# nowcoder
2022刷题总结

## 华为机试题

#### 1. 计算字符串最后一个单词的长度，单词以空格隔开。

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

#### 2.写出一个程序，接受一个由字母、数字和空格组成的字符串，和一个字母，然后输出输入字符串中该字母的出现次数。不区分大小写。

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

#### 3.明明想在学校中请一些同学一起做一项问卷调查，为了实验的客观性，他先用计算机生成了N个1到1000之间的随机整数（N≤1000），对于其中重复的数字，只保留一个，把其余相同的数去掉，不同的数对应着不同的学生的学号。然后再把这些数从小到大排序，按照排好的顺序去找同学做调查。请你协助明明完成“去重”与“排序”的工作(同一个测试用例里可能会有多组数据(用于不同的调查)，希望大家能正确处理)。


注：测试用例保证输入参数的正确性，答题者无需验证。测试用例不止一组。

当没有新的输入时，说明输入结束。

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