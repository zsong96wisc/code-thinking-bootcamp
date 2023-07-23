# 代码随想录算法训练营第五十四天| 647. 回文子串 ，516.最长回文子序列  
作者：Zhiwei Song 
日期：2023-07-19

## 647. 回文子串
题目链接：[https://leetcode.com/problems/palindromic-substrings/](https://leetcode.com/problems/palindromic-substrings/)

思路：不太会，二刷再看。

答案：

```java
class Solution {
    public int countSubstrings(String s) {
        boolean[][] dp = new boolean[s.length()][s.length()];
        
        int res = 0;
        for (int i = s.length() - 1; i >= 0; i--) {
            for (int j = i; j < s.length(); j++) {
                if (s.charAt(i) == s.charAt(j) && (j - i <= 1 || dp[i + 1][j - 1])) {
                    res++;
                    dp[i][j] = true;
                }
            }
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 516.最长回文子序列
题目链接：[https://leetcode.com/problems/longest-palindromic-subsequence/](https://leetcode.com/problems/longest-palindromic-subsequence/)

思路：没看懂题目，需要二刷。

答案：

```java
class Solution {
    public int longestPalindromeSubseq(String s) {
        int len = s.length();
        int[][] dp = new int[len + 1][len + 1];
        for (int i = len - 1; i >= 0; i--) { // 从后往前遍历 保证情况不漏
            dp[i][i] = 1; // 初始化
            for (int j = i + 1; j < len; j++) {
                if (s.charAt(i) == s.charAt(j)) {
                    dp[i][j] = dp[i + 1][j - 1] + 2;
                } else {
                    dp[i][j] = Math.max(dp[i + 1][j], Math.max(dp[i][j], dp[i][j - 1]));
                }
            }
        }
        return dp[0][len - 1];
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
