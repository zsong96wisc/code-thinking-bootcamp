# 代码随想录算法训练营第三十二天| 122.买卖股票的最佳时机II ，55. 跳跃游戏 ，45.跳跃游戏II
作者：Zhiwei Song 
日期：2023-06-23

## 122.买卖股票的最佳时机II
题目链接：[https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/](https://leetcode.com/problems/best-time-to-buy-and-sell-stock-ii/)

思路：简单greedy。

答案：

```java
class Solution {
    public int maxProfit(int[] prices) {
        int res = 0;
        for (int i = 1; i < prices.length; i++) {
            if (prices[i] - prices[i - 1] > 0) res += prices[i] - prices[i - 1];
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 55. 跳跃游戏
题目链接：[https://leetcode.com/problems/jump-game/](https://leetcode.com/problems/jump-game/)

思路：记录当前能到的最大长度。

答案：

```java
class Solution {
    public boolean canJump(int[] nums) {
        int max = 0;
        int i = 0;
        while (i <= max) {
            if (max >= nums.length - 1) return true;
            max = Math.max(i + nums[i], max);
            i++;
        }
        return false;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 45.跳跃游戏II
题目链接：[https://leetcode.com/problems/jump-game-ii/](https://leetcode.com/problems/jump-game-ii/)

思路：需要每一层去track一下终点。

答案：

```java
class Solution {
    public int jump(int[] nums) {
        int cur = 0;
        int next = 0;
        int res = 0;

        for (int i = 0; i < nums.length; i++) {
            next = Math.max(nums[i] + i, next);
            if (i == cur) {
                if (i != nums.length - 1) {
                    cur = next;
                    res++;
                }
                if (cur >= nums.length - 1) break;
            }
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

