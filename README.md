# nowcoder
2022刷题总结

## 华为机试题

#### 1. 题目描述

   计算字符串最后一个单词的长度，单词以空格隔开。

   ####   输入描述:

   ```
   输入一行，代表要计算的字符串，非空，长度小于5000。
   ```

   #### 输出描述:

   ```
   输出一个整数，表示输入字符串最后一个单词的长度。
   ```

   示例1

   #### 输入

   ```
   hello nowcoder
   ```

   #### 输出

   ```
   8
   ```

#### 思路

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

