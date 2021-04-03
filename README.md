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

#### 5.进制转换

###### 输入描述:

```
输入一个十六进制的数值字符串。
```

###### 输出描述:

```
输出该数值的十进制字符串。不同组的测试用例用\n隔开。
```

示例1

###### 输入

```
0xA
0xAA
```

###### 输出

```
10
170
```

```
import java.util.*;
import java.io.*;
 
public class Main{
    public static void main(String[] args) throws IOException{
        BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
        String input;
        while((input = bf.readLine())!=null){
            String temp = input.substring(2,input.length());
            int sum = 0;
            int length = temp.length();
            for(int i= length-1;i>=0;i--){
                char c = temp.charAt(i);
                int tempNum = (int)c;
                if(tempNum>=65){
                    tempNum = tempNum - 65 + 10;
                }else{
                    tempNum = tempNum - 48;
                }
                sum = sum + (int) Math.pow(16, length-i-1)*tempNum;
            }
            System.out.println(sum);
        }
    }
}
```

#### 6.合并表记录

###### 输入描述:

```
先输入键值对的个数
然后输入成对的index和value值，以空格隔开
```

###### 输出描述:

```
输出合并后的键值对（多行）
```

示例1

###### 输入

```
4
0 1
0 2
1 2
3 4
```

###### 输出

```
0 3
1 2
3 4
```
```
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        sc.nextLine();
        Map<Integer, Integer> map = new TreeMap<>();
        for(int i = 0; i < N; ++i) {
            String[] str = sc.nextLine().split(" ");
            int key = Integer.parseInt(str[0]);
            int val = Integer.parseInt(str[1]);
            map.put(key, map.getOrDefault(key, 0) + val);
        }
        for(int key : map.keySet()) {
            System.out.println(key + " " + map.get(key));
        }
    }
}
```

#### 7.提取不重复的整数

###### 输入描述:

```
输入一个int型整数
```

###### 输出描述:

```
按照从右向左的阅读顺序，返回一个不含重复数字的新的整数
```

示例1

###### 输入

```
9876673
```

###### 输出

```
37689
```
```
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        long num = sc.nextLong();
        long ans = 0;
        Set<Long> set = new HashSet<>();
        while(num != 0) {
            long i = num % 10;
            if(set.contains(i)) {
                num /= 10;
                continue;
            }
            set.add(i);
            ans = ans * 10 + i;
            num /= 10;
        }
        System.out.println(ans);
    }
}
```

#### 8.字符个数统计

###### 输入描述:

```
输入一行没有空格的字符串。
```

###### 输出描述:

```
输出范围在(0~127)字符的个数。
```

示例1

###### 输入
```
abc
```

###### 输出

```
3
```
````
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String str = sc.nextLine();
        Set<Character> set = new HashSet<>();
        int ans = 0;
        for(char c : str.toCharArray()) {
            if(c >= 0 && c <= 127 && !set.contains(c)) {
                ++ans;
            }
            set.add(c);
        }
        System.out.println(ans);
    }
}
````

#### 9.数字颠倒

###### 输入描述:

```
输入一个int整数
```

###### 输出描述:

```
将这个整数以字符串的形式逆序输出
```

示例1

###### 输入


```
1516000
```

###### 输出

```
0006151
```

```
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int num = sc.nextInt();
        System.out.println(reverse(num));
    }
    
    private static String reverse(int num) {
        StringBuilder sb = new StringBuilder();
        while(num != 0) {
            sb.append(num % 10 + "");
            num /= 10;
        }
        return sb.toString();
    }
}
```

#### 10.句子逆转

###### 输入描述:

```
输入一个英文语句，每个单词用空格隔开。保证输入只包含空格和字母。
```

###### 输出描述:

```
得到逆序的句子
```

示例1

###### 输入

```
I am a boy
```

###### 输出

```
boy a am I
```
> 先使用trim取出字符串前后的字符串，遍历字符串，如果为空格，则将空格之前的子串加入到栈中，不为空格则将字符追加到子串后面，最后将栈中的字符串加入到结果中


````
import java.util.*;

public class Solution7 {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        String str = sc.nextLine();
        System.out.println(reverse(str));
    }

    private static String reverse(String str) {
        str = str.trim();
        StringBuilder ans = new StringBuilder();
        StringBuilder sb = new StringBuilder();
        Stack<String> stack = new Stack<>();
        for(int i = 0; i < str.length(); ++i) {
            if(str.charAt(i) == ' ') {
                stack.add(sb.toString());
                sb = new StringBuilder();
            } else {
                sb.append(str.charAt(i));
            }
        }
        stack.add(sb.toString());
        while(!stack.isEmpty()) {
            ans.append(" ").append(stack.pop());
        }
        return ans.substring(1, ans.length());
    }
}
````

#### 11.int型整数转为二进制后1的个数

###### 输入描述:

```
 输入一个整数（int类型）
```

###### 输出描述:

```
 这个数转换成2进制后，输出1的个数
```

示例1

###### 输入

```
5
```

###### 输出

```
2
```

```
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int num = sc.nextInt();
        int ans = 0;
        while(num != 0) {
            ++ans;
            num &= (num - 1);
        }
        System.out.println(ans);
    }
}
```

#### 12.坐标移动

###### 输入描述:

```
一行字符串
```

###### 输出描述:

```
最终坐标，以逗号分隔
```

示例1

###### 输入

```
A10;S20;W10;D30;X;A1A;B10A11;;A10;
```

###### 输出

```
10,-10
```

```
import java.util.*;
public class Main {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        while(sc.hasNext()) {
            String str = sc.nextLine();
            String[] strs = str.split(";");
            int x = 0, y = 0;
            for(String s : strs) {
                if(s.length() > 1) {
                    if(s.charAt(0) == 'D' && s.substring(1).matches("[0-9]+")) {
                    x += Integer.parseInt(s.substring(1));
                    }
                    if(s.charAt(0) == 'W' && s.substring(1).matches("[0-9]+")) {
                        y += Integer.parseInt(s.substring(1));
                    }
                    if(s.charAt(0) == 'S' && s.substring(1).matches("[0-9]+")) {
                        y -= Integer.parseInt(s.substring(1));
                    }
                    if(s.charAt(0) == 'A' && s.substring(1).matches("[0-9]+")) {
                        x -= Integer.parseInt(s.substring(1));
                    }
                }
            }
            System.out.println(x + "," + y);
        }
    }
}
```

## 剑指offer
#### 栈的压入、弹出系列

###### 题目描述

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

示例1

###### 输入

```
[1,2,3,4,5],[4,3,5,1,2]
```

###### 返回值

```
false
```

```
import java.util.*;

public class Solution {
    public boolean IsPopOrder(int [] pushA,int [] popA) {
        Stack<Integer> stack = new Stack<>();
        int index = 0;
        for(int i = 0; i < pushA.length; ++i) {
            while(!stack.isEmpty() && stack.peek() == popA[index]) {
                ++index;
                stack.pop();
            }
            stack.push(pushA[i]);
        }
        while(!stack.isEmpty() && stack.peek() == popA[index]) {
            ++index;
            stack.pop();
        }
        return index == popA.length;
    }
}
```

#### 二维数组的查找

## 题目描述

在一个二维数组中（每个一维数组的长度相同），每一行都按照从左到右递增的顺序排序，每一列都按照从上到下递增的顺序排序。请完成一个函数，输入这样的一个二维数组和一个整数，判断数组中是否含有该整数。

