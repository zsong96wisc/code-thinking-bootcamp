# 代码随想录算法训练营第四十三天| 518. 零钱兑换 II ， 377. 组合总和 Ⅳ
作者：Zhiwei Song 
日期：2023-07-06

## 518. 零钱兑换 II
题目链接：[https://leetcode.com/problems/coin-change-ii/](https://leetcode.com/problems/coin-change-ii/)

思路：完全背包就是每一个物品都可以放无限次。所以我们要从前往后遍历。如果先遍历物品，物品放入顺序就是固定的。

答案：

```java
class Solution {
    public int change(int amount, int[] coins) {
        int[] table = new int[amount + 1];
        table[0] = 1;
        for (int i = 0; i < coins.length; i++) {
            for (int j = 1; j < amount + 1; j++) {
                if (j >= coins[i]) table[j] += table[j - coins[i]];
            }
        }
        return table[amount];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``

## 377. 组合总和 Ⅳ
题目链接：[https://leetcode.com/problems/combination-sum-iv/](https://leetcode.com/problems/combination-sum-iv/)

思路：如果是排列组合，那么就需要先遍历背包，再遍历物品。

答案：

```java
class Solution {
    public int combinationSum4(int[] nums, int target) {
        int[] table = new int[target + 1];
        table[0] = 1;
        for (int i = 0; i < target + 1; i++) {
            for (int j = 0; j < nums.length; j++) {
                if (i >= nums[j]) table[i] += table[i - nums[j]];
            }
        }
        return table[target];
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``
