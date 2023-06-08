# 代码随想录算法训练营第十六天| 104.二叉树的最大深度 ， 111.二叉树的最小深度 ， 222.完全二叉树的节点个数 
作者：Zhiwei Song 
日期：2023-06-08

## 104.二叉树的最大深度
题目链接：[https://leetcode.com/problems/maximum-depth-of-binary-tree/](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

思路：递归，常规题。需要二刷。

答案：

```java
class Solution {
    public int maxDepth(TreeNode root) {
        return getDepth(root);
    }

    public int getDepth(TreeNode node) {
        if (node == null) return 0;
        return Math.max(getDepth(node.left), getDepth(node.right)) + 1;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 111.二叉树的最小深度
题目链接：[https://leetcode.com/problems/minimum-depth-of-binary-tree/](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

思路：注意如果一个node只有一个child是null，不能用min function，而是返回不是null的child的值。

答案：

```java
class Solution {
    public int minDepth(TreeNode root) {
        Deque<TreeNode> deque = new LinkedList<>();
        int res = 0;

        if (root != null) deque.addLast(root);

        while (!deque.isEmpty()) {
            int size = deque.size();
            for (int i = 0; i < size; i++) {
                TreeNode cur = deque.removeFirst();
                if (cur.left != null) deque.addLast(cur.left);
                if (cur.right != null) deque.addLast(cur.right);
                if (cur.left == null && cur.right == null) return res + 1;
            }
            res++;
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 222.完全二叉树的节点个数
题目链接：[https://leetcode.com/problems/count-complete-tree-nodes/](https://leetcode.com/problems/count-complete-tree-nodes/)

思路：这个解题思路学习了Karl的视频。详见：https://programmercarl.com/0222.%E5%AE%8C%E5%85%A8%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E8%8A%82%E7%82%B9%E4%B8%AA%E6%95%B0.html
需要二刷！

答案：

```java
class Solution {
    public int countNodes(TreeNode root) {
        return count(root);
    }

    private int count(TreeNode node) {
        if (node == null) return 0;
        TreeNode left = node.left;
        TreeNode right = node.right;
        int leftDepth = 0; int rightDepth = 0;
        
        while (left != null) {
            left = left.left;
            leftDepth++;
        }

        while (right != null) {
            right = right.right;
            rightDepth++;
        }

        if (leftDepth == rightDepth) {
            return (int)(Math.pow(2, leftDepth + 1)) - 1;
        } else {
            return count(node.left) + count(node.right) + 1;
        }
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``
