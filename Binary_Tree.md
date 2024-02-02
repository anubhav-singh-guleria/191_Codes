## Table of Content

## Morris Inorder Traversal
<h4 id="approach-3-morris-traversal">Morris Traversal</h4>
<p>In this method, we have to use a new data structure - Threaded Binary Tree, and the strategy is as follows:</p>
<blockquote>
<p>Step 1: Initialize current as root</p>
<p>Step 2: While current is not NULL,</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-sql" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">If</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">current</span><span> does </span><span class="token" style="color: rgb(212, 212, 212);">not</span><span> have </span><span class="token" style="color: rgb(86, 156, 214);">left</span><span> child
</span></span><span>
</span><span><span>    a</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">Add</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">current</span><span>’s </span><span class="token" style="color: rgb(86, 156, 214);">value</span><span>
</span></span><span>
</span><span><span>    b</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span> Go </span><span class="token" style="color: rgb(86, 156, 214);">to</span><span> the </span><span class="token" style="color: rgb(86, 156, 214);">right</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>e</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">current</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">current</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">right</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">Else</span><span>
</span></span><span>
</span><span><span>    a</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">In</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">current</span><span>'s </span><span class="token" style="color: rgb(86, 156, 214);">left</span><span> subtree</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> make </span><span class="token" style="color: rgb(86, 156, 214);">current</span><span> the </span><span class="token" style="color: rgb(86, 156, 214);">right</span><span> child </span><span class="token" style="color: rgb(86, 156, 214);">of</span><span> the rightmost node
</span></span><span>
</span><span><span>    b</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span> Go </span><span class="token" style="color: rgb(86, 156, 214);">to</span><span> this </span><span class="token" style="color: rgb(86, 156, 214);">left</span><span> child</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>e</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">current</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">current</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">left</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
</blockquote>
<p>For example:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>
</span></span><span>          1
</span><span>        /   \
</span><span>       2     3
</span><span>      / \   /
</span><span>     4   5 6
</span><span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>First, 1 is the root, so initialize 1 as current, 1 has left child which is 2, the current's left subtree is</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>         2
</span></span><span>        / \
</span><span>       4   5</span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>So in this subtree, the rightmost node is 5, then make the current(1) as the right child of 5. Set current = current.left (current = 2).<br>
The tree now looks like:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>         2
</span></span><span>        / \
</span><span>       4   5
</span><span>            \
</span><span>             1
</span><span>              \
</span><span>               3
</span><span>              /
</span><span>             6</span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>For current 2, which has left child 4, we can continue with the same process as we did above</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>        4
</span></span><span>         \
</span><span>          2
</span><span>           \
</span><span>            5
</span><span>             \
</span><span>              1
</span><span>               \
</span><span>                3
</span><span>               /
</span><span>              6</span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>then add 4 because it has no left child, then add 2, 5, 1, 3 one by one, for node 3 which has left child 6, do the same as above.<br>
Finally, the inorder traversal is [4,2,5,1,6,3].</p>
<p>For more details, please check<br>
<a href="https://en.wikipedia.org/wiki/Threaded_binary_tree" target="_blank">Threaded binary tree</a> and<br>
<a href="https://stackoverflow.com/questions/5502916/explain-morris-inorder-tree-traversal-without-using-stacks-or-recursion" target="_blank">Explanation of Morris Method</a></p>

