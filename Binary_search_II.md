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
<div class="markdown-body"><section class="main"><h2 id="problem-statement" level="2">Problem Statement</h2><p>A binary tree will be given in the problem and we need to find the boundary traversal of that binary tree.
<span class="highlight--red">Boundary traversal</span> of a binary tree means traversing the binary tree along the boundary. The boundary includes the left boundary, right boundary and leaf nodes. Therefore in the boundary traversal of binary trees we will first include the left boundary then leaf nodes and then right boundary.</p></section>
<section class="main"><h2 id="important-terms-in-boundary-traversal-of-binary-tree" level="2">Important Terms in Boundary Traversal of Binary Tree</h2><p>In order to solve the above problem we need to know certain terms like:</p><ul>
<li>The left boundary is the path from the root to the left most node.</li>
<li>Right boundary is the path from the root to the right most node.</li>
<li>Leftmost node is a leaf node that we can reach by traversing the left subtree first everytime, if it exists. If there is no left subtree then we go to the right subtree. This we do until we reach the leaf node. This leaf node is known as the rightmost node.</li>
<li>Similarly we can get the rightmost most node by traversing the right subtree in the above given manner.</li>
</ul></section>
<section class="main"><h2 id="example" level="2">Example</h2><h3 id="input" level="3">Input</h3><p><img alt="boundary-traversal-of-binary-tree-example1" loading="eager" width="864" height="200" decoding="async" data-nimg="1" class="markdown_image_container__jjYk1 markdown_loaded__iZ4O5" src="https://scaler.com/topics/images/boundary-traversal-of-binary-tree-example1.webp" style="color: transparent; height: auto; max-width: 100%;"></p><h3 id="output" level="3">Output</h3><pre><div class="code-box_snippetContainer__cJ6zK"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(171, 178, 191); background: rgb(40, 44, 52);"><code class="language-plaintext" style="white-space: pre;"><span>1, 7, 2, 5, 11, 5, 9, 9
</span></code></pre><button type="button" class="btn-icon cursor code-box_copyIcon__nChUJ" data-for="copy" data-tip="Copied" data-place="left" data-effect="solid" data-event="click" data-scroll-hide="true" data-iscapture="true" currentitem="false"><svg fill="currentColor" class="code-box_copy_icon__87vHM" version="1.1" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 32 32"><path d="M25.629 27.591v-18.051h-14.127v18.051h14.127zM25.629 7.005q1.026 0 1.811 0.755t0.785 1.781v18.051q0 1.026-0.785 1.811t-1.811 0.785h-14.127q-1.026 0-1.811-0.785t-0.785-1.811v-18.051q0-1.026 0.785-1.781t1.811-0.755h14.127zM21.766 1.813v2.596h-15.455v18.051h-2.536v-18.051q0-1.026 0.755-1.811t1.781-0.785h15.455z"></path></svg><div class="__react_component_tooltip te5204224-4258-453b-a780-8b4bc448e6a9 place-top type-dark" id="copy" data-id="tooltip"><style aria-hidden="true">
  	.te5204224-4258-453b-a780-8b4bc448e6a9 {
	    color: #fff;
	    background: #222;
	    border: 1px solid transparent;
	    border-radius: undefinedpx;
	    padding: 8px 21px;
  	}

  	.te5204224-4258-453b-a780-8b4bc448e6a9.place-top {
        margin-top: -10px;
    }
    .te5204224-4258-453b-a780-8b4bc448e6a9.place-top::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: 2;
        width: 20px;
        height: 12px;
    }
    .te5204224-4258-453b-a780-8b4bc448e6a9.place-top::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        bottom: -6px;
        left: 50%;
        margin-left: -6px;
        transform: rotate(135deg);
    }

    .te5204224-4258-453b-a780-8b4bc448e6a9.place-bottom {
        margin-top: 10px;
    }
    .te5204224-4258-453b-a780-8b4bc448e6a9.place-bottom::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 18px;
        height: 10px;
    }
    .te5204224-4258-453b-a780-8b4bc448e6a9.place-bottom::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        top: -6px;
        left: 50%;
        margin-left: -6px;
        transform: rotate(45deg);
    }

    .te5204224-4258-453b-a780-8b4bc448e6a9.place-left {
        margin-left: -10px;
    }
    .te5204224-4258-453b-a780-8b4bc448e6a9.place-left::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 10px;
        height: 18px;
    }
    .te5204224-4258-453b-a780-8b4bc448e6a9.place-left::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        right: -6px;
        top: 50%;
        margin-top: -6px;
        transform: rotate(45deg);
    }

    .te5204224-4258-453b-a780-8b4bc448e6a9.place-right {
        margin-left: 10px;
    }
    .te5204224-4258-453b-a780-8b4bc448e6a9.place-right::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 10px;
        height: 18px;
    }
    .te5204224-4258-453b-a780-8b4bc448e6a9.place-right::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        left: -6px;
        top: 50%;
        margin-top: -6px;
        transform: rotate(-135deg);
    }
  </style></div></button></div></pre></section>
