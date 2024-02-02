## Maximum Depth of Binary Tree
<div class="elfjS" data-track-load="description_content"><p>Given the <code>root</code> of a binary tree, return <em>its maximum depth</em>.</p>

<p>A binary tree's <strong>maximum depth</strong>&nbsp;is the number of nodes along the longest path from the root node down to the farthest leaf node.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/26/tmp-tree.jpg" style="width: 400px; height: 277px;">
<pre><strong>Input:</strong> root = [3,9,20,null,null,15,7]
<strong>Output:</strong> 3
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> root = [1,null,2]
<strong>Output:</strong> 2
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 10<sup>4</sup>]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>
</div>

### Solution

```
int maxDepth(TreeNode* root) {
        if(!root) return 0;
        int maxLeft = maxDepth(root->left);
        int maxRight = maxDepth(root->right);
        return max(maxLeft, maxRight)+1;
    }

```
## Diameter of Binary Tree
<div class="elfjS" data-track-load="description_content"><p>Given the <code>root</code> of a binary tree, return <em>the length of the <strong>diameter</strong> of the tree</em>.</p>

<p>The <strong>diameter</strong> of a binary tree is the <strong>length</strong> of the longest path between any two nodes in a tree. This path may or may not pass through the <code>root</code>.</p>

<p>The <strong>length</strong> of a path between two nodes is represented by the number of edges between them.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/06/diamtree.jpg" style="width: 292px; height: 302px;">
<pre><strong>Input:</strong> root = [1,2,3,4,5]
<strong>Output:</strong> 3
<strong>Explanation:</strong> 3 is the length of the path [4,2,1,3] or [5,2,1,3].
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> root = [1,2]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 10<sup>4</sup>]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>
</div>  

### Solution

```
public class Solution {
    int max = 0;
    
    public int diameterOfBinaryTree(TreeNode root) {
        maxDepth(root);
        return max;
    }
    
    private int maxDepth(TreeNode root) {
        if (root == null) return 0;
        
        int left = maxDepth(root.left);
        int right = maxDepth(root.right);
        
        max = Math.max(max, left + right);
        
        return Math.max(left, right) + 1;
    }
}
```

## Balanced Binary Tree
<div class="elfjS" data-track-load="description_content"><p>Given a binary tree, determine if it is <span data-keyword="height-balanced" class=" cursor-pointer relative text-dark-blue-s text-sm"><div class="popover-wrapper inline-block" data-headlessui-state=""><div><div aria-expanded="false" data-headlessui-state="" id="headlessui-popover-button-:rt:"><div><strong>height-balanced</strong></div></div><div style="position: fixed; z-index: 40; inset: 0px auto auto 0px; transform: translate(306px, 182px);"></div></div></div></span>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/06/balance_1.jpg" style="width: 342px; height: 221px;">
<pre><strong>Input:</strong> root = [3,9,20,null,null,15,7]
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/06/balance_2.jpg" style="width: 452px; height: 301px;">
<pre><strong>Input:</strong> root = [1,2,2,3,3,null,null,4,4]
<strong>Output:</strong> false
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> root = []
<strong>Output:</strong> true
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 5000]</code>.</li>
	<li><code>-10<sup>4</sup> &lt;= Node.val &lt;= 10<sup>4</sup></code></li>
</ul>
</div>

### Solution

```
class solution {
public:
int dfsHeight (TreeNode *root) {
        if (root == NULL) return 0;
        
        int leftHeight = dfsHeight (root -> left);
        if (leftHeight == -1) return -1;
        int rightHeight = dfsHeight (root -> right);
        if (rightHeight == -1) return -1;
        
        if (abs(leftHeight - rightHeight) > 1)  return -1;
        return max (leftHeight, rightHeight) + 1;
    }
    bool isBalanced(TreeNode *root) {
        return dfsHeight (root) != -1;
    }
};
```

## Lowest Common Ancestor of a Binary Tree
<div class="elfjS" data-track-load="description_content"><p>Given a binary tree, find the lowest common ancestor (LCA) of two given nodes in the tree.</p>

