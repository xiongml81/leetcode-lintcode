# 113 Path Sum II



```java
/**
 * Definition for a binary tree node.
 * public class TreeNode {
 *     int val;
 *     TreeNode left;
 *     TreeNode right;
 *     TreeNode() {}
 *     TreeNode(int val) { this.val = val; }
 *     TreeNode(int val, TreeNode left, TreeNode right) {
 *         this.val = val;
 *         this.left = left;
 *         this.right = right;
 *     }
 * }
 */
class Solution {
    public List<List<Integer>> pathSum(TreeNode root, int targetSum) {
        List<List<Integer>> res = new ArrayList<>();
        List<Integer> cur = new ArrayList<>();
        dfs(root, targetSum, res, cur);
        return res;
    }
    
    public void dfs(TreeNode root, int targetSum, List<List<Integer>> res, List<Integer> cur){
        if(root == null){
            return;
        }
        
        
         if(root != null && root.left == null && root.right == null){
            if(targetSum == root.val){
                cur.add(root.val);
                res.add(new ArrayList<Integer>(cur));
                cur.remove(cur.size() - 1);
                return;
            }
            return;
        }
        
        
        cur.add(root.val);
        dfs(root.left, targetSum - root.val, res, cur);
        dfs(root.right, targetSum - root.val, res, cur);
        cur.remove(cur.size() - 1);
        
        
    }
}
```