<section class="main"><h2 id="example-explanation" level="2">Example Explanation</h2><p>We need to find the boundary traversal of binary tree given above, we will do it in following manner:</p><ul>
<li>Visit root (1)</li>
<li>Path to leftmost node (7,2)</li>
<li>Leafs nodes (5,11,5)</li>
<li>Path to rightmost node (9,9)</li>
</ul><p>Thus the boundary traversal of the binary tree becomes : ( 1, 7, 2, 5, 11, 5, 9, 9)</p></section>
<section class="main"><h2 id="constraints" level="2">Constraints</h2><ul>
<li><span><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mn>1</mn><mo>&lt;</mo><mo>=</mo><mi>n</mi><mo>&lt;</mo><mo>=</mo></mrow><annotation encoding="application/x-tex"> 1 &lt;= n &lt;=</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="strut" style="height:0.64444em;"></span><span class="strut bottom" style="height:0.68354em;vertical-align:-0.0391em;"></span><span class="base"><span class="mord">1</span><span class="mord rule" style="margin-right:0.2777777777777778em;"></span><span class="mrel">&lt;</span><span class="mrel">=</span><span class="mord rule" style="margin-right:0.2777777777777778em;"></span><span class="mord mathit">n</span><span class="mord rule" style="margin-right:0.2777777777777778em;"></span><span class="mrel">&lt;</span><span class="mrel">=</span></span></span></span></span> <span><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mn>1</mn><msup><mn>0</mn><mn>5</mn></msup></mrow><annotation encoding="application/x-tex">10^5</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="strut" style="height:0.8141079999999999em;"></span><span class="strut bottom" style="height:0.8141079999999999em;vertical-align:0em;"></span><span class="base"><span class="mord">1</span><span class="mord"><span class="mord">0</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height:0.8141079999999999em;"><span style="top:-3.063em;margin-right:0.05em;"><span class="pstrut" style="height:2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight">5</span></span></span></span></span></span></span></span></span></span></span></span></li>
<li><span><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mo>−</mo><mn>1</mn><msup><mn>0</mn><mn>4</mn></msup></mrow><annotation encoding="application/x-tex">-10^4</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="strut" style="height:0.8141079999999999em;"></span><span class="strut bottom" style="height:0.897438em;vertical-align:-0.08333em;"></span><span class="base"><span class="mord">−</span><span class="mord">1</span><span class="mord"><span class="mord">0</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height:0.8141079999999999em;"><span style="top:-3.063em;margin-right:0.05em;"><span class="pstrut" style="height:2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight">4</span></span></span></span></span></span></span></span></span></span></span></span> &lt;= node.val <span><span class="katex"><span class="katex-mathml"><math><semantics><mrow><mo>&lt;</mo><mo>=</mo><mn>1</mn><msup><mn>0</mn><mn>4</mn></msup></mrow><annotation encoding="application/x-tex">&lt;= 10^4</annotation></semantics></math></span><span class="katex-html" aria-hidden="true"><span class="strut" style="height:0.8141079999999999em;"></span><span class="strut bottom" style="height:0.853208em;vertical-align:-0.0391em;"></span><span class="base"><span class="mrel">&lt;</span><span class="mrel">=</span><span class="mord rule" style="margin-right:0.2777777777777778em;"></span><span class="mord">1</span><span class="mord"><span class="mord">0</span><span class="msupsub"><span class="vlist-t"><span class="vlist-r"><span class="vlist" style="height:0.8141079999999999em;"><span style="top:-3.063em;margin-right:0.05em;"><span class="pstrut" style="height:2.7em;"></span><span class="sizing reset-size6 size3 mtight"><span class="mord mtight">4</span></span></span></span></span></span></span></span></span></span></span></span></li>
</ul></section>
<section class="main"><h2 id="approach-1:-traversing-the-boundary-in-three-parts:-left-boundary,-leaf-nodes,-and-right-boundary" level="2">Approach 1: Traversing the Boundary in Three Parts: Left Boundary, Leaf Nodes, and Right Boundary</h2><p>The approach to find the boundary traversal of binary tree is simple and can be done by following these three steps :</p><ul>
<li>Traverse the left boundary in a top down manner, that is we start from the root and then we go towards the leaf node. In this step we keep traversing the tree until we reach the leftmost node.</li>
<li>Then we traverse all the leaf nodes from left to right. That is, from the leftmost node we move towards the right and only print the leaf nodes.</li>
<li>Lastly we traverse the right boundary in a bottom up manner, that is we start from the rightmost node and go towards the root node by following the right boundary path.</li>
</ul></section>
<section class="main"><h2 id="code-for-boundary-traversal-of-binary-tree" level="2">Code for Boundary Traversal of Binary Tree</h2><p>Let's look into the code of boundary traversal of a binary tree.
We will create the given below binary tree in the code and then we will find its boundary traversal.</p><p><img alt="boundary-traversal-of-binary-tree-example2" loading="lazy" width="864" height="200" decoding="async" data-nimg="1" class="markdown_image_container__jjYk1 markdown_loaded__iZ4O5" src="https://scaler.com/topics/images/boundary-traversal-of-binary-tree-example2.webp" style="color: transparent; height: auto; max-width: 100%;"></p><h3 id="c---code-implementation" level="3">C++ Code implementation</h3><pre><div class="code-box_snippetContainer__cJ6zK"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(171, 178, 191); background: rgb(40, 44, 52);"><code class="language-cpp" style="white-space: pre;"><span style="color: rgb(97, 174, 238);">#</span><span class="hljs-meta-keyword" style="color: rgb(97, 174, 238);">include</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(152, 195, 121);">&lt;iostream&gt;</span><span>
</span><span></span><span style="color: rgb(249, 38, 114);">using</span><span> </span><span style="color: rgb(249, 38, 114);">namespace</span><span> std;
</span> 

<span></span><span class="hljs-class" style="color: rgb(249, 38, 114);">struct</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(97, 174, 238);">Node</span><span class="hljs-class">{</span><span>
</span><span>    </span><span style="color: rgb(249, 38, 114);">int</span><span> data;
</span>    Node *left, *right;
 
<span>    </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(249, 38, 114);">int</span><span> data){
</span><span>        </span><span style="color: rgb(249, 38, 114);">this</span><span>-&gt;data = data;
</span><span>        </span><span style="color: rgb(249, 38, 114);">this</span><span>-&gt;left = </span><span style="color: rgb(249, 38, 114);">this</span><span>-&gt;right = </span><span style="color: rgb(86, 182, 194);">nullptr</span><span>;
</span>    }
    
