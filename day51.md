# 代码随想录算法训练营第五十一天| 1143.最长公共子序列 ， 1035.不相交的线 ， 718. 最长重复子数组
作者：Zhiwei Song 
日期：2023-07-15

## 1143.最长公共子序列
题目链接：[https://leetcode.com/problems/longest-common-subsequence/](https://leetcode.com/problems/longest-common-subsequence/)

思路：详细的解法看 https://www.bilibili.com/video/BV1ye4y1L7CQ。需要二刷！

答案：

```java
class Solution {
    public int longestCommonSubsequence(String text1, String text2) {
        int[][] table = new int[text1.length() + 1][text2.length() + 1];
        for (int i = 1; i < text1.length() + 1; i++) {
            for (int j = 1; j < text2.length() + 1; j++) {
                if (text1.charAt(i - 1) == text2.charAt(j - 1)) table[i][j] = table[i - 1][j - 1] + 1;
                else table[i][j] = Math.max(table[i - 1][j], table[i][j - 1]);
            }
        }
        return table[text1.length()][text2.length()];
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 1035.不相交的线
题目链接：[https://leetcode.com/problems/uncrossed-lines/](https://leetcode.com/problems/uncrossed-lines/)

思路：跟第1147题解法完全一样。

答案：

```java
class Solution {
    public int maxUncrossedLines(int[] nums1, int[] nums2) {
        int[][] table = new int[nums1.length + 1][nums2.length + 1];
        for (int i = 1; i < nums1.length + 1; i++) {
            for (int j = 1; j < nums2.length + 1; j++) {
                if (nums1[i - 1] == nums2[j - 1]) table[i][j] = table[i - 1][j - 1] + 1;
                else table[i][j] = Math.max(table[i - 1][j], table[i][j - 1]);
            }
        }
        return table[nums1.length][nums2.length];
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 53. 最大子序和
题目链接：[https://leetcode.com/problems/maximum-subarray/](https://leetcode.com/problems/maximum-subarray/)

思路：跟贪心思路一样。

答案：

```java
class Solution {
    public int maxSubArray(int[] nums) {
        int res = nums[0];
        int[] dp = new int[nums.length];
        dp[0] = nums[0];
        for (int i = 1; i < nums.length; i++) {
            dp[i] = Math.max(dp[i - 1] + nums[i], nums[i]);
            res = res > dp[i] ? res : dp[i];
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
