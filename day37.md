# 代码随想录算法训练营第三十七天| 738.单调递增的数字 ，968.监控二叉树
作者：Zhiwei Song 
日期：2023-06-29

## 738.单调递增的数字
题目链接：[https://leetcode.com/problems/monotone-increasing-digits/](https://leetcode.com/problems/monotone-increasing-digits/)

思路：如果前面一个数大于了后面的数，前面的数字减一，后面都为九。

答案：

```java
class Solution {
    public int monotoneIncreasingDigits(int n) {
        String s = String.valueOf(n);
        char[] chars = s.toCharArray();
        int start = s.length();
        for (int i = s.length() - 2; i >= 0; i--) {
            if (chars[i] > chars[i + 1]) {
                chars[i]--;
                start = i+1;
            }
        }

        for (int i = start; i < s.length(); i++) {
            chars[i] = '9';
        }
        return Integer.parseInt(String.valueOf(chars));
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 968.监控二叉树
题目链接：[https://leetcode.com/problems/binary-tree-cameras/](https://leetcode.com/problems/binary-tree-cameras/)

思路：

答案：

```java

```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