<span></span><span style="color: rgb(249, 38, 114);">public</span><span>:
</span><span>    </span><span style="color: rgb(249, 38, 114);">bool</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">checkLeaf</span><span style="color: rgb(97, 174, 238);">()</span><span>{
</span><span>        </span><span style="color: rgb(249, 38, 114);">return</span><span> </span><span style="color: rgb(249, 38, 114);">this</span><span>-&gt;left == </span><span style="color: rgb(86, 182, 194);">nullptr</span><span> &amp;&amp; </span><span style="color: rgb(249, 38, 114);">this</span><span>-&gt;right == </span><span style="color: rgb(86, 182, 194);">nullptr</span><span>;
</span>    }
};
 

<span></span><span style="color: rgb(249, 38, 114);">void</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">LeftBoundary</span><span style="color: rgb(97, 174, 238);">(Node* root)</span><span>{
</span><span>    </span><span style="color: rgb(249, 38, 114);">if</span><span> (!root)
</span><span>        </span><span style="color: rgb(249, 38, 114);">return</span><span>;
</span> 
    Node* node = root;
 
<span>    </span><span style="color: rgb(249, 38, 114);">while</span><span> (!node-&gt;</span><span style="color: rgb(230, 192, 123);">checkLeaf</span><span>()){
</span><span>        cout &lt;&lt; node-&gt;data &lt;&lt; </span><span style="color: rgb(152, 195, 121);">' '</span><span>;
</span>        node = (node-&gt;left) ? node-&gt;left: node-&gt;right;
    }
}
 
<span></span><span style="color: rgb(249, 38, 114);">void</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">RightBoundary</span><span style="color: rgb(97, 174, 238);">(Node* root)</span><span>{
</span><span>    </span><span style="color: rgb(249, 38, 114);">if</span><span> (!root || root-&gt;</span><span style="color: rgb(230, 192, 123);">checkLeaf</span><span>()) {
</span><span>        </span><span style="color: rgb(249, 38, 114);">return</span><span>;
</span>    }
<span>    </span><span style="color: rgb(230, 192, 123);">RightBoundary</span><span>(root-&gt;right ? root-&gt;right: root-&gt;left);
</span><span>    cout &lt;&lt; root-&gt;data &lt;&lt; </span><span style="color: rgb(152, 195, 121);">' '</span><span>;
</span>}
 
<span></span><span style="color: rgb(249, 38, 114);">void</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">printLeafNodes</span><span style="color: rgb(97, 174, 238);">(Node* root)</span><span>{
</span><span>    </span><span style="color: rgb(249, 38, 114);">if</span><span> (root == </span><span style="color: rgb(86, 182, 194);">nullptr</span><span>) {
</span><span>        </span><span style="color: rgb(249, 38, 114);">return</span><span>;
</span>    }
 
<span>    </span><span style="color: rgb(230, 192, 123);">printLeafNodes</span><span>(root-&gt;left);
</span>
<span>    </span><span style="color: rgb(249, 38, 114);">if</span><span> (root-&gt;</span><span style="color: rgb(230, 192, 123);">checkLeaf</span><span>()) {
</span><span>        cout &lt;&lt; root-&gt;data &lt;&lt; </span><span style="color: rgb(152, 195, 121);">' '</span><span>;
</span>    }
 
<span>    </span><span style="color: rgb(230, 192, 123);">printLeafNodes</span><span>(root-&gt;right);
</span>}

<span></span><span style="color: rgb(249, 38, 114);">void</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">BoundaryTraversal</span><span style="color: rgb(97, 174, 238);">(Node* root)</span><span>{
</span><span>    </span><span style="color: rgb(249, 38, 114);">if</span><span> (root == </span><span style="color: rgb(86, 182, 194);">nullptr</span><span>) {
</span><span>        </span><span style="color: rgb(249, 38, 114);">return</span><span>;
</span>    }
<span>    cout &lt;&lt; root-&gt;data &lt;&lt; </span><span style="color: rgb(152, 195, 121);">' '</span><span>;
</span><span>    </span><span style="color: rgb(230, 192, 123);">LeftBoundary</span><span>(root-&gt;left);
</span>
<span>    </span><span style="color: rgb(249, 38, 114);">if</span><span> (!root-&gt;</span><span style="color: rgb(230, 192, 123);">checkLeaf</span><span>()) {
</span><span>        </span><span style="color: rgb(230, 192, 123);">printLeafNodes</span><span>(root);
</span>    }
<span>    </span><span style="color: rgb(230, 192, 123);">RightBoundary</span><span>(root-&gt;right);
</span>}
 
