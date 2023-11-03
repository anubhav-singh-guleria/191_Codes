## Linked List & Arrays - Rotate List
<div class="elfjS" data-track-load="description_content"><p>Given the <code>head</code> of a linked&nbsp;list, rotate the list to the right by <code>k</code> places.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/13/rotate1.jpg" style="width: 450px; height: 191px;">
<pre><strong>Input:</strong> head = [1,2,3,4,5], k = 2
<strong>Output:</strong> [4,5,1,2,3]
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/13/roate2.jpg" style="width: 305px; height: 350px;">
<pre><strong>Input:</strong> head = [0,1,2], k = 4
<strong>Output:</strong> [2,0,1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is in the range <code>[0, 500]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
	<li><code>0 &lt;= k &lt;= 2 * 10<sup>9</sup></code></li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>Since n may be  a large number compared to the length of list. So we need to know the length of linked list.After that, move the list after the (l-n%l )th node to the front to finish the rotation.</p>
<p>Ex: {1,2,3} k=2 Move the list after the 1st node to the front</p>
<p>Ex: {1,2,3} k=5, In this case Move the list after (3-5%3=1)st node to the front.</p>
<p>So  the code has three parts.</p>
<ol>
<li>
<p>Get the length</p>
</li>
<li>
<p>Move to the (l-n%l)th node</p>
</li>
</ol>
<p>3)Do the rotation</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">rotateRight</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>head</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">||</span><span>head</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> dummy</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    dummy</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>dummy</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>slow</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>dummy</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(106, 153, 85);">//Get the total length </span><span>
</span></span><span><span>    	fast</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">%</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">--</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//Get the i-n%i th node</span><span>
</span></span><span><span>    	slow</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>    
</span><span><span>    fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>dummy</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//Do the rotation</span><span>
</span></span><span><span>    dummy</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> dummy</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## Linked List & Arrays - Copy List with Random Pointer
<div class="elfjS" data-track-load="description_content"><p>A linked list of length <code>n</code> is given such that each node contains an additional random pointer, which could point to any node in the list, or <code>null</code>.</p>

<p>Construct a <a href="https://en.wikipedia.org/wiki/Object_copying#Deep_copy" target="_blank"><strong>deep copy</strong></a> of the list. The deep copy should consist of exactly <code>n</code> <strong>brand new</strong> nodes, where each new node has its value set to the value of its corresponding original node. Both the <code>next</code> and <code>random</code> pointer of the new nodes should point to new nodes in the copied list such that the pointers in the original list and copied list represent the same list state. <strong>None of the pointers in the new list should point to nodes in the original list</strong>.</p>

<p>For example, if there are two nodes <code>X</code> and <code>Y</code> in the original list, where <code>X.random --&gt; Y</code>, then for the corresponding two nodes <code>x</code> and <code>y</code> in the copied list, <code>x.random --&gt; y</code>.</p>

<p>Return <em>the head of the copied linked list</em>.</p>

<p>The linked list is represented in the input/output as a list of <code>n</code> nodes. Each node is represented as a pair of <code>[val, random_index]</code> where:</p>

<ul>
	<li><code>val</code>: an integer representing <code>Node.val</code></li>
	<li><code>random_index</code>: the index of the node (range from <code>0</code> to <code>n-1</code>) that the <code>random</code> pointer points to, or <code>null</code> if it does not point to any node.</li>
</ul>

<p>Your code will <strong>only</strong> be given the <code>head</code> of the original linked list.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2019/12/18/e1.png" style="width: 700px; height: 142px;">
<pre><strong>Input:</strong> head = [[7,null],[13,0],[11,4],[10,2],[1,0]]
<strong>Output:</strong> [[7,null],[13,0],[11,4],[10,2],[1,0]]
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2019/12/18/e2.png" style="width: 700px; height: 114px;">
<pre><strong>Input:</strong> head = [[1,1],[2,1]]
<strong>Output:</strong> [[1,1],[2,1]]
</pre>

<p><strong class="example">Example 3:</strong></p>

<p><strong><img alt="" src="https://assets.leetcode.com/uploads/2019/12/18/e3.png" style="width: 700px; height: 122px;"></strong></p>