[

 [1,2,8,9],
 [2,4,9,12],
 [4,7,10,13],
 [6,8,11,15]

]

给定 target = 7，返回 true。

给定 target = 3，返回 false。


示例1

###### 输入

```
7,[[1,2,8,9],[2,4,9,12],[4,7,10,13],[6,8,11,15]]
```

###### 返回值

```
true
```

###### 说明

```
存在7，返回true
```

示例2

###### 输入

```
3,[[1,2,8,9],[2,4,9,12],[4,7,10,13],[6,8,11,15]]
```

###### 返回值

```
false
```

###### 说明

```
不存在3，返回false
```

```
public class Solution {
    public boolean Find(int target, int [][] array) {
        if(array == null || array.length == 0 || array[0].length == 0) {
            return false;
        }
        int right = array[0].length - 1, top = 0;
        while(right >= 0 && top < array.length) {
            int num = array[top][right];
            if(num == target) {
                return true;
            }
            if(num > target) {
                --right;
            } else {
                ++top;
            }
        }
        return false;
    }
}
```

#### 替换空格

###### 题目描述

请实现一个函数，将一个字符串中的每个空格替换成“%20”。例如，当字符串为We Are Happy.则经过替换之后的字符串为We%20Are%20Happy。

示例1

###### 输入

```
"We Are Happy"
```

###### 返回值

```
"We%20Are%20Happy"
```

```
import java.util.*;


public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param s string字符串 
     * @return string字符串
     */
    public String replaceSpace (String s) {
        // write code here
        if(s == null || s.length() == 0) {
            return s;
        }
        int len = s.length();
        for(int i = 0; i < s.length(); ++i) {
            if(s.charAt(i) == ' ') {
                len += 2;
            }
        }
        char[] arr = new char[len];
        --len;
        for(int i = s.length() - 1; i >= 0; --i) {
            if(s.charAt(i) == ' ') {
                arr[len--] = '0';
                arr[len--] = '2';
                arr[len--] = '%';
            } else {
                arr[len--] = s.charAt(i);
            }
        }
        return new String(arr);
    }
}
```

#### 从尾到头打印链表

###### 题目描述

输入一个链表，按链表从尾到头的顺序返回一个ArrayList。

示例1

###### 输入

```
{67,0,24,58}
```

###### 返回值

```
[58,24,0,67]
```

```
/**
*    public class ListNode {
*        int val;
*        ListNode next = null;
*
*        ListNode(int val) {
*            this.val = val;
*        }
*    }
*
*/
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> printListFromTailToHead(ListNode listNode) {
        ArrayList<Integer> ans = new ArrayList<>();
        dfs(listNode, ans);
        return ans;
    }
    
    private void dfs(ListNode listNode, ArrayList<Integer> ans) {
        if(listNode == null) {
            return ;
        }
        dfs(listNode.next, ans);
        ans.add(listNode.val);
    }
}
```

#### 重建二叉树

###### 题目描述

输入某二叉树的前序遍历和中序遍历的结果，请重建出该二叉树。假设输入的前序遍历和中序遍历的结果中都不含重复的数字。例如输入前序遍历序列{1,2,4,7,3,5,6,8}和中序遍历序列{4,7,2,1,5,3,8,6}，则重建二叉树并返回。

示例1

###### 输入

```
[1,2,3,4,5,6,7],[3,2,4,1,6,5,7]
```

###### 返回值

```
{1,2,5,3,4,6,7}
```

```
/**
 * Definition for binary tree
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
public class Solution {
    public TreeNode reConstructBinaryTree(int [] pre,int [] in) {
        if(pre == null || in == null || pre.length != in.length) {
            return null;
        }
        int len = pre.length;
        return buildTree(pre, 0, len - 1, in, 0, len - 1);
    }
    
    private TreeNode buildTree(int[] pre, int pleft, int pright, 
                              int[] in, int ileft, int iright) {
        if(pleft > pright) {
            return null;
        }
        int val = pre[pleft];
        TreeNode root = new TreeNode(val);
        int index = 0;
        while(ileft + index <= iright && in[ileft + index] != val) {
            ++index;
        }
        root.left = buildTree(pre, pleft + 1, pleft + index,
                             in, ileft, ileft + index - 1);
        root.right = buildTree(pre, pleft + index + 1, pright, 
                              in, ileft + index + 1, iright);
        return root;
    }
}
```

#### 用两个栈实现队列

###### 题目描述

用两个栈来实现一个队列，完成队列的Push和Pop操作。 队列中的元素为int类型。

```
import java.util.Stack;

public class Solution {
    Stack<Integer> stack1 = new Stack<Integer>();
    Stack<Integer> stack2 = new Stack<Integer>();
    
    public void push(int node) {
        stack1.push(node);
    }
    
    public int pop() {
        if(stack2.isEmpty()) {
            if(stack1.isEmpty()) {
                return -1;
            } else {
                while(!stack1.isEmpty()) {
                    stack2.push(stack1.pop());
                }
            }
        }
        return stack2.pop();
    }
}
```

#### 旋转数组最小的数字

###### 题目描述

把一个数组最开始的若干个元素搬到数组的末尾，我们称之为数组的旋转。
输入一个非递减排序的数组的一个旋转，输出旋转数组的最小元素。
NOTE：给出的所有元素都大于0，若数组大小为0，请返回0。

示例1

###### 输入

```
[3,4,5,1,2]
```

###### 返回值

```
1
```

```
import java.util.ArrayList;
public class Solution {
    public int minNumberInRotateArray(int [] array) {
        if(array == null || array.length == 0) {
            return 0;
        }
        int left = 0, right = array.length - 1;
        while(left <= right) {
            int mid = (left + right) >> 1;
            if(array[mid] > array[right]) {
                left = mid;
            } else {
                right = mid;
            }
            if(left + 1 == right) {
                return array[right];
            }
        }
        return 0;
    }
}
```

#### 斐波那契数列

###### 题目描述

大家都知道斐波那契数列，现在要求输入一个整数n，请你输出斐波那契数列的第n项（从0开始，第0项为0，第1项是1）。

n <= 39

示例1

###### 输入

```
4
```

###### 返回值

```
3
```

```
public class Solution {
    public int Fibonacci(int n) {
        if(n <= 0) {
            return 0;
        }
        if(n == 1) {
            return 1;
        }
        int p = 0, q = 1;
        int tmp = 0;
        for(int i = 1; i <= n; ++i) {
            tmp = p + q;
            q = p;
            p = tmp;
        }
        return p;
    }
}
```

#### 跳台阶扩展问题

###### 题目描述

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶总共有多少种跳法。

示例1

###### 输入

```
3
```

###### 返回值

```
4
```

> f(n) = f(n - 1) + f(n - 2) + f(n - 3) + ... + f(2) + f(1),
>
> f(n - 1) = f(n - 2) + f(n - 3) + ... + f(2) + f(1)
>
> ==> f(n) = 2 * f(n - 1)
>
> ​		f(1) = 1
>
> ==> f(n) = (int)Math.pow(2, n - 1);

```
import java.util.*;
public class Solution {
    public int jumpFloorII(int target) {
        if(target <= 1) {
            return target;
        }
        return (int)Math.pow(2, target - 1);
    }
}
```

#### 矩阵覆盖

###### 题目描述