<p>According to the <a href="https://en.wikipedia.org/wiki/Lowest_common_ancestor" target="_blank">definition of LCA on Wikipedia</a>: “The lowest common ancestor is defined between two nodes <code>p</code> and <code>q</code> as the lowest node in <code>T</code> that has both <code>p</code> and <code>q</code> as descendants (where we allow <b>a node to be a descendant of itself</b>).”</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/14/binarytree.png" style="width: 200px; height: 190px;">
<pre><strong>Input:</strong> root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 1
<strong>Output:</strong> 3
<strong>Explanation:</strong> The LCA of nodes 5 and 1 is 3.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/14/binarytree.png" style="width: 200px; height: 190px;">
<pre><strong>Input:</strong> root = [3,5,1,6,2,0,8,null,null,7,4], p = 5, q = 4
<strong>Output:</strong> 5
<strong>Explanation:</strong> The LCA of nodes 5 and 4 is 5, since a node can be a descendant of itself according to the LCA definition.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> root = [1,2], p = 1, q = 2
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[2, 10<sup>5</sup>]</code>.</li>
	<li><code>-10<sup>9</sup> &lt;= Node.val &lt;= 10<sup>9</sup></code></li>
	<li>All <code>Node.val</code> are <strong>unique</strong>.</li>
	<li><code>p != q</code></li>
	<li><code>p</code> and <code>q</code> will exist in the tree.</li>
</ul>
</div>

### Solution

```
TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
    if (!root || root == p || root == q) return root;
    TreeNode* left = lowestCommonAncestor(root->left, p, q);
    TreeNode* right = lowestCommonAncestor(root->right, p, q);
    return !left ? right : !right ? left : root;
}
```

## Same Tree
<div class="elfjS" data-track-load="description_content"><p>Given the roots of two binary trees <code>p</code> and <code>q</code>, write a function to check if they are the same or not.</p>

<p>Two binary trees are considered the same if they are structurally identical, and the nodes have the same value.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/20/ex1.jpg" style="width: 622px; height: 182px;">
<pre><strong>Input:</strong> p = [1,2,3], q = [1,2,3]
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/20/ex2.jpg" style="width: 382px; height: 182px;">
<pre><strong>Input:</strong> p = [1,2], q = [1,null,2]
<strong>Output:</strong> false
</pre>

<p><strong class="example">Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/20/ex3.jpg" style="width: 622px; height: 182px;">
<pre><strong>Input:</strong> p = [1,2,1], q = [1,1,2]
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in both trees is in the range <code>[0, 100]</code>.</li>
	<li><code>-10<sup>4</sup> &lt;= Node.val &lt;= 10<sup>4</sup></code></li>
</ul>
</div>

### Solution

```
class Solution {
public:
    bool isSameTree(TreeNode* p, TreeNode* q) {
        if(p == NULL &&  q== NULL) return true;
        if(p == NULL ||  q== NULL) return false;
        if(p->val != q->val) return false;
        return isSameTree(p->right, q->right) && isSameTree(p->left, q->left) ;
    }
};
```

## Binary Tree Zigzag Level Order Traversal
<div class="elfjS" data-track-load="description_content"><p>Given the <code>root</code> of a binary tree, return <em>the zigzag level order traversal of its nodes' values</em>. (i.e., from left to right, then right to left for the next level and alternate between).</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/tree1.jpg" style="width: 277px; height: 302px;">
<pre><strong>Input:</strong> root = [3,9,20,null,null,15,7]
<strong>Output:</strong> [[3],[20,9],[15,7]]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> root = [1]
<strong>Output:</strong> [[1]]
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> root = []
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 2000]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>
</div>

