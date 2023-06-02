# 代码随想录算法训练营第十天| 232.用栈实现队列 ，225. 用队列实现栈
作者：Zhiwei Song 
日期：2023-06-02

## 232.用栈实现队列
题目链接： [https://leetcode.com/problems/implement-queue-using-stacks/](https://leetcode.com/problems/implement-queue-using-stacks/)

思路：注意pop的时候要把第一个list里面的东西都放到第二个stack里面

答案：

```java
class MyQueue {

    Stack<Integer> first;
    Stack<Integer> second;

    public MyQueue() {
        first = new Stack<>();
        second = new Stack<>();
    }
    
    public void push(int x) {
        first.push(x);
    }
    
    public int pop() {
        if (!second.isEmpty()) return second.pop();
        else {
            if (first.isEmpty()) return -1;
            else {
                while (!first.isEmpty()) second.push(first.pop());
            }
            return second.pop();
        }
    }
    
    public int peek() {
        if (!second.isEmpty()) return second.peek();
        else {
            if (first.isEmpty()) return -1;
            else {
                while (!first.isEmpty()) second.push(first.pop());
            }
            return second.peek();
        }
    }
    
    public boolean empty() {
        return first.isEmpty() && second.isEmpty();
    }
}

/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```

## 225. 用队列实现栈
题目链接：[https://leetcode.com/problems/implement-stack-using-queues/](https://leetcode.com/problems/implement-stack-using-queues/)

思路：用一个queue就能完成。

答案：

```java
class MyStack {

    Queue<Integer> first;

    public MyStack() {
        first = new LinkedList<>();
    }
    
    public void push(int x) {
        first.add(x);
    }
    
    public int pop() {
        for (int i = 1; i < first.size(); i++) {
            first.add(first.poll());
        }
        return first.poll();
    }
    
    public int top() {
        for (int i = 1; i < first.size(); i++) {
            first.add(first.poll());
        }
        int result = first.poll();
        first.add(result);
        return result;
    }
    
    public boolean empty() {
        return first.isEmpty();
    }
}

/**
 * Your MyStack object will be instantiated and called as such:
 * MyStack obj = new MyStack();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.top();
 * boolean param_4 = obj.empty();
 */
```
