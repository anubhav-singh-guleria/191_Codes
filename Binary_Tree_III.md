## Table of Content

## Binary Tree Maximum Path Sum
<div class="elfjS" data-track-load="description_content"><p>A <strong>path</strong> in a binary tree is a sequence of nodes where each pair of adjacent nodes in the sequence has an edge connecting them. A node can only appear in the sequence <strong>at most once</strong>. Note that the path does not need to pass through the root.</p>

<p>The <strong>path sum</strong> of a path is the sum of the node's values in the path.</p>

<p>Given the <code>root</code> of a binary tree, return <em>the maximum <strong>path sum</strong> of any <strong>non-empty</strong> path</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/13/exx1.jpg" style="width: 322px; height: 182px;">
<pre><strong>Input:</strong> root = [1,2,3]
<strong>Output:</strong> 6
<strong>Explanation:</strong> The optimal path is 2 -&gt; 1 -&gt; 3 with a path sum of 2 + 1 + 3 = 6.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/13/exx2.jpg">
<pre><strong>Input:</strong> root = [-10,9,20,null,null,15,7]
<strong>Output:</strong> 42
<strong>Explanation:</strong> The optimal path is 15 -&gt; 20 -&gt; 7 with a path sum of 15 + 20 + 7 = 42.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 3 * 10<sup>4</sup>]</code>.</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
</ul>
</div>

### Solution 