### Solution 
<div class="FN9Jv WRmCx"><p>Assuming after traversing the 1st level, nodes in queue are {9, 20, 8}, And we are going to traverse 2nd level, which is even line and should print value from right to left [8, 20, 9].</p>
<p>We know there are 3 nodes in current queue, so the vector for this level in final result should be of size 3.<br>
Then,     queue [i] -&gt; goes to -&gt;  vector[queue.size() - 1 - i]<br>
i.e. the ith node in current queue should be placed in (queue.size() - 1 - i) position in vector for that line.</p>
<p>For example, for node(9), it's index in queue is 0, so its index in vector should be (3-1-0) = 2.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">zigzagLevelOrder</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token generic-function" style="color: rgb(220, 220, 170);">vector</span><span class="token generic-function generic" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generic-function generic" style="color: rgb(78, 201, 176);">vector</span><span class="token generic-function generic" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generic-function generic" style="color: rgb(86, 156, 214);">int</span><span class="token generic-function generic" style="color: rgb(212, 212, 212);">&gt;</span><span class="token generic-function generic" style="color: rgb(78, 201, 176);"> </span><span class="token generic-function generic" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> result</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>    queue</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> nodesQueue</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    nodesQueue</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">bool</span><span> leftToRight </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">true</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>nodesQueue</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">empty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> size </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nodesQueue</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">row</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>size</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> size</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> node </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nodesQueue</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">front</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            nodesQueue</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>            </span><span class="token" style="color: rgb(106, 153, 85);">// find position to fill node's value</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> index </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>leftToRight</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>size </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>            row</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>index</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>val</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                nodesQueue</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                nodesQueue</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// after this level</span><span>
</span></span><span><span>        leftToRight </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>leftToRight</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        result</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push_back</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>row</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> result</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div></div>

## Boundary Traversal of Binary Tree
<ninjas-problems-ui-problem-details-tab-description _ngcontent-serverapp-c230="" _nghost-serverapp-c229=""><div _ngcontent-serverapp-c229="" class="problem-description-container pt-16 pb-56"><div _ngcontent-serverapp-c229="" class="problem-statement-title-container"><h2 _ngcontent-serverapp-c229="" class="problem-statement-title zen-typo-subtitle-small"> Problem statement </h2><ninjas-problems-ui-send-feedback-button _ngcontent-serverapp-c229="" _nghost-serverapp-c228=""><div _ngcontent-serverapp-c228=""><button _ngcontent-serverapp-c228="" zen-gray-underlined-text-cta="" size="small" class="zen-base-cta zen-gray-underlined-text-cta zen-cta-base zen-cta-small"><span class="zen-cta-wrapper"><span _ngcontent-serverapp-c228=""> Send feedback </span></span></button></div></ninjas-problems-ui-send-feedback-button></div><div _ngcontent-serverapp-c229="" imageoverlay="" class="description pt-8 ng-star-inserted"><p id="you-are-given-a-binary-tree-having-n-nodes">You are given a binary tree having <em><strong>'n'</strong></em> nodes.</p>

<p><br></p>

<p id="the-boundary-nodes-of-a-binary-tree-include-the-nodes-from-the-left-and-right-boundaries-and-the-leaf-nodes-each-node-considered-once">The boundary nodes of a binary tree include the nodes from the left and right boundaries and the leaf nodes, each node considered once.</p>

<p><br></p>

<p id="figure-out-the-boundary-nodes-of-this-binary-tree-in-an-anti-clockwise-direction-starting-from-the-root-node">Figure out the boundary nodes of this binary tree in an Anti-Clockwise direction starting from the root node.</p>

<p><br></p>

<b id="example">Example :</b>

<pre><code>Input: Consider the binary tree A as shown in the figure:
</code></pre>

<p><img src="https://files.codingninjas.in/boundarytraversal-5149.png" alt="alt text" style="cursor: zoom-in;"></p>

<pre><code>Output: [10, 5, 3, 7, 18, 25, 20]

Explanation: As shown in the figure

The nodes on the left boundary are [10, 5, 3]

The nodes on the right boundary are [10, 20, 25]

The leaf nodes are [3, 7, 18, 25].

Please note that nodes 3 and 25 appear in two places but are considered once.
</code></pre>

