# 代码随想录算法训练营第五十五天| 739. 每日温度 ，496.下一个更大元素 I
作者：Zhiwei Song 
日期：2023-07-20

## 739. 每日温度
题目链接：[https://leetcode.com/problems/daily-temperatures/](https://leetcode.com/problems/daily-temperatures/)

思路：今天新学的单调栈，重点在于判断单调栈是递增还是递减，如果右侧找第一个比当前数大的，则用单调增栈。

答案：

```java
class Solution {
    public int[] dailyTemperatures(int[] temperatures) {
        int[] res = new int[temperatures.length];
        Stack<Integer> pq = new Stack<>();
        pq.push(0);

        for (int i = 1; i < temperatures.length; i++) {
            if (temperatures[i] <= temperatures[pq.peek()]) pq.push(i);
            else {
                while (!pq.isEmpty() && temperatures[i] > temperatures[pq.peek()]) {
                    res[pq.peek()] = i - pq.peek();
                    pq.pop();
                }
                pq.push(i);
            }
        }

        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``

## 496.下一个更大元素 I
题目链接：[https://leetcode.com/problems/next-greater-element-i/](https://leetcode.com/problems/next-greater-element-i/)

思路：单调栈 + HashMap

答案：

```java
class Solution {
    public int[] nextGreaterElement(int[] nums1, int[] nums2) {
        int[] res = new int[nums1.length];
        Stack<Integer> st = new Stack<>();
        HashMap<Integer, Integer> map = new HashMap<>();
        st.push(0);
        for (int i = 1; i < nums2.length; i++) {
            if (nums2[i] > nums2[st.peek()]) {
                while (!st.isEmpty() && nums2[i] > nums2[st.peek()]) map.put(nums2[st.pop()], nums2[i]);
            }
            st.push(i);
        }
        while (!st.isEmpty()) map.put(nums2[st.pop()], -1);
        for (int i = 0; i < nums1.length; i++) res[i] = map.get(nums1[i]);
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(1)``
