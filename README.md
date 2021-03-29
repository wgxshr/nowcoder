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

