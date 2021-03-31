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

