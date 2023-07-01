# 代码随想录算法训练营第三十四天| 1005.K次取反后最大化的数组和 ，134. 加油站 ，45.跳跃游戏II
作者：Zhiwei Song 
日期：2023-06-26

## 1005.K次取反后最大化的数组和
题目链接：[https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/](https://leetcode.com/problems/maximize-sum-of-array-after-k-negations/)

思路：需要按照数组的绝对值大小来排列。

答案：

```java
class Solution {
    public int largestSumAfterKNegations(int[] nums, int k) {
        nums = IntStream.of(nums)
		     .boxed()
		     .sorted((o1, o2) -> Math.abs(o2) - Math.abs(o1))
		     .mapToInt(Integer::intValue).toArray();
            
        for (int i = 0; i < nums.length; i++) {
            if (nums[i] < 0 && k > 0) {
                nums[i] = -nums[i];
                k--;
            }
        }

        if (k % 2 == 1) nums[nums.length - 1] = -nums[nums.length - 1];
        return sum(nums);
    }

    private int sum(int[] nums) {
        int res = 0;
        for (int i : nums) res += i;
        return res;
    }
}
```

时间复杂度：``O(nlogn)``, 空间复杂度：``O(1)``

## 134. 加油站
题目链接：[https://leetcode.com/problems/gas-station/](https://leetcode.com/problems/gas-station/)

思路：这道题的解题思路比较奇特，从0点出发，如果途中遇到了负油的情况，就从下一个站出发。需要二刷！

答案：

```java
class Solution {
    public int canCompleteCircuit(int[] gas, int[] cost) {
        int curSum = 0;
        int totalSum = 0;
        int start = 0;

        for (int i = 0; i < gas.length; i++) {
            curSum += gas[i] - cost[i];
            totalSum += gas[i] - cost[i];
            if (curSum < 0) {
                start = i + 1;
                curSum = 0;
            }
        }
        if (totalSum < 0) return -1;
        return start;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 135. 分发糖果
题目链接：[https://leetcode.com/problems/candy/](https://leetcode.com/problems/candy/)

思路：从左往右greedy一遍，然后从右向左greedy一遍。

答案：

```java
class Solution {
    public int candy(int[] ratings) {
        int[] res = new int[ratings.length];
        res[0] = 1;
        for (int i = 0; i < res.length - 1; i++) {
            if (ratings[i + 1] > ratings[i]) res[i + 1] = res[i] + 1;
            else res[i + 1] = 1;
        }
        for (int i = res.length - 2; i >= 0; i--) {
            if (ratings[i] > ratings[i + 1]) res[i] = Math.max(res[i + 1] + 1, res[i]);
        }
        int sum = 0;
        for (int i : res) sum += i;
        return sum;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

