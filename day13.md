# 代码随想录算法训练营第十三天|  239. 滑动窗口最大值 ， 347.前 K 个高频元素 
作者：Zhiwei Song 
日期：2023-06-05

## 239. 滑动窗口最大值
题目链接： [https://leetcode.com/problems/sliding-window-maximum/](https://leetcode.com/problems/sliding-window-maximum/)

思路：这道题我是直接去看视频，了解单调队列的思路。https://programmercarl.com/0239.%E6%BB%91%E5%8A%A8%E7%AA%97%E5%8F%A3%E6%9C%80%E5%A4%A7%E5%80%BC.html。
需要二刷！！！

答案：

```java
class Solution {
    public int[] maxSlidingWindow(int[] nums, int k) {
        if (nums.length == 1) {
            return nums;
        }

        int[] res = new int[nums.length - k + 1];
        int num = 0;

        MyQueue myQueue = new MyQueue();
        for (int i = 0; i < k; i++) {
            myQueue.add(nums[i]);
        }
        res[num++] = myQueue.peek();

        for (int i = k; i < nums.length; i++) {
            myQueue.poll(nums[i - k]);
            myQueue.add(nums[i]);
            res[num++] = myQueue.peek();
        }

        return res;
    }
}

class MyQueue {
    Deque<Integer> deque = new LinkedList<>();

    void poll(int val) {
        if (!deque.isEmpty() && deque.peekFirst() == val)
            deque.pollFirst();
    }

    void add(int val) {
        while(!deque.isEmpty() && deque.peekLast() < val) 
            deque.pollLast();
        deque.addLast(val);
    }

    int peek() {
        return deque.peekFirst();
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 347.前 K 个高频元素
题目链接：[https://leetcode.com/problems/top-k-frequent-elements/](https://leetcode.com/problems/top-k-frequent-elements/)

思路：这道题我是直接去看了视频，在选用大顶堆还是小顶堆上的抉择非常的聪明，这个需要在二刷的时候去继续学习的。
https://programmercarl.com/0347.%E5%89%8DK%E4%B8%AA%E9%AB%98%E9%A2%91%E5%85%83%E7%B4%A0.html。 需要二刷！！！

答案：

```java
class Solution {
    public int[] topKFrequent(int[] nums, int k) {
        PriorityQueue<int[]> pq = new PriorityQueue<>((o1, o2) -> o1[1] - o2[1]);
        Map<Integer, Integer> map = new HashMap<>();
        int[] res = new int[k];

        for(int num : nums) map.put(num, map.getOrDefault(num, 0) + 1);

        for(var x : map.entrySet()) {
            int[] tmp = new int[2];
            tmp[0] = x.getKey();
            tmp[1] = x.getValue();
            pq.offer(tmp);
            if (pq.size() > k) {
                pq.poll();
            }
        }

        for(int i = 0; i < k; i ++) {
            res[i] = pq.poll()[0];
        }
        return res;
    }
}
```

时间复杂度：``O(nlogk)``, 空间复杂度：``O(n+k)``