<span></span><span style="color: rgb(249, 38, 114);">int</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">main</span><span style="color: rgb(97, 174, 238);">()</span><span>{
</span><span>    Node* root = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">1</span><span>);
</span><span>    root-&gt;left = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">2</span><span>);
</span><span>    root-&gt;right = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">3</span><span>);
</span><span>    root-&gt;left-&gt;left = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">4</span><span>);
</span><span>    root-&gt;left-&gt;right = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">5</span><span>);
</span><span>    root-&gt;right-&gt;left = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">6</span><span>);
</span><span>    root-&gt;right-&gt;right = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">7</span><span>);
</span><span>    root-&gt;left-&gt;left-&gt;left = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">8</span><span>);
</span><span>    root-&gt;left-&gt;left-&gt;right = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">9</span><span>);
</span><span>    root-&gt;left-&gt;right-&gt;right = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">10</span><span>);
</span><span>    root-&gt;right-&gt;right-&gt;left = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">11</span><span>);
</span><span>    root-&gt;left-&gt;left-&gt;right-&gt;left = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">12</span><span>);
</span><span>    root-&gt;left-&gt;left-&gt;right-&gt;right = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">13</span><span>);
</span><span>    root-&gt;right-&gt;right-&gt;left-&gt;left = </span><span style="color: rgb(249, 38, 114);">new</span><span> </span><span style="color: rgb(230, 192, 123);">Node</span><span>(</span><span style="color: rgb(209, 154, 102);">14</span><span>);
</span> 
<span>    </span><span style="color: rgb(230, 192, 123);">BoundaryTraversal</span><span>(root);
</span><span>    </span><span style="color: rgb(249, 38, 114);">return</span><span> </span><span style="color: rgb(209, 154, 102);">0</span><span>;
</span>}
</code></pre><button type="button" class="btn-icon cursor code-box_copyIcon__nChUJ" data-for="copy" data-tip="Copied" data-place="left" data-effect="solid" data-event="click" data-scroll-hide="true" data-iscapture="true" currentitem="false"><svg fill="currentColor" class="code-box_copy_icon__87vHM" version="1.1" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 32 32"><path d="M25.629 27.591v-18.051h-14.127v18.051h14.127zM25.629 7.005q1.026 0 1.811 0.755t0.785 1.781v18.051q0 1.026-0.785 1.811t-1.811 0.785h-14.127q-1.026 0-1.811-0.785t-0.785-1.811v-18.051q0-1.026 0.785-1.781t1.811-0.755h14.127zM21.766 1.813v2.596h-15.455v18.051h-2.536v-18.051q0-1.026 0.755-1.811t1.781-0.785h15.455z"></path></svg><div class="__react_component_tooltip t1a2e44de-db74-4743-9227-63a60eae8822 place-top type-dark" id="copy" data-id="tooltip"><style aria-hidden="true">
  	.t1a2e44de-db74-4743-9227-63a60eae8822 {
	    color: #fff;
	    background: #222;
	    border: 1px solid transparent;
	    border-radius: undefinedpx;
	    padding: 8px 21px;
  	}

  	.t1a2e44de-db74-4743-9227-63a60eae8822.place-top {
        margin-top: -10px;
    }
    .t1a2e44de-db74-4743-9227-63a60eae8822.place-top::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: 2;
        width: 20px;
        height: 12px;
    }
    .t1a2e44de-db74-4743-9227-63a60eae8822.place-top::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        bottom: -6px;
        left: 50%;
        margin-left: -6px;
        transform: rotate(135deg);
    }

    .t1a2e44de-db74-4743-9227-63a60eae8822.place-bottom {
        margin-top: 10px;
    }
    .t1a2e44de-db74-4743-9227-63a60eae8822.place-bottom::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 18px;
        height: 10px;
    }
    .t1a2e44de-db74-4743-9227-63a60eae8822.place-bottom::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        top: -6px;
        left: 50%;
        margin-left: -6px;
        transform: rotate(45deg);
    }

    .t1a2e44de-db74-4743-9227-63a60eae8822.place-left {
        margin-left: -10px;
    }
    .t1a2e44de-db74-4743-9227-63a60eae8822.place-left::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 10px;
        height: 18px;
    }
    .t1a2e44de-db74-4743-9227-63a60eae8822.place-left::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        right: -6px;
        top: 50%;
        margin-top: -6px;
        transform: rotate(45deg);
    }

    .t1a2e44de-db74-4743-9227-63a60eae8822.place-right {
        margin-left: 10px;
    }
    .t1a2e44de-db74-4743-9227-63a60eae8822.place-right::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 10px;
        height: 18px;
    }
    .t1a2e44de-db74-4743-9227-63a60eae8822.place-right::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        left: -6px;
        top: 50%;
        margin-top: -6px;
        transform: rotate(-135deg);
    }
  </style></div></button></div></pre><h3 id="java-code-implementation" level="3">Java Code Implementation</h3><pre><div class="code-box_snippetContainer__cJ6zK"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(171, 178, 191); background: rgb(40, 44, 52);"><code class="language-java" style="white-space: pre;"><span>
</span><span></span><span class="hljs-class" style="color: rgb(249, 38, 114);">class</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(97, 174, 238);">Node</span><span class="hljs-class">
</span><span class="hljs-class"></span><span>{
</span><span>    </span><span style="color: rgb(249, 38, 114);">int</span><span> data;
</span>    Node left, right;
 
<span>    Node(</span><span style="color: rgb(249, 38, 114);">int</span><span> data){
</span><span>        </span><span style="color: rgb(249, 38, 114);">this</span><span>.data = data;
</span><span>        </span><span style="color: rgb(249, 38, 114);">this</span><span>.left = </span><span style="color: rgb(249, 38, 114);">this</span><span>.right = </span><span style="color: rgb(249, 38, 114);">null</span><span>;
</span>    }

<span>    </span><span style="color: rgb(249, 38, 114);">boolean</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">checkLeaf</span><span style="color: rgb(97, 174, 238);">()</span><span style="color: rgb(97, 174, 238);"> </span><span>{
</span><span>        </span><span style="color: rgb(249, 38, 114);">return</span><span> </span><span style="color: rgb(249, 38, 114);">this</span><span>.left == </span><span style="color: rgb(249, 38, 114);">null</span><span> &amp;&amp; </span><span style="color: rgb(249, 38, 114);">this</span><span>.right == </span><span style="color: rgb(249, 38, 114);">null</span><span>;
</span>    }
}
 
<span></span><span class="hljs-class" style="color: rgb(249, 38, 114);">class</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(97, 174, 238);">Main</span><span>{
</span><span>    </span><span style="color: rgb(249, 38, 114);">public</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(249, 38, 114);">static</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(249, 38, 114);">void</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">LeftBoundary</span><span style="color: rgb(97, 174, 238);">(Node root)</span><span>{
</span><span>        </span><span style="color: rgb(249, 38, 114);">if</span><span> (root == </span><span style="color: rgb(249, 38, 114);">null</span><span>) {
</span><span>            </span><span style="color: rgb(249, 38, 114);">return</span><span>;
</span>        }
 
        Node node = root;
 
<span>        </span><span style="color: rgb(249, 38, 114);">while</span><span> (!node.checkLeaf()){
</span><span>            System.out.print(node.data + </span><span style="color: rgb(152, 195, 121);">" "</span><span>);
</span><span>            node = (node.left != </span><span style="color: rgb(249, 38, 114);">null</span><span>) ? node.left: node.right;
</span>        }
    }
    
