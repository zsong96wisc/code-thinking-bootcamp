# 代码随想录算法训练营第五十天| 300.最长递增子序列 ， 714.买卖股票的最佳时机含手续费 ， 718. 最长重复子数组
作者：Zhiwei Song 
日期：2023-07-14

## 300.最长递增子序列
题目链接：[https://leetcode.com/problems/longest-increasing-subsequence/](https://leetcode.com/problems/longest-increasing-subsequence/)

思路：就是存以第i个位置结尾的最长子数列的长度。

答案：

```java
class Solution {
    public int lengthOfLIS(int[] nums) {
        if (nums.length == 0) return 0;
        int[] table = new int[nums.length];
        for (int i = 0; i < table.length; i++) table[i] = 1;
        int max = 1;

        for (int i = 1; i < table.length; i++) {
            for (int j = 0; j < i; j++) {
                if (nums[i] > nums[j]) table[i] = Math.max(table[i], table[j] + 1);
                // else table[i] = Math.max(table[i], table[j]);
            }
            if (table[i] > max) max = table[i];
        }

        return max;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 674. 最长连续递增序列
题目链接：[https://leetcode.com/problems/longest-continuous-increasing-subsequence/](https://leetcode.com/problems/longest-continuous-increasing-subsequence/)

思路：只要看第i个和第i-1个位置上面的数能不能叠加即可。

答案：

```java
class Solution {
    public int findLengthOfLCIS(int[] nums) {
        if (nums.length == 0) return 0;
        int max = 1;
        int count = 1;
        for (int i = 1; i < nums.length; i++) {
            if (nums[i] > nums[i - 1]) {
                if (++count > max) max = count;
            }
            else count = 1;
        }
        return max;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 718. 最长重复子数组
题目链接：[https://leetcode.com/problems/maximum-length-of-repeated-subarray/](https://leetcode.com/problems/maximum-length-of-repeated-subarray/)

思路：2维的dp数组，第i和第j位置上是nums1从0到i-1和nums2从0到j-1的最长子数列。

答案：

```java
class Solution {
    public int findLength(int[] nums1, int[] nums2) {
        int[][] table = new int[nums1.length + 1][nums2.length + 1];
        int res = 0;
        for (int i = 1; i < nums1.length + 1; i++) {
            for (int j = 1; j < nums2.length + 1; j++) {
                if (nums1[i - 1] == nums2[j - 1]) {
                    table[i][j] = table[i - 1][j - 1] + 1;
                    res = Math.max(table[i][j], res);
                }
            }
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
