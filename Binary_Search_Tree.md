## Table of Content

1. [Populating Next Right Pointers in Each Node](#populating-next-right-pointers-in-each-node)
2. [Search in a Binary Search Tree](#search-in-a-binary-search-tree)
3. [Convert Sorted Array to Binary Search Tree](#convert-sorted-array-to-binary-search-tree)
4. [Construct Binary Search Tree from Preorder Traversal](#construct-binary-search-tree-from-preorder-traversal)
5. [Validate Binary Search Tree](#validate-binary-search-tree)
6. [Lowest Common Ancestor of a Binary Search Tree](#lowest-common-ancestor-of-a-binary-search-tree)
7. [Predecessor and Successor](#predecessor-and-successor)

## Populating Next Right Pointers in Each Node
<div class="elfjS" data-track-load="description_content"><p>You are given a <strong>perfect binary tree</strong> where all leaves are on the same level, and every parent has two children. The binary tree has the following definition:</p>

<pre>struct Node {
  int val;
  Node *left;
  Node *right;
  Node *next;
}
</pre>

<p>Populate each next pointer to point to its next right node. If there is no next right node, the next pointer should be set to <code>NULL</code>.</p>

<p>Initially, all next pointers are set to <code>NULL</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2019/02/14/116_sample.png" style="width: 500px; height: 171px;">
<pre><strong>Input:</strong> root = [1,2,3,4,5,6,7]
<strong>Output:</strong> [1,#,2,3,#,4,5,6,7,#]
<strong>Explanation: </strong>Given the above perfect binary tree (Figure A), your function should populate each next pointer to point to its next right node, just like in Figure B. The serialized output is in level order as connected by the next pointers, with '#' signifying the end of each level.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> root = []
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[0, 2<sup>12</sup> - 1]</code>.</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow-up:</strong></p>

<ul>
	<li>You may only use constant extra space.</li>
	<li>The recursive approach is fine. You may assume implicit stack space does not count as extra space for this problem.</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>We are given a perfect binary tree and we need to populate next pointers in each node of the tree</p>
<hr>
<p>✔️ <em><strong>Solution - I (BFS - Right to Left)</strong></em></p>
<p>It's important to see that the given tree is a <strong>perfect binary tree</strong>. This means that each node will always have both children and only the last level of nodes will have no children.</p>
<p align="middle"><img src="https://assets.leetcode.com/uploads/2019/02/14/116_sample.png" alt="" width="500">
</p><p>Now, we need to populate next pointers of each node with nodes that occur to its immediate right on the same level. This can easily be done with BFS. Since for each node, we require the right node on the same level, we will perform a <strong>right-to-left BFS</strong> instead of the standard left-to-right BFS.</p>
<p>Before starting the traversal of each level, we would initialize a <code>rightNode</code> variable set to NULL. Then, since we are performing right-to-left BFS, we would be starting at rightmost node of each level. We set the next node of <code>cur</code> as <code>rightNode</code> and update <code>rightNode = cur</code>. This would ensure that each node would be assigned its <code>rightNode</code> properly while traversing from right to left.<br>
Also, if <code>cur</code> has a child, we would first push its right child and only then its left child (since we are doing right-to-left BFS). Once BFS is completed (after queue becomes empty), all next node would be populated and we can finally return <code>root</code>.</p>
<p>The process is illustrated below -</p>






<table><tbody><tr><td colspan="4">
<p align="middle">
<img src="https://assets.leetcode.com/users/images/01e68f51-4905-4f58-b2dd-061aa64c8a91_1640764834.4913242.png" alt="" width="350">
</p>
</td></tr><tr></tr><tr><td colspan="4">
<p align="middle">
<img src="https://assets.leetcode.com/users/images/e2a49b2c-1493-4e3f-bb36-28b89153bf73_1640768916.6068268.png" alt="" width="350">
<img src="https://assets.leetcode.com/users/images/67ff2271-2b5d-4b5f-8e31-6e14809146ad_1640765277.2783518.png" alt="" width="350">
</p>
</td></tr><tr></tr><tr><td colspan="4">
<p align="middle">
<img src="https://assets.leetcode.com/users/images/e1067d5d-3c94-4efc-b202-f4d18b93a0ac_1640765388.5706594.png" alt="" width="350">
<img src="https://assets.leetcode.com/users/images/d8a07cf0-aa8c-44b9-ab35-98a2e1422d43_1640765420.4366648.png" alt="" width="350">
<img src="https://assets.leetcode.com/users/images/ce1046fb-3212-46a5-b2f7-445ab32df816_1640765451.180103.png" alt="" width="350">
<img src="https://assets.leetcode.com/users/images/bd5a4aff-19fe-4aad-b4e6-5dee5156536f_1640765483.7865818.png" alt="" width="350">
</p>
</td></tr></tbody></table>
<p><strong>C++</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    Node</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>Node</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">nullptr</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        queue</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>Node</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> q</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>        
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            Node</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> rightNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">nullptr</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>                    </span><span class="token" style="color: rgb(106, 153, 85);">// set rightNode to null initially</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">--</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>                </span><span class="token" style="color: rgb(106, 153, 85);">// traversing each level</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">auto</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">front</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>            </span><span class="token" style="color: rgb(106, 153, 85);">// pop a node from current level and,</span><span>
</span></span><span><span>                cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> rightNode</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>                  </span><span class="token" style="color: rgb(106, 153, 85);">// set its next pointer to rightNode</span><span>
</span></span><span><span>                rightNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>                          </span><span class="token" style="color: rgb(106, 153, 85);">// update rightNode as cur for next iteration</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> right</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>                          </span><span class="token" style="color: rgb(106, 153, 85);">// if a child exists</span><span>
</span></span><span><span>                    q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> right</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>                 </span><span class="token" style="color: rgb(106, 153, 85);">// IMP: push right first to do right-to-left BFS</span><span>
</span></span><span><span>                    q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>                  </span><span class="token" style="color: rgb(106, 153, 85);">// then push left</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p><strong>Python</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-python" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">def</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>self</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">not</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">None</span><span>
</span></span><span><span>        q </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> deque</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> q</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>            rightNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">None</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> _ </span><span class="token" style="color: rgb(86, 156, 214);">in</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">range</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(206, 145, 120);">len</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>                cur </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>popleft</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>                cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> rightNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> rightNode</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> cur
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>                    q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>extend</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> root</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p><strong>Java</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Node</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">Node</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">Queue</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(78, 201, 176);">Node</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span> q </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">LinkedList</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">offer</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(78, 201, 176);">Node</span><span> rightNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">--</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(78, 201, 176);">Node</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> rightNode</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                rightNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">offer</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                    q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">offer</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>        
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p><em><strong>Time Complexity :</strong></em> <code>O(N)</code>, where <code>N</code> is the number of nodes in the given tree. We only traverse the tree once using BFS which  requires <code>O(N)</code>.<br>
<em><strong>Space Complexity :</strong></em> <code>O(W) = O(N)</code>, where <code>W</code> is the width of given tree. This is required to store the nodes in queue. Since the given tree is a perfect binary tree, its width is given as <code>W = (N+1)/2 ≈ O(N)</code></p>
<hr>
<p>✔️ <em><strong>Solution - II (DFS)</strong></em></p>
<p>We can also populate the next pointers recursively using DFS. This is slightly different logic than above but relies on the fact that the given tree is a perfect binary tree.</p>
<p>In the above solution, we had access to right nodes since we traversed in level-order. But in DFS, once we go to the next level, we cant get access to right node. So, we must update next pointers of the child of each node from the its parent's level itself. Thus at each recursive call -</p>
<ul>
<li>
<p>If child node exists:</p>
<ul>
<li>assign next of left child node as right child node: <code>root -&gt; left -&gt; next = root -&gt; right</code>. Note that, if once child exists, the other exists as well.</li>
<li>assign next of right child node as left child of root's next (if root's next exists): <code>root -&gt; right -&gt; next = root -&gt; next -&gt; left</code>.<br>
<strong>How?</strong> We need right immediate node of right child. This wont exist if current root's next node doesnt exists. If next node of current root is present (the next pointer of root would already be populated in above level) , the right immediate node of root's right child must be root's next's left child because if child of root exists, then the child of root's next must also exist.</li>
</ul>
</li>
<li>
<p>If child node doesn't exist, we have reached the last level, we can directly return since there's no child nodes to populate their next pointers</p>
</li>
</ul>
<p>The process is very similar to the one illustrated in the image below with just the difference that we are traversing with DFS instead of BFS shown below.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    Node</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>Node</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">nullptr</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">auto</span><span> L </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> R </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> right</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> N </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>L</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            L </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> R</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>                                </span><span class="token" style="color: rgb(106, 153, 85);">// next of root's left is assigned as root's right</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>N</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> R </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> N </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>                  </span><span class="token" style="color: rgb(106, 153, 85);">// next of root's right is assigned as root's next's left (if root's next exist)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>L</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>                                   </span><span class="token" style="color: rgb(106, 153, 85);">// recurse left  - simple DFS </span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>R</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>                                   </span><span class="token" style="color: rgb(106, 153, 85);">// recurse right</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p><strong>Python</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-python" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">def</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>self</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">not</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">None</span><span>
</span></span><span><span>        L</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> R</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> N </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> L</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>            L</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> R
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> N</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> R</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> N</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left
</span></span><span><span>            self</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>L</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            self</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>R</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> root</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p><strong>Java</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Node</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">Node</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">Node</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">L</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">R</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">N</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">L</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(78, 201, 176);">L</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">R</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">N</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">R</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">N</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">L</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">R</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p><em><strong>Time Complexity :</strong></em> <code>O(N)</code>, each node is only traversed once<br>
<em><strong>Space Complexity :</strong></em> <code>O(logN)</code>, required for recursive stack. The maximum depth of recursion is equal to the height of tree which in this case of perfect binary tree is equal to <code>O(logN)</code></p>
<hr>
<p>✔️ <em><strong>Solution - III (BFS - Space-Optimized Appraoch)</strong></em></p>
<p>This is a combination of logic of above logics- we will traverse in BFS manner but populate the next pointers of bottom level just as we did in the DFS solution.</p>
<p>Usually standard DFS/BFS takes <code>O(N)</code> space, but since we are given the next pointers in each node, we can use them to space-optimize our traversal to <code>O(1)</code>.</p>
<ul>
<li>We first populate the next pointers of child nodes of current level. This makes it possible to traverse the next level without using a queue. To populate next pointers of child, the exact same logic as above is used</li>
<li>We simply traverse to root's left child and repeat the process - traverse current level, fill next pointers of child nodes and then again update <code>root = root -&gt; left</code>. So, we are basically performing standard BFS traversal in <code>O(1)</code> space by using next pointers to our advantage</li>
<li>The process continues till we reach the last level of tree</li>
</ul>
<p>The process is illustrated in images below -</p>

  
  
  
  
  
  
  
  
  
  <table><tbody><tr><th>Image</th><th>Description</th></tr><tr><td><img src="https://assets.leetcode.com/users/images/b681da39-4c99-4e52-8cb8-779583022898_1640761933.124148.png" alt="" width="500"></td><td>We start with a perfect binary tree with all next pointers initially NULL</td></tr><tr></tr><tr><td>
<img src="https://assets.leetcode.com/users/images/ebbbfada-bd94-4432-ac4b-e0326fc34fd4_1640761979.3636644.png" alt="" width="500"></td><td>We start traversal level-by-level, from left to right on each level<br>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>cur </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>Every iteration, the next pointers of a node's child will be updated<br></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>	cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> right</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> right </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
</td></tr><tr></tr><tr><td><img src="https://assets.leetcode.com/users/images/4935430e-af1b-4fe1-9fc7-c5d35be45b90_1640761999.0506494.png" alt="" width="500"></td><td>Move to next level<br>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>root </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left
</span></span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">// next iteration</span><span>
</span></span><span><span>cur </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>&amp; repeat:<br></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>	cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> right</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> right </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
</td></tr><tr></tr><tr><td><img src="https://assets.leetcode.com/users/images/9ada5f9e-34f7-4c0b-b513-2bd6ff758cbc_1640762014.5024235.png" alt="" width="500"></td><td>Continue the same process with all nodes on current level<br>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(106, 153, 85);">// ...</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
</td></tr><tr></tr><tr><td><img src="https://assets.leetcode.com/users/images/8656dc5e-93fb-4260-87a7-a2261171b70d_1640762030.292751.png" alt="" width="500"></td><td>No child node exists<br>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(106, 153, 85);">// ...</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">break</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>So, we break here. On the next iteration, root becomes NULL as well and we stop the process.</p>
</td></tr></tbody></table>
<p><strong>C++</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    Node</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>Node</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">auto</span><span> head </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> root </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> 
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">auto</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>   </span><span class="token" style="color: rgb(106, 153, 85);">// traverse each level - it's just BFS taking advantage of next pointers          </span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>                          </span><span class="token" style="color: rgb(106, 153, 85);">// update next pointers of children if they exist               </span><span>
</span></span><span><span>                    cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> right</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> right </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">break</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>                                </span><span class="token" style="color: rgb(106, 153, 85);">// if no children exist, stop iteration                                                  </span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p><strong>Python</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-python" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">def</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>self</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>        head </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>            cur</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> root </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>                    cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right
</span></span><span><span>                    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">break</span><span>
</span></span><span><span>                cur </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span>                
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> head</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p><strong>Java</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Node</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">connect</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">Node</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">Node</span><span> head </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> root </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> root </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> 
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">Node</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> cur </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> 
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">break</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p><em><strong>Time Complexity :</strong></em> <code>O(N)</code>, we only traverse each node once, basically doing a standard BFS.<br>
<em><strong>Space Complexity :</strong></em> <code>O(1)</code>, only constant extra space is being used</p>
</div>

## Go To
[Table of Content](#table-of-content)
## Search in a Binary Search Tree
<div class="elfjS" data-track-load="description_content"><p>You are given the <code>root</code> of a binary search tree (BST) and an integer <code>val</code>.</p>

<p>Find the node in the BST that the node's value equals <code>val</code> and return the subtree rooted with that node. If such a node does not exist, return <code>null</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/12/tree1.jpg" style="width: 422px; height: 302px;">
<pre><strong>Input:</strong> root = [4,2,7,1,3], val = 2
<strong>Output:</strong> [2,1,3]
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/12/tree2.jpg" style="width: 422px; height: 302px;">
<pre><strong>Input:</strong> root = [4,2,7,1,3], val = 5
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 5000]</code>.</li>
	<li><code>1 &lt;= Node.val &lt;= 10<sup>7</sup></code></li>
	<li><code>root</code> is a binary search tree.</li>
	<li><code>1 &lt;= val &lt;= 10<sup>7</sup></code></li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>recursion:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-kotlin" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> TreeNode </span><span class="token" style="color: rgb(220, 220, 170);">searchBST</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>TreeNode root</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> int </span><span class="token" style="color: rgb(86, 156, 214);">val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>val </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">val</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>val</span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">searchBST</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(86, 156, 214);">val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span class="token" style="color: rgb(220, 220, 170);">searchBST</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(86, 156, 214);">val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>iteration:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-kotlin" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> TreeNode </span><span class="token" style="color: rgb(220, 220, 170);">searchBST</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>TreeNode root</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> int </span><span class="token" style="color: rgb(86, 156, 214);">val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>val </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            root </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">val</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>val</span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div></div>

## Go To
[Table of Content](#table-of-content)
## Convert Sorted Array to Binary Search Tree
<div class="elfjS" data-track-load="description_content"><p>Given an integer array <code>nums</code> where the elements are sorted in <strong>ascending order</strong>, convert <em>it to a </em><span data-keyword="height-balanced" class=" cursor-pointer relative text-dark-blue-s text-sm"><div class="popover-wrapper inline-block" data-headlessui-state=""><div><div aria-expanded="false" data-headlessui-state="" id="headlessui-popover-button-:rt:"><div><strong><em>height-balanced</em></strong></div></div><div style="position: fixed; z-index: 40; inset: 0px auto auto 0px; transform: translate(79px, 203px);"></div></div></div></span> <em>binary search tree</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/18/btree1.jpg" style="width: 302px; height: 222px;">
<pre><strong>Input:</strong> nums = [-10,-3,0,5,9]
<strong>Output:</strong> [0,-3,9,-10,null,5]
<strong>Explanation:</strong> [0,-10,5,null,-3,null,9] is also accepted:
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/18/btree2.jpg" style="width: 302px; height: 222px;">
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/18/btree.jpg" style="width: 342px; height: 142px;">
<pre><strong>Input:</strong> nums = [1,3]
<strong>Output:</strong> [3,1]
<strong>Explanation:</strong> [1,null,3] and [3,1] are both height-balanced BSTs.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>4</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li><code>nums</code> is sorted in a <strong>strictly increasing</strong> order.</li>
</ul>
</div>

### Solution

```
public TreeNode sortedArrayToBST(int[] num) {
    if (num.length == 0) {
        return null;
    }
    TreeNode head = helper(num, 0, num.length - 1);
    return head;
}

public TreeNode helper(int[] num, int low, int high) {
    if (low > high) { // Done
        return null;
    }
    int mid = (low + high) / 2;
    TreeNode node = new TreeNode(num[mid]);
    node.left = helper(num, low, mid - 1);
    node.right = helper(num, mid + 1, high);
    return node;
}
```
## Go To
[Table of Content](#table-of-content)
## Construct Binary Search Tree from Preorder Traversal
<div class="elfjS" data-track-load="description_content"><p>Given an array of integers preorder, which represents the <strong>preorder traversal</strong> of a BST (i.e., <strong>binary search tree</strong>), construct the tree and return <em>its root</em>.</p>

<p>It is <strong>guaranteed</strong> that there is always possible to find a binary search tree with the given requirements for the given test cases.</p>

<p>A <strong>binary search tree</strong> is a binary tree where for every node, any descendant of <code>Node.left</code> has a value <strong>strictly less than</strong> <code>Node.val</code>, and any descendant of <code>Node.right</code> has a value <strong>strictly greater than</strong> <code>Node.val</code>.</p>

<p>A <strong>preorder traversal</strong> of a binary tree displays the value of the node first, then traverses <code>Node.left</code>, then traverses <code>Node.right</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2019/03/06/1266.png" style="height: 386px; width: 590px;">
<pre><strong>Input:</strong> preorder = [8,5,1,7,10,12]
<strong>Output:</strong> [8,5,10,1,7,null,12]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> preorder = [1,3]
<strong>Output:</strong> [1,null,3]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= preorder.length &lt;= 100</code></li>
	<li><code>1 &lt;= preorder[i] &lt;= 1000</code></li>
	<li>All the values of <code>preorder</code> are <strong>unique</strong>.</li>
</ul>
</div>

## Go To
[Table of Content](#table-of-content)
### Solution

<div><div class="FN9Jv WRmCx"><ul>
<li>Idea is simple.</li>
<li>First item in preorder list is the root to be considered.</li>
<li>For next item in preorder list, there are 2 cases to consider:
<ul>
<li>If value is less than last item in stack, it is the left child of last item.</li>
<li>If value is greater than last item in stack, pop it.
<ul>
<li>The last popped item will be the parent and the item will be the right child of the parent.</li>
</ul>
</li>
</ul>
</li>
</ul>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-kotlin" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> Solution</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    def </span><span class="token" style="color: rgb(220, 220, 170);">bstFromPreorder</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>self</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> preorder</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> List</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>int</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>        root </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>preorder</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        stack </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> value </span><span class="token" style="color: rgb(86, 156, 214);">in</span><span> preorder</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> value </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> stack</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>val</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>                stack</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>value</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>                stack</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">append</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>stack</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> stack </span><span class="token" style="color: rgb(212, 212, 212);">and</span><span> stack</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>val </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> value</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>                    last </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> stack</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>                last</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>value</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>                stack</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">append</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>last</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> root</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div></div></div>

## Go To
[Table of Content](#table-of-content)
## Validate Binary Search Tree
<div class="elfjS" data-track-load="description_content"><p>Given the <code>root</code> of a binary tree, <em>determine if it is a valid binary search tree (BST)</em>.</p>

<p>A <strong>valid BST</strong> is defined as follows:</p>

<ul>
	<li>The left <span data-keyword="subtree" class=" cursor-pointer relative text-dark-blue-s text-sm"><div class="popover-wrapper inline-block" data-headlessui-state=""><div><div aria-expanded="false" data-headlessui-state="" id="headlessui-popover-button-:rt:"><div>subtree</div></div><div style="position: fixed; z-index: 40; inset: 0px auto auto 0px; transform: translate(115px, 256px);"></div></div></div></span> of a node contains only nodes with keys <strong>less than</strong> the node's key.</li>
	<li>The right subtree of a node contains only nodes with keys <strong>greater than</strong> the node's key.</li>
	<li>Both the left and right subtrees must also be binary search trees.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/01/tree1.jpg" style="width: 302px; height: 182px;">
<pre><strong>Input:</strong> root = [2,1,3]
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/12/01/tree2.jpg" style="width: 422px; height: 292px;">
<pre><strong>Input:</strong> root = [5,1,4,null,null,3,6]
<strong>Output:</strong> false
<strong>Explanation:</strong> The root node's value is 5 but its right child's value is 4.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[1, 10<sup>4</sup>]</code>.</li>
	<li><code>-2<sup>31</sup> &lt;= Node.val &lt;= 2<sup>31</sup> - 1</code></li>
</ul>
</div>

### Solution

```
public class Solution {
    public boolean isValidBST(TreeNode root) {
        return helper(root, null, null);
    }
    
    boolean helper(TreeNode root, Integer min, Integer max) {
        if (root == null)
            return true;
        
        if ((min != null && root.val <= min) || (max != null && root.val >= max))
            return false;
        
        return helper(root.left, min, root.val) && helper(root.right, root.val, max);
    }
}
```
## Go To
[Table of Content](#table-of-content)
## Lowest Common Ancestor of a Binary Search Tree
<div class="elfjS" data-track-load="description_content"><p>Given a binary search tree (BST), find the lowest common ancestor (LCA) node of two given nodes in the BST.</p>

<p>According to the <a href="https://en.wikipedia.org/wiki/Lowest_common_ancestor" target="_blank">definition of LCA on Wikipedia</a>: “The lowest common ancestor is defined between two nodes <code>p</code> and <code>q</code> as the lowest node in <code>T</code> that has both <code>p</code> and <code>q</code> as descendants (where we allow <strong>a node to be a descendant of itself</strong>).”</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png" style="width: 200px; height: 190px;">
<pre><strong>Input:</strong> root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 8
<strong>Output:</strong> 6
<strong>Explanation:</strong> The LCA of nodes 2 and 8 is 6.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/14/binarysearchtree_improved.png" style="width: 200px; height: 190px;">
<pre><strong>Input:</strong> root = [6,2,8,0,4,7,9,null,null,3,5], p = 2, q = 4
<strong>Output:</strong> 2
<strong>Explanation:</strong> The LCA of nodes 2 and 4 is 2, since a node can be a descendant of itself according to the LCA definition.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> root = [2,1], p = 2, q = 1
<strong>Output:</strong> 2
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is in the range <code>[2, 10<sup>5</sup>]</code>.</li>
	<li><code>-10<sup>9</sup> &lt;= Node.val &lt;= 10<sup>9</sup></code></li>
	<li>All <code>Node.val</code> are <strong>unique</strong>.</li>
	<li><code>p != q</code></li>
	<li><code>p</code> and <code>q</code> will exist in the BST.</li>
</ul>
</div>

### Solution
<ul>
<li>Let <code>large = max(p.val, q.val)</code>, <code>small = min(p.val, q.val)</code>.</li>
<li>We keep iterate <code>root</code> in our BST:
<ul>
<li>If <code>root.val &gt; large</code> then both node <code>p</code> and <code>q</code> belong to the left subtree, go to left by <code>root = root.left</code>.</li>
<li>If <code>root.val &lt; small</code> then both node <code>p</code> and <code>q</code> belong to the right subtree, go to right by <code>root = root.right</code>.</li>
<li>Now, <code>small &lt;= root.val &lt;= large</code> the current <code>root</code> is the LCA between <code>q</code> and <code>p</code>.</li>
</ul>
</li>
</ul>
<p><img src="https://assets.leetcode.com/users/images/c9441871-3cdd-49fa-b4f4-7ab1f88779f1_1626682525.9321432.png" alt="image"></p>

```
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        int small = min(p->val, q->val);
        int large = max(p->val, q->val);
        while (root != nullptr) {
            if (root->val > large) // p, q belong to the left subtree
                root = root->left;
            else if (root->val < small) // p, q belong to the right subtree
                root = root->right;
            else // Now, small <= root.val <= large -> This root is the LCA between p and q
                return root;
        }
        return nullptr;
    }
};
```
## Go To
[Table of Content](#table-of-content)
## Predecessor and Successor
<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">There is BST given with the root node with the key part as an integer only. You need to find the in-order <strong>successor</strong> and <strong>predecessor</strong> of a given key. If either predecessor or successor is not found, then set it to <strong>NULL</strong>.</span></p>
<p><span style="font-size: 18px;"><strong>Note</strong>:- In an inorder traversal the number just <strong>smaller</strong> than the target is the predecessor and the number just <strong>greater</strong> than the target is the successor.&nbsp;</span></p>
<p><span style="font-size: 18px;"><strong>Example 1:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input:<br></strong></span></pre>
<pre>      8
&nbsp;   /   \
&nbsp;  1     9
&nbsp;   \     \
&nbsp;    4    10
&nbsp;   /
&nbsp;  3</pre>
<pre><span style="font-size: 18px;">key = 8 <strong>Output: <br></strong>4 9<strong> Explanation: <br></strong>In the given BST the inorder predecessor of 8 is 4 and inorder successor of 8 is 9.</span></pre>
<p><span style="font-size: 18px;"><strong>Example 2:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input:</strong><br></span></pre>
<pre>        10
&nbsp;     /   \
&nbsp;    2    11
&nbsp;  /  \ 
&nbsp; 1    5
&nbsp;     /  \
&nbsp;    3    6
&nbsp;     \
&nbsp;      4</pre>
<pre><span style="font-size: 18px;">key = 11 <strong>Output: <br></strong>10 -1<strong> Explanation: <br></strong>In given BST, the inorder predecessor of 11 is 10 whereas it does not have any inorder successor.</span></pre>
<p><span style="font-size: 14pt;"><strong>Your Task: </strong>You don't need to print anything. You need to update <strong>pre </strong>with the predecessor of the key or <strong>NULL </strong>if the predecessor doesn't exist and <strong>succ </strong>to the successor of the key&nbsp;</span><span style="font-size: 18.6667px;">or <strong>NULL </strong>if the </span><span style="font-size: 18.6667px;">successor </span><span style="font-size: 18.6667px;">doesn't exist</span><span style="font-size: 14pt;">. pre and succ are passed as an argument to the function&nbsp;</span><strong><span style="font-size: 18.6667px;">findPreSuc()</span></strong><span style="font-size: 14pt;">.&nbsp;</span></p>
<p><strong style="font-size: 18px;"><strong>Expected Time Complexity:&nbsp;</strong><span style="font-weight: 400;">O(Height of the BST).</span><br style="font-weight: 400;"><strong>Expected Auxiliary Space:&nbsp;</strong><span style="font-weight: 400;">O(Height of the BST).</span></strong></p>
<p><strong style="font-size: 18px;">Constraints:&nbsp;</strong><span style="font-size: 18px;"><br>1 &lt;= Number of nodes &lt;= 10<sup>4</sup><br>1 &lt;= key of node &lt;= 10<sup>7</sup><br>1 &lt;= key &lt;= 10<sup>7</sup></span><br>&nbsp;</p></div>

### Solution 
<p>The main idea is to use binary search approach for finding key node as this is a BST and for predecessor and successor nodes we can use the below concept:</p>
<ul><li>A node’s predecessor in a BST is the greatest value present in its left subtree. If the left subtree doesn’t exist, then the predecessor can be one of his ancestors.</li><li>Similarly, a node’s successor in a BST is the smallest value present in its right subtree. If the right subtree doesn’t exist, then the successor can be one of his ancestors.</li></ul>
<ul><li>Check if root is NULL then return <strong>(Base case)</strong>.</li><li>If the<strong> value of the current node is smaller than the given node</strong>, we will set the predecessor as the current node and move to its right child.</li><li>Else, <strong>we will set the successor as the current node</strong> and move to its left child.</li><li>And if we reach the node which is equal to the value of given node, then find the maximum value of the left subtree and the minimum value of the right subtree from the current root node. Then set the values of the predecessor and successor, accordingly.</li></ul>
<blockquote><figure class="image"><img src="https://media.geeksforgeeks.org/wp-content/uploads/20230603164444/treeee111.gif" srcset="https://media.geeksforgeeks.org/wp-content/uploads/20230603164444/treeee111.gif 1920w, " sizes="100vw" width="1920"><figcaption>&nbsp;</figcaption></figure></blockquote>
<ul><li><strong>Time Complexity: O(H),</strong> where H is the height of the tree. In the worst case, we travel the whole height of the tree.</li><li><strong>Auxiliary Space: O(H),</strong> Space taken by the recursive stack.</li></ul>

```
class Solution
{
    public:
    void findPreSuc(Node* root, Node*& pre, Node*& suc, int key)
    {
    	// Base case
    	if (root == NULL) return ;
    
    	// If key is present at root
    	if (root->key == key)
    	{
    		// the maximum value in left subtree is predecessor
    		if (root->left != NULL)
    		{
    			Node* tmp = root->left;
    			while (tmp->right)
    				tmp = tmp->right;
    			pre = tmp ;
    		}
    
    		// the minimum value in right subtree is successor
    		if (root->right != NULL)
    		{
    			Node* tmp = root->right ;
    			while (tmp->left)
    				tmp = tmp->left ;
    			suc = tmp ;
    		}
    		return ;
    	}
    
    	// If key is smaller than root's key, go to left subtree
    	if (root->key > key)
    	{
    		suc = root ;
    		findPreSuc(root->left, pre, suc, key) ;
    	}
    	else // go to right subtree
    	{
    		pre = root ;
    		findPreSuc(root->right, pre, suc, key) ;
    	}
    }
};
```
## Go To
[Table of Content](#table-of-content)