<span>    </span><span style="color: rgb(249, 38, 114);">public</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(249, 38, 114);">static</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(249, 38, 114);">void</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">RightBoundary</span><span style="color: rgb(97, 174, 238);">(Node root)</span><span>{
</span><span>        </span><span style="color: rgb(249, 38, 114);">if</span><span> (root == </span><span style="color: rgb(249, 38, 114);">null</span><span> || root.checkLeaf()) {
</span><span>            </span><span style="color: rgb(249, 38, 114);">return</span><span>;
</span>        }
 
<span>        RightBoundary(root.right != </span><span style="color: rgb(249, 38, 114);">null</span><span> ? root.right: root.left);
</span> 
<span>        System.out.print(root.data + </span><span style="color: rgb(152, 195, 121);">" "</span><span>);
</span>    }
    
<span>    </span><span style="color: rgb(249, 38, 114);">public</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(249, 38, 114);">static</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(249, 38, 114);">void</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">printLeaf</span><span style="color: rgb(97, 174, 238);">(Node root)</span><span>{
</span>        
<span>        </span><span style="color: rgb(249, 38, 114);">if</span><span> (root == </span><span style="color: rgb(249, 38, 114);">null</span><span>) {
</span><span>            </span><span style="color: rgb(249, 38, 114);">return</span><span>;
</span>        }
 
        
        printLeaf(root.left);
 
      
<span>        </span><span style="color: rgb(249, 38, 114);">if</span><span> (root.checkLeaf()) {
</span><span>            System.out.print(root.data + </span><span style="color: rgb(152, 195, 121);">" "</span><span>);
</span>        }
 
        printLeaf(root.right);
    }
 
    
<span>    </span><span style="color: rgb(249, 38, 114);">public</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(249, 38, 114);">static</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(249, 38, 114);">void</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">BoundaryTraversal</span><span style="color: rgb(97, 174, 238);">(Node root)</span><span>{
</span><span>        </span><span style="color: rgb(249, 38, 114);">if</span><span> (root == </span><span style="color: rgb(249, 38, 114);">null</span><span>) {
</span><span>            </span><span style="color: rgb(249, 38, 114);">return</span><span>;
</span>        }
 
      
<span>        System.out.print(root.data + </span><span style="color: rgb(152, 195, 121);">" "</span><span>);
</span> 
        LeftBoundary(root.left);
 
    
<span>        </span><span style="color: rgb(249, 38, 114);">if</span><span> (!root.checkLeaf()) {
</span>            printLeaf(root);
        }
 
        RightBoundary(root.right);
    }
 
<span>    </span><span style="color: rgb(249, 38, 114);">public</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(249, 38, 114);">static</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(249, 38, 114);">void</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">main</span><span style="color: rgb(97, 174, 238);">(String[] args)</span><span>{
</span>       
<span>        Node root = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">1</span><span>);
</span><span>        root.left = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">2</span><span>);
</span><span>        root.right = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">3</span><span>);
</span><span>        root.left.left = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">4</span><span>);
</span><span>        root.left.right = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">5</span><span>);
</span><span>        root.right.left = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">6</span><span>);
</span><span>        root.right.right = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">7</span><span>);
</span><span>        root.left.left.left = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">8</span><span>);
</span><span>        root.left.left.right = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">9</span><span>);
</span><span>        root.left.right.right = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">10</span><span>);
</span><span>        root.right.right.left = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">11</span><span>);
</span><span>        root.left.left.right.left = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">12</span><span>);
</span><span>        root.left.left.right.right = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">13</span><span>);
</span><span>        root.right.right.left.left = </span><span style="color: rgb(249, 38, 114);">new</span><span> Node(</span><span style="color: rgb(209, 154, 102);">14</span><span>);
</span> 
        BoundaryTraversal(root);
    }
}
</code></pre><button type="button" class="btn-icon cursor code-box_copyIcon__nChUJ" data-for="copy" data-tip="Copied" data-place="left" data-effect="solid" data-event="click" data-scroll-hide="true" data-iscapture="true" currentitem="false"><svg fill="currentColor" class="code-box_copy_icon__87vHM" version="1.1" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 32 32"><path d="M25.629 27.591v-18.051h-14.127v18.051h14.127zM25.629 7.005q1.026 0 1.811 0.755t0.785 1.781v18.051q0 1.026-0.785 1.811t-1.811 0.785h-14.127q-1.026 0-1.811-0.785t-0.785-1.811v-18.051q0-1.026 0.785-1.781t1.811-0.755h14.127zM21.766 1.813v2.596h-15.455v18.051h-2.536v-18.051q0-1.026 0.755-1.811t1.781-0.785h15.455z"></path></svg><div class="__react_component_tooltip te6da86b3-22a6-4131-86bd-484a6245f7c2 place-top type-dark" id="copy" data-id="tooltip"><style aria-hidden="true">
  	.te6da86b3-22a6-4131-86bd-484a6245f7c2 {
	    color: #fff;
	    background: #222;
	    border: 1px solid transparent;
	    border-radius: undefinedpx;
	    padding: 8px 21px;
  	}

  	.te6da86b3-22a6-4131-86bd-484a6245f7c2.place-top {
        margin-top: -10px;
    }
    .te6da86b3-22a6-4131-86bd-484a6245f7c2.place-top::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: 2;
        width: 20px;
        height: 12px;
    }
    .te6da86b3-22a6-4131-86bd-484a6245f7c2.place-top::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        bottom: -6px;
        left: 50%;
        margin-left: -6px;
        transform: rotate(135deg);
    }

    .te6da86b3-22a6-4131-86bd-484a6245f7c2.place-bottom {
        margin-top: 10px;
    }
    .te6da86b3-22a6-4131-86bd-484a6245f7c2.place-bottom::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 18px;
        height: 10px;
    }
    .te6da86b3-22a6-4131-86bd-484a6245f7c2.place-bottom::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        top: -6px;
        left: 50%;
        margin-left: -6px;
        transform: rotate(45deg);
    }

    .te6da86b3-22a6-4131-86bd-484a6245f7c2.place-left {
        margin-left: -10px;
    }
    .te6da86b3-22a6-4131-86bd-484a6245f7c2.place-left::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 10px;
        height: 18px;
    }
    .te6da86b3-22a6-4131-86bd-484a6245f7c2.place-left::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        right: -6px;
        top: 50%;
        margin-top: -6px;
        transform: rotate(45deg);
    }

    .te6da86b3-22a6-4131-86bd-484a6245f7c2.place-right {
        margin-left: 10px;
    }
    .te6da86b3-22a6-4131-86bd-484a6245f7c2.place-right::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 10px;
        height: 18px;
    }
    .te6da86b3-22a6-4131-86bd-484a6245f7c2.place-right::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        left: -6px;
        top: 50%;
        margin-top: -6px;
        transform: rotate(-135deg);
    }
  </style></div></button></div></pre><h3 id="python-code-implementation" level="3">Python Code Implementation</h3><pre><div class="code-box_snippetContainer__cJ6zK"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(171, 178, 191); background: rgb(40, 44, 52);"><code class="language-python" style="white-space: pre;"><span>
