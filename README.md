# Closest Binary Search Tree Value
## https://leetcode.com/problems/closest-binary-search-tree-value

Given a non-empty binary search tree and a target value, find the value in the BST that is closest to the target.

**Note:**
1. Given target value is a floating point.
2. You are guaranteed to have only one unique value in the BST that is closest to the target.
```
Example:

Input: root = [4,2,5,1,3], target = 3.714286

    4
   / \
  2   5
 / \
1   3

Output: 4
```

# Implementation :

```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode(int x) { val = x; }
 * }
 */
class Solution {
    public int closestValue(TreeNode root, double target) {
        // Note that we are given, that BST would not be empty
        int closestValue = root.val;
        while(root != null){
            if(Math.abs(root.val - target) < Math.abs(closestValue - target))
                closestValue = root.val;
            root = target < root.val ? root.left : root.right;
        }
        return closestValue;
    }
    
}

```

# References :
https://www.youtube.com/watch?v=_sz0Y4g1Gos
