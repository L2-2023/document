## 二叉树
https://leetcode.cn/problems/maximum-depth-of-binary-tree/description/?envType=study-plan-v2&envId=top-100-liked

### 104 二叉树的最大深度


给定一个二叉树 root ，返回其最大深度。

二叉树的 最大深度 是指从根节点到最远叶子节点的最长路径上的节点数。

![alt text](image.png)

```

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
    public int maxDepth(TreeNode root) {
    if(root == null) {
        return 0;
    }
    int leftMax = maxDepth(root.left);
    int rightMax = maxDepth(root.right);
    return Math.max(leftMax, rightMax) + 1;
        
    }

}
```
解法
当前节点的最大深度 = max(左子树深度, 右子树深度) + 1

⏱ 时间复杂度
	•	每个节点只访问一次
	•	O(n)（n 是节点总数）

📦 空间复杂度
	•	递归调用栈的深度 = 树的高度
	•	最坏情况（链表型二叉树）：O(n)
	•	平衡二叉树：O(log n)


### 226. 翻转二叉树

给你一棵二叉树的根节点 root ，翻转这棵二叉树，并返回其根节点。

![alt text](image-1.png)


```
 public TreeNode invertTree(TreeNode root) {
    if(root == null) {
        return root;
    }
    TreeNode tmpNode = root.left;
    root.left = root.right;
    root.right= tmpNode;
    invertTree(root.left);
    invertTree(root.right);
    return root;

        
    }
```

	⏱ 时间复杂度：O(n)
每个节点访问一次
	•	📦 空间复杂度：O(h)
h 是树高（递归栈）





### 101.对称二叉树

给你一个二叉树的根节点 root ， 检查它是否轴对称。

![alt text](image-2.png)

```
 public boolean isSymmetric(TreeNode root) {
    if(root == null) {
        return true;
    }
    return isSymmetric(root.left, root.right);

    }

    boolean isSymmetric(TreeNode leftNode, TreeNode rightNode) {
        if(leftNode == null && rightNode == null) {
            return true;
        }
        if(leftNode == null || rightNode == null) {
            return false;
        }
        if(leftNode.val != rightNode.val) {
            return false;
        }
        return isSymmetric(leftNode.left, rightNode.right) && isSymmetric(leftNode.right, rightNode.left);
    }


```



	•	⏱ 时间复杂度：O(n)
每个节点最多访问一次
	•	📦 空间复杂度：O(h)
递归栈深度（h 为树高）




### 543 二叉树的直径
给你一棵二叉树的根节点，返回该树的 直径 。

二叉树的 直径 是指树中任意两个节点之间最长路径的 长度 。这条路径可能经过也可能不经过根节点 root 。

两节点之间路径的 长度 由它们之间边数表示。


![alt text](image-3.png)

```
class Solution {
    int max = 0;
    public int diameterOfBinaryTree(TreeNode root) {
       findMax(root);
       return max;
    }


    int findMax(TreeNode node) {
        if(node == null) {
            return 0;
        }
        int leftMax = findMax(node.left);
        int rightMax = findMax(node.right);
        max = Math.max(max, leftMax + rightMax );
        return Math.max(leftMax, rightMax) + 1;
    }
}

```

时间复杂度 O(n) 空间复杂度O(h);




### 102 二叉树的层序遍历



![alt text](image-4.png)

```
    public List<List<Integer>> levelOrder(TreeNode root) {
        List<List<Integer>> res = new LinkedList();
        if(root == null) {
            return res;
        }
        LinkedList<TreeNode> queue  = new LinkedList();
        queue.addLast(root);
        while(!queue.isEmpty()) {
            int size = queue.size();
            ArrayList<Integer> tmpList = new ArrayList();
            for(int i = 0 ; i < size; i++) {
                TreeNode tmpNode = queue.pollFirst();
                tmpList.add(tmpNode.val);
                if(tmpNode.left != null) {
                    queue.addLast(tmpNode.left);
                }
                if(tmpNode.right != null) {
                    queue.addLast(tmpNode.right);
                }
            }
            res.add(tmpList);
        }
        return res;


    }

    


```

	•	⏱ 时间复杂度：O(n)