<pre><strong>Input:</strong> head = [[3,null],[3,0],[3,null]]
<strong>Output:</strong> [[3,null],[3,0],[3,null]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= n &lt;= 1000</code></li>
	<li><code>-10<sup>4</sup> &lt;= Node.val &lt;= 10<sup>4</sup></code></li>
	<li><code>Node.random</code> is <code>null</code> or is pointing to some node in the linked list.</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>An intuitive solution is to keep a hash table for each node in the list, via which we just need to iterate the list in 2 rounds respectively to create nodes and assign the values for their random pointers. As a result, the space complexity of this solution is <code>O(N)</code>, although with a linear time complexity.</p>
<p><em>Note:  if we do not consider the space reversed for the output, then we could say that the algorithm does not consume any additional memory during the processing, i.e. O(1) space complexity</em></p>
<p>As an optimised solution, we could reduce the space complexity into constant. <em><strong>The idea is to associate the original node with its copy node in a single linked list. In this way, we don't need extra space to keep track of the new nodes.</strong></em></p>
<p>The algorithm is composed of the follow three steps which are also 3 iteration rounds.</p>
<ol>
<li>Iterate the original list and duplicate each node. The duplicate<br>
of each node follows its original immediately.</li>
<li>Iterate the new list and assign the random pointer for each<br>
duplicated node.</li>
<li>Restore the original list and extract the duplicated nodes.</li>
</ol>
<p>The algorithm is implemented as follows:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">RandomListNode</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">copyRandomList</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">RandomListNode</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(78, 201, 176);">RandomListNode</span><span> iter </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>  </span><span class="token" style="color: rgb(106, 153, 85);">// First round: make copy of each node,</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(106, 153, 85);">// and link them together side-by-side in a single list.</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>iter </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> iter</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>    </span><span class="token" style="color: rgb(78, 201, 176);">RandomListNode</span><span> copy </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">RandomListNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>iter</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>label</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    iter</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> copy</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    copy</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>    iter </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span>  </span><span class="token" style="color: rgb(106, 153, 85);">// Second round: assign random pointers for the copy nodes.</span><span>
</span></span><span><span>  iter </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>iter </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>iter</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>random </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>      iter</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>random </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> iter</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>random</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    iter </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> iter</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span>  </span><span class="token" style="color: rgb(106, 153, 85);">// Third round: restore the original list, and extract the copy list.</span><span>
</span></span><span><span>  iter </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(78, 201, 176);">RandomListNode</span><span> pseudoHead </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">RandomListNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(78, 201, 176);">RandomListNode</span><span> copy</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> copyIter </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> pseudoHead</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>iter </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> iter</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>    </span><span class="token" style="color: rgb(106, 153, 85);">// extract the copy</span><span>
</span></span><span><span>    copy </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> iter</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    copyIter</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> copy</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    copyIter </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> copy</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>    </span><span class="token" style="color: rgb(106, 153, 85);">// restore the original list</span><span>
</span></span><span><span>    iter</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>    iter </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> pseudoHead</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

<img src="https://raw.githubusercontent.com/hot13399/leetcode-graphic-answer/master/138.%20Copy%20List%20with%20Random%20Pointer.jpg" alt="alt text">

## Linked List & Arrays - 3Sum
<div class="elfjS" data-track-load="description_content"><p>Given an integer array nums, return all the triplets <code>[nums[i], nums[j], nums[k]]</code> such that <code>i != j</code>, <code>i != k</code>, and <code>j != k</code>, and <code>nums[i] + nums[j] + nums[k] == 0</code>.</p>

<p>Notice that the solution set must not contain duplicate triplets.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [-1,0,1,2,-1,-4]
<strong>Output:</strong> [[-1,-1,2],[-1,0,1]]
<strong>Explanation:</strong> 
nums[0] + nums[1] + nums[2] = (-1) + 0 + 1 = 0.
nums[1] + nums[2] + nums[4] = 0 + 1 + (-1) = 0.
nums[0] + nums[3] + nums[4] = (-1) + 2 + (-1) = 0.
The distinct triplets are [-1,0,1] and [-1,-1,2].
Notice that the order of the output and the order of the triplets does not matter.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [0,1,1]
<strong>Output:</strong> []
<strong>Explanation:</strong> The only possible triplet does not sum up to 0.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> nums = [0,0,0]
<strong>Output:</strong> [[0,0,0]]
<strong>Explanation:</strong> The only possible triplet sums up to 0.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>3 &lt;= nums.length &lt;= 3000</code></li>
	<li><code>-10<sup>5</sup> &lt;= nums[i] &lt;= 10<sup>5</sup></code></li>
</ul>
</div>

### Solution

```
/*

    Time Complexity : O(N^3), Here three nested loop creates the time complexity. Where N is the size of the
    array(nums).

    Space Complexity : O(N), Hash Table(set) space.

    Solved using Array(Three Nested Loop) + Sorting + Hash Table(set). Brute Force Approach.

    Note : this will give TLE.

*/


/***************************************** Approach 1 *****************************************/

class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        set<vector<int>> set;
        vector<vector<int>> output;
        for(int i=0; i<n-2; i++){
            for(int j=i+1; j<n-1; j++){
                for(int k=j+1; k<n; k++){
                    if((nums[i] + nums[j] + nums[k] == 0) && i != j && j != k && k != i){
                        set.insert({nums[i], nums[j], nums[k]});
                    }
                }
            }
        }
        for(auto it : set){
            output.push_back(it);
        }
        return output;
    }
};






/*

    Time Complexity : O(N^2), Here Two nested loop creates the time complexity. Where N is the size of the
    array(nums).

    Space Complexity : O(N), Hash Table(set) space.

    Solved using Array(Two Nested Loop) + Sorting + Hash Table(set).

*/


/***************************************** Approach 2 *****************************************/

class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        set<vector<int>> set;
        vector<vector<int>> output;
        for(int i=0; i<n-2; i++){
            int low = i+1, high = n-1;
            while(low < high){
                if(nums[i] + nums[low] + nums[high] < 0){
                    low++;
                }
                else if(nums[i] + nums[low] + nums[high] > 0){
                    high--;
                }
                else{
                    set.insert({nums[i], nums[low], nums[high]});
                    low++;
                    high--;
                }
            }
        }
        for(auto it : set){
            output.push_back(it);
        }
        return output;
    }
};






/*

    Time Complexity : O(N^2), Here Two nested loop creates the time complexity. Where N is the size of the
    array(nums).

    Space Complexity : O(1), Constant space. Extra space is only allocated for the Vector(output), however the
    output does not count towards the space complexity.

    Solved using Array(Two Nested Loop) + Sorting. Optimized Approach.

*/


/***************************************** Approach 3 *****************************************/

class Solution {
public:
    vector<vector<int>> threeSum(vector<int>& nums) {
        int n = nums.size();
        sort(nums.begin(), nums.end());
        vector<vector<int>> output;
        for(int i=0; i<n-1; i++){
            int low = i+1, high = n-1;
            while(low < high){
                if(nums[i] + nums[low] + nums[high] < 0){
                    low++;
                }
                else if(nums[i] + nums[low] + nums[high] > 0){
                    high--;
                }
                else{
                    output.push_back({nums[i], nums[low], nums[high]});
                    int tempIndex1 = low, tempIndex2 = high;
                    while(low < high && nums[low] == nums[tempIndex1]) low++;
                    while(low < high && nums[high] == nums[tempIndex2]) high--;
                }
            }
            while(i+1 < n && nums[i] == nums[i+1]) i++;
        }
        return output;
    }
};
```

## Linked List & Arrays - Trapping Rain Water

<div class="elfjS" data-track-load="description_content"><p>Given <code>n</code> non-negative integers representing an elevation map where the width of each bar is <code>1</code>, compute how much water it can trap after raining.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img src="https://assets.leetcode.com/uploads/2018/10/22/rainwatertrap.png" style="width: 412px; height: 161px;">
<pre><strong>Input:</strong> height = [0,1,0,2,1,0,1,3,2,1,2,1]
<strong>Output:</strong> 6
<strong>Explanation:</strong> The above elevation map (black section) is represented by array [0,1,0,2,1,0,1,3,2,1,2,1]. In this case, 6 units of rain water (blue section) are being trapped.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> height = [4,2,0,3,2,5]
<strong>Output:</strong> 9
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == height.length</code></li>
	<li><code>1 &lt;= n &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>0 &lt;= height[i] &lt;= 10<sup>5</sup></code></li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p><strong>✔️ Solution 1: Max Left, Max Right So Far!</strong></p>
<ul>
<li>A <code>ith</code> bar can trap the water if and only if there exists a higher bar to the left and a higher bar to the right of <code>ith</code> bar.</li>
<li>To calculate how much amount of water the <code>ith</code> bar can trap, we need to look at the maximum height of the left bar and the maximum height of the right bar, then
<ul>
<li>The water level can be formed at <code>ith</code> bar is: <code>waterLevel = min(maxLeft[i], maxRight[i])</code></li>
<li>If <code>waterLevel &gt;= height[i]</code> then <code>ith</code> bar can trap <code>waterLevel - height[i]</code> amount of water.</li>
</ul>
</li>
<li>To achieve in O(1) when looking at the maximum height of the bar on the left side and on the right side of <code>ith</code> bar, we pre-compute it:
<ul>
<li>Let <code>maxLeft[i]</code> is the maximum height of the bar on the left side of <code>ith</code> bar.</li>
<li>Let <code>maxRight[i]</code> is the maximum height of the bar on the right side of <code>ith</code> bar.</li>
</ul>
</li>
</ul>
<p><img src="https://assets.leetcode.com/users/images/defee20d-dca9-4244-8817-2f158efecc55_1627750629.6494076.png" alt="image"></p>

```
class Solution { // 4 ms, faster than 89.31%
public:
    int trap(vector<int>& height) {
        int n = height.size();
        vector<int> leftMax(n), rightMax(n);
        for (int i = 1; i < n; ++i) 
            leftMax[i] = max(height[i-1], leftMax[i-1]);
        for (int i = n-2; i >= 0; --i) 
            rightMax[i] = max(height[i+1], rightMax[i+1]);
        
        int ans = 0;
        for (int i = 0; i < n; ++i) {
            int waterLevel = min(leftMax[i], rightMax[i]);
            if (waterLevel >= height[i]) ans += waterLevel - height[i];
        }
        return ans;
    }
};
```

<p><strong>Complexity</strong></p>
<ul>
<li>Time: <code>O(N)</code>, where <code>N &lt;= 3*10^4</code> is number of bars.</li>
<li>Space: <code>O(N)</code></li>
</ul>
<hr>
<p><strong>✔️ Solution 2: Two Pointers</strong></p>
<ul>
<li>Same idea with solution 1, but now we don't need to build <code>maxLeft</code> and <code>maxRight</code> arrays, we will calculate <code>maxLeft</code> and <code>maxRight</code> as we go.</li>
<li>We start with <code>maxLeft = height[0], maxRight = height[n-1]</code>, using 2 pointers <code>left</code> point to the next bar on the left side, <code>right</code> point to the next bar on the right side.</li>
<li>How to decide to move <code>left</code> or move <code>right</code>?
<ul>
<li>If <code>maxLeft &lt; maxRight</code>, it means the water level is based on the left side (the left bar is smaller) then move left side:
<ul>
<li>If <code>height[left] &gt; maxLeft</code> then there is no trap water, we update maxLeft by <code>maxLeft = height[left]</code>.</li>
<li>Else if <code>height[left] &lt; maxLeft</code> then it can trap an amount of water, which is <code>maxLeft - height[left]</code>.</li>
<li>Move left by <code>left += 1</code></li>
</ul>
</li>
<li>Else if <code>maxLeft &gt; maxRight</code>, it means the water level is based on the right side (the right bar is smaller) then move right side:
<ul>
<li>If <code>height[right] &gt; maxRight</code> then there is no trap water, we update maxRight by <code>maxRight = height[right]</code>.</li>
<li>Else if <code>height[right] &lt; maxRight</code> then it can trap an amount of water, which is <code>maxRight - height[right]</code>.</li>
<li>Move right by <code>right -= 1</code>.</li>
</ul>
</li>
</ul>
</li>
</ul>

```
class Solution { // 0 ms, faster than 100.00%
public:
    int trap(vector<int>& height) {
        if (height.size() <= 2) return 0;
        int n = height.size(), maxLeft = height[0], maxRight = height[n-1];
        int left = 1, right = n - 2, ans = 0;
        while (left <= right) {
            if (maxLeft < maxRight) {
                if (height[left] > maxLeft)
                    maxLeft = height[left];
                else
                    ans += maxLeft - height[left];
                left += 1;
            } else {
                if (height[right] > maxRight)
                    maxRight = height[right];
                else
                    ans += maxRight - height[right];
                right -= 1;
            }
        }
        return ans;
    }
};
```

<p><strong>Complexity</strong></p>
<ul>
<li>Time: <code>O(N)</code>, where <code>N &lt;= 3*10^4</code> is number of bars.</li>
<li>Space: <code>O(1)</code></li>
</ul>
<p>If you think this <strong>post is useful</strong>, I'm happy if you <strong>give a vote</strong>. Any <strong>questions or discussions are welcome!</strong> Thank a lot.</p></div>

## Linked List & Arrays - Remove Duplicates from Sorted Array
<div class="elfjS" data-track-load="description_content"><p>Given an integer array <code>nums</code> sorted in <strong>non-decreasing order</strong>, remove the duplicates <a href="https://en.wikipedia.org/wiki/In-place_algorithm" target="_blank"><strong>in-place</strong></a> such that each unique element appears only <strong>once</strong>. The <strong>relative order</strong> of the elements should be kept the <strong>same</strong>. Then return <em>the number of unique elements in </em><code>nums</code>.</p>

<p>Consider the number of unique elements of <code>nums</code> to be <code>k</code>, to get accepted, you need to do the following things:</p>

<ul>
	<li>Change the array <code>nums</code> such that the first <code>k</code> elements of <code>nums</code> contain the unique elements in the order they were present in <code>nums</code> initially. The remaining elements of <code>nums</code> are not important as well as the size of <code>nums</code>.</li>
	<li>Return <code>k</code>.</li>
</ul>

<p><strong>Custom Judge:</strong></p>

<p>The judge will test your solution with the following code:</p>

<pre>int[] nums = [...]; // Input array
int[] expectedNums = [...]; // The expected answer with correct length

int k = removeDuplicates(nums); // Calls your implementation

assert k == expectedNums.length;
for (int i = 0; i &lt; k; i++) {
    assert nums[i] == expectedNums[i];
}
</pre>

<p>If all assertions pass, then your solution will be <strong>accepted</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,1,2]
<strong>Output:</strong> 2, nums = [1,2,_]
<strong>Explanation:</strong> Your function should return k = 2, with the first two elements of nums being 1 and 2 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [0,0,1,1,1,2,2,3,3,4]
<strong>Output:</strong> 5, nums = [0,1,2,3,4,_,_,_,_,_]
<strong>Explanation:</strong> Your function should return k = 5, with the first five elements of nums being 0, 1, 2, 3, and 4 respectively.
It does not matter what you leave beyond the returned k (hence they are underscores).
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>-100 &lt;= nums[i] &lt;= 100</code></li>
	<li><code>nums</code> is sorted in <strong>non-decreasing</strong> order.</li>
