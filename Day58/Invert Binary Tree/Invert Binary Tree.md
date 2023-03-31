# 226. Invert Binary Tree

Given the root of a binary tree, invert the tree, and return its root.

**Example 1:**

<img src="https://assets.leetcode.com/uploads/2021/03/14/invert1-tree.jpg" alt="img" style="height: 200px; width: 400px;"/>

```
Input: root = [4,2,7,1,3,6,9]
Output: [4,7,2,9,6,3,1]
```
**Example 2:**

<img src="https://assets.leetcode.com/uploads/2021/03/14/invert2-tree.jpg" alt="img" style="height: 200px; width: 400px;"/>

```
Input: root = [2,1,3]
Output: [2,3,1]
```
**Example 3:**
```
Input: root = []
Output: []
``` 

**Constraints:**

* The number of nodes in the tree is in the range `[0, 100]`.
* `-100 <= Node.val <= 100`

**Solution:**
```
class Solution {
    public void swap(TreeNode curr) {
        if(curr == null) {
            return;
        }

        swap(curr.left);
        swap(curr.right);

        TreeNode temp;
        temp = curr.left;
        curr.left = curr.right;
        curr.right = temp;
    }

    public TreeNode invertTree(TreeNode root) {
        swap(root);
        return root;
    }
}
```