每个节点进队、出队一次
	•	📦 空间复杂度：O(n)
队列最坏情况下存一整层节点


### 108. 将有序数组转换为二叉搜索树

给你一个整数数组 nums ，其中元素已经按 升序 排列，请你将其转换为一棵 平衡 二叉搜索树。



```
  public TreeNode sortedArrayToBST(int[] nums) {
    return buildBST(0, nums.length - 1, nums);


        
    }

    TreeNode buildBST(int left, int right , int [] nums) {
        if(left > right) {
            return null;
        }
        int mid = left + (right - left) / 2;
        TreeNode node = new TreeNode(nums[mid]);
        node.left = buildBST(left, mid - 1, nums);
        node.right = buildBST(mid + 1, right , nums);
        return node;
    }

```


•	时间复杂度 O(n)，空间复杂度 O(log n)（递归栈）




### 98. 验证二叉搜索树


给你一个二叉树的根节点 root ，判断其是否是一个有效的二叉搜索树。

有效 二叉搜索树定义如下：

节点的左子树只包含 严格小于 当前节点的数。
节点的右子树只包含 严格大于 当前节点的数。
所有左子树和右子树自身必须也是二叉搜索树。

![alt text](image-5.png)

```
public boolean isValidBST(TreeNode root) {
    return isValidBST(Long.MIN_VALUE, Long.MAX_VALUE, root);
        
    }
    boolean isValidBST(long min , long max , TreeNode node) {
        if(node == null) {
            return true;
        }
        if(node.val <= min || node.val >= max) {
            return false;
        }
        return isValidBST(min, node.val, node.left) && isValidBST(node.val, max, node.right);
    }

```


中序遍历 + 单调递增

	•	BST 的性质：中序遍历得到的序列是 严格递增的
	•	因此：
	1.	对树做中序遍历
	2.	记录前一个节点的值
	3.	每个节点必须 大于前一个值
	•	如果出现不满足的情况 → 不是 BST


```
class Solution {
    private TreeNode prev = null; // 用于记录中序遍历的前一个节点

    public boolean isValidBST(TreeNode root) {
        return inorder(root);
    }

    private boolean inorder(TreeNode node) {
        if (node == null) return true;

        // 遍历左子树
        if (!inorder(node.left)) return false;

        // 当前节点必须大于前一个节点
        if (prev != null && node.val <= prev.val) return false;

        // 更新前一个节点
        prev = node;

        // 遍历右子树
        return inorder(node.right);
    }
}
```


⏱ 时间复杂度
	•	每个节点访问一次
	•	O(n)

📦 空间复杂度
	•	递归栈深度 = 树高 h
	•	平衡树：O(log n)
	•	退化链表：O(n)



### 230. 二叉搜索树中第 K 小的元素


给定一个二叉搜索树的根节点 root ，和一个整数 k ，请你设计一个算法查找其中第 k 小的元素（k 从 1 开始计数）。

![alt text](image-6.png)


```
int k , res;
public int kthSmallest(TreeNode root, int k) {
    this.k = k;
    dfs(root);
    return res;

        
    }
    
    void dfs(TreeNode node) {
        if(node == null) {
            return ;
        }
        if(k < 0) {
            return ;
        }
        dfs(node.left);
        if(--k == 0) {
            res = node.val;
            return ;
        }
        dfs(node.right);
    }
```


优化 提前返回
```
class Solution {
    private int k;
    private int res;

    public int kthSmallest(TreeNode root, int k) {
        this.k = k;
        dfs(root);
        return res;
    }

    private boolean dfs(TreeNode node) {
        if (node == null) return false;

        // 遍历左子树
        if (dfs(node.left)) return true;

        // 当前节点
        k--;
        if (k == 0) {
            res = node.val;
            return true; // 找到答案，直接返回
        }

        // 遍历右子树
        return dfs(node.right);
    }
}

```