</ul>
</div>

### Solution

```
class Solution {
public:
    int removeDuplicates(vector<int>& nums) {
        int j = 1;
        for(int i = 1; i < nums.size(); i++){
            if(nums[i] != nums[i - 1]){
                nums[j] = nums[i];
                j++;
            }
        }
        return j;
    }
};
```

## Linked List & Arrays - Max Consecutive Ones
<div class="elfjS" data-track-load="description_content"><p>Given a binary array <code>nums</code>, return <em>the maximum number of consecutive </em><code>1</code><em>'s in the array</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,1,0,1,1,1]
<strong>Output:</strong> 3
<strong>Explanation:</strong> The first two digits or the last three digits are consecutive 1s. The maximum number of consecutive 1s is 3.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [1,0,1,1,0,1]
<strong>Output:</strong> 2
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>nums[i]</code> is either <code>0</code> or <code>1</code>.</li>
</ul>
</div>

### Solution
<div class="break-words"><div><div class="FN9Jv WRmCx"><div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">findMaxConsecutiveOnes</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> maxHere </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> max </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> n </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            max </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> Math</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">max</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>max</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> maxHere </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> n </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> maxHere </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> max</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span> </span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>The idea is to reset <code>maxHere</code> to 0 if we see 0, otherwise increase <code>maxHere</code> by 1<br>
The max of all <code>maxHere</code> is the solution</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>110111
</span></span><span>^ maxHere = 1
</span><span>
</span><span>110111
</span><span>.^ maxHere = 2
</span><span>
</span><span>110111
</span><span>..^ maxHere = 0
</span><span>
</span><span>110111
</span><span>...^ maxHere = 1
</span><span>
</span><span>110111
</span><span>....^ maxHere = 2
</span><span>
</span><span>110111
</span><span>.....^ maxHere = 3</span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>We can also solve this problem by setting <code>k = 0</code> of <a href="https://discuss.leetcode.com/topic/75445/java-clean-solution-easily-extensible-to-flipping-k-zero-and-follow-up-handled" target="_blank">Max Consecutive Ones II</a></p></div></div></div>


