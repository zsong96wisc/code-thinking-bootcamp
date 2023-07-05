# 代码随想录算法训练营第四十二天| 1049. 最后一块石头的重量 II ， 494. 目标和 ， 474.一和零
作者：Zhiwei Song 
日期：2023-07-05

## 1049. 最后一块石头的重量 II
题目链接：[https://leetcode.com/problems/last-stone-weight-ii/](https://leetcode.com/problems/last-stone-weight-ii/)

思路：基本思路是01背包，需要把背包分成尽可能大的两堆，然后让它们相撞。

答案：

```java
class Solution {
    public int lastStoneWeightII(int[] stones) {
        int sum = 0;
        for (int i : stones) {
            sum += i;
        }
        int target = sum / 2;
        int[] dp = new int[target + 1];
        for (int i = 0; i < stones.length; i++) {
            for (int j = target; j >= stones[i]; j--) {
                dp[j] = Math.max(dp[j], dp[j - stones[i]] + stones[i]);
            }
        }
        return sum - 2 * dp[target];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``

## 494. 目标和
题目链接：[https://leetcode.com/problems/target-sum/](https://leetcode.com/problems/target-sum/)

思路：基本思路是01背包，但是这道题不一样的点在于它是计算排列组合的次数。

答案：

```java
class Solution {
    public int findTargetSumWays(int[] nums, int target) {
        int sum = 0;
        for (int i : nums) sum += i;
        if ((sum + target) % 2 != 0) return 0;
        if (target < 0 && sum < -target) return 0;
        int pos = (sum + target)/ 2;
        if (pos < 0) pos = -pos;
 
        int[] table = new int[pos + 1];
        table[0] = 1;
        for (int i = 0; i < nums.length; i++) {
            for (int j = pos; j >= nums[i]; j--) {
                table[j] += table[j - nums[i]];
            }
        }
        return table[pos];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``

## 474.一和零
题目链接：[https://leetcode.com/problems/ones-and-zeroes/](https://leetcode.com/problems/ones-and-zeroes/)

思路：基本思路是01背包。

答案：

```java
class Solution {
    public int findMaxForm(String[] strs, int m, int n) {
        int[][] table = new int[m + 1][n + 1];
        for (int i = 0; i < m; i++) table[i][0] = 0;
        for (int i = 0; i < n; i++) table[0][i] = 0;

        for (int i = 0; i < strs.length; i++) {
            int num_1 = 0;
            int num_0 = 0;
            for (int l = 0; l < strs[i].length(); l++) {
                if (strs[i].charAt(l) == '0') num_0++;
                else num_1++;
            }
            for (int j = m; j >= num_0; j--) {
                for (int k = n; k >= num_1; k--) {
                    table[j][k] = Math.max(table[j - num_0][k - num_1] + 1, table[j][k]);
                }
            }
        }
        return table[m][n];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``
