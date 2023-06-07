# 代码随想录算法训练营第十五天| 102.二叉树的层序遍历 ， 107.二叉树的层次遍历II ， 199.二叉树的右视图 ， 637.二叉树的层平均值 ， 429.N叉树的层序遍历 ， 
# 515.在每个树行中找最大值 ， 116.填充每个节点的下一个右侧节点指针 ， 117.填充每个节点的下一个右侧节点指针II ， 104.二叉树的最大深度 ， 111.二叉树的最小深度
# 226.翻转二叉树 ， 101.对称二叉树
作者：Zhiwei Song
日期：2023-06-07

## 102.二叉树的层序遍历
题目链接： [https://leetcode.com/problems/binary-tree-level-order-traversal/](https://leetcode.com/problems/binary-tree-level-order-traversal/)

思路：层序遍历运用的是queue的结构，但是要去保存每一层有多少个元素，然后里面loop的时候的次数就是当前层有多少个元素。需要二刷！

答案：

```java
class Solution {
    public List<List<Integer>> levelOrder(TreeNode root) {
        Deque<TreeNode> deque = new LinkedList<>();
        List<List<Integer>> res = new ArrayList<>();

        if (root != null) deque.addLast(root);

        while (!deque.isEmpty()) {
            int size = deque.size();
            List<Integer> level_res = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                TreeNode cur = deque.removeFirst();
                level_res.add(cur.val);
                if (cur.left != null) deque.addLast(cur.left);
                if (cur.right != null) deque.addLast(cur.right);
            }
            res.add(level_res);
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 107.二叉树的层次遍历II
题目链接：[https://leetcode.com/problems/binary-tree-level-order-traversal-ii](https://leetcode.com/problems/binary-tree-level-order-traversal-ii)

思路：层序遍历运用的是queue的结构，但是要去保存每一层有多少个元素，然后里面loop的时候的次数就是当前层有多少个元素。最后需要反转list。

答案：

```java
class Solution {
    public List<List<Integer>> levelOrderBottom(TreeNode root) {
        List<List<Integer>> res = new ArrayList<>();
        Deque<TreeNode> deque = new LinkedList<>();

        if (root != null) deque.addLast(root);

        while (!deque.isEmpty()) {
            int size = deque.size();
            List<Integer> level_res = new ArrayList<>();
            while (size-- > 0) {
                TreeNode cur = deque.pop();
                level_res.add(cur.val);
                if (cur.left != null) deque.addLast(cur.left);
                if (cur.right != null) deque.addLast(cur.right);
            }
            res.add(level_res);
        }

        Collections.reverse(res);
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 199.二叉树的右视图
题目链接：[https://leetcode.com/problems/binary-tree-right-side-view/](https://leetcode.com/problems/binary-tree-right-side-view/)

思路：层序遍历运用的是queue的结构，但是要去保存每一层有多少个元素，然后里面loop的时候的次数就是当前层有多少个元素。

答案：

```java
class Solution {
    public List<Integer> rightSideView(TreeNode root) {
        Deque<TreeNode> deque = new LinkedList<>();
        List<Integer> res = new ArrayList<>();

        if (root != null) deque.addLast(root);

        while (!deque.isEmpty()) {
            int size = deque.size();
            for (int i = 0; i < size; i++) {
                TreeNode cur = deque.removeFirst();
                if (i == size - 1) res.add(cur.val);
                if (cur.left != null) deque.addLast(cur.left);
                if (cur.right != null) deque.addLast(cur.right);
            }
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 637.二叉树的层平均值
题目链接：[https://leetcode.com/problems/average-of-levels-in-binary-tree/](https://leetcode.com/problems/average-of-levels-in-binary-tree/)

思路：层序遍历运用的是queue的结构，但是要去保存每一层有多少个元素，然后里面loop的时候的次数就是当前层有多少个元素。

答案：

```java
class Solution {
    public List<Double> averageOfLevels(TreeNode root) {
        Deque<TreeNode> deque = new LinkedList<>();
        List<Double> res = new ArrayList<>();

        if (root != null) deque.addLast(root);

        while (!deque.isEmpty()) {
            int size = deque.size();
            double sum = 0;
            for (int i = 0; i < size; i++) {
                TreeNode cur = deque.removeFirst();
                sum += (double)cur.val;
                if (cur.left != null) deque.addLast(cur.left);
                if (cur.right != null) deque.addLast(cur.right);
            }
            res.add(sum / size);
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 429.N叉树的层序遍历
题目链接：[https://leetcode.com/problems/n-ary-tree-level-order-traversal/](https://leetcode.com/problems/n-ary-tree-level-order-traversal/)

思路：层序遍历运用的是queue的结构，但是要去保存每一层有多少个元素，然后里面loop的时候的次数就是当前层有多少个元素。

答案：

```java
class Solution {
    public List<List<Integer>> levelOrder(Node root) {
        Deque<Node> deque = new LinkedList<>();
        List<List<Integer>> res = new ArrayList<>();

        if (root != null) deque.addLast(root);

        while (!deque.isEmpty()) {
            int size = deque.size();
            List<Integer> level_res = new ArrayList<>();
            for (int i = 0; i < size; i++) {
                Node cur = deque.removeFirst();
                level_res.add(cur.val);
                for (Node child : cur.children) {
                    deque.addLast(child);
                }
            }
            res.add(level_res);
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 515.在每个树行中找最大值
题目链接：[https://leetcode.com/problems/find-largest-value-in-each-tree-row/](https://leetcode.com/problems/find-largest-value-in-each-tree-row/)

思路：层序遍历运用的是queue的结构，但是要去保存每一层有多少个元素，然后里面loop的时候的次数就是当前层有多少个元素。

答案：

```java
class Solution {
    public List<Integer> largestValues(TreeNode root) {
        Deque<TreeNode> deque = new LinkedList<>();
        List<Integer> res = new ArrayList<>();

        if (root != null) deque.addLast(root);

        while (!deque.isEmpty()) {
            int size = deque.size();
            int max = Integer.MIN_VALUE;
            for (int i = 0; i < size; i++) {
                TreeNode cur = deque.removeFirst();
                if (cur.val > max) max = cur.val;
                if (cur.left != null) deque.addLast(cur.left);
                if (cur.right != null) deque.addLast(cur.right);
            }
            res.add(max);
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 116.填充每个节点的下一个右侧节点指针
题目链接：[https://leetcode.com/problems/populating-next-right-pointers-in-each-node/](https://leetcode.com/problems/populating-next-right-pointers-in-each-node/)

思路：层序遍历运用的是queue的结构，但是要去保存每一层有多少个元素，然后里面loop的时候的次数就是当前层有多少个元素。

答案：

```java
class Solution {
    public Node connect(Node root) {
        Deque<Node> deque = new LinkedList<>();

        if (root != null) deque.addLast(root);

        while (!deque.isEmpty()) {
            int size = deque.size();
            for (int i = 0; i < size; i++) {
                Node cur1 = deque.removeFirst();
                if (i != size - 1) {
                    Node cur2 = deque.peekFirst();
                    cur1.next = cur2;
                }
                if (cur1.left != null) deque.addLast(cur1.left);
                if (cur1.right != null) deque.addLast(cur1.right);
            }
        }
        return root;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 117.填充每个节点的下一个右侧节点指针II
题目链接：[https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/](https://leetcode.com/problems/populating-next-right-pointers-in-each-node-ii/)

思路：同题目116

答案：

```java
class Solution {
    public Node connect(Node root) {
        Deque<Node> deque = new LinkedList<>();

        if (root != null) deque.addLast(root);

        while (!deque.isEmpty()) {
            int size = deque.size();
            for (int i = 0; i < size; i++) {
                Node cur1 = deque.removeFirst();
                if (i != size - 1) {
                    Node cur2 = deque.peekFirst();
                    cur1.next = cur2;
                }
                if (cur1.left != null) deque.addLast(cur1.left);
                if (cur1.right != null) deque.addLast(cur1.right);
            }
        }
        return root;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 104.二叉树的最大深度
题目链接：[https://leetcode.com/problems/maximum-depth-of-binary-tree/](https://leetcode.com/problems/maximum-depth-of-binary-tree/)

思路：层序遍历运用的是queue的结构，但是要去保存每一层有多少个元素，然后里面loop的时候的次数就是当前层有多少个元素。

答案：

```java
class Solution {
    public int maxDepth(TreeNode root) {
        Deque<TreeNode> deque = new LinkedList<>();
        int res = 0;

        if (root != null) deque.addLast(root);

        while (!deque.isEmpty()) {
            int size = deque.size();
            for (int i = 0; i < size; i++) {
                TreeNode cur = deque.removeFirst();
                if (cur.left != null) deque.addLast(cur.left);
                if (cur.right != null) deque.addLast(cur.right);
            }
            res++;
        }
        return res;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 111.二叉树的最小深度
题目链接：[https://leetcode.com/problems/minimum-depth-of-binary-tree/](https://leetcode.com/problems/minimum-depth-of-binary-tree/)

思路：层序遍历运用的是queue的结构，但是要去保存每一层有多少个元素，然后里面loop的时候的次数就是当前层有多少个元素。

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

## 226.翻转二叉树
题目链接：[https://leetcode.com/problems/invert-binary-tree/](https://leetcode.com/problems/invert-binary-tree/)

思路：这道题只能用BFS和前后顺序遍历，不用用中序遍历，因为在处理子节点的时候，左右的child已经互换了。

答案：

```java
class Solution {
    public TreeNode invertTree(TreeNode root) {
        Deque<TreeNode> deque = new LinkedList<>();
        if (root != null) deque.addLast(root);

        while (!deque.isEmpty()) {
            TreeNode cur = deque.removeFirst();
            if (cur.left != null) deque.addLast(cur.left);
            if (cur.right != null) deque.addLast(cur.right);
            TreeNode swap = cur.left;
            cur.left = cur.right;
            cur.right = swap;
        }

        return root;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 101.对称二叉树
题目链接：[https://leetcode.com/problems/symmetric-tree/](https://leetcode.com/problems/symmetric-tree/)

思路：比较左右两棵subtree。

答案：

```java
class Solution {
    public boolean isSymmetric(TreeNode root) {
        return check(root, root);
    }

    public boolean check(TreeNode node1, TreeNode node2) {
        if (node1 == null || node2 == null) {
            if (node1 == null && node2 == null) return true;
            else return false;
        }
        
        if (node1.val != node2.val) return false;
        return check(node1.left, node2.right) && check(node1.right, node2.left);
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``