我们可以用2*1的小矩形横着或者竖着去覆盖更大的矩形。请问用n个2*1的小矩形无重叠地覆盖一个2*n的大矩形，总共有多少种方法？

比如n=3时，2*3的矩形块有3种覆盖方法：

![img](https://uploadfiles.nowcoder.com/images/20201028/59_1603852524038_7FBC41C976CACE07CB222C3B890A0995)

示例1

###### 输入

```
4
```

###### 返回值

```
5
```

```
public class Solution {
    public int rectCover(int target) {
        if(target <= 2) {
            return target;
        }
        int[] memo = new int[target + 1];
        memo[1] = 1;
        memo[2] = 2;
        dfs(target, memo);
        return memo[target];
    }
    
    private int dfs(int target, int[] memo) {
        if(target > memo.length) {
            return 0;
        }
        if(memo[target] != 0) {
            return memo[target];
        }
        memo[target] = dfs(target - 1, memo) + dfs(target - 2, memo);
        return memo[target];
    }
}
```

#### 数值的整数次方

###### 题目描述

给定一个double类型的浮点数base和int类型的整数exponent。求base的exponent次方。

保证base和exponent不同时为0

示例1

###### 输入

```
2,3
```

###### 返回值

```
8.00000
```

```
public class Solution {
    public double Power(double base, int exponent) {
        double ans = 1.0;
        int k;
        if(exponent < 0) {
            k = -exponent;
        } else if(exponent > 0) {
            k = exponent;
        } else {
            if(base == 0) {
                throw new RuntimeException("除数不能为0");
            } else {
                return 1.0;
            }
        }
        while(k != 0) {
            if(k % 2 == 1) {
                ans *= base;
            }
            base *= base;
            k >>= 1;
        }
        return exponent < 0 ? 1 / ans : ans;
    }
}
```

#### 调整数组顺序使奇数位于偶数前面

###### 题目描述

输入一个整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前半部分，所有的偶数位于数组的后半部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

示例1

###### 输入

```
[1,2,3,4]
```

###### 返回值

```
[1,3,2,4]
```

```
import java.util.*;


public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param array int整型一维数组 
     * @return int整型一维数组
     */
    public int[] reOrderArray (int[] array) {
        // write code here
        if(array == null || array.length < 2) {
            return array;
        }
        int left = 0, right = 0;
        while(right < array.length) {
            if(array[right] % 2 != 0) {
                for(int i = right; i > left; --i) {
                    int tmp = array[i];
                    array[i] = array[i - 1];
                    array[i - 1] = tmp;
                }
                ++left;
            }
            ++right;
        }
        return array;
    }
}
```

#### 链表的倒数第k个节点

###### 题目描述

输入一个链表，输出该链表中倒数第k个结点。

如果该链表长度小于k，请返回空。

示例1

###### 输入

```
{1,2,3,4,5},1 
```

###### 返回值

```
{5}
```

```
import java.util.*;

/*
 * public class ListNode {
 *   int val;
 *   ListNode next = null;
 *   public ListNode(int val) {
 *     this.val = val;
 *   }
 * }
 */

public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param pHead ListNode类 
     * @param k int整型 
     * @return ListNode类
     */
    public ListNode FindKthToTail (ListNode pHead, int k) {
        // write code here
        if(pHead == null) {
            return pHead;
        }
        ListNode slow = pHead, fast = pHead;
        while(fast != null) {
            fast = fast.next;
            if(k <= 0) {
                slow = slow.next;
            }
            --k;
        }
        return k <= 0 ? slow : null;
    }
}
```

#### 反转链表

###### 题目描述

输入一个链表，反转链表后，输出新链表的表头。

示例1

###### 输入

```
{1,2,3}
```

###### 返回值

```
{3,2,1}
```

**递归解法**

> /*
> public class ListNode {
>     int val;
>     ListNode next = null;
>
>     ListNode(int val) {
>         this.val = val;
>     }
> }*/
> public class Solution {
>     public ListNode ReverseList(ListNode head) {
>         if(head == null || head.next == null) {
>             return head;
>         }
>         ListNode newHead = ReverseList(head.next);
>         head.next.next = head;
>         head.next = null;
>         return newHead;
>     }
> }

**迭代解法**

> /*
> public class ListNode {
>     int val;
>     ListNode next = null;
>
>     ListNode(int val) {
>         this.val = val;
>     }
> }*/
> public class Solution {
>     public ListNode ReverseList(ListNode head) {
>         ListNode cur = head, pre = null, nxt = null;
>         while(cur != null) {
>             nxt = cur.next;
>             cur.next = pre;
>             pre = cur;
>             cur = nxt;
>         }
>         return pre;
>     }
> }

#### 合并两个排序的链表

###### 题目描述

输入两个单调递增的链表，输出两个链表合成后的链表，当然我们需要合成后的链表满足单调不减规则。

示例1

###### 输入

```
{1,3,5},{2,4,6}
```

###### 返回值

```
{1,2,3,4,5,6}
```

```
/*
public class ListNode {
    int val;
    ListNode next = null;

    ListNode(int val) {
        this.val = val;
    }
}*/
public class Solution {
    public ListNode Merge(ListNode list1,ListNode list2) {
        if(list1 == null) {
            return list2;
        }
        if(list2 == null) {
            return list1;
        }
        ListNode cur1 = list1, cur2 = list2;
        ListNode dummy = new ListNode(-1), cur = dummy;
        while(cur1 != null && cur2 != null) {
            if(cur1.val < cur2.val) {
                cur.next = cur1;
                cur1 = cur1.next;
            } else {
                cur.next = cur2;
                cur2 = cur2.next;
            }
            cur = cur.next;
        }
        if(cur1 != null) {
            cur.next = cur1;
        } else {
            cur.next = cur2;
        }
        return dummy.next;
    }
}
```

#### 树的子结构

###### 题目描述

输入两棵二叉树A，B，判断B是不是A的子结构。（ps：我们约定空树不是任意一个树的子结构）

示例1

###### 输入

```
{8,8,#,9,#,2,#,5},{8,9,#,2}
```

###### 返回值

```
true
```

```
/**
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

}
*/
public class Solution {
    public boolean HasSubtree(TreeNode root1,TreeNode root2) {
        if(root1 == null || root2 == null) {
            return false;
        }
        return dfs(root1, root2)
            || HasSubtree(root1.left, root2)
            || HasSubtree(root1.right, root2);
    }
    
    private boolean dfs(TreeNode root1, TreeNode root2) {
        if(root2 == null) {
            return true;
        }
        if(root1 == null) {
            return false;
        }
        if(root1.val == root2.val) {
            return dfs(root1.left, root2.left) 
                && dfs(root1.right, root2.right);
        } else {
            return false;
        }
    }
}
```

#### 二叉树的镜像

###### 题目描述

操作给定的二叉树，将其变换为源二叉树的镜像。

```
比如：    源二叉树 
            8
           /  \
          6   10
         / \  / \
        5  7 9 11
        镜像二叉树
            8
           /  \
          10   6
         / \  / \
        11 9 7  5
```

示例1

###### 输入

```
{8,6,10,5,7,9,11}
```

###### 返回值

```
{8,10,6,11,9,7,5}
```

```
import java.util.*;

/*
 * public class TreeNode {
 *   int val = 0;
 *   TreeNode left = null;
 *   TreeNode right = null;
 *   public TreeNode(int val) {
 *     this.val = val;
 *   }
 * }
 */

public class Solution {
    /**
     * 代码中的类名、方法名、参数名已经指定，请勿修改，直接返回方法规定的值即可
     *
     * 
     * @param pRoot TreeNode类 
     * @return TreeNode类
     */
    public TreeNode Mirror (TreeNode pRoot) {
        // write code here
        if(pRoot == null) {
            return pRoot;
        }
        TreeNode node = pRoot.left;
        pRoot.left = pRoot.right;
        pRoot.right = node;
        Mirror(pRoot.left);
        Mirror(pRoot.right);
        return pRoot;
    }
}
```

#### 顺时针打印矩阵

###### 题目描述

输入一个矩阵，按照从外向里以顺时针的顺序依次打印出每一个数字，例如，如果输入如下4 X 4矩阵： 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 则依次打印出数字1,2,3,4,8,12,16,15,14,13,9,5,6,7,11,10.

示例1

###### 输入

```
[[1,2],[3,4]]
```

###### 返回值

```
[1,2,4,3]
```

```
import java.util.ArrayList;
public class Solution {
    public ArrayList<Integer> printMatrix(int [][] matrix) {
        ArrayList<Integer> ans = new ArrayList<>();
       if(matrix == null || matrix.length == 0 || matrix[0].length == 0) {
           return ans;
       }
       int top = 0, bottom = matrix.length - 1;
       int left = 0, right = matrix[0].length - 1;
       while(true) {
           for(int i = left; i <= right; ++i) {
               ans.add(matrix[top][i]);
           }
           if(++top > bottom) {
               break;
           }
           for(int i = top; i <= bottom; ++i) {
               ans.add(matrix[i][right]);
           }
           if(--right < left) {
               break;
           }
           for(int i = right; i >= left; --i) {
               ans.add(matrix[bottom][i]);
           }
           if(--bottom < top) {
               break;
           }
           for(int i = bottom; i >= top; --i) {
               ans.add(matrix[i][left]);
           }
           if(++left > right) {
               break;
           }
       }
        return ans;
    }
}
```

#### 包含min函数的栈

###### 题目描述

定义栈的数据结构，请在该类型中实现一个能够得到栈中所含最小元素的min函数（时间复杂度应为O（1））。

```
import java.util.Stack;

public class Solution {

    Stack<Integer> stack = new Stack<>();
    Stack<Integer> minStack = new Stack<>();
    
    public void push(int node) {
        if(!minStack.isEmpty()) {
            minStack.push(Math.min(minStack.peek(), node));
        } else {
            minStack.push(node);
        }
        stack.push(node);
    }
    
    public void pop() {
        if(!stack.isEmpty()) {
            stack.pop();
            minStack.pop();
        }
    }
    
    public int top() {
        return stack.peek();
    }
    
    public int min() {
        return minStack.peek();
    }
}
```

#### 栈的压入、弹出序列

###### 题目描述

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。（注意：这两个序列的长度是相等的）

示例1

###### 输入

```
[1,2,3,4,5],[4,3,5,1,2]
```

###### 返回值

```
false
```

> 用一个栈模拟既可

```
import java.util.*;

public class Solution {
    public boolean IsPopOrder(int [] pushA,int [] popA) {
        Stack<Integer> stack = new Stack<>();
        int index = 0;
        for(int i = 0; i < pushA.length; ++i) {
            while(!stack.isEmpty() && stack.peek() == popA[index]) {
                ++index;
                stack.pop();
            }
            stack.push(pushA[i]);
        }
        while(!stack.isEmpty() && stack.peek() == popA[index]) {
            ++index;
            stack.pop();
        }
        return index == popA.length;
    }
}
```

#### 二叉搜索树的后序遍历序列

###### 题目描述

输入一个整数数组，判断该数组是不是某二叉搜索树的后序遍历的结果。如果是则返回true,否则返回false。假设输入的数组的任意两个数字都互不相同。（ps：我们约定空树不是二叉搜素树）

示例1

###### 输入

```
[4,8,6,12,16,14,10]
```

###### 返回值

```
true
```

> 后续遍历序列的最后一个是根节点，根据二叉搜索树的性质，根节点的左边节点的值小于根节点的值，右边节点的值大于根节点的值，根据这条性质将后序遍历序列分为左右两个，分别递归判断既可

```
public class Solution {
    public boolean VerifySquenceOfBST(int [] sequence) {
        if(sequence == null || sequence.length == 0) {
            return false;
        }
        return dfs(sequence, 0, sequence.length - 1);
    }
    
    private boolean dfs(int[] sequence, int left, int right) {
        if(left > right) {
            return true;
        }
        int index = left;
        for(; index < right; ++index) {
            if(sequence[index] > sequence[right]) {
                break;
            }
        }
        for(int i = index; i < right; ++i) {
            if(sequence[i] < sequence[right]) {
                return false;
            }
        }
        return dfs(sequence, left, index - 1) && dfs(sequence, index, right - 1);
    }
}
```

#### 二叉树中和为某一值的路径

###### 题目描述

输入一颗二叉树的根节点和一个整数，按字典序打印出二叉树中结点值的和为输入整数的所有路径。路径定义为从树的根结点开始往下一直到叶结点所经过的结点形成一条路径。

示例1

###### 输入

```
{10,5,12,4,7},22
```

###### 返回值

```
[[10,5,7],[10,12]]
```

示例2

###### 输入

```
{10,5,12,4,7},15
```

###### 返回值;)

```
[]
```

```
import java.util.ArrayList;
/**
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

}
*/
public class Solution {
    ArrayList<ArrayList<Integer>> ans = new ArrayList<>();
    public ArrayList<ArrayList<Integer>> FindPath(TreeNode root,int target) {
        if(root == null) {
            return ans;
        }
        dfs(root, target, new ArrayList<Integer>());
        return ans;
    }
    
    private void dfs(TreeNode root, int remainTarget, ArrayList<Integer> tmp) {
        if(root == null) {
            return ;
        }
        remainTarget -= root.val;
        tmp.add(root.val);
        if(remainTarget == 0 && root.left == null && root.right == null) {
            ans.add(new ArrayList<>(tmp));
            tmp.remove(tmp.size() - 1);
            return ;
        }
        dfs(root.left, remainTarget, tmp);
        dfs(root.right, remainTarget, tmp);
        tmp.remove(tmp.size() - 1);
    }
}
```

#### 复杂链表的赋值

###### 题目描述

输入一个复杂链表（每个节点中有节点值，以及两个指针，一个指向下一个节点，另一个特殊指针random指向一个随机节点），请对此链表进行深拷贝，并返回拷贝后的头结点。（注意，输出结果中请不要返回参数中的节点引用，否则判题程序会直接返回空）

```
/*
public class RandomListNode {
    int label;
    RandomListNode next = null;
    RandomListNode random = null;

    RandomListNode(int label) {
        this.label = label;
    }
}
*/
public class Solution {
    public RandomListNode Clone(RandomListNode pHead) {
        if(pHead == null) {
            return pHead;
        }
        RandomListNode cur = pHead;
        while(cur != null) {
            RandomListNode next = cur.next;
            RandomListNode node = new RandomListNode(cur.label);
            cur.next = node;
            node.next = next;
            cur = next;
        }
        cur = pHead;
        while(cur != null && cur.next != null) {
            if(cur.random != null) {
                cur.next.random = cur.random.next;
            }
            cur = cur.next.next;
        }
        RandomListNode dummyHead = new RandomListNode(-1);
        RandomListNode dCur = dummyHead;
        cur = pHead;
        while(cur != null && cur.next != null) {
            RandomListNode next = cur.next.next;
            dCur.next = cur.next;
            dCur = dCur.next;
            cur.next = next;
            cur = cur.next;
        }
        return dummyHead.next;
    }
}
```

#### 字符串的排列

###### 题目描述

输入一个字符串,按字典序打印出该字符串中字符的所有排列。例如输入字符串abc,则按字典序打印出由字符a,b,c所能排列出来的所有字符串abc,acb,bac,bca,cab和cba。

###### 输入描述:

```
输入一个字符串,长度不超过9(可能有字符重复),字符只包括大小写字母。
```

示例1

###### 输入

```
"ab"
```

###### 返回值

```
["ab","ba"]
```

```
import java.util.ArrayList;
public class Solution {
    ArrayList<String> ans = new ArrayList<>();
    public ArrayList<String> Permutation(String str) {
       if(str == null || str.length() == 0) {
           return ans;
       }
       char[] chars = str.toCharArray();
       int len = chars.length;
       boolean[] visited = new boolean[len];
       dfs(chars, new StringBuilder(), visited);
       return ans;
    }
    
    private void dfs(char[] chars, StringBuilder sb, boolean[] visited) {
        if(sb.length() == chars.length) {
            ans.add(sb.toString());
            return ;
        }
        for(int i = 0; i < chars.length; ++i) {
            if(visited[i]) {
                continue;
            }
            if(i != 0 && chars[i] == chars[i - 1] && !visited[i - 1]) {
                continue;
            }
            visited[i] = true;
            sb.append(chars[i]);
            dfs(chars, sb, visited);
            sb.deleteCharAt(sb.length() - 1);
            visited[i] = false;
        }
    }
}
```

#### 数组中出现次数超过一半的数字

###### 题目描述

数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。例如输入一个长度为9的数组{1,2,3,2,2,2,5,4,2}。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。如果不存在则输出0。

示例1

###### 输入

```
[1,2,3,2,2,2,5,4,2]
```

###### 返回值

```
2
```

```
public class Solution {
    public int MoreThanHalfNum_Solution(int [] array) {
        if(array == null || array.length == 0) {
            return 0;
        }
        int cur = array[0], count = 1;
        for(int i = 1; i < array.length; ++i) {
            if(array[i] != cur) {
                if(count > 0) {
                    --count;
                } else {
                    cur = array[i];
                    count = 1;
                }
            } else {
                ++count;
            }
        }
        count = 0;
        for(int num : array) {
            if(num == cur) {
                ++count;
            }
        }
        return count > array.length / 2 ? cur : 0;
    }
}
```

## 4.10猿辅导面试准备

| 题目                                      | 频次 |
| ----------------------------------------- | ---- |
| ~~189. 旋转数组~~                         | 3    |
| ~~剑指 Offer 27. 二叉树的镜像~~           | 3    |
| ~~113. 路径总和 II~~                      | 3    |
| ~~1. 两数之和~~                           | 2    |
| ~~面试题 03.05. 栈排序~~                  | 2    |
| ~~74. 搜索二维矩阵~~                      | 2    |
| ~~110. 平衡二叉树~~                       | 2    |
| ~~222. 完全二叉树的节点个数~~             | 2    |
| ~~25. K 个一组翻转链表~~                  | 2    |
| 剑指 Offer 36. [二叉搜索树与双向链表]()   | 2    |
| ~~98. 验证二叉搜索树~~                    | 2    |
| 215. 数组中的第K个最大元素                | 2    |
| 7. 整数反转                               | 1    |
| 102. [二叉树]()的层序遍历                 | 1    |
| 562.矩阵中最长的连续1线段                 | 1    |
| 41. 缺失的第一个正数                      | 1    |
| 448. 找到所有数组中消失的数字             | 1    |
| 82. 删除[排序]()[链表]()中的重复元素 II   | 1    |
| 94. [二叉树]()的中序遍历                  | 1    |
| 257. [二叉树]()的所有路径                 | 1    |
| 124. [二叉树]()中的最大路径和             | 1    |
| 450. 删除二叉搜索树中的节点               | 1    |
| 40. 组合总和 II                           | 1    |
| 658. 找到 K 个最接近的元素                | 1    |
| 316. 去除重复字母                         | 1    |
| 86. 分隔[链表]()                          | 1    |
| 226. 翻转[二叉树]()                       | 1    |
| 剑指 Offer 22. [链表]()中倒数第k个节点    | 1    |
| 560. 和为K的子数组                        | 1    |
| 442. 数组中重复的数据                     | 1    |
| 1325. 删除给定值的叶子节点                | 1    |
| 剑指 Offer 25. 合并两个[排序]()的[链表]() | 1    |
| 240. 搜索二维矩阵 II                      | 1    |
| 958. [二叉树]()的完全性检验               | 1    |
| 239. 滑动窗口最大值                       | 1    |
| 208. 实现 Trie (前缀树)                   | 1    |
| 99. 恢复二叉搜索树                        | 1    |
| 83. 删除[排序]()[链表]()中的重复元素      | 1    |

#### 旋转数组

###### 题目描述

一个数组A中存有N（N&gt0）个整数，在不允许使用另外数组的前提下，将每个整数循环向右移M（M>=0）个位置，即将A中的数据由（A0 A1 ……AN-1 ）变换为（AN-M …… AN-1 A0 A1 ……AN-M-1 ）（最后M个数循环移至最前面的M个位置）。如果需要考虑程序移动数据的次数尽量少，要如何设计移动的方法？

示例1

###### 输入

```
6,2,[1,2,3,4,5,6]
```

###### 返回值

```
[5,6,1,2,3,4]
```

###### 备注:

```
(1<=N<=100,M>=0)
```

> 对数组进行三次反转既可，以[1, 2, 3, 4, 5, 6]为例，先反转整个数组，变为[6, 5, 4, 3, 2, 1]，再反转0到m - 1，结果为[5, 6, 4, 3, 2, 1]，最后反转m到数组结束的位置既可。

```
import java.util.*;


public class Solution {
    /**
     * 旋转数组
     * @param n int整型 数组长度
     * @param m int整型 右移距离
     * @param a int整型一维数组 给定数组
     * @return int整型一维数组
     */
    public int[] solve (int n, int m, int[] a) {
        // write code here
        if(a == null || a.length == 0 || m == 0) {
            return a;
        }
        m %= a.length;
        reverse(a, 0, a.length - 1);
        reverse(a, 0, m - 1);
        reverse(a, m, a.length - 1);
        return a;
    }
    
    private void reverse(int[] a, int left, int right) {
        while(left < right) {
            int tmp = a[left];
            a[left++] = a[right];
            a[right--] = tmp;
        }
    }
}
```

#### 二叉树的镜像

###### 题目描述

操作给定的二叉树，将其变换为源二叉树的镜像。

###### 输入描述:

```
二叉树的镜像定义：源二叉树 
    	    8
    	   /  \
    	  6   10
    	 / \  / \
    	5  7 9 11
    	镜像二叉树
    	    8
    	   /  \
    	  10   6
    	 / \  / \
    	11 9 7  5
```

> 二叉树反转，先反转根节点的左右节点，再递归一次反转根节点的左子树和右子树既可

**先序遍历解法**

```
/**
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

}
*/
public class Solution {
    public void Mirror(TreeNode root) {
        if(root == null) {
            return ;
        }
        TreeNode tmp = root.left;
        root.left = root.right;
        root.right = tmp;
        Mirror(root.left);
        Mirror(root.right);
        return ;
    }
}
```

**后序遍历解法**

```
/**
public class TreeNode {
    int val = 0;
    TreeNode left = null;
    TreeNode right = null;

    public TreeNode(int val) {
        this.val = val;

    }

}
*/
public class Solution {
    public void Mirror(TreeNode root) {
        if(root == null) {
            return ;
        }
        reverse(root);
    }
    
    private TreeNode reverse(TreeNode root) {
        if(root == null) {
            return root;
        }
        TreeNode left = reverse(root.left);
        TreeNode right = reverse(root.right);
        root.left = right;
        root.right = left;
        return root;
    }
}
```

#### 路径总合

给你二叉树的根节点 root 和一个整数目标和 targetSum ，找出所有 从根节点到叶子节点 路径总和等于给定目标和的路径。

叶子节点 是指没有子节点的节点。

 

示例 1：

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsumii1.jpg)
```
输入：root = [5,4,8,11,null,13,4,7,2,null,null,5,1], targetSum = 22
输出：[[5,4,11,2],[5,8,4,5]]
```
示例 2：

