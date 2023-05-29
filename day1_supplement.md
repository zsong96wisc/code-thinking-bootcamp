# 代码随想录算法训练营第一天（额外练习）| 35. Search Insert Position 、34. Find First and Last Position of Element in Sorted Array
作者：Zhiwei Song 
日期：2023-05-29

## 35. Search Insert Position
题目链接： [https://leetcode.com/problems/search-insert-position/](https://leetcode.com/problems/search-insert-position/)

思路：这道题是二分法查找的一个变体。在二分法查找的基础上，如果没有找到，就要去返回插入的位置。这个插入的位置是``return left``。因为while loop循环的结束是``left > right``，所以这个left就指向了要插入的位置。

答案：

```java
class Solution {
    public int searchInsert(int[] nums, int target) {
        int left = 0;
        int right = nums.length - 1;

        while (left <= right) {
            int mid = left + (right - left) / 2;
            if (target < nums[mid]) right = mid - 1;
            else if (target > nums[mid]) left = mid + 1;
            else return mid;
        }
        return left;
    }
}
```

时间复杂度：``O(log(n))``, 空间复杂度：``O(1)``

## 34. Find First and Last Position of Element in Sorted Array
题目链接：[https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/](https://leetcode.com/problems/find-first-and-last-position-of-element-in-sorted-array/)

思路：这道题考验的是如何找到两边的临界点。答案抄的tutorial的。需要二刷。

答案：

```java
class Solution {
    public int[] searchRange(int[] nums, int target) {
        int leftpos = findoccurence(nums, target, true);
        if (leftpos == -1) return new int[] {-1,-1};
        int rightpos = findoccurence(nums, target, false);
        return new int[] {leftpos, rightpos};
    }

    private int findoccurence(int[] nums, int target, boolean isFirst) {
        int begin = 0, end = nums.length - 1;

        while (begin <= end) {
            int mid = (begin + end) / 2;
            
            if (nums[mid] == target) {
                if (isFirst) {
                    if (mid == begin || nums[mid - 1] != target) {
                        return mid;
                    }
                    end = mid - 1;
                } else {
                    if (mid == end || nums[mid + 1] != target) {
                        return mid;
                    }
                    begin = mid + 1;
                }
            } else if (nums[mid] > target) {
                end = mid - 1;
            } else {
                begin = mid + 1;
            }
        }
        return -1;
    }
}
```

时间复杂度：``O(log(n))``, 空间复杂度：``O(1)``
