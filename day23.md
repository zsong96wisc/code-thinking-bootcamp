# 代码随想录算法训练营第二十三天| 669. 修剪二叉搜索树 ， 108.将有序数组转换为二叉搜索树 ， 538.把二叉搜索树转换为累加树 
作者：Zhiwei Song 
日期：2023-06-15

## 669. 修剪二叉搜索树
题目链接：[https://leetcode.com/problems/trim-a-binary-search-tree/](https://leetcode.com/problems/trim-a-binary-search-tree/)

思路：这道题借鉴了karl的思路，主要是怎么处理recursion返回的值，需要二刷。

答案：

```java
class Solution {
    public TreeNode trimBST(TreeNode root, int low, int high) {
        if (root == null) return null;
        if (root.val < low) return trimBST(root.right, low, high);
        if (root.val > high) return trimBST(root.left, low, high);
        root.left = trimBST(root.left, low, high);
        root.right = trimBST(root.right, low, high);
        return root;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 701.二叉搜索树中的插入操作 
题目链接：[https://leetcode.com/problems/insert-into-a-binary-search-tree/](https://leetcode.com/problems/insert-into-a-binary-search-tree/)

思路：搜索二叉树插入节点只能插在leaf上面。

答案：

```java
class Solution {
    public TreeNode insertIntoBST(TreeNode root, int val) {
        if (root == null) return new TreeNode(val);
        if (root.val > val) root.left = insertIntoBST(root.left, val);
        else root.right = insertIntoBST(root.right, val);
        return root;
    }
}
```

时间复杂度：``O(log(n))``, 空间复杂度：``O(log(n))``

## 108.将有序数组转换为二叉搜索树
题目链接：[https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/](https://leetcode.com/problems/convert-sorted-array-to-binary-search-tree/)

思路：从中间不断的二分来创造树。注意终止条件。

答案：

```java
class Solution {
    public TreeNode sortedArrayToBST(int[] nums) {
        return helper(nums, 0, nums.length);
    }

    private TreeNode helper(int[] nums, int left, int right) {
        if (left >= right) return null;
        TreeNode node = new TreeNode(nums[(left + right) / 2]);
        node.left = helper(nums, left, (left + right) / 2);
        node.right = helper(nums, (left + right) / 2 + 1, right);
        return node;
    }
}
```

时间复杂度：``O(log(n))``, 空间复杂度：``O(log(n))``

## 538.把二叉搜索树转换为累加树
题目链接：[https://leetcode.com/problems/convert-bst-to-greater-tree/](https://leetcode.com/problems/convert-bst-to-greater-tree/)

思路：中序遍历，右中左。需要一个全局变量。

答案：

```java
class Solution {
    int i = 0;
    public TreeNode convertBST(TreeNode root) {
        helper(root);
        return root;
    }

    private void helper(TreeNode node) {
        if (node == null) return;
        helper(node.right);
        i += node.val;
        node.val = i;
        helper(node.left);
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``
