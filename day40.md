# 代码随想录算法训练营第四十天| 343. 整数拆分 ，96.不同的二叉搜索树
作者：Zhiwei Song 
日期：2023-07-03

## 343. 整数拆分
题目链接：[https://leetcode.com/problems/integer-break/](https://leetcode.com/problems/integer-break/)

思路：这道题要考虑到一个整数可以拆分成两个数，然后第二个数可以再次被差分。所以在两层for loop中要用到两次Math.max。

答案：

```java
class Solution {
    public int integerBreak(int n) {
        int[] table = new int[n + 1];
        table[1] = 1;
        
        for (int i = 2; i < n + 1; i++) {
            int val = 0;
            for (int j = 1; j <= i / 2; j++) {
                int cur = Math.max(j * (i - j), j * table[i - j]);
                val = Math.max(cur, val);
            }
            table[i] = val;
        }
        return table[n];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``

## 96.不同的二叉搜索树
题目链接：[https://leetcode.com/problems/unique-binary-search-trees/](https://leetcode.com/problems/unique-binary-search-trees/)

思路：这道题的难点在于如何去发现相同pattern的子题目。在每一个结果下面，左右两边的subtree就是两个子问题。

答案：

```java
class Solution {
    public int numTrees(int n) {
        int[] dp = new int[n + 1];
        dp[0] = 1;
        dp[1] = 1;

        for (int i = 2; i < n + 1; i++) {
            for (int j = 1; j <= i; j++) {
                dp[i] += dp[j - 1] * dp[i - j];
            }
        }

        return dp[n];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``