```
class Solution {
    public List<Integer> inorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        TreeNode curr = root;
        TreeNode pre;
        while (curr != null) {
            if (curr.left == null) {
                res.add(curr.val);
                curr = curr.right; // move to next right node
            } else { // has a left subtree
                pre = curr.left;
                while (pre.right != null) { // find rightmost
                    pre = pre.right;
                }
                pre.right = curr; // put cur after the pre node
                TreeNode temp = curr; // store cur node
                curr = curr.left; // move cur to the top of the new tree
                temp.left = null; // original cur left be null, avoid infinite loops
            }
        }
        return res;
    }
}
```
## Go To
[Table of Content](#table-of-content)
## Morris Preorder Traversal

```
class Solution {
    public List<Integer> preorderTraversal(TreeNode root) {
        List<Integer> res = new ArrayList<>();
        TreeNode curr = root;
        while (curr != null) {
            res.add(curr.val);
            
            if (curr.left != null) {
                TreeNode node1 = getRightMostNodeOfLeftSubtree(curr);
                node1.right = curr.right;
                curr = curr.left;
            } else {
                curr = curr.right;
            }
        }
        return res;
    }
    
    private TreeNode getRightMostNodeOfLeftSubtree(TreeNode node) {
        TreeNode curr = node.left;
        while (curr.right != null) {
            curr = curr.right;
        }
        return curr;
    }
}
```
## Go To
[Table of Content](#table-of-content)
## Binary Tree Right Side View
<div class="elfjS" data-track-load="description_content"><p>Given the <code>root</code> of a binary tree, imagine yourself standing on the <strong>right side</strong> of it, return <em>the values of the nodes you can see ordered from top to bottom</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/14/tree.jpg" style="width: 401px; height: 301px;">
<pre><strong>Input:</strong> root = [1,2,3,null,5,null,4]
<strong>Output:</strong> [1,3,4]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> root = [1,null,3]
<strong>Output:</strong> [1,3]
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> root = []
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 100]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>
</div>

### Solution

```
class Solution {
public:
    vector<int> rightSideView(TreeNode* root) {
        if (!root) {
            return {};
        }
        vector<int> view;
        queue<TreeNode*> todo;
        todo.push(root);
        while (!todo.empty()) {
            int n = todo.size();
            for (int i = 0; i < n; i++) {
                TreeNode* node = todo.front();
                todo.pop();
                if (i == n - 1) {
                    view.push_back(node -> val);
                }
                if (node -> left) {
                    todo.push(node -> left);
                }
                if (node -> right) {
                    todo.push(node -> right);
                }
            }
        }
        return view;
    }
};
```
## Go To
[Table of Content](#table-of-content)
## Bottom View of Binary Tree
<div class="problems_problem_content__Xm_eO"><p><span style="font-size:18px">Given a binary tree, print the bottom view from left to right.<br>
A node is included in bottom view if it can be seen when we look at the tree from bottom.</span></p>

<p><span style="font-size:18px">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 20<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /&nbsp;&nbsp;&nbsp; \<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 8&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 22<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /&nbsp;&nbsp; \&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; \<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 3&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; 25<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /&nbsp;&nbsp; \&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 10&nbsp;&nbsp;&nbsp; 14</span></p>

<p><span style="font-size:18px">For the above tree, the bottom view is 5 10 3 14 25.</span><br>
<span style="font-size:18px">If there are <strong>multiple </strong>bottom-most nodes for a horizontal distance from root, then print the later one in level traversal. For example, in the below diagram, 3 and 4 are both the bottommost nodes at horizontal distance 0, we need to print 4.</span></p>

<p><span style="font-size:18px">&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 20<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /&nbsp;&nbsp;&nbsp; \<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 8&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 22<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; /&nbsp;&nbsp; \&nbsp;&nbsp; &nbsp; /&nbsp;&nbsp; \<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 5&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 3 4&nbsp;&nbsp;&nbsp;&nbsp; 25<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; &nbsp; &nbsp;&nbsp;&nbsp; /&nbsp; &nbsp; \&nbsp;&nbsp;&nbsp;&nbsp; &nbsp;<br>
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; 10 &nbsp;&nbsp; &nbsp;&nbsp; 14</span></p>

<p><span style="font-size:18px">For the above tree the output should be 5 10 4 14 25.<br>
<br>
<strong>Note:&nbsp;</strong>The <strong>Input/Output</strong> format and <strong>Example</strong> given are used for the system's internal purpose, and should be used by a user for <strong>Expected Output </strong>only. As it is a function problem, hence a user should not read any input from the stdin/console. The task is to complete the function specified, and not to write the full code.</span><br>
&nbsp;</p>

<p><span style="font-size:18px"><strong>Example 1:</strong></span></p>

<pre><span style="font-size:18px"><strong>Input:
</strong>       1
&nbsp;    /   \
&nbsp;   3     2
<strong>Output: </strong>3 1 2<strong>
Explanation:</strong>
First case represents a tree with 3 nodes
and 2 edges where root is 1, left child of
1 is 3 and right child of 1 is 2.
<img alt="" src="https://contribute.geeksforgeeks.org/wp-content/uploads/BT-1.jpg">
Thus nodes of the binary tree will be
printed as such 3 1 2.</span></pre>

<p><span style="font-size:18px"><strong>Example 2:</strong></span></p>

<pre><span style="font-size:18px"><strong>Input:
</strong>         10
&nbsp;      /    \
&nbsp;     20    30
&nbsp;    /  \
&nbsp;   40   60
<strong>Output: </strong>40 20 60 30
</span></pre>

<p><span style="font-size:18px"><strong>Your Task:</strong><br>
This is a functional problem, you <strong>don't </strong>need to care about input, just complete the function <strong>bottomView</strong>() which takes the root node of the tree as input and returns an array&nbsp;containing the bottom view of the given tree.</span></p>

<p><span style="font-size:18px"><strong>Expected Time Complexity:&nbsp;</strong>O(N*logN).<br>
<strong>Expected Auxiliary Space:&nbsp;</strong>O(N).</span></p>

<p><span style="font-size:18px"><strong>Constraints:</strong><br>
1 &lt;= Number of nodes &lt;= 10<sup>5</sup><br>
1 &lt;= Data of a node &lt;= 10<sup>5</sup></span></p>
</div>

### Solution
<h4 id="hashmap-and-recursion-approach">Hashmap and Recursion Approach</h4>
<p>The bottom view of a binary tree refers to the bottommost nodes present at the same level.</p>
<p><strong>Algorithm</strong></p>
<ul><li>Perform a preorder traversal to calculate the level of each node of the binary tree.</li><li>Consider a hashmap and store the height into the map, where the <strong>key</strong> is the level or the horizontal distance of the <strong>ith </strong>node and the value is a pair <strong>(p, q)</strong>, where <strong>p</strong> is the value of the node and <strong>q</strong> is the height of the node.</li><li>For every node:<ul><li>Add the node to the resultant map if it is the first node to have the current horizontal distance.</li><li>Else, if a node is already present for the particular distance, replace the previous node with the current node, if the node has a height greater than the previous node.</li></ul></li></ul>

```
void bottomview(Tree * root, map<int,vector<int>>& m, int lev, int h_dist){
 if (root == NULL)
   return;
 
 if (m.find(h_dist) == m.end()) {  
   m[h_dist].push_back(lev);
   m[h_dist].push_back(root -> data);
 }
  else {
   if (m[h_dist][0] <= lev) {
     m[h_dist][0] = lev;
     m[h_dist][1]= root -> data;
   }
 }
 // Calling the function for the right and left subtrees
 // with the appropriate parameters.
 bottomview(root -> left, m, lev + 1, h_dist - 1);
 bottomview(root -> right, m, lev + 1, h_dist + 1);
}
Void print_bottom_of_binary_tree(Tree* root){
   map<int,vector<int>> Map;
   bottomview(root, Map, 1, 0);
   for (auto it = Map.begin(); it != Map.end(); ++it)
   {
     cout << (it-> second)[1]<< " ";
   }
}
```
<h4 id="queue-approach">Queue Approach</h4>
<p>The approach is to perform a level order traversal of the given binary tree and store them in a queue. Also, consider a map, which stores the horizontal distance of the nodes from root as the key.</p>
<p><strong>Algorithm</strong></p>
<ul><li>Initialise a queue to store the nodes on performing level order traversal.</li><li>Push the <strong>root</strong> of the binary tree into the queue along with its horizontal distance(<strong>hd)</strong>, which is <strong>0.</strong></li><li>Keep on pushing the left child to the queue along with their horizontal distance as <strong>hd – 1</strong> and <strong>right child </strong>&nbsp;as <strong>hd + 1</strong>.</li><li>While the queue is not empty, perform the following operations:<ul><li>Store the front element of the queue is a variable, say, <strong>res.</strong></li><li>Pop the element.</li><li>Put the dequeued element, stored in <strong>res</strong> and update its value in the map.</li><li>If a left child is present, push the left child into the queue along with its horizontal distance as <strong>hd – 1</strong>.</li><li>If a right child is present, push the right child into the queue along with its horizontal distance as <strong>hd + 1</strong>.</li></ul></li><li>Print the values in the map which contains the <strong>bottom </strong>key of the binary tree.</li></ul>

```
void bottomview(Tree * root){
    int horizontalDistance = 0;
    map<int, Tree*> mp;
    queue<pair<Tree*, int>> q;
    q.push({root, 0});
    while (!q.empty()) {
        pair<BinaryTreeNode<int> *, int> p = q.front();
        q.pop();
        mp[p.second] = p.first;
        if (p.first->left != NULL) {
            q.push({p.first->left, p.second - 1});
        }
        if (p.first->right != NULL) {
            q.push({p.first->right, p.second + 1});
        }
    }
     
   for (auto i = mp.begin(); i != mp.end(); i++) {
        cout <<(i->second->data) <<” “;
    }
}
```
## Go To
[Table of Content](#table-of-content)

## Preorder Inorder Postorder Traversals in One Traversal
<h3><strong>Solution :</strong></h3>
<p><strong>Intuition: </strong>If we study the preorder, inorder and postorder traversals, we will observe a pattern. To understand this pattern, we take a simple example:</p>
<p><img class="lazy-loaded" loading="lazy" width="624" height="224" src="https://lh6.googleusercontent.com/bOiqRQje6phiQ4PuZAfzOSKVkSFZvcKyKF7-iHtUznYdiBcMx3Rmj8YkSRbvQrKhgPS4oTamr6paZeyY72Nl1tmOnOOMOJgHR7tpv72aKgLTPSGkhXjpkpcwtmp9y3GW6wx7eNla" data-lazy-type="image" data-src="https://lh6.googleusercontent.com/bOiqRQje6phiQ4PuZAfzOSKVkSFZvcKyKF7-iHtUznYdiBcMx3Rmj8YkSRbvQrKhgPS4oTamr6paZeyY72Nl1tmOnOOMOJgHR7tpv72aKgLTPSGkhXjpkpcwtmp9y3GW6wx7eNla"><noscript><img loading="lazy" width="624" height="224" src="https://lh6.googleusercontent.com/bOiqRQje6phiQ4PuZAfzOSKVkSFZvcKyKF7-iHtUznYdiBcMx3Rmj8YkSRbvQrKhgPS4oTamr6paZeyY72Nl1tmOnOOMOJgHR7tpv72aKgLTPSGkhXjpkpcwtmp9y3GW6wx7eNla"></noscript></p>
<p>The number inside the red boxes is the visit when we print the node. In preorder traversal, we print a node at the first visit itself. Whereas, in inorder traversal at the first visit to a node, we simply traverse to the left child. It is only when we return from the left child and visit that node the second time, that we print it. Similarly, in postorder traversal, we print a node in its third visit after visiting both its children.</p>
<p><strong>Approach:&nbsp;</strong></p>
<p>The algorithm steps can be described as follows:</p>
<p>We take a stack data structure and push a pair&lt;val, num&gt; to it. Here Val is the value of the root node and num the visit to the node. Initially, the num is 1 as we are visiting the root node for the first time. We also create three separate lists for preorder, inorder and postorder traversals. Then we set an iterative loop to run till the time our stack is non-empty.</p>
<p>In every iteration, we pop the top of the stack (say, T). Then we check the second value(num) of T. Three cases can arise:</p>
<ul><li><strong>Case 1 : When num==1</strong></li></ul>
<p>This means that we are visiting the node for the very first time, therefore we push the node value to our preorder list. Then we push the same node with num=2(for Case 2). After this, we want to visit the left child. Therefore we make a new pair Y(&lt;val, num&gt;) and push it to the stack (if there exists a left child). The val of Y is equal to the left child’s node value and num is equal to 1.</p>
<ul><li><strong>Case</strong> <strong>2 : When num==2</strong></li></ul>
<p>This means that we are visiting the node for the second time, therefore on our second visit to the node, we push the node value to our inorder list. Then we push the same node with num=3( for Case 3). After this, we want to visit the right child. Therefore as in the first case, we check if there exists a right child or not. If there is, we push the right child and num value=1 as a pair to our stack.</p>
<ul><li><strong>Case 3 When num==3</strong></li></ul>
<p>This means that we are visiting the node for the third time. Therefore we will push that node’s value to our postorder list. Next, we simply want to return to the parent so we will not push anything else to the stack.</p>
<p><strong>Dry Run: </strong>In case you want to watch the dry run for this approach, please watch the video attached below.</p>

```
#include <bits/stdc++.h>

using namespace std;

struct node {
  int data;
  struct node * left, * right;
};

void allTraversal(node * root, vector < int > & pre, vector < int > & in , vector < int > & post) {
  stack < pair < node * , int >> st;
  st.push({
    root,
    1
  });
  if (root == NULL) return;

  while (!st.empty()) {
    auto it = st.top();
    st.pop();

    // this is part of pre
    // increment 1 to 2 
    // push the left side of the tree
    if (it.second == 1) {
      pre.push_back(it.first -> data);
      it.second++;
      st.push(it);

      if (it.first -> left != NULL) {
        st.push({
          it.first -> left,
          1
        });
      }
    }

    // this is a part of in 
    // increment 2 to 3 
    // push right 
    else if (it.second == 2) {
      in .push_back(it.first -> data);
      it.second++;
      st.push(it);

      if (it.first -> right != NULL) {
        st.push({
          it.first -> right,
          1
        });
      }
    }
    // don't push it back again 
    else {
      post.push_back(it.first -> data);
    }
  }
}

struct node * newNode(int data) {
  struct node * node = (struct node * ) malloc(sizeof(struct node));
  node -> data = data;
  node -> left = NULL;
  node -> right = NULL;

  return (node);
}

int main() {

  struct node * root = newNode(1);
  root -> left = newNode(2);
  root -> left -> left = newNode(4);
  root -> left -> right = newNode(5);
  root -> right = newNode(3);
  root -> right -> left = newNode(6);
  root -> right -> right = newNode(7);

  vector < int > pre, in , post;
  allTraversal(root, pre, in , post);

  cout << "The preorder Traversal is : ";
  for (auto nodeVal: pre) {
    cout << nodeVal << " ";
  }
  cout << endl;
  cout << "The inorder Traversal is : ";
  for (auto nodeVal: in ) {
    cout << nodeVal << " ";
  }
  cout << endl;
  cout << "The postorder Traversal is : ";
  for (auto nodeVal: post) {
    cout << nodeVal << " ";
  }
  cout << endl;

  return 0;
}
```

## Go To
[Table of Content](#table-of-content)

## Vertical Order Traversal of a Binary Tree
<div class="elfjS" data-track-load="description_content"><p>Given the <code>root</code> of a binary tree, calculate the <strong>vertical order traversal</strong> of the binary tree.</p>

<p>For each node at position <code>(row, col)</code>, its left and right children will be at positions <code>(row + 1, col - 1)</code> and <code>(row + 1, col + 1)</code> respectively. The root of the tree is at <code>(0, 0)</code>.</p>

<p>The <strong>vertical order traversal</strong> of a binary tree is a list of top-to-bottom orderings for each column index starting from the leftmost column and ending on the rightmost column. There may be multiple nodes in the same row and same column. In such a case, sort these nodes by their values.</p>

<p>Return <em>the <strong>vertical order traversal</strong> of the binary tree</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/29/vtree1.jpg" style="width: 431px; height: 304px;">
<pre><strong>Input:</strong> root = [3,9,20,null,null,15,7]
<strong>Output:</strong> [[9],[3,15],[20],[7]]
<strong>Explanation:</strong>
Column -1: Only node 9 is in this column.
Column 0: Nodes 3 and 15 are in this column in that order from top to bottom.
Column 1: Only node 20 is in this column.
Column 2: Only node 7 is in this column.</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/29/vtree2.jpg" style="width: 512px; height: 304px;">
<pre><strong>Input:</strong> root = [1,2,3,4,5,6,7]
<strong>Output:</strong> [[4],[2],[1,5,6],[3],[7]]
<strong>Explanation:</strong>
Column -2: Only node 4 is in this column.
Column -1: Only node 2 is in this column.
Column 0: Nodes 1, 5, and 6 are in this column.
          1 is at the top, so it comes first.
          5 and 6 are at the same position (2, 0), so we order them by their value, 5 before 6.
Column 1: Only node 3 is in this column.
Column 2: Only node 7 is in this column.
</pre>

<p><strong class="example">Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/29/vtree3.jpg" style="width: 512px; height: 304px;">
<pre><strong>Input:</strong> root = [1,2,3,4,6,5,7]
<strong>Output:</strong> [[4],[2],[1,5,6],[3],[7]]
<strong>Explanation:</strong>
This case is the exact same as example 2, but with nodes 5 and 6 swapped.
Note that the solution remains the same since 5 and 6 are in the same location and should be ordered by their values.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 1000]</code>.</li>
	<li><code>0 &lt;= Node.val &lt;= 1000</code></li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><ol>
<li>we use a hashmap to record the x-coordinate of the nodes, and record the minX and maxX to get the values</li>
<li>we use a treemap to record the y-coordinate of the nodes, and use a priorityQueue to keep the ascending order</li>
</ol>
<p>Possible Questions:</p>
<ol>
<li>
<p>why use hashmap first then treemap？<br>
This is because hashmap can get the key in constant time, while treemap gets the key in O(logn) time, where n is the number of nodes. We need to traverse the hashmap from the smallest x to the highest x. And it is easy to realize that the value of x is always continuous. That is, the difference between two continugous x will only be 1. Thus, to traverse the hashmap, we just need to record the number of minimum x and maximum x.</p>
<p>Unlike x, the value of y is not contiuous. And that's why we need a treemap. The function "keySet()" of treemap will return a series of keys in ascending order. And we can easily traverse the treemap by that.</p>
</li>
<li>
<p>Why use priorityQueue?<br>
Acutally it does not matter whether you use a priorityQueue or a List. The time complexity does not differ a lot. I think it is also a good idea to use ArrayList, and we need to sort it when we copy it to the final output.</p>
</li>
</ol>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-csharp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(78, 201, 176);">Map</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(78, 201, 176);"> TreeMap</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(78, 201, 176);"> PriorityQueue</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> map </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">HashMap</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> minX </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> maxX </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(78, 201, 176);">List</span><span class="token return-type" style="color: rgb(212, 212, 212);">&lt;</span><span class="token return-type" style="color: rgb(78, 201, 176);">List</span><span class="token return-type" style="color: rgb(212, 212, 212);">&lt;</span><span class="token return-type" style="color: rgb(78, 201, 176);">Integer</span><span class="token return-type" style="color: rgb(212, 212, 212);">&gt;</span><span class="token return-type" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">verticalTraversal</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">helper</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">List</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(78, 201, 176);">List</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> vertical </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">ArrayList</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> minX</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> maxX</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(78, 201, 176);">List</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> level </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">ArrayList</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">Integer</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> key </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> map</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">keySet</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>map</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>key</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    level</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>map</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>key</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            vertical</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>level</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> vertical</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token return-type" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">helper</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> x</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> y</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        minX </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> Math</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">min</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>minX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        maxX </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> Math</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">max</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>maxX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>map</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span> map</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">put</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>x</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">TreeMap</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">Integer</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">,</span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);"> PriorityQueue</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">Integer</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>map</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>y</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span> map</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">put</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>y</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">PriorityQueue</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">Integer</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        map</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>y</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">helper</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> x </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> y </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">helper</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> x </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> y </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>   
</span></span><span>
</span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div></div>

## Go To
[Table of Content](#table-of-content)

## Print Root to Node Path in a Binary Tree
<p><strong>Examples</strong>:</p>
<pre class="wp-block-preformatted"><img class="lazy-loaded" loading="lazy" src="https://lh6.googleusercontent.com/3Y6B1aQuy3qLmqr0CpuGqyJoExise4gMGNEuScunj_D9FCBKLO0O44xAEme7zj6sEBodlMnz4lGc3kF2rLn3OTM8W_7C9tSzU5aIi8NerFoWb3iwhkwz34P-dZToSgOxmGkLx4Ps" data-lazy-type="image" data-src="https://lh6.googleusercontent.com/3Y6B1aQuy3qLmqr0CpuGqyJoExise4gMGNEuScunj_D9FCBKLO0O44xAEme7zj6sEBodlMnz4lGc3kF2rLn3OTM8W_7C9tSzU5aIi8NerFoWb3iwhkwz34P-dZToSgOxmGkLx4Ps" width="624" height="351"><noscript><img loading="lazy" src="https://lh6.googleusercontent.com/3Y6B1aQuy3qLmqr0CpuGqyJoExise4gMGNEuScunj_D9FCBKLO0O44xAEme7zj6sEBodlMnz4lGc3kF2rLn3OTM8W_7C9tSzU5aIi8NerFoWb3iwhkwz34P-dZToSgOxmGkLx4Ps" width="624" height="351"></noscript></pre>
<pre class="wp-block-preformatted"><img class="lazy-loaded" loading="lazy" src="https://lh6.googleusercontent.com/oD5GCw00nvrkMxJNXpimy4YGbQ_YgdQ6xItZ8lD-63qxJc9TCY3gfN0hJDYPEJraKazgejxYhS3Eta997-xsvxbT11mru327vKZZV0XGV884wjoE3KupSalGMZ7SxeJmq0lB7nIk" data-lazy-type="image" data-src="https://lh6.googleusercontent.com/oD5GCw00nvrkMxJNXpimy4YGbQ_YgdQ6xItZ8lD-63qxJc9TCY3gfN0hJDYPEJraKazgejxYhS3Eta997-xsvxbT11mru327vKZZV0XGV884wjoE3KupSalGMZ7SxeJmq0lB7nIk" width="624" height="351"><noscript><img loading="lazy" src="https://lh6.googleusercontent.com/oD5GCw00nvrkMxJNXpimy4YGbQ_YgdQ6xItZ8lD-63qxJc9TCY3gfN0hJDYPEJraKazgejxYhS3Eta997-xsvxbT11mru327vKZZV0XGV884wjoE3KupSalGMZ7SxeJmq0lB7nIk" width="624" height="351"></noscript></pre>
<p><strong>Intuition:&nbsp;</strong></p>
<p>First of all, we need to find the node V in our tree for which we need to find the path. We can use any depth-first traversal technique (preorder, inorder, postorder) in order to find the required node.</p>
<p>If we look at the diagram below, we see that whenever we find the required node, its path is well present in our recursion call stack. We just need to figure out how we can use the recursive calls to print the required path.</p>
<p><img class="lazy-loaded" loading="lazy" width="624" height="351" src="https://lh3.googleusercontent.com/9KlhSI_huiydySMjCmLzo1LDOCd3MAvnobdLZqQH_EA-R6AX32H7BsHT0yNxv2D3IfpVdUKJLpeo0uNIqRzCY3w4sFWCAKVF9Seo9NZ82FOTssLdnLQxLFWFQRTuRQT28kp-K8I6" data-lazy-type="image" data-src="https://lh3.googleusercontent.com/9KlhSI_huiydySMjCmLzo1LDOCd3MAvnobdLZqQH_EA-R6AX32H7BsHT0yNxv2D3IfpVdUKJLpeo0uNIqRzCY3w4sFWCAKVF9Seo9NZ82FOTssLdnLQxLFWFQRTuRQT28kp-K8I6"><noscript><img loading="lazy" width="624" height="351" src="https://lh3.googleusercontent.com/9KlhSI_huiydySMjCmLzo1LDOCd3MAvnobdLZqQH_EA-R6AX32H7BsHT0yNxv2D3IfpVdUKJLpeo0uNIqRzCY3w4sFWCAKVF9Seo9NZ82FOTssLdnLQxLFWFQRTuRQT28kp-K8I6"></noscript></p>
<p><strong>Approach:&nbsp;</strong></p>
<p>We will use an external list to store our path. This list will be passed by reference to our recursive function. Moreover, we can set the return value of our function as boolean, this will help us to know whether node V was found in a subtree or not.</p>
<p>The algorithm steps can be stated as follows:</p>
<ul><li>We pass the function with our root node, the path list and node V.</li><li>For the base case, if root is pointing to NULL, we return false as clearly node V can’t be found.</li><li>Now we first push the node to our path list.</li><li>Then we check whether the current node is the target node or not, if it is then no further execution is needed and we return to the parent function.</li><li>If not, then we recursively call its left and right child to find the target node V. If any one of them returns true, it means we have found node V at lower levels and return true from the current function.</li><li>If the value is not found at the current node and neither in any of the recursive calls, it means that the value is not present in the current sub-tree, therefore we pop out the current node from the path list and return false.</li></ul>

```
#include <bits/stdc++.h>

using namespace std;

struct node {
  int data;
  struct node * left, * right;
};

bool getPath(node * root, vector < int > & arr, int x) {
  // if root is NULL
  // there is no path
  if (!root)
    return false;

  // push the node's value in 'arr'
  arr.push_back(root -> data);

  // if it is the required node
  // return true
  if (root -> data == x)
    return true;

  // else check whether the required node lies
  // in the left subtree or right subtree of
  // the current node
  if (getPath(root -> left, arr, x) ||
    getPath(root -> right, arr, x))
    return true;

  // required node does not lie either in the
  // left or right subtree of the current node
  // Thus, remove current node's value from
  // 'arr'and then return false   
  arr.pop_back();
  return false;
}

struct node * newNode(int data) {
  struct node * node = (struct node * ) malloc(sizeof(struct node));
  node -> data = data;
  node -> left = NULL;
  node -> right = NULL;

  return (node);
}

int main() {

  struct node * root = newNode(1);
  root -> left = newNode(2);
  root -> left -> left = newNode(4);
  root -> left -> right = newNode(5);
  root -> left -> right -> left = newNode(6);
  root -> left -> right -> right = newNode(7);
  root -> right = newNode(3);

  vector < int > arr;

  bool res;
  res = getPath(root, arr, 7);

  cout << "The path is ";
  for (auto it: arr) {
    cout << it << " ";
  }

  return 0;
}
```

## Go To
[Table of Content](#table-of-content)

## Maximum Width of Binary Tree
<div class="elfjS" data-track-load="description_content"><p>Given the <code>root</code> of a binary tree, return <em>the <strong>maximum width</strong> of the given tree</em>.</p>

<p>The <strong>maximum width</strong> of a tree is the maximum <strong>width</strong> among all levels.</p>

<p>The <strong>width</strong> of one level is defined as the length between the end-nodes (the leftmost and rightmost non-null nodes), where the null nodes between the end-nodes that would be present in a complete binary tree extending down to that level are also counted into the length calculation.</p>

<p>It is <strong>guaranteed</strong> that the answer will in the range of a <strong>32-bit</strong> signed integer.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/05/03/width1-tree.jpg" style="width: 359px; height: 302px;">
<pre><strong>Input:</strong> root = [1,3,2,5,3,null,9]
<strong>Output:</strong> 4
<strong>Explanation:</strong> The maximum width exists in the third level with length 4 (5,3,null,9).
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2022/03/14/maximum-width-of-binary-tree-v3.jpg" style="width: 442px; height: 422px;">
<pre><strong>Input:</strong> root = [1,3,2,5,null,null,9,6,null,7]
<strong>Output:</strong> 7
<strong>Explanation:</strong> The maximum width exists in the fourth level with length 7 (6,null,null,null,null,null,7).
</pre>

<p><strong class="example">Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/05/03/width3-tree.jpg" style="width: 289px; height: 299px;">
<pre><strong>Input:</strong> root = [1,3,2,5]
<strong>Output:</strong> 2
<strong>Explanation:</strong> The maximum width exists in the second level with length 2 (3,2).
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 3000]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
</ul>
</div>

### Solution

```
/**
 * Definition for a binary tree node.
 * struct TreeNode {
 *     int val;
 *     TreeNode *left;
 *     TreeNode *right;
 *     TreeNode() : val(0), left(nullptr), right(nullptr) {}
 *     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
 *     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
 * };
 */
class Solution {
public:
    int widthOfBinaryTree(TreeNode* root) {
        if (!root) return 0;
        int maxWidth = 0;
        queue<TreeNode*> node_q;
        queue<unsigned long long> index_q;
        node_q.push(root);
        index_q.push(1);
        while (!node_q.empty()) {
            int size = node_q.size();
            unsigned long long leftIndex = index_q.front(), rightIndex = 0;
            for (int i = 0; i < size; ++i) {
                TreeNode* curr = node_q.front();
                unsigned long long index = index_q.front();
                node_q.pop();
                index_q.pop();
                rightIndex = index;
                if (curr->left) {
                    node_q.push(curr->left);
                    index_q.push(index * 2);
                }
                if (curr->right) {
                    node_q.push(curr->right);
                    index_q.push(index * 2 + 1);
                }
            }
            maxWidth = max(maxWidth, (int)(rightIndex - leftIndex + 1));
        }
        return maxWidth;
    }
};
```

## Go To
[Table of Content](#table-of-content)
