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

##