</span><span></span><span class="hljs-class" style="color: rgb(249, 38, 114);">class</span><span class="hljs-class"> </span><span class="hljs-class" style="color: rgb(97, 174, 238);">Node</span><span class="hljs-class">:</span><span>
</span><span>    </span><span style="color: rgb(249, 38, 114);">def</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">__init__</span><span style="color: rgb(97, 174, 238);">(</span><span style="color: rgb(97, 174, 238);">self, val, left=</span><span style="color: rgb(86, 182, 194);">None</span><span style="color: rgb(97, 174, 238);">, right=</span><span style="color: rgb(86, 182, 194);">None</span><span style="color: rgb(97, 174, 238);">):</span><span>
</span>        self.val = val
        self.left = left
        self.right = right
 
<span>    </span><span style="color: rgb(249, 38, 114);">def</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">areLeaf</span><span style="color: rgb(97, 174, 238);">(</span><span style="color: rgb(97, 174, 238);">self</span><span style="color: rgb(97, 174, 238);">):</span><span>
</span><span>        </span><span style="color: rgb(249, 38, 114);">return</span><span> self.left </span><span style="color: rgb(249, 38, 114);">is</span><span> </span><span style="color: rgb(86, 182, 194);">None</span><span> </span><span style="color: rgb(249, 38, 114);">and</span><span> self.right </span><span style="color: rgb(249, 38, 114);">is</span><span> </span><span style="color: rgb(86, 182, 194);">None</span><span>
</span> 
<span></span><span style="color: rgb(249, 38, 114);">def</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">LeftBoundary</span><span style="color: rgb(97, 174, 238);">(</span><span style="color: rgb(97, 174, 238);">root</span><span style="color: rgb(97, 174, 238);">):</span><span>
</span><span>    </span><span style="color: rgb(249, 38, 114);">if</span><span> root </span><span style="color: rgb(249, 38, 114);">is</span><span> </span><span style="color: rgb(86, 182, 194);">None</span><span>:
</span><span>        </span><span style="color: rgb(249, 38, 114);">return</span><span>
</span> 
    node = root
 
<span>    </span><span style="color: rgb(249, 38, 114);">while</span><span> </span><span style="color: rgb(249, 38, 114);">not</span><span> node.areLeaf():
</span><span>        </span><span style="color: rgb(230, 192, 123);">print</span><span>(node.val, end=</span><span style="color: rgb(152, 195, 121);">' '</span><span>)
</span><span>        node = node.left </span><span style="color: rgb(249, 38, 114);">if</span><span> node.left </span><span style="color: rgb(249, 38, 114);">else</span><span> node.right
</span> 

<span></span><span style="color: rgb(249, 38, 114);">def</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">RightBoundary</span><span style="color: rgb(97, 174, 238);">(</span><span style="color: rgb(97, 174, 238);">root</span><span style="color: rgb(97, 174, 238);">):</span><span>
</span><span>    </span><span style="color: rgb(249, 38, 114);">if</span><span> root </span><span style="color: rgb(249, 38, 114);">is</span><span> </span><span style="color: rgb(86, 182, 194);">None</span><span> </span><span style="color: rgb(249, 38, 114);">or</span><span> root.areLeaf():
</span><span>        </span><span style="color: rgb(249, 38, 114);">return</span><span>
</span> 
<span>    RightBoundary(root.right </span><span style="color: rgb(249, 38, 114);">if</span><span> root.right </span><span style="color: rgb(249, 38, 114);">else</span><span> root.left)
</span> 
<span>    </span><span style="color: rgb(230, 192, 123);">print</span><span>(root.val, end=</span><span style="color: rgb(152, 195, 121);">' '</span><span>)
</span> 

<span></span><span style="color: rgb(249, 38, 114);">def</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">LeafNodes</span><span style="color: rgb(97, 174, 238);">(</span><span style="color: rgb(97, 174, 238);">root</span><span style="color: rgb(97, 174, 238);">):</span><span>
</span><span>    </span><span style="color: rgb(249, 38, 114);">if</span><span> root </span><span style="color: rgb(249, 38, 114);">is</span><span> </span><span style="color: rgb(86, 182, 194);">None</span><span>:
</span><span>        </span><span style="color: rgb(249, 38, 114);">return</span><span>
</span>    LeafNodes(root.left)

