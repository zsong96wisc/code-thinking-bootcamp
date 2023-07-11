# 代码随想录算法训练营第四十六天| 198.打家劫舍 ， 213.打家劫舍II ， 337.打家劫舍III
作者：Zhiwei Song 
日期：2023-07-10

## 198.打家劫舍
题目链接：[https://leetcode.com/problems/house-robber/](https://leetcode.com/problems/house-robber/)

思路：递推公式是要么第i天偷，那就是第i-2天加上第i天。要么第i天不偷，就是跟第i-1天一样。

答案：

```java
class Solution {
    public int rob(int[] nums) {
        if (nums.length == 1) return nums[0];
        int[] table = new int[nums.length];
        table[0] = nums[0];
        table[1] = Math.max(nums[0], nums[1]);

        for (int i = 2; i < table.length; i++) {
            table[i] = Math.max(table[i - 1], table[i - 2] + nums[i]);
        }

        return table[nums.length - 1];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``

## 213.打家劫舍II
题目链接：[https://leetcode.com/problems/house-robber-ii/](https://leetcode.com/problems/house-robber-ii/)

思路：这个就是要么从第0天到第i-1天，要么从第1天到第i天。

答案：

```java
class Solution {
    public int rob(int[] nums) {
        if (nums == null || nums.length == 0)
            return 0;
        int len = nums.length;
        if (len == 1)
            return nums[0];
        return Math.max(robRange(nums, 0, len - 2), robRange(nums, 1, len - 1));
    }

    int robRange(int[] nums, int start, int end) {
        if (end == start) return nums[start];
        int[] dp = new int[nums.length];
        dp[start] = nums[start];
        dp[start + 1] = Math.max(nums[start], nums[start + 1]);
        for (int i = start + 2; i <= end; i++) {
            dp[i] = Math.max(dp[i - 2] + nums[i], dp[i - 1]);
        }
        return dp[end];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``

## 337.打家劫舍III
题目链接：[https://leetcode.com/problems/house-robber-iii/](https://leetcode.com/problems/house-robber-iii/)

思路：注意后续遍历。

答案：

```java
class Solution {
    public int rob(TreeNode root) {
        int[] res = robAction1(root);
        return Math.max(res[0], res[1]);
    }

    int[] robAction1(TreeNode root) {
        int res[] = new int[2];
        if (root == null)
            return res;

        int[] left = robAction1(root.left);
        int[] right = robAction1(root.right);

        res[0] = Math.max(left[0], left[1]) + Math.max(right[0], right[1]);
        res[1] = root.val + left[0] + right[0];
        return res;
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``
