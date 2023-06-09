# 代码随想录算法训练营第十七天| 110.平衡二叉树 ， 257. 二叉树的所有路径 ， 404.左叶子之和 
作者：Zhiwei Song 
日期：2023-06-09

## 110.平衡二叉树
题目链接：[https://leetcode.com/problems/balanced-binary-tree/](https://leetcode.com/problems/balanced-binary-tree/)

思路：递归的方法，如果遇到不平衡的subtree，就要返回-1。遇到leaf node，返回0。

答案：

```java
class Solution {
    public boolean isBalanced(TreeNode root) {
        return getHeight(root) != -1;
    }

    public int getHeight(TreeNode node) {
        if (node == null) return 0;
        int leftheight = getHeight(node.left);
        if (leftheight == -1) return -1;
        int rightheight = getHeight(node.right);
        if (rightheight == -1) return -1;
        if (Math.abs(leftheight - rightheight) > 1) return -1;
        else return Math.max(leftheight, rightheight) + 1;
    }
}
```

时间复杂度：``O(nlog(n))``, 空间复杂度：``O(n)``

## 257. 二叉树的所有路径
题目链接：[https://leetcode.com/problems/binary-tree-paths/](https://leetcode.com/problems/binary-tree-paths/)

思路：用递归法，helper function中的传入参数是当前node，当前路径和存结果的list。用迭代法，需要两个stack，一个存node，一个存路径。

答案：

```java
class Solution {
    public List<String> binaryTreePaths(TreeNode root) {
        List<String> res = new ArrayList<>();
        if (root == null) return res;
        else searchPaths(root, Integer.toString(root.val), res);
        return res; 
    }
    
    private void searchPaths(TreeNode node, String path, List<String> res) {
        if (node.left == null && node.right == null) res.add(path);
        else {
            if (node.left != null) searchPaths(node.left, path + "->" + Integer.toString(node.left.val), res);
            if (node.right != null) searchPaths(node.right, path + "->" + Integer.toString(node.right.val), res);
        }
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 404.左叶子之和
题目链接：[https://leetcode.com/problems/sum-of-left-leaves/](https://leetcode.com/problems/sum-of-left-leaves/)

思路：递归的思路，如果一个节点是有左节点的leaf node，那就返回做节点leaf node的值，不然就回0。这道题看karl的解法会更好的。

答案：

```java
class Solution {
    public int sumOfLeftLeaves(TreeNode root) {
        return helper(root, false);
    }

    public int helper(TreeNode node, boolean left) {
        if (node != null && (node.left == null && node.right == null) && left) return node.val;
        if (node == null) return 0;
        return helper(node.left, true) + helper(node.right, false);
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``