![img](https://assets.leetcode.com/uploads/2021/01/18/pathsum2.jpg)

```
输入：root = [1,2,3], targetSum = 5
输出：[]
```
示例 3：
```
输入：root = [1,2], targetSum = 0
输出：[]
```

> 回溯，当root为空的时候，直接返回，如果剩下的target为0，且当前节点为叶子节点，则将路径加入到结果集中，并将叶子节点移除保存的路径list进行回溯。

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    List<List<Integer>> ans = new ArrayList<>();
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        if(root == null) {
            return ans;
        }
        dfs(root, targetSum, new ArrayList<Integer>());
        return ans;
    }

    private void dfs(TreeNode root, int remain, List<Integer> tmp) {
        if(root == null) {
            return ;
        }
        remain -= root.val;
        tmp.add(root.val);
        if(remain == 0 && root.left == null && root.right == null) {
            ans.add(new ArrayList<>(tmp));
            tmp.remove(tmp.size() - 1);
            return ;
        }
        dfs(root.left, remain, tmp);
        dfs(root.right, remain, tmp);
        tmp.remove(tmp.size() - 1);
    }
}
```

#### 两数之和

###### 题目描述

给出一个整数数组，请在数组中找出两个加起来等于目标值的数，

你给出的函数twoSum 需要返回这两个数字的下标（index1，index2），需要满足 index1 小于index2.。注意：下标是从1开始的

假设给出的数组中只存在唯一解

例如：

给出的数组为 {20, 70, 110, 150},目标值为90
输出 index1=1, index2=2

示例1

###### 输入

```
[3,2,4],6
```

###### 返回值

```
[2,3]
```

> 首先判断边界条件，如果输入数组为空或者长度小于2，则无结果；
>
> 使用map保存遍历过的数组元素，key为target与数组元素的差值，值为数组元素的下标，如果遍历过程中发现map中有key的值与数组元素相等，则说明找到了结果集，将map中取出的val和数组下标分别加一返回既可

```
import java.util.*;