<span>    </span><span style="color: rgb(249, 38, 114);">if</span><span> root.areLeaf():
</span><span>        </span><span style="color: rgb(230, 192, 123);">print</span><span>(root.val, end=</span><span style="color: rgb(152, 195, 121);">' '</span><span>)
</span>    LeafNodes(root.right)
 
 
<span></span><span style="color: rgb(249, 38, 114);">def</span><span style="color: rgb(97, 174, 238);"> </span><span style="color: rgb(97, 174, 238);">BoundaryTraversal</span><span style="color: rgb(97, 174, 238);">(</span><span style="color: rgb(97, 174, 238);">root</span><span style="color: rgb(97, 174, 238);">):</span><span>
</span><span>    </span><span style="color: rgb(249, 38, 114);">if</span><span> root </span><span style="color: rgb(249, 38, 114);">is</span><span> </span><span style="color: rgb(86, 182, 194);">None</span><span>:
</span><span>        </span><span style="color: rgb(249, 38, 114);">return</span><span>
</span><span>    </span><span style="color: rgb(230, 192, 123);">print</span><span>(root.val, end=</span><span style="color: rgb(152, 195, 121);">' '</span><span>)
</span> 
    LeftBoundary(root.left)
 
<span>    </span><span style="color: rgb(249, 38, 114);">if</span><span> </span><span style="color: rgb(249, 38, 114);">not</span><span> root.areLeaf():
</span>        LeafNodes(root)
 
    RightBoundary(root.right)
 
 
<span></span><span style="color: rgb(249, 38, 114);">if</span><span> __name__ == </span><span style="color: rgb(152, 195, 121);">'__main__'</span><span>:
</span> 
<span>    root = Node(</span><span style="color: rgb(209, 154, 102);">1</span><span>)
</span><span>    root.left = Node(</span><span style="color: rgb(209, 154, 102);">2</span><span>)
</span><span>    root.right = Node(</span><span style="color: rgb(209, 154, 102);">3</span><span>)
</span><span>    root.left.left = Node(</span><span style="color: rgb(209, 154, 102);">4</span><span>)
</span><span>    root.left.right = Node(</span><span style="color: rgb(209, 154, 102);">5</span><span>)
</span><span>    root.right.left = Node(</span><span style="color: rgb(209, 154, 102);">6</span><span>)
</span><span>    root.right.right = Node(</span><span style="color: rgb(209, 154, 102);">7</span><span>)
</span><span>    root.left.left.left = Node(</span><span style="color: rgb(209, 154, 102);">8</span><span>)
</span><span>    root.left.left.right = Node(</span><span style="color: rgb(209, 154, 102);">9</span><span>)
</span><span>    root.left.right.right = Node(</span><span style="color: rgb(209, 154, 102);">10</span><span>)
</span><span>    root.right.right.left = Node(</span><span style="color: rgb(209, 154, 102);">11</span><span>)
</span><span>    root.left.left.right.left = Node(</span><span style="color: rgb(209, 154, 102);">12</span><span>)
</span><span>    root.left.left.right.right = Node(</span><span style="color: rgb(209, 154, 102);">13</span><span>)
</span><span>    root.right.right.left.left = Node(</span><span style="color: rgb(209, 154, 102);">14</span><span>)
</span> 
    BoundaryTraversal(root)
</code></pre><button type="button" class="btn-icon cursor code-box_copyIcon__nChUJ" data-for="copy" data-tip="Copied" data-place="left" data-effect="solid" data-event="click" data-scroll-hide="true" data-iscapture="true" currentitem="false"><svg fill="currentColor" class="code-box_copy_icon__87vHM" version="1.1" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 32 32"><path d="M25.629 27.591v-18.051h-14.127v18.051h14.127zM25.629 7.005q1.026 0 1.811 0.755t0.785 1.781v18.051q0 1.026-0.785 1.811t-1.811 0.785h-14.127q-1.026 0-1.811-0.785t-0.785-1.811v-18.051q0-1.026 0.785-1.781t1.811-0.755h14.127zM21.766 1.813v2.596h-15.455v18.051h-2.536v-18.051q0-1.026 0.755-1.811t1.781-0.785h15.455z"></path></svg><div class="__react_component_tooltip t940a46d6-12de-4b5d-8784-76f862fb4207 place-top type-dark" id="copy" data-id="tooltip"><style aria-hidden="true">
  	.t940a46d6-12de-4b5d-8784-76f862fb4207 {
	    color: #fff;
	    background: #222;
	    border: 1px solid transparent;
	    border-radius: undefinedpx;
	    padding: 8px 21px;
  	}

  	.t940a46d6-12de-4b5d-8784-76f862fb4207.place-top {
        margin-top: -10px;
    }
    .t940a46d6-12de-4b5d-8784-76f862fb4207.place-top::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: 2;
        width: 20px;
        height: 12px;
    }
    .t940a46d6-12de-4b5d-8784-76f862fb4207.place-top::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        bottom: -6px;
        left: 50%;
        margin-left: -6px;
        transform: rotate(135deg);
    }

    .t940a46d6-12de-4b5d-8784-76f862fb4207.place-bottom {
        margin-top: 10px;
    }
    .t940a46d6-12de-4b5d-8784-76f862fb4207.place-bottom::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 18px;
        height: 10px;
    }
    .t940a46d6-12de-4b5d-8784-76f862fb4207.place-bottom::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        top: -6px;
        left: 50%;
        margin-left: -6px;
        transform: rotate(45deg);
    }

    .t940a46d6-12de-4b5d-8784-76f862fb4207.place-left {
        margin-left: -10px;
    }
    .t940a46d6-12de-4b5d-8784-76f862fb4207.place-left::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 10px;
        height: 18px;
    }
    .t940a46d6-12de-4b5d-8784-76f862fb4207.place-left::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        right: -6px;
        top: 50%;
        margin-top: -6px;
        transform: rotate(45deg);
    }

    .t940a46d6-12de-4b5d-8784-76f862fb4207.place-right {
        margin-left: 10px;
    }
    .t940a46d6-12de-4b5d-8784-76f862fb4207.place-right::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 10px;
        height: 18px;
    }
    .t940a46d6-12de-4b5d-8784-76f862fb4207.place-right::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        left: -6px;
        top: 50%;
        margin-top: -6px;
        transform: rotate(-135deg);
    }
  </style></div></button></div></pre><p><strong>Output :</strong></p><pre><div class="code-box_snippetContainer__cJ6zK"><pre style="display: block; overflow-x: auto; padding: 0.5em; color: rgb(171, 178, 191); background: rgb(40, 44, 52);"><code class="language-plaintext" style="white-space: pre;"><span>1 2 4 8 12 13 10 6 14 11 7 3
