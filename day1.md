# 代码随想录算法训练营第一天| 704. 二分查找、27. 移除元素
作者：Zhiwei Song 
日期：2023-05-24

## 704. 二分查找
题目链接： [https://leetcode.com/problems/binary-search/](https://leetcode.com/problems/binary-search/)

思路：二分法的基础逻辑大部分人都懂，但是对于边界的处理不是特别懂。看完了karl的B站的视频，让我醍醐灌顶。首先是要决定合理的区间是左闭右闭，还是左开右闭。
如果是左闭右闭，那``left <= right``。然后更改left和right的值时，``left = middle + 1``和``right = middle - 1``。
如果是左闭右开，那``left < right``。然后更改left和right的值时，``left = middle + 1``和``right = middle``。

答案：

```java
class Solution {
    public int search(int[] nums, int target) {
        int begin = 0; 
        int last = nums.length - 1;

        while (begin <= last){
            int mid = (last - begin) / 2 + begin;
            if (target < nums[mid]){
                last = mid - 1;
            } else if (target > nums[mid]) {
                begin = mid + 1;
            } else return mid;
        }
        return -1;
    }
}
```

时间复杂度：``O(log(n))``, 空间复杂度：``O(1)``

## 27. 移除元素
题目链接：[https://leetcode.com/problems/remove-element/](https://leetcode.com/problems/remove-element/)

思路：我一开始给出的算法是用了双指针，一个从头开始，一个从尾开始。如果头上又不想要的数字，就跟结尾的数字调换。直到头指针和尾指针相遇。
但是carl给出了快慢指针，相当于快指针把数组都扫一遍，慢指针指向所有copy的正确的数组。

答案：

```java
class Solution {
    public int removeElement(int[] nums, int val) {
        int right = nums.length - 1;
        int left = 0;

        while (left <= right){
            if (nums[left] == val){
                nums[left] = nums[right];
                right--;
            } else left++;
        }

        return left;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
