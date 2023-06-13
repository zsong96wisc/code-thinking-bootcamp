# 代码随想录算法训练营第二十一天| 530.二叉搜索树的最小绝对差 ， 501.二叉搜索树中的众数 ， 700.二叉搜索树中的搜索 ， 98.验证二叉搜索树
作者：Zhiwei Song 
日期：2023-06-13

## 530.二叉搜索树的最小绝对差
题目链接：[https://leetcode.com/problems/minimum-absolute-difference-in-bst/](https://leetcode.com/problems/minimum-absolute-difference-in-bst/)

思路：中序遍历排一排，需要二刷！

答案：

```java
class Solution {
    int res = Integer.MAX_VALUE;
    int last = -1;
    public int getMinimumDifference(TreeNode root) {
        helper(root);
        return res;
    }

    private void helper(TreeNode node) {
        if (node == null) return;
        helper(node.left);
        if (last == -1) last = node.val;
        else if (node.val - last < res) res = node.val - last;
        last = node.val;
        helper(node.right);
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 501.二叉搜索树中的众数
题目链接：[https://leetcode.com/problems/find-mode-in-binary-search-tree/](https://leetcode.com/problems/find-mode-in-binary-search-tree/)

思路：中序遍历排一排，需要二刷！

答案：

```java
class Solution {
    ArrayList<Integer> resList;
    int maxCount;
    int count;
    TreeNode pre;

    public int[] findMode(TreeNode root) {
        resList = new ArrayList<>();
        maxCount = 0;
        count = 0;
        pre = null;
        findMode1(root);
        int[] res = new int[resList.size()];
        for (int i = 0; i < resList.size(); i++) {
            res[i] = resList.get(i);
        }
        return res;
    }

    public void findMode1(TreeNode root) {
        if (root == null) {
            return;
        }
        findMode1(root.left);

        int rootValue = root.val;
        // 计数
        if (pre == null || rootValue != pre.val) {
            count = 1;
        } else {
            count++;
        }
        // 更新结果以及maxCount
        if (count > maxCount) {
            resList.clear();
            resList.add(rootValue);
            maxCount = count;
        } else if (count == maxCount) {
            resList.add(rootValue);
        }
        pre = root;

        findMode1(root.right);
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``

## 236. 二叉树的最近公共祖先
题目链接：[https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/](https://leetcode.com/problems/lowest-common-ancestor-of-a-binary-tree/)

思路：后序遍历，需要在二刷的时候再理解一遍。

答案：

```java
class Solution {
    public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
        if (root == null) return null;
        if (root == p || root == q) return root;
        TreeNode left = lowestCommonAncestor(root.left, p, q);
        TreeNode right = lowestCommonAncestor(root.right, p ,q);
        if (left != null && right != null) return root;
        if (left == null && right != null) return right;
        else if (left != null && right == null) return left;
        return null;
    }
}
```

时间复杂度：``O(n)``, 空间复杂度：``O(n)``