public class Solution {
    /**
     * 
     * @param numbers int整型一维数组 
     * @param target int整型 
     * @return int整型一维数组
     */
    public int[] twoSum (int[] numbers, int target) {
        // write code here
        if(numbers == null || numbers.length < 2) {
            return new int[0];
        }
        Map<Integer, Integer> map = new HashMap<>();
        for(int i = 0; i < numbers.length; ++i) {
            if(map.containsKey(numbers[i])) {
                return new int[]{map.get(numbers[i]) + 1, i + 1};
            }
            map.put(target - numbers[i], i);
        }
        return new int[0];
    }
}
```

#### 栈排序

栈排序。 编写程序，对栈进行排序使最小元素位于栈顶。最多只能使用一个其他的临时栈存放数据，但不得将元素复制到别的数据结构（如数组）中。该栈支持如下操作：push、pop、peek 和 isEmpty。当栈为空时，peek 返回 -1。

示例1:
```
 输入：
["SortedStack", "push", "push", "peek", "pop", "peek"]
[[], [1], [2], [], [], []]
 输出：
[null,null,null,1,null,2]
```
示例2:
```
 输入： 
["SortedStack", "pop", "pop", "push", "pop", "isEmpty"]
[[], [], [], [1], [], []]
 输出：
[null,null,null,null,null,true]
```

> 主要从入栈操作下手，本体要实现一个最小元素位于栈顶的栈，也就是最小元素出栈后，栈顶是次小元素，这就是一个递增的单调栈
>
> 入栈时，先将栈中比入栈元素大的元素弹出栈，放到辅助栈中，将需要入栈的元素入栈，然后将辅助栈中的元素依次弹出放到主栈中既可

```
class SortedStack {

