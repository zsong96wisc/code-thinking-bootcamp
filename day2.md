# 代码随想录算法训练营第二天| 977.有序数组的平方 ，209.长度最小的子数组 ，59.螺旋矩阵II
作者：Zhiwei Song 
日期：2023-05-25

## 977.有序数组的平方
题目链接： [https://leetcode.com/problems/squares-of-a-sorted-array/](https://leetcode.com/problems/squares-of-a-sorted-array/)

思路：在做之前并没有想到双指针做法，然后想到后想着去找正数和负数的临界点，然后两个指针向外推进。但是听完carl的讲解后，发现可以从两头开始向中间移动，
然后填的新的数组是从大到小排的。此题需要二刷。

答案：

```java
class Solution {
    public int[] sortedSquares(int[] nums) {
        int[] result = new int[nums.length];
        int left = 0;
        int right = nums.length - 1;
        int pointer = nums.length - 1;

        while(left <= right){
            if (Math.abs(nums[left]) > Math.abs(nums[right])){
                result[pointer--] = nums[left] * nums[left];
                left++;
            } else {
                result[pointer--] = nums[right] * nums[right];
                right--;
            }
        }

        return result;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 209.长度最小的子数组
题目链接：[https://leetcode.com/problems/minimum-size-subarray-sum/](https://leetcode.com/problems/minimum-size-subarray-sum/)

思路：这道题一开始真的没有想出来有什么好的解法，后来看到karl讲解的滑动窗口，非常的清晰。对于取最小区间的问题，可以用滑动窗口来做。需要二刷。

答案：

```java
class Solution {
    public int minSubArrayLen(int target, int[] nums) {
        int start = 0;
        int sum = 0; 
        int len = Integer.MAX_VALUE;

        for (int end = 0; end < nums.length; end++){
            sum += nums[end];

            while (sum >= target){
                int si = end - start + 1;
                len = Math.min(si, len);
                sum -= nums[start++];
            }
        }
        return len == Integer.MAX_VALUE ? 0 : len;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 59.螺旋矩阵II
题目链接：[https://leetcode.com/problems/spiral-matrix-ii/](https://leetcode.com/problems/spiral-matrix-ii/)

思路：这道题目就是要看每一个边是左开右闭的算法。以及要判断这个要转几圈。要转``loop++ < n/2``圈。如果``n``是奇数，要填坐中间的数字。需要二刷。

答案：

```java
class Solution {
    public int[][] generateMatrix(int n) {
        int[][] result = new int[n][n];
        int loop = 0;
        int num = 1;
        int curlen = n;

        while (loop++ < n/2){
            for (int i = 0; i < curlen - 1; i++){
                result[loop-1][loop-1+i] = num++;
            }

            for (int i = 0; i < curlen - 1; i++){
                result[loop-1+i][n-loop] = num++;
            }

            for (int i = 0; i < curlen - 1; i++){
                result[n-loop][n-loop-i] = num++;
            }

            for (int i = 0; i < curlen - 1; i++){
                result[n-loop-i][loop-1] = num++;
            }
            curlen-=2;
        }
        if (n%2 == 1) result[n/2][n/2] = num;
        return result;
    }
}
```