</div><!----><div _ngcontent-serverapp-c229="" class="problem-other-details-container py-8 mt-16 closed ng-star-inserted"><div _ngcontent-serverapp-c229="" class="problem-other-details-heading-section"><div _ngcontent-serverapp-c229="" class="problem-other-details-heading-left-section"><span _ngcontent-serverapp-c229="" class="problem-other-details-text zen-typo-subtitle-small"> Detailed explanation </span><span _ngcontent-serverapp-c229="" class="problem-other-details-subtext zen-typo-caption-medium"> ( Input/output format, Notes, Images ) </span></div><div _ngcontent-serverapp-c229="" class="problem-other-details-heading-right-section"><mat-icon _ngcontent-serverapp-c229="" role="img" fontset="zen-icon" fonticon="icon-chevron-down" class="mat-icon notranslate icon-chevron-down zen-icon mat-icon-no-color" aria-hidden="true" data-mat-icon-type="font" data-mat-icon-name="icon-chevron-down" data-mat-icon-namespace="zen-icon"></mat-icon></div></div><div _ngcontent-serverapp-c229="" disableselect="" imageoverlay="" class="problem-other-details prevent-select" style="display: none;"><b id="input-format">Input Format:</b>

<pre><code>The only line contains elements in the level order form. The line consists of values of nodes separated by a single space. In case a node is null, we take -1 in its place.

For example, the input for the tree depicted in the below image will be:
</code></pre>

<p><img src="https://files.codingninjas.in/0000000000004189.png" alt="alt text" style="cursor: zoom-in;"></p>

<pre><code>1
2 3
4 -1 5 6
-1 7 -1 -1 -1 -1
-1 -1

Explanation :
Level 1 :
The root node of the tree is 1

Level 2 :
Left child of 1 = 2
Right child of 1 = 3

Level 3 :
Left child of 2 = 4
Right child of 2 = null (-1)
Left child of 3 = 5
Right child of 3 = 6

Level 4 :
Left child of 4 = null (-1)
Right child of 4 = 7
Left child of 5 = null (-1)
Right child of 5 = null (-1)
Left child of 6 = null (-1)
Right child of 6 = null (-1)

Level 5 :
Left child of 7 = null (-1)
Right child of 7 = null (-1)

The first not-null node(of the previous level) is treated as the parent of the first two nodes of the current level. The second not-null node (of the previous level) is treated as the parent node for the next two nodes of the current level and so on.

The input ends when all nodes at the last level are null(-1).

The sequence will be put together in a single line separated by a single space. Hence, for the above-depicted tree, the input will be given as:

1 2 3 4 -1 5 6 -1 7 -1 -1 -1 -1 -1 -1
</code></pre>

<p><br></p>

<b id="output-format">Output Format:</b>

<pre><code>Print the boundary nodes of the given binary tree separated by single spaces.
</code></pre>

<p><br></p>

<b id="note">Note :</b>

<pre><code>You do not need to print anything; it has already been taken care of. Just implement the given function.
</code></pre></div></div><!----><!----><div _ngcontent-serverapp-c229="" imageoverlay="" class="description mt-16 sample-cases border-radius-8 ng-star-inserted"><b>Sample Input 1:</b>

<pre><code>10 5 20 3 8 18 25 -1 -1 7 -1 -1 -1 -1 -1 -1 -1
</code></pre>

<b>Sample Output 1:</b>

<pre><code>10 5 3 7 18 25 20
</code></pre>

<b>Explanation of Sample Input 1:</b>

<pre><code>The nodes on the left boundary are [10, 5, 3]

The nodes on the right boundary are [10, 20, 25]

The leaf nodes are [3, 7, 18, 25].

Please note that nodes 3 and 25 appear in two places but are considered once.
</code></pre>

<b>Sample Input 2:</b>

<pre><code>100 50 150 25 75 140 200 -1 30 70 80 -1 -1 -1 -1 -1 35 -1 -1 -1 -1 -1 -1
</code></pre>

<b>Sample Output 2:</b>

<pre><code>100 50 25 30 35 70 80 140 200 150
</code></pre>

<b>Constraints:</b>

<pre><code>1 &lt;= n &lt;= 10000

Where 'n' is the total number of nodes in the binary tree.

Time Limit: 1 sec
</code></pre>
</div><!----><!----><!----><!----></div></ninjas-problems-ui-problem-details-tab-description>