    Stack<Integer> stack;
    Stack<Integer> assistStack;
    public SortedStack() {
        this.stack = new Stack<>();
        this.assistStack = new Stack<>();
    }
    
    public void push(int val) {
        while(!stack.isEmpty() && stack.peek() < val) {
            assistStack.push(stack.pop());
        }
        stack.push(val);
        while(!assistStack.isEmpty()) {
            stack.push(assistStack.pop());
        }
    }
    
    public void pop() {
        if(stack.isEmpty()) {
            return ;
        }
        stack.pop();
    }
    
    public int peek() {
        if(stack.isEmpty()) {
            return -1;
        }
        return stack.peek();
    }
    
    public boolean isEmpty() {
        return stack.isEmpty();
    }
}

/**
 * Your SortedStack object will be instantiated and called as such:
 * SortedStack obj = new SortedStack();
 * obj.push(val);
 * obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.isEmpty();
 */
```

#### 搜索二维矩阵

编写一个高效的算法来判断 m x n 矩阵中，是否存在一个目标值。该矩阵具有如下特性：

每行中的整数从左到右按升序排列。
每行的第一个整数大于前一行的最后一个整数。

示例 1：

![img](https://assets.leetcode.com/uploads/2020/10/05/mat.jpg)

```
输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 3
输出：true
```
示例 2：

![img](https://assets.leetcode-cn.com/aliyun-lc-upload/uploads/2020/11/25/mat2.jpg)

```
输入：matrix = [[1,3,5,7],[10,11,16,20],[23,30,34,60]], target = 13
输出：false
```

> 由于矩阵从从做到右是递增的，从上到下是递增的，所以可以从对角线开始，类似于二分查找，数组对应位置的元素等于target则返回true，小于说明这一行所有的元素都小于target，到下一行查找，大于说明本列及后面所有列的值都大于target，到前一列查找。

```
class Solution {
    public boolean searchMatrix(int[][] matrix, int target) {
        if(matrix == null || matrix.length == 0 || matrix[0].length == 0
        || matrix[0][0] > target || matrix[matrix.length - 1][matrix[0].length - 1] < target) {
            return false;
        }
        int top = 0, right = matrix[0].length - 1;
        while(top < matrix.length && right >= 0) {
            int val = matrix[top][right];
            if(val == target) {
                return true;
            }
            if(val > target) {
                --right;
            } else {
                ++top;
            }
        }
        return false;
    }
}
```

#### 平衡二叉树

###### 题目描述

输入一棵二叉树，判断该二叉树是否是平衡二叉树。

在这里，我们只需要考虑其平衡性，不需要考虑其是不是排序二叉树

**平衡二叉树**（Balanced Binary Tree），具有以下性质：它是一棵空树或它的左右两个子树的高度差的绝对值不超过1，并且左右两个子树都是一棵平衡二叉树。

示例1

###### 输入

```
{1,2,3,4,5,6,7}
```

###### 返回值

```
true
```

> 平衡二叉树的性质是左右子树的高度之差不超过1，用递归既可，获取节点左右子树的高度，如果高度之差超过1，则不是平衡二叉树

```
public class Solution {
    public boolean IsBalanced_Solution(TreeNode root) {
        if(root == null) {
            return true;
        }
        return getNodes(root) != -1;
    }
    