### 199. 二叉树的右视图
给定一个二叉树的 根节点 root，想象自己站在它的右侧，按照从顶部到底部的顺序，返回从右侧所能看到的节点值

输入：root = [1,2,3,null,5,null,4]

输出：[1,3,4]

解释：


![alt text](image-7.png)


```


  public List<Integer> rightSideView(TreeNode root) {
    List<Integer> res = new ArrayList();
    rightSideView(0, root, res);
    return res;

    }

    void rightSideView(int deep, TreeNode node, List<Integer> res) {
        if(node == null) {
            return ;
        }
        if(deep == res.size()) {
            res.add(node.val);
        }
        rightSideView(deep + 1, node.right, res);
        rightSideView(deep + 1, node.left, res);

    }

```


	•	⏱ 时间复杂度：O(n)
	•	每个节点访问一次
	•	📦 空间复杂度：O(h)
	•	递归栈深度 = 树高 h
	•	最坏情况链状二叉树：O(n)
	•	平衡二叉树：O(log n)




### 114. 二叉树展开为链表

给你二叉树的根结点 root ，请你将它展开为一个单链表：

展开后的单链表应该同样使用 TreeNode ，其中 right 子指针指向链表中下一个结点，而左子指针始终为 null 。
展开后的单链表应该与二叉树 先序遍历 顺序相同。



![alt text](image-8.png)









### 105. 从前序与中序遍历序列构造二叉树

给定两个整数数组 preorder 和 inorder ，其中 preorder 是二叉树的先序遍历， inorder 是同一棵树的中序遍历，请构造二叉树并返回其根节点。

![alt text](image-9.png)



### 437. 路径总和 III

给定一个二叉树的根节点 root ，和一个整数 targetSum ，求该二叉树里节点值之和等于 targetSum 的 路径 的数目。

路径 不需要从根节点开始，也不需要在叶子节点结束，但是路径方向必须是向下的（只能从父节点到子节点）。
![alt text](image-10.png)

```
输入：root = [10,5,-3,3,2,null,11,3,-2,null,1], targetSum = 8
输出：3
解释：和等于 8 的路径有 3 条，如图所示。
```




### 236. 二叉树的最近公共祖先

给定一个二叉树, 找到该树中两个指定节点的最近公共祖先。

百度百科中最近公共祖先的定义为：“对于有根树 T 的两个节点 p、q，最近公共祖先表示为一个节点 x，满足 x 是 p、q 的祖先且 x 的深度尽可能大（一个节点也可以是它自己的祖先）。

![alt text](image-11.png)

输入：root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
输出：3
解释：节点 5 和节点 1 的最近公共祖先是节点 3 。



```
 public TreeNode lowestCommonAncestor(TreeNode root, TreeNode p, TreeNode q) {
    if(root == null || root == p || root == q) {
        return root;
    }
    TreeNode leftNode = lowestCommonAncestor(root.left, p, q);
    TreeNode rightNode = lowestCommonAncestor(root.right, p, q);
    if(leftNode == null) {
        return rightNode;
    }
    if(rightNode == null) {
        return leftNode;
    }
    return root;
    
        
    }


```


### 124 二叉树的最大路径和



```
int max = Integer.MIN_VALUE;
public int maxPathSum(TreeNode root) {
    findMax(root);
    return max;   
    }

    int findMax(TreeNode node) {
        if(node == null) {
            return 0;
        }
        int leftMax = Math.max(0, findMax(node.left));
        int rightMax = Math.max(0, findMax(node.right));
        max = Math.max(max, rightMax + leftMax + node.val);
        return Math.max(leftMax, rightMax) + node.val;
    }


```

为什么要 Math.max(0, ……)

int leftMax = Math.max(0, findMax(node.left));
int rightMax = Math.max(0, findMax(node.right));
这是这道题的灵魂点。

含义是：
如果子树路径是负数，那我 宁可不要

举个例子：

   10
  /
-20

如果不截断：
10 + (-20) = -10 ❌

正确做法：
10 + 0 = 10 ✅

















