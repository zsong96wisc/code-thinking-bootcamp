# 代码随想录算法训练营第四十一天| 416. 分割等和子集
作者：Zhiwei Song 
日期：2023-07-04

## 416. 分割等和子集
题目链接：[https://leetcode.com/problems/partition-equal-subset-sum/](https://leetcode.com/problems/partition-equal-subset-sum/)

思路：基本思路是01背包，先把数组中的sum算出来，然后求出平均值。这个就是背包的总体积。然后不停往里面放数字，最后看table[target] == target。

答案：

```java
class Solution {
    public boolean canPartition(int[] nums) {
        int sum = 0;
        for (int i : nums) sum += i;
        if (sum % 2 != 0) return false;
        int target = sum / 2;

        int[] table = new int[target + 1];
        for (int i = 0; i < nums.length; i++) {
            for (int j = target; j >= nums[i]; j--) {
                table[j] = Math.max(table[j], table[j - nums[i]] + nums[i]);
            }
        }
        return table[target] == target;
    }
}
```

时间复杂度：``O(n^2)``, 空间复杂度：``O(n)``