    private int getNodes(TreeNode root) {
        if(root == null) {
            return 0;
        }
        int left = getNodes(root.left);
        int right = getNodes(root.right);
        if(Math.abs(left - right) > 1 || left == -1 || right == -1) {
            return -1;
        }
        return Math.max(left, right) + 1;
    }
}
```

#### 判断二叉树是否为完全二叉树（补充）

> 讲二叉树的节点加入到队列中，当出队元素为空时，停止遍历二叉树。由于完全二叉树的性质要求在空节点之后不会再出现非空节点，因此遍历对内元素，如果有非空元素，则说明这个树不是完全二叉树

```
public class Solution {
	public boolean isCompleteTree(TreeNode root) {
		if(root == null) {
			return true;
		}
		Queue<TreeMap> queue = new LinkedList<>();
		queue.offer(root);
		while(!queue.isEmpty()) {
			TreeNode node = queue.poll();
			if(node == null) {
				break;
			}
			queue.offer(node.left);
			queue.offer(node.right);
		}
		while(!queue.isEmpty()) {
			if(queue.poll() != null) {
				return false;
			}
		}
		return true;
	}
}
```

#### 验证二叉搜索树

> 由二叉搜索树的性质可知，对二叉搜索树进行中序遍历，会得到一个单调递增的序列，因此，只需对二叉树进行遍历，并在遍历过程中判断当前节点和前一个节点的大小关系

```
public class Solution {
	TreeNode pre = null;
	public boolean isSearchTree(TreeNode root) {
		if(root == null) {
			return true;
		}
		if(!isSearchTree(root.left)){
			return false;
		}
		if(pre != null && pre.val >= root.val) {
			return false;
		}
		pre = root;
		return isSearchTree(root.right);
	}
}
```

#### 完全二叉树的节点个数

给你一棵 完全二叉树 的根节点 root ，求出该树的节点个数。

完全二叉树 的定义如下：在完全二叉树中，除了最底层节点可能没填满外，其余每层节点数都达到最大值，并且最下面一层的节点都集中在该层最左边的若干位置。若最底层为第 h 层，则该层包含 1~ 2h 个节点。

 

示例 1：

![img](https://assets.leetcode.com/uploads/2021/01/14/complete.jpg)
```
输入：root = [1,2,3,4,5,6]
输出：6
```
示例 2：
```
输入：root = []
输出：0
```
示例 3：
```
输入：root = [1]
输出：1
```

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public int countNodes(TreeNode root) {
        if(root == null) {
            return 0;
        }
        int hl = 0, hr = 0;
        TreeNode node = root;
        while(node != null) {
            ++hl;
            node = node.left;
        }
        node = root;
        while(node != null) {
            ++hr;
            node = node.right;
        }
        if(hl == hr) {
            return (int)Math.pow(2, hl) - 1;
        }
        return countNodes(root.left) + countNodes(root.right) + 1;
    }
}
```

#### k个一组反转链表

###### 题目描述

将给出的链表中的节点每*k* 个一组翻转，返回翻转后的链表
如果链表中的节点数不是 *k* 的倍数，将最后剩下的节点保持原样
你不能更改节点中的值，只能更改节点本身。
要求空间复杂度 *O*(1)

例如：

给定的链表是 1→2→3→4→5

对于 *k*=2, 你应该返回 2→1→4→3→5

对于*k*=3, 你应该返回 3→2→1→4→5

示例1

###### 输入

```
{1,2,3,4,5},2
```

###### 返回值

```
{2,1,4,3,5}
```

```
import java.util.*;

/*
 * public class ListNode {
 *   int val;
 *   ListNode next = null;
 * }
 */

public class Solution {
    /**
     * 
     * @param head ListNode类 
     * @param k int整型 
     * @return ListNode类
     */
    public ListNode reverseKGroup (ListNode head, int k) {
        // write code here
        ListNode A = head, B = head;
        for(int i = 0; i < k; ++i) {
            if(B == null) {
                return head;
            }
            B = B.next;
        }
        ListNode newHead = reverse(A, B);
        A.next = reverseKGroup(B, k);
        return newHead;
    }
    
    private ListNode reverse(ListNode A, ListNode B) {
        ListNode cur = A, pre = null, nxt = null;
        while(cur != B) {
            nxt = cur.next;
            cur.next = pre;
            pre = cur;
            cur = nxt;
        }
        return pre;
    }
}
```

#### 数组中的第K个最大元素

在未排序的数组中找到第 k 个最大的元素。请注意，你需要找的是数组排序后的第 k 个最大的元素，而不是第 k 个不同的元素。

示例 1:
```
输入: [3,2,1,5,6,4] 和 k = 2
输出: 5
```
示例 2:
```
输入: [3,2,3,1,2,4,5,5,6] 和 k = 4
输出: 4
```

```
class Solution {
    public int findKthLargest(int[] nums, int k) {
        int len = nums.length;
        PriorityQueue<Integer> queue = new PriorityQueue<>((a, b) -> a - b);
        for(int i = 0; i < k; ++i) {
            queue.offer(nums[i]);
        }
        for(int i = k; i < len; ++i) {
            if(nums[i] > queue.peek()) {
                queue.poll();
                queue.offer(nums[i]);
            }
        }
        return queue.peek();
    }
}
```

#### 反转整数

给你一个 32 位的有符号整数 x ，返回将 x 中的数字部分反转后的结果。

如果反转后整数超过 32 位的有符号整数的范围 [−231,  231 − 1] ，就返回 0。

假设环境不允许存储 64 位整数（有符号或无符号）。


示例 1：
```
输入：x = 123
输出：321
```
示例 2：
```
输入：x = -123
输出：-321
```
示例 3：
```
输入：x = 120
输出：21
```
示例 4：
```
输入：x = 0
输出：0
```

> 主要考察对边界情况的判断，当超过Integer的最大值和最小值时，需要单独判断

```
class Solution {
    public int reverse(int x) {
        int ans = 0;
        while(x != 0) {
            int num = x % 10;
            if(ans > Integer.MAX_VALUE / 10 || (ans == Integer.MAX_VALUE / 10 && num > 7)) {
                return 0;
            }
            if(ans < Integer.MIN_VALUE / 10 || (ans == Integer.MAX_VALUE / 10 && num < -8)) {
                return 0;
            }
            ans = ans * 10 + num;
            x /= 10;
        }
        return ans;
    }
}
```

#### 二叉树的层次遍历

给你一个二叉树，请你返回其按 层序遍历 得到的节点值。 （即逐层地，从左到右访问所有节点）。

