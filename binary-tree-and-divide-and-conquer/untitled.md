# 242. Convert Binary Tree to Linked Lists by Depth

[https://www.lintcode.com/problem/convert-binary-tree-to-linked-lists-by-depth/](https://www.lintcode.com/problem/convert-binary-tree-to-linked-lists-by-depth/)  


Solution 1: DFS

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    /**
     * @param root the root of binary tree
     * @return a lists of linked list
     */
    public List<ListNode> binaryTreeToLists(TreeNode root) {
        // Write your code here
        List<ListNode> res = new ArrayList<ListNode>();
        dfs(root, 1, res);
        return res;
    }

    public void dfs(TreeNode root, int depth, List<ListNode> res){
        if(root == null){
            return;
        }
        ListNode node = new ListNode(root.val);

        if(res.size() < depth){
            res.add(node);
        }
        else{
            node.next = res.get(depth - 1);
            res.set(depth - 1, node);
        }


        dfs(root.right, depth + 1, res);
        dfs(root.left, depth + 1, res);
    }
}
```

depth代表当前调用在树的哪一层，当前层对应的链表应该是res\[depth - 1\] res.size\(\) &lt; depth 是指当前层链表还没创建呢。所以node直接add进去当head。

else就是当前层链表已经创建过了。node应该add进去当head。 node.next = res.get\(depth - 1\);就是把node放到链表头  
  


```text
    dfs(root.right, depth + 1, res);
    dfs(root.left, depth + 1, res);
```

这个顺序不能换。因为咱们从tail构建链表，树咱们得从右往左看。所以得优先右子树。

![](../.gitbook/assets/image%20%286%29.png)



  
Solution 2: BFS

```java
/**
 * Definition of TreeNode:
 * public class TreeNode {
 *     public int val;
 *     public TreeNode left, right;
 *     public TreeNode(int val) {
 *         this.val = val;
 *         this.left = this.right = null;
 *     }
 * }
 * Definition for singly-linked list.
 * public class ListNode {
 *     int val;
 *     ListNode next;
 *     ListNode(int x) { val = x; }
 * }
 */
public class Solution {
    /**
     * @param root the root of binary tree
     * @return a lists of linked list
     */
    public List<ListNode> binaryTreeToLists(TreeNode root) {

        Queue<TreeNode> queue = new LinkedList<>();
        queue.offer(root);
        List<ListNode> res = new ArrayList<ListNode>();

        if(root == null) return res;

        while(!queue.isEmpty()){
            int size = queue.size();
            ListNode headNode = null;
            ListNode tailNode = null;
            for(int i = 0; i < size; i++){
                TreeNode node = queue.poll();
                if(headNode == null){
                    headNode = new ListNode(node.val);
                    tailNode = headNode;
                }
                else{
                    tailNode.next = new ListNode(node.val);
                    tailNode = tailNode.next;
                }

                if(node.left != null){
                    queue.offer(node.left);
                }
                if(node.right != null){
                    queue.offer(node.right);
                }
            }
            res.add(headNode);
        }

        return res;
        
    }
}
```

