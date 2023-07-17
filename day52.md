# 代码随想录算法训练营第五十二天| 392.判断子序列 ，115.不同的子序列  
作者：Zhiwei Song 
日期：2023-07-17

## 392.判断子序列
题目链接：[https://leetcode.com/problems/is-subsequence](https://leetcode.com/problems/is-subsequence)

思路：经典双指针题目。也可以用动态规划来解。

答案：

```java
class Solution {
    public boolean isSubsequence(String s, String t) {
        int length1 = s.length(); int length2 = t.length();
        int[][] dp = new int[length1+1][length2+1];
        for(int i = 1; i <= length1; i++){
            for(int j = 1; j <= length2; j++){
                if(s.charAt(i-1) == t.charAt(j-1)){
                    dp[i][j] = dp[i-1][j-1] + 1;
                }else{
                    dp[i][j] = dp[i][j-1];
                }
            }
        }
        if(dp[length1][length2] == length1){
            return true;
        }else{
            return false;
        }
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 115.不同的子序列  
题目链接：[https://leetcode.com/problems/distinct-subsequences/](https://leetcode.com/problems/distinct-subsequences/)

思路：没看懂题目，需要二刷。

答案：

```java
class Solution {
    public int numDistinct(String s, String t) {
        int[][] dp = new int[s.length() + 1][t.length() + 1];
        for (int i = 0; i < s.length() + 1; i++) {
            dp[i][0] = 1;
        }
        
        for (int i = 1; i < s.length() + 1; i++) {
            for (int j = 1; j < t.length() + 1; j++) {
                if (s.charAt(i - 1) == t.charAt(j - 1)) {
                    dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];
                }else{
                    dp[i][j] = dp[i - 1][j];
                }
            }
        }
        
        return dp[s.length()][t.length()];
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