```
public class Solution {
    int maxValue;
    
    public int maxPathSum(TreeNode root) {
        maxValue = Integer.MIN_VALUE;
        maxPathDown(root);
        return maxValue;
    }
    
    private int maxPathDown(TreeNode node) {
        if (node == null) return 0;
        int left = Math.max(0, maxPathDown(node.left));
        int right = Math.max(0, maxPathDown(node.right));
        maxValue = Math.max(maxValue, left + right + node.val);
        return Math.max(left, right) + node.val;
    }
}
```
## Go To
[Table of Content](#table-of-content)
## Construct Binary Tree from Preorder and Inorder Traversal
<div class="elfjS" data-track-load="description_content"><p>Given two integer arrays <code>preorder</code> and <code>inorder</code> where <code>preorder</code> is the preorder traversal of a binary tree and <code>inorder</code> is the inorder traversal of the same tree, construct and return <em>the binary tree</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/tree.jpg" style="width: 277px; height: 302px;">
<pre><strong>Input:</strong> preorder = [3,9,20,15,7], inorder = [9,3,15,20,7]
<strong>Output:</strong> [3,9,20,null,null,15,7]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> preorder = [-1], inorder = [-1]
<strong>Output:</strong> [-1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= preorder.length &lt;= 3000</code></li>
	<li><code>inorder.length == preorder.length</code></li>
	<li><code>-3000 &lt;= preorder[i], inorder[i] &lt;= 3000</code></li>
	<li><code>preorder</code> and <code>inorder</code> consist of <strong>unique</strong> values.</li>
	<li>Each value of <code>inorder</code> also appears in <code>preorder</code>.</li>
	<li><code>preorder</code> is <strong>guaranteed</strong> to be the preorder traversal of the tree.</li>
	<li><code>inorder</code> is <strong>guaranteed</strong> to be the inorder traversal of the tree.</li>
</ul>
</div>

### Solution
<img src="https://leetcode.com/problems/construct-binary-tree-from-preorder-and-inorder-traversal/Figures/105/105-Page-2.png" alt="image"></p>
<p><strong>Recursive Approach(C++):</strong><br>
<strong>Intuition:</strong> Basically we start from <code>Idx</code> 0 &amp; find <code>preorder</code>[Idx] from <code>inorder</code>, let's call it as index <code>pivot</code>.<br>
Then we create a <code>new</code> <code>node</code> with <code>inorder</code>[pivot] simultaneoulsy create its <code>left</code> child <code>recursively</code> and it's <code>right</code> child <code>recursively</code> and finally return the <code>new</code> node.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">buildTree</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> preorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> inorder</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> n </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> inorder</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> Idx </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">helper</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>preorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> inorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> Idx</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span>    TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">helper</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> preorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> inorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> Idx</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> right</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>left </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> right</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> pivot </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>  </span><span class="token" style="color: rgb(106, 153, 85);">// find the root from inorder</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>inorder</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>pivot</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> preorder</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>Idx</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> pivot</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        Idx</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> newNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>inorder</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>pivot</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        newNode</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>left </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">helper</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>preorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> inorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> Idx</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> pivot</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        newNode</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>right </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">helper</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>preorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> inorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> Idx</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> pivot</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> right</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> newNode</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<hr>
<p><strong>Time Complexity: O(N^2)</strong><br>
<strong>Space Complexity : O(N)</strong></p>
<hr>
<p><strong>Using Map Approach(C++):</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">buildTree</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> preorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> inorder</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        map</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> mp</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>preorder</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            mp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>inorder</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> root </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">construct</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>preorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>preorder</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>inorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>inorder</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>mp</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">construct</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span>preorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> preStart</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> preEnd</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span>inorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> inStart</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> inEnd</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> map</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span>mp</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>preStart</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span>preEnd </span><span class="token" style="color: rgb(212, 212, 212);">||</span><span> inStart</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span>inEnd</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> root </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>preorder</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>preStart</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> inRoot </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> mp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>val</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> numsLeft </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> inRoot</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span>inStart</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        root</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>left </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">construct</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>preorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>preStart</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>preStart</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span>numsLeft</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>inorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>inStart</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>inRoot</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>mp</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        root</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>right </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">construct</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>preorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>preStart</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span>numsLeft</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>preEnd</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>inorder</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>inRoot</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>inEnd</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>mp</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<hr>
<p><strong>Time Complexity: O(N)</strong><br>
<strong>Space Complexity : O(N)</strong></p>
<hr></div></div>

## Go To
[Table of Content](#table-of-content)
## Construct Binary Tree from Inorder and Postorder Traversal
<div class="elfjS" data-track-load="description_content"><p>Given two integer arrays <code>inorder</code> and <code>postorder</code> where <code>inorder</code> is the inorder traversal of a binary tree and <code>postorder</code> is the postorder traversal of the same tree, construct and return <em>the binary tree</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/tree.jpg" style="width: 277px; height: 302px;">
<pre><strong>Input:</strong> inorder = [9,3,15,20,7], postorder = [9,15,7,20,3]
<strong>Output:</strong> [3,9,20,null,null,15,7]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> inorder = [-1], postorder = [-1]
<strong>Output:</strong> [-1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= inorder.length &lt;= 3000</code></li>
	<li><code>postorder.length == inorder.length</code></li>
	<li><code>-3000 &lt;= inorder[i], postorder[i] &lt;= 3000</code></li>
	<li><code>inorder</code> and <code>postorder</code> consist of <strong>unique</strong> values.</li>
	<li>Each value of <code>postorder</code> also appears in <code>inorder</code>.</li>
	<li><code>inorder</code> is <strong>guaranteed</strong> to be the inorder traversal of the tree.</li>
	<li><code>postorder</code> is <strong>guaranteed</strong> to be the postorder traversal of the tree.</li>
</ul>
</div>

### Solution
<P> Similar to the upper question</P>

```
class Solution {
public:
    unordered_map<int, int>mp; // Stores (node -> index in inorder array)
    
    TreeNode* make_tree(int start, int end, int &idx, vector<int>& postorder, vector<int>& inorder){
        
		// If range for inorder is NOT valid then return NULL
        if(start > end) return NULL;
        
		// Create a node for our root node of current subtree
        TreeNode* root = new TreeNode(postorder[idx]);
        
		// Find position of current root in inorder array
        int i = mp[root->val];
		
		// Decrement our pointer to postorder array for our next upcoming root if any
        idx--;
		
		// Make a call to create right subtree, inorder range [i+1, end]
        root->right = make_tree(i+1, end, idx, postorder, inorder);
		
		// Make a call to create left subtree, inorder range [start, i-1]
        root->left = make_tree(start, i-1, idx, postorder, inorder);
        
        return root;
    }
    
    TreeNode* buildTree(vector<int>& inorder, vector<int>& postorder) {
        int idx=postorder.size()-1;
        
		// Create (nodes -> index of inorder array) mapping
        for(int i{}; i<inorder.size(); ++i){
            
            mp[inorder[i]] = i;
        }
		// Create tree starting from root at position (n-1) in postorder array
		// Range for current inirder array : [0, n-1]
        return make_tree(0, inorder.size()-1, idx, postorder, inorder);
    }
};
```
## Go To
[Table of Content](#table-of-content)
## Symmetric Tree
<div class="elfjS" data-track-load="description_content"><p>Given the <code>root</code> of a binary tree, <em>check whether it is a mirror of itself</em> (i.e., symmetric around its center).</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/symtree1.jpg" style="width: 354px; height: 291px;">
<pre><strong>Input:</strong> root = [1,2,2,3,4,4,3]
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/symtree2.jpg" style="width: 308px; height: 258px;">
<pre><strong>Input:</strong> root = [1,2,2,null,3,null,3]
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 1000]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you solve it both recursively and iteratively?</div>

### Solution

```
public boolean isSymmetric(TreeNode root) {
    return root==null || isSymmetricHelp(root.left, root.right);
}

private boolean isSymmetricHelp(TreeNode left, TreeNode right){
    if(left==null || right==null)
        return left==right;
    if(left.val!=right.val)
        return false;
    return isSymmetricHelp(left.left, right.right) && isSymmetricHelp(left.right, right.left);
}
```
## Go To
[Table of Content](#table-of-content)
## Flatten Binary Tree to Linked List
<div class="elfjS" data-track-load="description_content"><p>Given the <code>root</code> of a binary tree, flatten the tree into a "linked list":</p>

<ul>
	<li>The "linked list" should use the same <code>TreeNode</code> class where the <code>right</code> child pointer points to the next node in the list and the <code>left</code> child pointer is always <code>null</code>.</li>
	<li>The "linked list" should be in the same order as a <a href="https://en.wikipedia.org/wiki/Tree_traversal#Pre-order,_NLR" target="_blank"><strong>pre-order</strong><strong> traversal</strong></a> of the binary tree.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/14/flaten.jpg" style="width: 500px; height: 226px;">
<pre><strong>Input:</strong> root = [1,2,5,3,4,null,6]
<strong>Output:</strong> [1,null,2,null,3,null,4,null,5,null,6]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> root = []
<strong>Output:</strong> []
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> root = [0]
<strong>Output:</strong> [0]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 2000]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Can you flatten the tree in-place (with <code>O(1)</code> extra space)?</div>

### Solution

```
private TreeNode prev = null;

public void flatten(TreeNode root) {
    if (root == null)
        return;
    flatten(root.right);
    flatten(root.left);
    root.right = prev;
    root.left = null;
    prev = root;
}
```
## Go To
[Table of Content](#table-of-content)
## Mirror Tree
<div class="problems_problem_content__Xm_eO"><p><span style="font-size:18px">Given a Binary Tree, convert it into its mirror.<br>
<img alt="MirrorTree1" class="aligncenter size-full wp-image-663" src="https://contribute.geeksforgeeks.org/wp-content/uploads/mirrortrees.jpg" style="height:338px; width:591px" title="MirrorTree1">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; </span></p>

<p><span style="font-size:18px"><strong>Example 1:</strong></span></p>

<pre><span style="font-size:18px"><strong>Input:
</strong>      1
&nbsp;   /  \
&nbsp;  2    3
<strong>Output: </strong>3 1 2<strong>
Explanation: </strong>The tree is
&nbsp;&nbsp; 1&nbsp;&nbsp;  (mirror)  1
 /&nbsp;&nbsp;\&nbsp;&nbsp;  =&gt;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /&nbsp; \
2&nbsp;&nbsp;&nbsp; 3&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 3&nbsp;&nbsp;  2
The inorder of mirror is 3 1 2</span>
</pre>

<p><span style="font-size:18px"><strong>Example 2:</strong></span></p>

<pre><span style="font-size:18px"><strong>Input:
</strong>      10
&nbsp;    /  \
&nbsp;   20   30
&nbsp;  /  \
&nbsp; 40  60
<strong>Output: </strong>30 10 60 20 40<strong>
Explanation: </strong>The tree is
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 10&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 10
&nbsp;&nbsp;  /&nbsp;&nbsp;&nbsp;&nbsp;\&nbsp;&nbsp;(mirror) /&nbsp;&nbsp;&nbsp; \
&nbsp;  20&nbsp;&nbsp;&nbsp; 30&nbsp;&nbsp;&nbsp; =&gt; &nbsp; 30&nbsp;&nbsp;&nbsp; 20
&nbsp; /&nbsp;&nbsp;\&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;    /&nbsp;&nbsp;&nbsp;\
&nbsp;40&nbsp; 60&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 60&nbsp;&nbsp;&nbsp;40
The inroder traversal of mirror is
30 10 60 20 40.</span></pre>

<p><span style="font-size:18px"><strong>Your Task:</strong><br>
Just complete the <strong>function mirror()&nbsp;</strong>that takes <strong>node </strong>as <strong>paramter&nbsp; </strong>and convert it into its mirror. The printing is done by the driver code only.</span></p>

<p><span style="font-size:18px"><strong>Expected Time Complexity:&nbsp;</strong>O(N).<br>
<strong>Expected Auxiliary Space:&nbsp;</strong>O(Height of the Tree).</span></p>

<p><span style="font-size:18px"><strong>Constraints:</strong><br>
1 ≤ Number of nodes ≤ 10<sup>5</sup><br>
1 ≤ Data of a node ≤ 10<sup>5</sup></span></p>
</div>


### Solution

```
    void mirror(Node* node) {
        // code here
        if(node==nullptr)return;
        mirror(node->left);mirror(node->right);
        Node* left = node->left;
        Node*right = node->right;
        node->left = right;
        node->right = left;
        
    }
```
## Go To
[Table of Content](#table-of-content)
## Children Sum Property 
<div class="entry-content clearfix">
<p><strong>Problem Statement:&nbsp;Children Sum Property in a Binary Tree.</strong> Write a program that converts any binary tree to one that follows the children sum property.</p>
<p>The children sum property is defined as, For every node of the tree, the value of a node is equal to the sum of values of its children(left child and right child).</p>
<p><strong>Note:&nbsp;</strong></p>
<ul><li>The node values can be increased by 1 any number of times but decrement of any node value is not allowed.</li><li>A value for a NULL node can be assumed as 0.</li><li>You are not allowed to change the structure of the given binary tree.</li></ul>
<pre class="wp-block-preformatted"><strong>Example:</strong>
<img class="lazy-loaded" loading="lazy" width="624" height="351" src="https://lh4.googleusercontent.com/1sgVnICzwk4IovVn5L6Ag_hJiLaYzWQPXOX2k59ZY8gCAbsA-Tb0hKA1UWbjeebUqVh31yhVf7Pr36OFIV5E0lPSFe0BqdcdiP7Hg8Lv78krBKYLLF1cKeoFx8eHSD8Y5MIYLt9S" data-lazy-type="image" data-src="https://lh4.googleusercontent.com/1sgVnICzwk4IovVn5L6Ag_hJiLaYzWQPXOX2k59ZY8gCAbsA-Tb0hKA1UWbjeebUqVh31yhVf7Pr36OFIV5E0lPSFe0BqdcdiP7Hg8Lv78krBKYLLF1cKeoFx8eHSD8Y5MIYLt9S"><noscript><img loading="lazy" width="624" height="351" src="https://lh4.googleusercontent.com/1sgVnICzwk4IovVn5L6Ag_hJiLaYzWQPXOX2k59ZY8gCAbsA-Tb0hKA1UWbjeebUqVh31yhVf7Pr36OFIV5E0lPSFe0BqdcdiP7Hg8Lv78krBKYLLF1cKeoFx8eHSD8Y5MIYLt9S"></noscript></pre>
<p><strong>Pre-req: Tree Traversals</strong></p>
<p><strong><em>Disclaimer</em></strong>: <em>Don’t jump directly to the solution, try it out yourself first.</em></p>
<h3><strong>Solution :</strong></h3>
<p><strong>Intuition:&nbsp;</strong></p>
<p>The first intuition that comes to our mind is to do a tree traversal and at every node make the node value equal to the sum of value(s) of its children. This approach will work in a tree-like this(given below), if we do a postorder traversal and update the node values after visiting the children.</p>
<p><img class="lazy-loaded" loading="lazy" width="624" height="351" src="https://lh4.googleusercontent.com/vNaZ4hlCtK0dQk4UDDR-Q_9P1kQVgkcXV_uF9FR6x68wm3-u2V8vehmKrGmiHoz2VYh1PDTBhu4cgo_UZ-xW9IYfvUkTJo-TB0Mv-WgfQFAB_qwhSKOiMA7l_6zSt-_DySqelhGy" data-lazy-type="image" data-src="https://lh4.googleusercontent.com/vNaZ4hlCtK0dQk4UDDR-Q_9P1kQVgkcXV_uF9FR6x68wm3-u2V8vehmKrGmiHoz2VYh1PDTBhu4cgo_UZ-xW9IYfvUkTJo-TB0Mv-WgfQFAB_qwhSKOiMA7l_6zSt-_DySqelhGy"><noscript><img loading="lazy" width="624" height="351" src="https://lh4.googleusercontent.com/vNaZ4hlCtK0dQk4UDDR-Q_9P1kQVgkcXV_uF9FR6x68wm3-u2V8vehmKrGmiHoz2VYh1PDTBhu4cgo_UZ-xW9IYfvUkTJo-TB0Mv-WgfQFAB_qwhSKOiMA7l_6zSt-_DySqelhGy"></noscript></p>
<p>As in the given tree, every node value is less than the sum of the node values of its children; this approach works. Now we will see where this approach will fail and why. If we consider the following case:</p>
<p><img class="lazy-loaded" loading="lazy" width="448" height="385" src="https://lh6.googleusercontent.com/KO6I3CQo3I1aUewJ0FHU4RK64R0lUrwref89GuHbRdd8ImcIqYjXHhcOMpjWQRR3tU7H5PXc9oeNKmxOFJk8cFTPnOHRrAzmlBZJiGXB6_r_2hVNSG2ibYNBbztVjuTIc0mRC1OA" data-lazy-type="image" data-src="https://lh6.googleusercontent.com/KO6I3CQo3I1aUewJ0FHU4RK64R0lUrwref89GuHbRdd8ImcIqYjXHhcOMpjWQRR3tU7H5PXc9oeNKmxOFJk8cFTPnOHRrAzmlBZJiGXB6_r_2hVNSG2ibYNBbztVjuTIc0mRC1OA"><noscript><img loading="lazy" width="448" height="385" src="https://lh6.googleusercontent.com/KO6I3CQo3I1aUewJ0FHU4RK64R0lUrwref89GuHbRdd8ImcIqYjXHhcOMpjWQRR3tU7H5PXc9oeNKmxOFJk8cFTPnOHRrAzmlBZJiGXB6_r_2hVNSG2ibYNBbztVjuTIc0mRC1OA"></noscript></p>
<ul><li>In case (i), we see that the root node’s value is greater than the sum of both the leaf nodes. In such a case it is not possible to assign a node as the sum of its children( as we are not allowed to decrement a value). In such a case we simply assign the node value of the children to its parent.</li><li>In case (ii) as we have a tree further down, we first implement the strategy discussed in case(i), now we see that at the second level we are having both the cases where, 35 is less than (43+14) and 35 is greater than (7+9). For the latter case we again implement the strategy and make both its children 35. For the former case, we simply traverse the tree and set it to the sum of its children.</li></ul>
<p><img class="lazy-loaded" loading="lazy" width="641" height="360" src="https://lh3.googleusercontent.com/yKu216OFkEtLSetoHOT3ktkW-tTLF8QqsaviGRoohdZ17tywS_kmSwM6kp5ZOj1Cs3aYsOHI_b1TOphj3FTk1HiaZHaFZUxcskKKHwP1D-C3jWFK1Hw7QTxTYQZuExH7uoXjI3CZ" data-lazy-type="image" data-src="https://lh3.googleusercontent.com/yKu216OFkEtLSetoHOT3ktkW-tTLF8QqsaviGRoohdZ17tywS_kmSwM6kp5ZOj1Cs3aYsOHI_b1TOphj3FTk1HiaZHaFZUxcskKKHwP1D-C3jWFK1Hw7QTxTYQZuExH7uoXjI3CZ"><noscript><img loading="lazy" width="641" height="360" src="https://lh3.googleusercontent.com/yKu216OFkEtLSetoHOT3ktkW-tTLF8QqsaviGRoohdZ17tywS_kmSwM6kp5ZOj1Cs3aYsOHI_b1TOphj3FTk1HiaZHaFZUxcskKKHwP1D-C3jWFK1Hw7QTxTYQZuExH7uoXjI3CZ"></noscript></p>
<p><strong>Approach:&nbsp;</strong></p>
<p>We perform a tree traversal and check whether the current node value is greater than the sum of node values of its children. If this is the case, we simply assign its children to the same value of the current node and then recurse for the children. We do so because we are not allowed to decrement a node value. So we set the children to a large value in order to increment the parent.</p>
<p>It can happen in subsequent recursions that this child value is further changed, therefore it is necessary that when we return to a node after returning from its children, we set it to the sum of node values of its children explicitly.</p>
<p>The algorithm approach can be stated as follows:</p>
<ul><li>We perform a simple dfs traversal on the tree.</li><li>For the base case, if the node is pointing to NULL, we simply return.</li><li>At every node, first we find the sum of values of the children( For a NULL child, value is assumed to be 0).</li><li>If node’s value &gt; sum of children node value, we assign both the children’s value to their parent’s node value.</li><li>Then we visit the children using recursion.</li><li>After we return to the node after visiting its children, we explicitly set its value to be equal to the sum of its values of its children.</li></ul>

```
#include <bits/stdc++.h>

using namespace std;

struct node {
  int data;
  struct node * left, * right;
};

void reorder(node * root) {
  if (root == NULL) return;
  int child = 0;
  if (root -> left) {
    child += root -> left -> data;
  }
  if (root -> right) {
    child += root -> right -> data;
  }

  if (child < root -> data) {
    if (root -> left) root -> left -> data = root -> data;
    else if (root -> right) root -> right -> data = root -> data;
  }

  reorder(root -> left);
  reorder(root -> right);

  int tot = 0;
  if (root -> left) tot += root -> left -> data;
  if (root -> right) tot += root -> right -> data;
  if (root -> left || root -> right) root -> data = tot;
}
void changeTree(node * root) {
  reorder(root);
}

struct node * newNode(int data) {
  struct node * node = (struct node * ) malloc(sizeof(struct node));
  node -> data = data;
  node -> left = NULL;
  node -> right = NULL;

  return (node);
}

int main() {

  struct node * root = newNode(2);
  root -> left = newNode(35);
  root -> left -> left = newNode(2);
  root -> left -> right = newNode(3);
  root -> right = newNode(10);
  root -> right -> left = newNode(5);
  root -> right -> right = newNode(2);

  changeTree(root);

  return 0;
}
```
## Go To
[Table of Content](#table-of-content)
