## Table of Content
## Floor in BST
<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">You are given a BST(Binary Search Tree) with <strong>n</strong>&nbsp;number of nodes and value <strong>x</strong>. your task is to find the greatest value node of the BST which is smaller than or equal to x.<br><strong>Note:</strong> when x is smaller than the smallest node of BST then returns -1.</span></p>
<p><strong><span style="font-size: 18px;">Example:</span></strong></p>
<pre><strong><span style="font-size: 18px;">Input:</span></strong><span style="font-size: 18px;">
n = 7               2
                     \
                      81
                    /     \
                 42       87
                   \       \
                    66      90
                   /
                 45
x = 87
<strong>Output:</strong>
87
<strong>Explanation:</strong>
87 is present in tree so floor will be 87.</span>
</pre>
<p><strong><span style="font-size: 18px;">Example 2:</span></strong></p>
<pre><span style="font-size: 18px;"><strong>Input:</strong>
n = 4                     6
                           \
                            8
                          /   \
                        7       9
x = 11
<strong>Output:</strong>
9</span>
</pre>
<p><strong><span style="font-size: 18px;">Your Task:-</span></strong><br><span style="font-size: 18px;">You don't need to read input or print anything. Complete the function <strong>floor() </strong>which takes<strong>&nbsp;</strong>the integer&nbsp;<strong>n</strong>&nbsp;and BST&nbsp;and integer x returns the floor&nbsp;value.</span></p>
<p><strong><span style="font-size: 18px;">Constraint:</span></strong><br><span style="font-size: 18px;">1 &lt;= Noda data &lt;= 10<sup>9</sup><br>1 &lt;= n &lt;= 10<sup>5</sup></span></p>
<p><span style="font-size: 18px;"><strong>Expected Time Complexity:</strong> O(height of tree)<br><strong>Expected Space Complexity:</strong>&nbsp;</span><span style="font-size: 18px;">O(height of tree)</span></p></div>

### Solution

```
// Function to search a node in BST.
class Solution{

public:
    // Function to find and return the floor value of x in the BST.
    int floor(Node* root, int x) {
        int fl = -1; // Variable to store the floor value, initialized as -1.
    
        // Traverse the BST until we reach a leaf node or find the target node.
        while (root) {
            if (root->data == x) {
                return root->data; // If the current node value matches the target, return the target value.
            }
    
            if (root->data < x) {
                fl = root->data; // If the current node value is less than the target, update the floor value.
                root = root->right; // Move to the right subtree.
            } else {
                root = root->left; // If the current node value is greater than or equal to the target, move to the left subtree.
            }
        }
        return fl; // Return the floor value.
    }
};
```

## Ceil in BST
<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given a&nbsp;BST and a number <strong>X</strong>, find <strong>Ceil of X</strong>.</span><br><span style="font-size: 18px;"><strong>Note:</strong> Ceil(X) is a number that is either equal to X or is immediately greater than X.</span></p>
<p><span style="font-size: 18px;">If Ceil could not be found, return -1.</span></p>
<p><span style="font-size: 18px;"><strong>Example 1:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input:
</strong>      5
&nbsp;   /   \
&nbsp;  1     7
&nbsp;   \
&nbsp;    2 
&nbsp;     \
&nbsp;      3
X = 3
<strong>Output: </strong>3<strong>
Explanation: </strong>We find 3 in BST, so ceil
of 3 is 3.</span></pre>
<p><span style="font-size: 18px;"><strong>Example 2:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input:
</strong>     10
&nbsp;   /  \
&nbsp;  5    11
&nbsp; / \ 
&nbsp;4   7
&nbsp;     \
&nbsp;      8
X = 6
<strong>Output: </strong>7<strong>
Explanation: </strong>We find 7 in BST, so ceil
of 6 is 7.</span></pre>
<p><span style="font-size: 18px;"><strong>Your task:</strong><br>You don't need to read input or print anything. Just complete the function <strong>findCeil</strong>() to implement ceil in BST which returns the ceil of&nbsp;<strong>X&nbsp;</strong>in the given&nbsp;<strong>BST.</strong></span></p>
<p><span style="font-size: 18px;"><strong>Expected Time Complexity:&nbsp;</strong>O(Height of the BST)<br><strong>Expected Auxiliary Space:&nbsp;</strong>O(Height of the BST).</span></p>
<p><span style="font-size: 18px;"><strong>Constraints:</strong><br>1 &lt;= Number of nodes &lt;= 10<sup>5</sup><br>1 &lt;= Value of nodes&lt;= 10<sup>5</sup></span></p></div>

### Solution

```
int findCeil(struct Node* root, int input) {
    // base case
    if (root == NULL) return -1;

    // if data at current struct node is equal to given number, we return it.
    if (root->data == input) return root->data;

    // if data at current struct node is smaller than given number, we call
    // the function recursively for right subtree.
    if (root->data < input) return findCeil(root->right, input);

    // else data at current struct node is greater than given number so we call
    // the function recursively for left subtree.
    int cceil = findCeil(root->left, input);

    // returning ceil of given number.
    return (cceil >= input) ? cceil : root->data;
}
```