</span></code></pre><button type="button" class="btn-icon cursor code-box_copyIcon__nChUJ" data-for="copy" data-tip="Copied" data-place="left" data-effect="solid" data-event="click" data-scroll-hide="true" data-iscapture="true" currentitem="false"><svg fill="currentColor" class="code-box_copy_icon__87vHM" version="1.1" xmlns="http://www.w3.org/2000/svg" width="32" height="32" viewBox="0 0 32 32"><path d="M25.629 27.591v-18.051h-14.127v18.051h14.127zM25.629 7.005q1.026 0 1.811 0.755t0.785 1.781v18.051q0 1.026-0.785 1.811t-1.811 0.785h-14.127q-1.026 0-1.811-0.785t-0.785-1.811v-18.051q0-1.026 0.785-1.781t1.811-0.755h14.127zM21.766 1.813v2.596h-15.455v18.051h-2.536v-18.051q0-1.026 0.755-1.811t1.781-0.785h15.455z"></path></svg><div class="__react_component_tooltip t66a87833-7673-4a08-b7dd-3de5fd1e8be9 place-top type-dark" id="copy" data-id="tooltip"><style aria-hidden="true">
  	.t66a87833-7673-4a08-b7dd-3de5fd1e8be9 {
	    color: #fff;
	    background: #222;
	    border: 1px solid transparent;
	    border-radius: undefinedpx;
	    padding: 8px 21px;
  	}

  	.t66a87833-7673-4a08-b7dd-3de5fd1e8be9.place-top {
        margin-top: -10px;
    }
    .t66a87833-7673-4a08-b7dd-3de5fd1e8be9.place-top::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: 2;
        width: 20px;
        height: 12px;
    }
    .t66a87833-7673-4a08-b7dd-3de5fd1e8be9.place-top::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        bottom: -6px;
        left: 50%;
        margin-left: -6px;
        transform: rotate(135deg);
    }

    .t66a87833-7673-4a08-b7dd-3de5fd1e8be9.place-bottom {
        margin-top: 10px;
    }
    .t66a87833-7673-4a08-b7dd-3de5fd1e8be9.place-bottom::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 18px;
        height: 10px;
    }
    .t66a87833-7673-4a08-b7dd-3de5fd1e8be9.place-bottom::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        top: -6px;
        left: 50%;
        margin-left: -6px;
        transform: rotate(45deg);
    }

    .t66a87833-7673-4a08-b7dd-3de5fd1e8be9.place-left {
        margin-left: -10px;
    }
    .t66a87833-7673-4a08-b7dd-3de5fd1e8be9.place-left::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 10px;
        height: 18px;
    }
    .t66a87833-7673-4a08-b7dd-3de5fd1e8be9.place-left::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        right: -6px;
        top: 50%;
        margin-top: -6px;
        transform: rotate(45deg);
    }

    .t66a87833-7673-4a08-b7dd-3de5fd1e8be9.place-right {
        margin-left: 10px;
    }
    .t66a87833-7673-4a08-b7dd-3de5fd1e8be9.place-right::before {
        content: "";
        background-color: inherit;
        position: absolute;
        z-index: -1;
        width: 10px;
        height: 18px;
    }
    .t66a87833-7673-4a08-b7dd-3de5fd1e8be9.place-right::after {
        content: "";
        position: absolute;
        width: 10px;
        height: 10px;
        border-top-right-radius: undefinedpx;
        border: 1px solid transparent;
        background-color: #222;
        z-index: -2;
        left: -6px;
        top: 50%;
        margin-top: -6px;
        transform: rotate(-135deg);
    }
  </style></div></button></div></pre><p>As discussed above, we will find boundary traversal of binary tree in three steps:</p><p>The left boundary in top down manner that is,
<strong>1,2,4,8</strong>
The leaf nodes from left to right that is,
<strong>12,13,10,6, 14</strong>
And finally the right boundary in bottom up manner , that is,
<strong>11,7,3</strong></p><p>Thus the final output for boundary traversal of binary tree is:
<strong>1 2 4 8 12 13 10 6 14 11 7 3</strong></p><p><strong>Time complexity:</strong>  <span class="highlight--red">O(n)</span>, n is the number of nodes in the tree. Since we are traversing each node at most once thus the worst case time complexity in this case would be the time taken to traverse each node once.
<br><strong>Space Complexity:</strong> <span class="highlight--red">O(h)</span>, h is the height of a tree.Because at any time the maximum number of nodes in the recursion call stack would be the height of the tree.</p></section>
<section class="summary"><h2 id="conclusion" level="2">Conclusion</h2><p>The important things that we have discussed so far are:</p><ul>
<li>We can do boundary traversal of a binary tree in three simple steps: traverse left boundary, traverse the leaf nodes and traverse right boundary.</li>
<li><span class="highlight--red">Left boundary</span> is the path from root to the leftmost node.</li>
<li><span class="highlight--red">Right boundary</span> is the path from root to the rightmost node.</li>
<li><span class="highlight--red">Leftmost node</span> is the leaf node of the left boundary.</li>
<li><span class="highlight--red">Rightmost node</span> is the leaf node of the right boundary.</li>
<li>We need to take care that the same nodes are not printed multiple times.</li>
<li>The time complexity is <span class="highlight--red">O(n)</span> where n is the number of nodes and space complexity is <span class="highlight--red">O(h)</span> where h is the height of the tree.</li>
</ul></section></div>
