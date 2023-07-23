# 代码随想录算法训练营第五十六天| 503.下一个更大元素II ，42. 接雨水
作者：Zhiwei Song 
日期：2023-07-21

## 503.下一个更大元素II
题目链接：[https://leetcode.com/problems/next-greater-element-ii/](https://leetcode.com/problems/next-greater-element-ii/)

思路：这个还是运用了单调栈的思想。

答案：

```java
class Solution {
    public int[] nextGreaterElements(int[] nums) {
        int[] res = new int[nums.length];
        Stack<Integer> st = new Stack<>();
        Arrays.fill(res,-1);
        for(int i = 0; i < 2 * nums.length; i++) {
            while(!st.empty() && nums[i % nums.length] > nums[st.peek()]) {
                res[st.peek()] = nums[i % nums.length];//更新result
                st.pop();//弹出栈顶
            }
            st.push(i % nums.length);
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 42. 接雨水
题目链接：[https://leetcode.com/problems/trapping-rain-water/](https://leetcode.com/problems/trapping-rain-water/)

思路：题没看懂，需要二刷！

答案：

```java
class Solution {
    public int trap(int[] height) {
        int length = height.length;
        if (length <= 2) return 0;
        int[] maxLeft = new int[length];
        int[] maxRight = new int[length];

        // 记录每个柱子左边柱子最大高度
        maxLeft[0] = height[0];
        for (int i = 1; i< length; i++) maxLeft[i] = Math.max(height[i], maxLeft[i-1]);

        // 记录每个柱子右边柱子最大高度
        maxRight[length - 1] = height[length - 1];
        for(int i = length - 2; i >= 0; i--) maxRight[i] = Math.max(height[i], maxRight[i+1]);

        // 求和
        int sum = 0;
        for (int i = 0; i < length; i++) {
            int count = Math.min(maxLeft[i], maxRight[i]) - height[i];
            if (count > 0) sum += count;
        }
        return sum;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