## Kth Smallest Element in a BST
<div class="elfjS" data-track-load="description_content"><p>Given the <code>root</code> of a binary search tree, and an integer <code>k</code>, return <em>the</em> <code>k<sup>th</sup></code> <em>smallest value (<strong>1-indexed</strong>) of all the values of the nodes in the tree</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/28/kthtree1.jpg" style="width: 212px; height: 301px;">
<pre><strong>Input:</strong> root = [3,1,4,null,2], k = 1
<strong>Output:</strong> 1
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/28/kthtree2.jpg" style="width: 382px; height: 302px;">
<pre><strong>Input:</strong> root = [5,3,6,2,4,null,null,1], k = 3
<strong>Output:</strong> 3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the tree is <code>n</code>.</li>
	<li><code>1 &lt;= k &lt;= n &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= Node.val &lt;= 10<sup>4</sup></code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> If the BST is modified often (i.e., we can do insert and delete operations) and you need to find the kth smallest frequently, how would you optimize?</p>
</div>

### Solution
<div class="FN9Jv WRmCx"><p><strong>✔️ Solution 1: Inorder Traversal</strong></p>
<ul>
<li>We traverse inorder in BST (Left - Root - Right) then we have <code>sortedArr</code> as non-decreasing sorted array af elements in BST.</li>
<li>The result is the <code>kth</code> element in our <code>sortedArr</code>.</li>
</ul>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(78, 201, 176);">List</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(78, 201, 176);">Integer</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span> sortedArr </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">ArrayList</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">kthSmallest</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> k</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">inorderTraverse</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> sortedArr</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>k</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">inorderTraverse</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">inorderTraverse</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        sortedArr</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">inorderTraverse</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p><strong>Complexity</strong></p>
<ul>
<li>Time: <code>O(N)</code></li>
<li>Space: <code>O(N)</code></li>
</ul>
<hr>
<p><strong>✔️ Solution 2: Using Stack as Iterator</strong></p>
<ul>
<li>We use idea from <a href="https://leetcode.com/problems/binary-search-tree-iterator/discuss/965584" target="_blank">173. Binary Search Tree Iterator</a> to iterate elements in order in O(H) in Space Comlpexity.</li>
<li>The idea is that we iterate through the BST, we pop from smallest elements and we just need to pop <code>k</code> times to get the <code>k_th</code> smallest element.<br>
<img src="https://assets.leetcode.com/users/hiepit/image_1589996326.png" alt="image"></li>
</ul>

```
class Solution {
    public int kthSmallest(TreeNode root, int k) {
        Stack<TreeNode> stack = new Stack<>();
        pushLeft(stack, root);
        TreeNode node = new TreeNode();
        for (int i = 0; i < k; ++i) {
            node = stack.pop(); // node is the i_th smallest element
            pushLeft(stack, node.right);
        }
        return node.val;
    }
    void pushLeft(Stack<TreeNode> stack, TreeNode root) {
        while (root != null) {
            stack.push(root);
            root = root.left;
        }
    }
}
```

<p><strong>Complexity</strong></p>
<ul>
<li>Time: <code>O(H + k)</code>, where <code>H</code> is the height of the BST.</li>
<li>Space: <code>O(H)</code></li>
</ul>
</div>

## Kth largest element in BST
<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given a <strong>Binary Search Tree</strong>. Your task is to complete the function which will return the <strong>Kth largest</strong> element without doing any modification in Binary Search Tree.</span></p>
<p><span style="font-size: 18px;"><strong>Example 1:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input:
&nbsp;     4</strong>
&nbsp;   /   \
<strong>   </strong>2     9
k = 2<strong> 
Output: </strong>4
</span></pre>
<p><span style="font-size: 18px;"><strong>Example 2:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input:
</strong>&nbsp; &nbsp; &nbsp; &nbsp;9
&nbsp; &nbsp; &nbsp;&nbsp;  \&nbsp;
&nbsp;  &nbsp;&nbsp;  &nbsp;  <strong>10</strong>
K = 1<strong>
Output: </strong>10</span>
</pre>
<p><span style="font-size: 18px;"><strong>Your Task:</strong><br>You don't need to read input or print anything. Your task is to complete the function&nbsp;<strong>kthLargest()</strong>&nbsp;which takes the root of the BST and an integer K as inputs and returns the Kth largest element in the given BST.</span></p>
<p><span style="font-size: 18px;"><strong>Expected Time Complexity:</strong>&nbsp;O(N).<br><strong>Expected Auxiliary Space:</strong> O(H) where H is max recursion stack of height H at a given time.</span></p>
<p><span style="font-size: 18px;"><strong>Constraints:</strong><br>1 &lt;= N &lt;= 10<sup>5</sup><br>1 &lt;= K &lt;= N</span></p></div>

### Solution
<p> Similar to above question just we will traverse right -> root -> left</p>

```
class Solution
{
    // return the Kth largest element in the given BST rooted at 'root'
    public int kthLargest(Node root,int K)
    {
        //Your code here
        Stack<Node> stack = new Stack<>();
        pushRight(stack,root);
        Node node = new Node(0);
        for(int i = 0;i < K ; i++){
            node = stack.pop();
            pushRight(stack, node.left);  
        }
        return node.data;
    }
    
    void pushRight(Stack<Node> stack, Node root){
        while(root != null){
            stack.push(root);
            root = root.right;
        }
    }
}
```

## 