示例：
```
二叉树：[3,9,20,null,null,15,7],

    3
   / \
  9  20
    /  \
   15   7
```
返回其层序遍历结果：
```
[
  [3],
  [9,20],
  [15,7]
]
```
```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    List<List<Integer>> ans = new ArrayList<>();
    public List<List<Integer>> levelOrder(TreeNode root) {
        if(root == null) {
            return ans;
        }
        dfs(root, 0);
        return ans;
    }

    private void dfs(TreeNode root, int depth) {
        if(root == null) {
            return ;
        }
        if(ans.size() == depth) {
            List<Integer> list = new ArrayList<>();
            list.add(root.val);
            ans.add(list);
        } else {
            ans.get(depth).add(root.val);
        }
        dfs(root.left, depth + 1);
        dfs(root.right, depth + 1);
    }
}
```

#### 矩阵中最长的连续1线段

给定一个01矩阵 M，找到矩阵中最长的连续1线段。
这条线段可以是水平的、垂直的、对角线的或者反对角线的。

```
示例:
输入:
[[0,1,1,0],
 [0,1,1,0],
 [0,0,0,1]]
输出: 3
提示: 给定矩阵中的元素数量不会超过 10,000。
```

```
public class Solution {
	public int longestLine(int[][] array) {
		if(array == null || array.length == 0 || array[0].length == 0) {
			return 0;
		}
		int m = array.length;
		int n = array[0].length;
		int[][][] dp = new int[m][n][4];
		for(int i = 0; i < m; ++i) {
			for(int j = 0; j < n; ++j) {
				if(array[m][n] == 0) {
					continue;
				}
				for(int k = 0; k < 4; ++k) {
					dp[i][j][k] = 1;
				}
				if(j - 1 >= 0) {
					dp[i][j][0] += dp[i][j - 1][0];
				}
				if(i - 1 >= 0) {
					dp[i][j][1] += dp[i - 1][j][1];
				}
				if(i - 1 >= 0 && j - 1 >= 0) {
					dp[i][j][2] += dp[i - 1][j - 1][2];
				}
				if(i - 1 >= 0 && j + 1 < n) {
					dp[i][j][3] += dp[i - 1][j + 1][3];
				}
				ans = Math.max(ans, Math.max(dp[i][j][0], dp[i][j][1]));
				ans = Math.max(ans, Math.max(dp[i][j][2], dp[i][j][3]));
			}
		}
		return ans;
	}
}
```

#### 缺失的第一个正数

 

进阶：你可以实现时间复杂度为 O(n) 并且只使用常数级别额外空间的解决方案吗？

示例 1：

```
输入：nums = [1,2,0]
输出：3
```

示例 2：

```
输入：nums = [3,4,-1,1]
输出：2
```

示例 3：

```
输入：nums = [7,8,9,11,12]
输出：1
```

O(n)空间复杂度解法

```
class Solution {
    public int firstMissingPositive(int[] nums) {
        if(nums == null || nums.length == 0) {
            return 1;
        }
        int len = nums.length;
        int[] array = new int[len + 1];
        for(int num : nums) {
            if(num > 0 && num <= len) {
                array[num]++;
            }
        }
        for(int i = 1; i < array.length; ++i) {
            if(array[i] == 0) {
                return i;
            }
        }
        return len + 1;
    }
}
```

常数空间复杂度解法

```
class Solution {
    public int firstMissingPositive(int[] nums) {
        int len = nums.length;
        for (int i = 0; i < len; i++) {
            while (nums[i] > 0 && nums[i] <= len && nums[nums[i] - 1] != nums[i]) {
                swap(nums, nums[i] - 1, i);
            }
        }
        for (int i = 0; i < len; i++) {
            if (nums[i] != i + 1) {
                return i + 1;
            }
        }
        return len + 1;
    }

    private void swap(int[] nums, int index1, int index2) {
        int temp = nums[index1];
        nums[index1] = nums[index2];
        nums[index2] = temp;
    }
}
```

#### 找到所有数组中消失的数字

给定一个范围在  1 ≤ a[i] ≤ n ( n = 数组大小 ) 的 整型数组，数组中的元素一些出现了两次，另一些只出现一次。

找到所有在 [1, n] 范围之间没有出现在数组中的数字。

您能在不使用额外空间且时间复杂度为O(n)的情况下完成这个任务吗? 你可以假定返回的数组不算在额外空间内。

示例:
```
输入:
[4,3,2,7,8,2,3,1]

输出:
[5,6]
```

```
class Solution {
    public List<Integer> findDisappearedNumbers(int[] nums) {
        List<Integer> ans = new ArrayList<>();
        if(nums == null || nums.length == 0) {
            return ans;
        }
        for(int i = 0; i < nums.length; ++i) {
            while(nums[nums[i] - 1] != nums[i]) {
                swap(nums, nums[i] - 1, i);
            }
        }
        for(int i = 0; i < nums.length; ++i) {
            if(nums[i] != i + 1) {
                ans.add(i + 1);
            }
        }
        return ans;
    }

    private void swap(int[] nums, int index1, int index2) {
        int tmp = nums[index1];
        nums[index1] = nums[index2];
        nums[index2] = tmp;
    }
}
```

#### 删除排序链表中重复的元素

存在一个按升序排列的链表，给你这个链表的头节点 head ，请你删除链表中所有存在数字重复情况的节点，只保留原始链表中 没有重复出现 的数字。

返回同样按升序排列的结果链表。

示例 1：

![img](https://assets.leetcode.com/uploads/2021/01/04/linkedlist1.jpg)

```
输入：head = [1,2,3,3,4,4,5]
输出：[1,2,5]
```
示例 2：

![img](https://assets.leetcode.com/uploads/2021/01/04/linkedlist2.jpg)

```
输入：head = [1,1,1,2,3]
输出：[2,3]
```

```
/**
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode() {}
 *     ListNode(int val) { this.val = val; }
 *     ListNode(int val, ListNode next) { this.val = val; this.next = next; }
 * }
 */
class Solution {
    public ListNode deleteDuplicates(ListNode head) {
        if(head == null || head.next == null) {
            return head;
        }
        ListNode dummy = new ListNode(-1), cur = dummy;
        dummy.next = head;
        while(cur.next != null && cur.next.next != null) {
            if(cur.next.val == cur.next.next.val) {
                ListNode tmp = cur.next;
                while(tmp != null && tmp.next != null && tmp.val == tmp.next.val) {
                    tmp = tmp.next;
                }
                cur.next = tmp.next;
            } else {
                cur = cur.next;
            }
        }
        return dummy.next;
    }
}
```

#### 二叉树的中序遍历

递归解法

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    List<Integer> ans = new ArrayList<>();
    public List<Integer> inorderTraversal(TreeNode root) {
        if(root == null) {
            return ans;
        }
        dfs(root);
        return ans;
    }

    private void dfs(TreeNode root) {
        if(root == null) {
            return ;
        }
        dfs(root.left);
        ans.add(root.val);
        dfs(root.right);
    }
}
```

迭代解法

```
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> ans = new ArrayList<>();
        if(root == null) {
            return ans;
        }
        Stack<TreeNode> stack = new Stack<>();
        while(!stack.isEmpty() || root != null) {
            while(root != null) {
                stack.push(root);
                root = root.left;
            }
            root = stack.pop();
            ans.add(root.val);
            root = root.right;
        }
        return ans;
    }
}
```

