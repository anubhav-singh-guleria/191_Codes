
## Table of Content
1. [Reverse Linked List](#linked-list---reverse-linked-list)
2. [Middle of the Linked List](#linked-list---middle-of-the-linked-list)
3. [Merge Two Sorted Lists](#linked-list---merge-two-sorted-lists)
4. [Remove Nth Node from End of List](#linked-list---remove-nth-node-from-end-of-list)
5. [Add Two Numbers](#linked-list---add-two-numbers)
6. [Delete Node in a Linked List](#linked-list---delete-node-in-a-linked-list)
7. [Intersection of Two Linked Lists](#linked-list---intersection-of-two-linked-lists)
8. [Linked List Cycle](#linked-list---linked-list-cycle)
9. [Reverse Nodes in k-Group](#linked-list---reverse-nodes-in-k-group)
10. [Palindrome Linked List](#linked-list---palindrome-linked-list)
11. [Linked List Cycle II](#linked-list-linked-list-cycle-ii)
12. [Flattening a Linked List](#linked-list---flattening-a-linked-list)

## Linked List - Reverse Linked List
<div class="elfjS" data-track-load="description_content"><p>Given the <code>head</code> of a singly linked list, reverse the list, and return <em>the reversed list</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/rev1ex1.jpg" style="width: 542px; height: 222px;">
<pre><strong>Input:</strong> head = [1,2,3,4,5]
<strong>Output:</strong> [5,4,3,2,1]
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/02/19/rev1ex2.jpg" style="width: 182px; height: 222px;">
<pre><strong>Input:</strong> head = [1,2]
<strong>Output:</strong> [2,1]
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> head = []
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is the range <code>[0, 5000]</code>.</li>
	<li><code>-5000 &lt;= Node.val &lt;= 5000</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> A linked list can be reversed either iteratively or recursively. Could you implement both?</p>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>Not sure how this problem is expecting me to use less memory than this, but here is the deal:</p>
<ul>
<li>we are going to use 3 variables: <code>prevNode</code>, <code>head</code> and <code>nextNode</code>, that you can easily guess what are meant to represent as we go;</li>
<li>we will initialise <code>prevNode</code> to <code>NULL</code>, while <code>nextNode</code> can stay empty;</li>
<li>we are then going to loop until our current main iterator (<code>head</code>) is truthy (ie: not <code>NULL</code>), which would imply we reached the end of the list;</li>
<li>during the iteration, we first of all update <code>nextNode</code> so that it acquires its namesake value, the one of the next node indeed: <code>head-&gt;next</code>;</li>
<li>we then proceeding "reversing" <code>head-&gt;next</code> and assigning it the value of <code>prevNode</code>, while <code>prevNode</code> will become take the current value of <code>head</code>;</li>
<li>finally, we update <code>head</code> with the value we stored in <code>nextNode</code> and go on with the loop until we can. After the loop, we return <code>prevNode</code>.</li>
</ul>
<p>I know it is complex, but I find this gif from another platform to make the whole logic much easier to understand (bear in mind we do not need <code>curr</code> and will just use <code>head</code> in its place):</p>
<p><img src="https://media.geeksforgeeks.org/wp-content/cdn-uploads/RGIF2.gif" alt="reverting a list"></p>
<p>The code:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">reverseList</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        ListNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>nextNode</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>prevNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>head</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            nextNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            head</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> prevNode</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            prevNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            head </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nextNode</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> prevNode</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>Relatively trivial refactor (the function does basically the same) with recursion and comma operator to make it one-line:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">reverseList</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>ListNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> ListNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>nextNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> ListNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>prevNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> head </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">reverseList</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>head</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>head</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> prevNode</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> nextNode</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> prevNode</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## Linked List - Middle of the Linked List
<div class="elfjS" data-track-load="description_content"><p>Given the <code>head</code> of a singly linked list, return <em>the middle node of the linked list</em>.</p>

<p>If there are two middle nodes, return <strong>the second middle</strong> node.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/07/23/lc-midlist1.jpg" style="width: 544px; height: 65px;">
<pre><strong>Input:</strong> head = [1,2,3,4,5]
<strong>Output:</strong> [3,4,5]
<strong>Explanation:</strong> The middle node of the list is node 3.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/07/23/lc-midlist2.jpg" style="width: 664px; height: 65px;">
<pre><strong>Input:</strong> head = [1,2,3,4,5,6]
<strong>Output:</strong> [4,5,6]
<strong>Explanation:</strong> Since the list has two middle nodes with values 3 and 4, we return the second one.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is in the range <code>[1, 100]</code>.</li>
	<li><code>1 &lt;= Node.val &lt;= 100</code></li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>Each time, <code>slow</code> go 1 steps while <code>fast</code> go 2 steps.<br>
When <code>fast</code> arrives at the end, <code>slow</code> will arrive right in the middle.</p>
<p><strong>C++:</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-ruby" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>    ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> middleNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        ListNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(86, 156, 214);">next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(86, 156, 214);">next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(86, 156, 214);">next</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(86, 156, 214);">next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p><strong>Java:</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">middleNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p><strong>Python:</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-python" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">def</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">middleNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>self</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>        slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> fast </span><span class="token" style="color: rgb(86, 156, 214);">and</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>            slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span><span>            fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> slow</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## Linked List - Merge Two Sorted Lists
<div class="elfjS" data-track-load="description_content"><p>You are given the heads of two sorted linked lists <code>list1</code> and <code>list2</code>.</p>

<p>Merge the two lists into one <strong>sorted</strong> list. The list should be made by splicing together the nodes of the first two lists.</p>

<p>Return <em>the head of the merged linked list</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/merge_ex1.jpg" style="width: 662px; height: 302px;">
<pre><strong>Input:</strong> list1 = [1,2,4], list2 = [1,3,4]
<strong>Output:</strong> [1,1,2,3,4,4]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> list1 = [], list2 = []
<strong>Output:</strong> []
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> list1 = [], list2 = [0]
<strong>Output:</strong> [0]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in both lists is in the range <code>[0, 50]</code>.</li>
	<li><code>-100 &lt;= Node.val &lt;= 100</code></li>
	<li>Both <code>list1</code> and <code>list2</code> are sorted in <strong>non-decreasing</strong> order.</li>
</ul>
</div>

### Solution

```
ListNode* mergeTwoLists(ListNode* l1, ListNode* l2) {
    if (l1 == NULL) return l2;
    if (l2 == NULL) return l1;
    if (l1->val <= l2->val) {
        l1->next = mergeTwoLists(l1->next, l2);
        return l1;
    } else {
        l2->next = mergeTwoLists(l1, l2->next);
        return l2;
    }
}
```

## Linked List - Remove Nth Node From End of List
<div class="elfjS" data-track-load="description_content"><p>Given the <code>head</code> of a linked list, remove the <code>n<sup>th</sup></code> node from the end of the list and return its head.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/remove_ex1.jpg" style="width: 542px; height: 222px;">
<pre><strong>Input:</strong> head = [1,2,3,4,5], n = 2
<strong>Output:</strong> [1,2,3,5]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> head = [1], n = 1
<strong>Output:</strong> []
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> head = [1,2], n = 1
<strong>Output:</strong> [1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is <code>sz</code>.</li>
	<li><code>1 &lt;= sz &lt;= 30</code></li>
	<li><code>0 &lt;= Node.val &lt;= 100</code></li>
	<li><code>1 &lt;= n &lt;= sz</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Could you do this in one pass?</p>
</div>

## Solution

<h4 id="idea"><em><strong>Idea:</strong></em></h4>
<p>With a singly linked list, the <em>only</em> way to find the end of the list, and thus the <strong>n</strong>'th node from the end, is to actually iterate all the way to the end. The challenge here is attemping to find the solution in only one pass. A naive approach here might be to store pointers to each node in an array, allowing us to calculate the <strong>n</strong>'th from the end once we reach the end, but that would take <strong>O(M) extra space</strong>, where <strong>M</strong> is the length of the linked list.</p>
<p>A slightly less naive approach would be to only store only the last <strong>n+1</strong> node pointers in the array. This could be achieved by overwriting the elements of the storage array in circlular fashion as we iterate through the list. This would lower the <strong>space complexity</strong> to <strong>O(N+1)</strong>.</p>
<p>In order to solve this problem in only one pass and <strong>O(1) extra space</strong>, however, we would need to find a way to <em>both</em> reach the end of the list with one pointer <em>and also</em> reach the <strong>n</strong>'th node from the end simultaneously with a second pointer.</p>
<p>To do that, we can simply stagger our two pointers by <strong>n</strong> nodes by giving the first pointer (<strong>fast</strong>) a head start before starting the second pointer (<strong>slow</strong>). Doing this will cause <strong>slow</strong> to reach the <strong>n</strong>'th node from the end at the same time that <strong>fast</strong> reaches the end.</p>
<p><img src="https://i.imgur.com/BSiLKj0.png" alt="Visual 1"></p>
<p>Since we will need access to the node <em>before</em> the target node in order to remove the target node, we can use <strong>fast.next == null</strong> as our exit condition, rather than <strong>fast == null</strong>, so that we stop one node earlier.</p>
<p>This will unfortunately cause a problem when <strong>n</strong> is the same as the length of the list, which would make the first node the target node, and thus make it impossible to find the node <em>before</em> the target node. If that's the case, however, we can just <strong>return head.next</strong> without needing to stitch together the two sides of the target node.</p>
<p>Otherwise, once we succesfully find the node <em>before</em> the target, we can then stitch it together with the node <em>after</em> the target, and then <strong>return head</strong>.</p>
<hr>
<h4 id="implementation"><em><strong>Implementation:</strong></em></h4>
<p>There are only minor differences between the code of all four languages.</p>
<hr>
<h4 id="javascript-code"><em><strong>Javascript Code:</strong></em></h4>
<p>The best result for the code below is <strong>60ms / 40.6MB</strong> (beats 100% / 13%).</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-javascript" style="color: rgb(156, 220, 254); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">var</span><span> </span><span class="token function-variable" style="color: rgb(220, 220, 170);">removeNthFromEnd</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">function</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(156, 220, 254);">head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(156, 220, 254);"> n</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">let</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head
</span></span><span><span>    </span><span class="token" style="color: rgb(197, 134, 192);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">let</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>fast</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(197, 134, 192);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span>
</span></span><span><span>    slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> head
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<h4 id="python-code"><em><strong>Python Code:</strong></em></h4>
<p>The best result for the code below is <strong>28ms / 13.9MB</strong> (beats 92% / 99%).</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-python" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">def</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">removeNthFromEnd</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>self</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> ListNode</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">int</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> ListNode</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>        fast</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> head
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> _ </span><span class="token" style="color: rgb(86, 156, 214);">in</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">range</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">not</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span><span>        slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> head</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<h4 id="java-code"><em><strong>Java Code:</strong></em></h4>
<p>The best result for the code below is <strong>0ms / 36.5MB</strong> (beats 100% / 97%).</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">removeNthFromEnd</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<h4 id="c-code"><em><strong>C++ Code:</strong></em></h4>
<p>The best result for the code below is <strong>0ms / 10.6MB</strong> (beats 100% / 93%).</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">removeNthFromEnd</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        ListNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>fast</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        slow</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

  ## Linked List - Add Two Numbers
<div class="elfjS" data-track-load="description_content"><p>You are given two <strong>non-empty</strong> linked lists representing two non-negative integers. The digits are stored in <strong>reverse order</strong>, and each of their nodes contains a single digit. Add the two numbers and return the sum&nbsp;as a linked list.</p>

<p>You may assume the two numbers do not contain any leading zero, except the number 0 itself.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/02/addtwonumber1.jpg" style="width: 483px; height: 342px;">
<pre><strong>Input:</strong> l1 = [2,4,3], l2 = [5,6,4]
<strong>Output:</strong> [7,0,8]
<strong>Explanation:</strong> 342 + 465 = 807.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> l1 = [0], l2 = [0]
<strong>Output:</strong> [0]
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> l1 = [9,9,9,9,9,9,9], l2 = [9,9,9,9]
<strong>Output:</strong> [8,9,9,9,0,0,0,1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in each linked list is in the range <code>[1, 100]</code>.</li>
	<li><code>0 &lt;= Node.val &lt;= 9</code></li>
	<li>It is guaranteed that the list represents a number that does not have leading zeros.</li>
</ul>
</div>

### Solution 
#### Intuition
<p>The Intuition is to iterate through two linked lists representing non-negative integers in reverse order, starting from the least significant digit. It performs digit-wise addition along with a carry value and constructs a new linked list to represent the sum. The process continues until both input lists and the carry value are exhausted. The resulting linked list represents the sum of the input numbers in the correct order.</p>

#### Explanation
<ol>
<li>Create a placeholder node called <code>dummyHead</code> with a value of 0. This node will hold the resulting linked list.</li>
<li>Initialize a pointer called <code>tail</code> and set it to <code>dummyHead</code>. This pointer will keep track of the last node in the result list.</li>
<li>Initialize a variable called <code>carry</code> to 0. This variable will store the carry value during addition.</li>
<li>Start a loop that continues until there are no more digits in both input lists (<code>l1</code> and <code>l2</code>) and there is no remaining carry value.</li>
<li>Inside the loop:
<ul>
<li>Check if there is a digit in the current node of <code>l1</code>. If it exists, assign its value to a variable called <code>digit1</code>. Otherwise, set <code>digit1</code> to 0.</li>
<li>Check if there is a digit in the current node of <code>l2</code>. If it exists, assign its value to a variable called <code>digit2</code>. Otherwise, set <code>digit2</code> to 0.</li>
<li>Add the current digits from <code>l1</code> and <code>l2</code>, along with the carry value from the previous iteration, and store the sum in a variable called <code>sum</code>.</li>
<li>Calculate the unit digit of <code>sum</code> by taking the modulus (<code>%</code>) of <code>sum</code> by 10. This digit will be placed in a new node for the result.</li>
<li>Update the <code>carry</code> variable by dividing <code>sum</code> by 10 and taking the integer division (<code>/</code>) part. This gives us the carry value for the next iteration.</li>
<li>Create a new node with the calculated digit as its value.</li>
<li>Attach the new node to the <code>tail</code> node of the result list.</li>
<li>Move the <code>tail</code> pointer to the newly added node.</li>
<li>Move to the next nodes in both <code>l1</code> and <code>l2</code>, if they exist. If either list is exhausted, set the corresponding pointer to <code>nullptr</code>.</li>
</ul>
</li>
<li>After the loop, obtain the actual result list by skipping the <code>dummyHead</code> node.</li>
<li>Delete the <code>dummyHead</code> node.</li>
<li>Return the resulting list.</li>
</ol>

```
class Solution {
public:
    ListNode* addTwoNumbers(ListNode* l1, ListNode* l2) {
        ListNode* dummyHead = new ListNode(0);
        ListNode* tail = dummyHead;
        int carry = 0;

        while (l1 != nullptr || l2 != nullptr || carry != 0) {
            int digit1 = (l1 != nullptr) ? l1->val : 0;
            int digit2 = (l2 != nullptr) ? l2->val : 0;

            int sum = digit1 + digit2 + carry;
            int digit = sum % 10;
            carry = sum / 10;

            ListNode* newNode = new ListNode(digit);
            tail->next = newNode;
            tail = tail->next;

            l1 = (l1 != nullptr) ? l1->next : nullptr;
            l2 = (l2 != nullptr) ? l2->next : nullptr;
        }

        ListNode* result = dummyHead->next;
        delete dummyHead;
        return result;
    }
};
```

## Linked List - Delete Node in a Linked List
<div class="elfjS" data-track-load="description_content"><p>There is a singly-linked list <code>head</code> and we want to delete a node <code>node</code> in it.</p>

<p>You are given the node to be deleted <code>node</code>. You will <strong>not be given access</strong> to the first node of <code>head</code>.</p>

<p>All the values of the linked list are <strong>unique</strong>, and it is guaranteed that the given node <code>node</code> is not the last node in the linked list.</p>

<p>Delete the given node. Note that by deleting the node, we do not mean removing it from memory. We mean:</p>

<ul>
	<li>The value of the given node should not exist in the linked list.</li>
	<li>The number of nodes in the linked list should decrease by one.</li>
	<li>All the values before <code>node</code> should be in the same order.</li>
	<li>All the values after <code>node</code> should be in the same order.</li>
</ul>

<p><strong>Custom testing:</strong></p>

<ul>
	<li>For the input, you should provide the entire linked list <code>head</code> and the node to be given <code>node</code>. <code>node</code> should not be the last node of the list and should be an actual node in the list.</li>
	<li>We will build the linked list and pass the node to your function.</li>
	<li>The output will be the entire list after calling your function.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/01/node1.jpg" style="width: 400px; height: 286px;">
<pre><strong>Input:</strong> head = [4,5,1,9], node = 5
<strong>Output:</strong> [4,1,9]
<strong>Explanation: </strong>You are given the second node with value 5, the linked list should become 4 -&gt; 1 -&gt; 9 after calling your function.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/09/01/node2.jpg" style="width: 400px; height: 315px;">
<pre><strong>Input:</strong> head = [4,5,1,9], node = 1
<strong>Output:</strong> [4,5,9]
<strong>Explanation: </strong>You are given the third node with value 1, the linked list should become 4 -&gt; 5 -&gt; 9 after calling your function.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of the nodes in the given list is in the range <code>[2, 1000]</code>.</li>
	<li><code>-1000 &lt;= Node.val &lt;= 1000</code></li>
	<li>The value of each node in the list is <strong>unique</strong>.</li>
	<li>The <code>node</code> to be deleted is <strong>in the list</strong> and is <strong>not a tail</strong> node.</li>
</ul>
</div>

### Solution

```
    void deleteNode(ListNode* node) {
        ListNode *temp = node->next;
        *node = *(node->next);
        delete temp;
    }
```

## Linked List - Intersection of Two Linked Lists
<div class="elfjS" data-track-load="description_content"><p>Given the heads of two singly linked-lists <code>headA</code> and <code>headB</code>, return <em>the node at which the two lists intersect</em>. If the two linked lists have no intersection at all, return <code>null</code>.</p>

<p>For example, the following two linked lists begin to intersect at node <code>c1</code>:</p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/05/160_statement.png" style="width: 500px; height: 162px;">
<p>The test cases are generated such that there are no cycles anywhere in the entire linked structure.</p>

<p><strong>Note</strong> that the linked lists must <strong>retain their original structure</strong> after the function returns.</p>

<p><strong>Custom Judge:</strong></p>

<p>The inputs to the <strong>judge</strong> are given as follows (your program is <strong>not</strong> given these inputs):</p>

<ul>
	<li><code>intersectVal</code> - The value of the node where the intersection occurs. This is <code>0</code> if there is no intersected node.</li>
	<li><code>listA</code> - The first linked list.</li>
	<li><code>listB</code> - The second linked list.</li>
	<li><code>skipA</code> - The number of nodes to skip ahead in <code>listA</code> (starting from the head) to get to the intersected node.</li>
	<li><code>skipB</code> - The number of nodes to skip ahead in <code>listB</code> (starting from the head) to get to the intersected node.</li>
</ul>

<p>The judge will then create the linked structure based on these inputs and pass the two heads, <code>headA</code> and <code>headB</code> to your program. If you correctly return the intersected node, then your solution will be <strong>accepted</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/05/160_example_1_1.png" style="width: 500px; height: 162px;">
<pre><strong>Input:</strong> intersectVal = 8, listA = [4,1,8,4,5], listB = [5,6,1,8,4,5], skipA = 2, skipB = 3
<strong>Output:</strong> Intersected at '8'
<strong>Explanation:</strong> The intersected node's value is 8 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [4,1,8,4,5]. From the head of B, it reads as [5,6,1,8,4,5]. There are 2 nodes before the intersected node in A; There are 3 nodes before the intersected node in B.
- Note that the intersected node's value is not 1 because the nodes with value 1 in A and B (2<sup>nd</sup> node in A and 3<sup>rd</sup> node in B) are different node references. In other words, they point to two different locations in memory, while the nodes with value 8 in A and B (3<sup>rd</sup> node in A and 4<sup>th</sup> node in B) point to the same location in memory.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/05/160_example_2.png" style="width: 500px; height: 194px;">
<pre><strong>Input:</strong> intersectVal = 2, listA = [1,9,1,2,4], listB = [3,2,4], skipA = 3, skipB = 1
<strong>Output:</strong> Intersected at '2'
<strong>Explanation:</strong> The intersected node's value is 2 (note that this must not be 0 if the two lists intersect).
From the head of A, it reads as [1,9,1,2,4]. From the head of B, it reads as [3,2,4]. There are 3 nodes before the intersected node in A; There are 1 node before the intersected node in B.
</pre>

<p><strong class="example">Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/05/160_example_3.png" style="width: 300px; height: 189px;">
<pre><strong>Input:</strong> intersectVal = 0, listA = [2,6,4], listB = [1,5], skipA = 3, skipB = 2
<strong>Output:</strong> No intersection
<strong>Explanation:</strong> From the head of A, it reads as [2,6,4]. From the head of B, it reads as [1,5]. Since the two lists do not intersect, intersectVal must be 0, while skipA and skipB can be arbitrary values.
Explanation: The two lists do not intersect, so return null.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes of <code>listA</code> is in the <code>m</code>.</li>
	<li>The number of nodes of <code>listB</code> is in the <code>n</code>.</li>
	<li><code>1 &lt;= m, n &lt;= 3 * 10<sup>4</sup></code></li>
	<li><code>1 &lt;= Node.val &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= skipA &lt;&nbsp;m</code></li>
	<li><code>0 &lt;= skipB &lt;&nbsp;n</code></li>
	<li><code>intersectVal</code> is <code>0</code> if <code>listA</code> and <code>listB</code> do not intersect.</li>
	<li><code>intersectVal == listA[skipA] == listB[skipB]</code> if <code>listA</code> and <code>listB</code> intersect.</li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you write a solution that runs in <code>O(m + n)</code> time and use only <code>O(1)</code> memory?</div>

### Solution

<h4 id="idea"><em><strong>Idea:</strong></em></h4>
<p>The naive approach here would be to store each node reference in a data structure until we saw the same one twice, but that would take <strong>O(N) extra space</strong>.</p>
<p>In order to solve this problem with only <strong>O(1) extra space</strong>, we'll need to find another way to align the two linked lists. More importantly, we need to find a way to line up the <em>ends</em> of the two lists. And the easiest way to do that is to concatenate them in opposite orders, <strong>A+B</strong> and <strong>B+A</strong>. This way, the ends of the two original lists will align on the second half of each merged list.</p>
<p><img src="https://i.imgur.com/hcpocCV.png" alt="Visual 1"></p>
<p><img src="https://i.imgur.com/dDUjSPk.png" alt="Visual 2"></p>
<p>Then we just need to check if at some point the two merged lists are pointing to the same node. In fact, even if the two merged lists don't intersect, the value of <strong>a</strong> and <strong>b</strong> will be the same (<strong>null</strong>) when we come to the end of the merged lists, so we can use that as our exit condition.</p>
<p>We just need to make sure to string <strong>headB</strong> onto <strong>a</strong> and vice versa if one (but not both) list ends.</p>
<hr>
<h4 id="implementation"><em><strong>Implementation:</strong></em></h4>
<p>There code for all four languages is almost identical.</p>
<hr>
<h4 id="javascript-code"><em><strong>Javascript Code:</strong></em></h4>
<p>The best result for the code below is <strong>96ms / 45.7MB</strong> (beats 98% / 95%).</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-javascript" style="color: rgb(156, 220, 254); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">var</span><span> </span><span class="token function-variable" style="color: rgb(220, 220, 170);">getIntersectionNode</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">function</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(156, 220, 254);">headA</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(156, 220, 254);"> headB</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">let</span><span> a </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> headA</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> b </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> headB
</span></span><span><span>    </span><span class="token" style="color: rgb(197, 134, 192);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>a </span><span class="token" style="color: rgb(212, 212, 212);">!==</span><span> b</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        a </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>a </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> headB </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> a</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span>
</span></span><span><span>        b </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>b </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> headA </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> b</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> a
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<h4 id="python-code"><em><strong>Python Code:</strong></em></h4>
<p>The best result for the code below is <strong>156ms / 29.3MB</strong> (beats 88% / 88%).</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-python" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">def</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">getIntersectionNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>self</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> headA</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> ListNode</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> headB</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> ListNode</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> ListNode</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>        a</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> b </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> headA</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> headB
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>a </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> b</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>            a </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> headB </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">not</span><span> a </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> a</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span><span>            b </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> headA </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">not</span><span> b </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> b</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> a</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<h4 id="java-code"><em><strong>Java Code:</strong></em></h4>
<p>The best result for the code below is <strong>1ms / 41.6MB</strong> (beats 98% / 88%).</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">getIntersectionNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> headA</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> headB</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> a </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> headA</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> b </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> headB</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>a </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> b</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            a </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> a </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> headB </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> a</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            b </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> b </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> headA </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> b</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> a</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<h4 id="c-code"><em><strong>C++ Code:</strong></em></h4>
<p>The best result for the code below is <strong>36ms / 14.5MB</strong> (beats 96% / 96%).</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    ListNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span class="token" style="color: rgb(220, 220, 170);">getIntersectionNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>ListNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>headA</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> ListNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>headB</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        ListNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>a </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> headA</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>b </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> headB</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>a </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> b</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            a </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>a </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> headB </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> a</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            b </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>b </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> headA </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> b</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> a</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div></div></div>

## Linked List - Linked List Cycle
<div class="elfjS" data-track-load="description_content"><p>Given <code>head</code>, the head of a linked list, determine if the linked list has a cycle in it.</p>

<p>There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the&nbsp;<code>next</code>&nbsp;pointer. Internally, <code>pos</code>&nbsp;is used to denote the index of the node that&nbsp;tail's&nbsp;<code>next</code>&nbsp;pointer is connected to.&nbsp;<strong>Note that&nbsp;<code>pos</code>&nbsp;is not passed as a parameter</strong>.</p>

<p>Return&nbsp;<code>true</code><em> if there is a cycle in the linked list</em>. Otherwise, return <code>false</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png" style="width: 300px; height: 97px; margin-top: 8px; margin-bottom: 8px;">
<pre><strong>Input:</strong> head = [3,2,0,-4], pos = 1
<strong>Output:</strong> true
<strong>Explanation:</strong> There is a cycle in the linked list, where the tail connects to the 1st node (0-indexed).
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png" style="width: 141px; height: 74px;">
<pre><strong>Input:</strong> head = [1,2], pos = 0
<strong>Output:</strong> true
<strong>Explanation:</strong> There is a cycle in the linked list, where the tail connects to the 0th node.
</pre>

<p><strong class="example">Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png" style="width: 45px; height: 45px;">
<pre><strong>Input:</strong> head = [1], pos = -1
<strong>Output:</strong> false
<strong>Explanation:</strong> There is no cycle in the linked list.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of the nodes in the list is in the range <code>[0, 10<sup>4</sup>]</code>.</li>
	<li><code>-10<sup>5</sup> &lt;= Node.val &lt;= 10<sup>5</sup></code></li>
	<li><code>pos</code> is <code>-1</code> or a <strong>valid index</strong> in the linked-list.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Can you solve it using <code>O(1)</code> (i.e. constant) memory?</p>
</div>

### Solution

```
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     ListNode *next;
 *     ListNode(int x) : val(x), next(NULL) {}
 * };
 */
 /**
 use faster and lower runner solution. (2 pointers)
 the faster one move 2 steps, and slower one move only one step.
 if there's a circle, the faster one will finally "catch" the slower one. 
 (the distance between these 2 pointers will decrease one every time.)
 
 if there's no circle, the faster runner will reach the end of linked list. (NULL)
 */
class Solution {
public:
    bool hasCycle(ListNode *head) {
        if(head == NULL || head -> next == NULL)    
            return false;
 
        ListNode *fast = head;
        ListNode *slow = head;
        
        while(fast -> next && fast -> next -> next){
            fast = fast -> next -> next;
            slow = slow -> next;
            if(fast == slow)
                return true;
        }
 
        return false;
    }
};
```

## Linked List - Reverse Nodes in k-Group
<div class="elfjS" data-track-load="description_content"><p>Given the <code>head</code> of a linked list, reverse the nodes of the list <code>k</code> at a time, and return <em>the modified list</em>.</p>

<p><code>k</code> is a positive integer and is less than or equal to the length of the linked list. If the number of nodes is not a multiple of <code>k</code> then left-out nodes, in the end, should remain as it is.</p>

<p>You may not alter the values in the list's nodes, only nodes themselves may be changed.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/reverse_ex1.jpg" style="width: 542px; height: 222px;">
<pre><strong>Input:</strong> head = [1,2,3,4,5], k = 2
<strong>Output:</strong> [2,1,4,3,5]
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/03/reverse_ex2.jpg" style="width: 542px; height: 222px;">
<pre><strong>Input:</strong> head = [1,2,3,4,5], k = 3
<strong>Output:</strong> [3,2,1,4,5]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is <code>n</code>.</li>
	<li><code>1 &lt;= k &lt;= n &lt;= 5000</code></li>
	<li><code>0 &lt;= Node.val &lt;= 1000</code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow-up:</strong> Can you solve the problem in <code>O(1)</code> extra memory space?</p>
</div>

### Solution

```
class Solution {
public:
    ListNode* reverse(ListNode* head, ListNode* tail) {
        ListNode* current = head;
        ListNode *prev = NULL, *next = NULL;
 
        while (current != tail) {
            next = current->next;
            current->next = prev;
            prev = current;
            current = next;
        }
        
        return prev;
    }
    
    ListNode* reverseKGroup(ListNode* head, int k) {
        ListNode* ptr = head;
        
        for (int i = 0; i < k; i++) {
            if (!ptr) return head;
            ptr = ptr->next;
            
        }
        ListNode* tmp = reverse(head, ptr);
        head->next = reverseKGroup(ptr, k);
        return tmp;
    }
};
```

## Linked List - Palindrome Linked List
<div class="elfjS" data-track-load="description_content"><p>Given the <code>head</code> of a singly linked list, return <code>true</code><em> if it is a </em><span data-keyword="palindrome-sequence" class=" cursor-pointer relative text-dark-blue-s text-sm"><div class="popover-wrapper inline-block" data-headlessui-state=""><div><div aria-expanded="false" data-headlessui-state="" id="headlessui-popover-button-:r1u:"><div><em>palindrome</em></div></div><div style="position: fixed; z-index: 40; inset: 0px auto auto 0px; transform: translate(422px, 178px);"></div></div></div></span><em> or </em><code>false</code><em> otherwise</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/03/pal1linked-list.jpg" style="width: 422px; height: 62px;">
<pre><strong>Input:</strong> head = [1,2,2,1]
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/03/03/pal2linked-list.jpg" style="width: 182px; height: 62px;">
<pre><strong>Input:</strong> head = [1,2]
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of nodes in the list is in the range <code>[1, 10<sup>5</sup>]</code>.</li>
	<li><code>0 &lt;= Node.val &lt;= 9</code></li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you do it in <code>O(n)</code> time and <code>O(1)</code> space?</div>

### Solution 


<h4 id="idea"><em><strong>Idea:</strong></em></h4>
<p>The naive approach here would be to run through the linked list and create an array of its values, then compare the array to its reverse to find out if it's a palindrome. Though this is easy enough to accomplish, we're challenged to find an approach with a <strong>space complexity</strong> of only <strong>O(1)</strong> while maintaining a <strong>time complexity</strong> of <strong>O(N)</strong>.</p>
<p>The only way to check for a palindrome in <strong>O(1) space</strong> would require us to be able to access both nodes for comparison at the same time, rather than storing values for later comparison. This would seem to be a challenge, as the linked list only promotes travel in one direction.</p>
<p>But what if it didn't?</p>
<p>The answer is to reverse the back half of the linked list to have the <strong>next</strong> attribute point to the previous node instead of the next node. (<em>Note: we could instead add a <strong>prev</strong> attribute as we iterate through the linked list, rather than overwriting <strong>next</strong> on the back half, but that would technically use <strong>O(N) extra space</strong>, just as if we'd created an external array of node values.</em>)</p>
<p>The first challenge then becomes finding the middle of the linked list in order to start our reversing process there. For that, we can look to <a href="https://en.wikipedia.org/wiki/Cycle_detection#Floyd's_tortoise_and_hare" target="_blank"><strong>Floyd's Cycle Detection Algorithm</strong></a>.</p>
<p>With Floyd's, we'll travel through the linked list with <strong>two pointers</strong>, one of which is moving twice as fast as the other. When the <strong>fast</strong> pointer reaches the end of the list, the <strong>slow</strong> pointer must then be in the middle.<br>
<img src="https://i.imgur.com/RERjbdB.png" alt="Diagram 1">With<strong>slow</strong> now at the middle, we can reverse the back half of the list with the help of another variable to contain a reference to the previous node (<strong>prev</strong>) and a three-way swap. Before we do this, however, we'll want to set <strong>prev.next = null</strong>, so that we break the reverse cycle and avoid an endless loop.<br>
<img src="https://i.imgur.com/mjbMYP4.png" alt="Diagram 2">Once the back half is properly reversed and<strong>slow</strong> is once again at the end of the list, we can now start <strong>fast</strong> back over again at the <strong>head</strong> and compare the two halves simultaneously, with no extra space required.<br>
<img src="https://i.imgur.com/EL3Fwze.png" alt="Diagram 3">If the two pointers ever disagree in value, we can<strong>return false</strong>, otherwise we can <strong>return true</strong> if both pointers reach the middle successfully.</p>
<p>(<em>Note: This process works regardless of whether the length of the linked list is odd or even, as the comparison will stop when <strong>slow</strong> reaches the "dead-end" node.</em>)</p>
<p><img src="https://i.imgur.com/Q4skHkb.png" alt="Diagram 4"></p>
<hr>
<h4 id="implementation"><em><strong>Implementation:</strong></em></h4>
<p>The code for all four languages is almost identical.</p>
<hr>
<h4 id="javascript-code"><em><strong>Javascript Code:</strong></em></h4>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-javascript" style="color: rgb(156, 220, 254); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">var</span><span> </span><span class="token function-variable" style="color: rgb(220, 220, 170);">isPalindrome</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">function</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(156, 220, 254);">head</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">let</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> prev</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> temp
</span></span><span><span>    </span><span class="token" style="color: rgb(197, 134, 192);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span>
</span></span><span><span>    prev </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> prev</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token null nil" style="color: rgb(86, 156, 214);">null</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(197, 134, 192);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>slow</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        temp </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> prev</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> prev </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> temp
</span></span><span><span>    fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> prev
</span></span><span><span>    </span><span class="token" style="color: rgb(197, 134, 192);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>slow</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">val</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!==</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">false</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(197, 134, 192);">else</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">next</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">true</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<h4 id="python-code"><em><strong>Python Code:</strong></em></h4>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-python" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">def</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">isPalindrome</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>self</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> ListNode</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">bool</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>        slow</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> prev </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">None</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> fast </span><span class="token" style="color: rgb(86, 156, 214);">and</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>            slow</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span><span>        prev</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> prev</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">None</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>            slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> prev</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> prev</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span><span>        fast</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> prev
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>val </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>val</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">False</span><span>
</span></span><span><span>            fast</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(206, 145, 120);">next</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">True</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<h4 id="java-code"><em><strong>Java Code:</strong></em></h4>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">boolean</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">isPalindrome</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> prev</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> temp</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        prev </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        prev</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>slow </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            temp </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> prev</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            prev </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> temp</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> prev</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>slow </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>val </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">false</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">true</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<h4 id="c-code"><em><strong>C++ Code:</strong></em></h4>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">bool</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">isPalindrome</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        ListNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>prev</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>temp</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        prev </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> prev</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>slow</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            temp </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> prev</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> prev </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> temp</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> prev</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>slow</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>val </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">false</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">true</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## Linked List Linked List Cycle II
<div class="elfjS" data-track-load="description_content"><p>Given the <code>head</code> of a linked list, return <em>the node where the cycle begins. If there is no cycle, return </em><code>null</code>.</p>

<p>There is a cycle in a linked list if there is some node in the list that can be reached again by continuously following the <code>next</code> pointer. Internally, <code>pos</code> is used to denote the index of the node that tail's <code>next</code> pointer is connected to (<strong>0-indexed</strong>). It is <code>-1</code> if there is no cycle. <strong>Note that</strong> <code>pos</code> <strong>is not passed as a parameter</strong>.</p>

<p><strong>Do not modify</strong> the linked list.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist.png" style="height: 145px; width: 450px;">
<pre><strong>Input:</strong> head = [3,2,0,-4], pos = 1
<strong>Output:</strong> tail connects to node index 1
<strong>Explanation:</strong> There is a cycle in the linked list, where tail connects to the second node.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test2.png" style="height: 105px; width: 201px;">
<pre><strong>Input:</strong> head = [1,2], pos = 0
<strong>Output:</strong> tail connects to node index 0
<strong>Explanation:</strong> There is a cycle in the linked list, where tail connects to the first node.
</pre>

<p><strong class="example">Example 3:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2018/12/07/circularlinkedlist_test3.png" style="height: 65px; width: 65px;">
<pre><strong>Input:</strong> head = [1], pos = -1
<strong>Output:</strong> no cycle
<strong>Explanation:</strong> There is no cycle in the linked list.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li>The number of the nodes in the list is in the range <code>[0, 10<sup>4</sup>]</code>.</li>
	<li><code>-10<sup>5</sup> &lt;= Node.val &lt;= 10<sup>5</sup></code></li>
	<li><code>pos</code> is <code>-1</code> or a <strong>valid index</strong> in the linked-list.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Can you solve it using <code>O(1)</code> (i.e. constant) memory?</p>
</div>

### Solution
<div class="FN9Jv WRmCx"><h4 id="alogrithm-description"><strong>Alogrithm Description:</strong></h4>
<p><strong>Step 1: Determine whether there is a cycle</strong></p>
<p>1.1) Using a slow pointer that move forward 1 step  each time</p>
<p>1.2) Using a fast  pointer that move forward 2 steps each time</p>
<p>1.3) If the slow pointer and fast pointer both point to the same location after several moving steps, there is a cycle;</p>
<p>1.4) Otherwise, if (fast-&gt;next == NULL || fast-&gt;next-&gt;next == NULL), there has no cycle.</p>
<p><strong>Step 2: If there is a cycle, return the entry location of the cycle</strong></p>
<p>2.1) L1 is defined as the distance between the head point and entry point</p>
<p>2.2) L2 is defined as the distance between the entry point and the meeting point</p>
<p>2.3) C   is defined as the length of the cycle</p>
<p>2.4) n   is defined as the travel times of the fast pointer around the cycle When the first encounter of the slow pointer and the fast pointer</p>
<p><strong>According to the definition of L1, L2 and C, we can obtain:</strong></p>
<ul>
<li>
<p>the total distance of the slow pointer traveled when encounter is L1 + L2</p>
</li>
<li>
<p>the total distance of the fast  pointer traveled when encounter is L1 + L2 + n * C</p>
</li>
<li>
<p>Because the total distance the fast pointer traveled is twice as the slow pointer, Thus:</p>
</li>
<li>
<p>2 * (L1+L2) = L1 + L2 + n * C =&gt; L1 + L2 = n * C =&gt; <em><em>L1 = (n - 1)</em> C + (C - L2)</em>*</p>
</li>
</ul>
<p><strong>It can be concluded that the distance between the head location and entry location is equal to the distance between the meeting location and the entry location along the direction of forward movement.</strong></p>
<p>So, when the slow pointer and the fast pointer encounter in the cycle, we can define a pointer "entry" that point to the head, this "entry" pointer moves one step each time so as the slow pointer. When this "entry" pointer and the slow pointer both point to the same location, this location is the node where the cycle begins.</p>
<p>================================================================</p>
<p>Here is the code:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-rust" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span class="token" style="color: rgb(220, 220, 170);">detectCycle</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>head</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>head </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">||</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>slow  </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>fast  </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(78, 201, 176);">ListNode</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>entry </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fast</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        slow </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        fast </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>slow </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> fast</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>                      </span><span class="token" style="color: rgb(106, 153, 85);">// there is a cycle</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>slow </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> entry</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>               </span><span class="token" style="color: rgb(106, 153, 85);">// found the entry location</span><span>
</span></span><span><span>                slow  </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> slow</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                entry </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> entry</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> entry</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>                                 </span><span class="token" style="color: rgb(106, 153, 85);">// there has no cycle</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## Linked List - Flattening a Linked List
<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given a Linked List of size N, where every node represents a sub-linked-list and contains two pointers:<br>(i) a<strong> next </strong>pointer to the next node,<br>(ii) a<strong>&nbsp;bottom</strong>&nbsp;pointer&nbsp;to a linked list where this node is head.<br>Each of the&nbsp;sub-linked-list is in sorted order.<br>Flatten the Link List such that all the nodes appear in a single level while maintaining the sorted order.&nbsp;</span><br><br><span style="font-size: 18px;"><strong>Note:</strong> The flattened list will be printed using the bottom pointer instead of the next pointer.<br>For more clarity have a look at the printList() function in the driver code.</span></p>
<p>&nbsp;</p>
<p><span style="font-size: 18px;"><strong>Example 1:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input:
</strong>5 -&gt; 10 -&gt; 19 -&gt; 28
|     |     |     | 
7     20    22   35
|           |     | 
8          50    40
|                 | 
30               45<strong>
Output: </strong>&nbsp;5-&gt; 7-&gt; 8- &gt; 10 -&gt; 19-&gt; 20-&gt;
22-&gt; 28-&gt; 30-&gt; 35-&gt; 40-&gt; 45-&gt; 50.
<strong>Explanation</strong>:
The resultant linked lists has every 
node in a single level.
(<strong>Note: </strong>| represents the bottom pointer.)</span>
</pre>
<p>&nbsp;</p>
<p><span style="font-size: 18px;"><strong>Example 2:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input:</strong>
5 -&gt; 10 -&gt; 19 -&gt; 28
|          |                
7          22   
|          |                 
8          50 
|                           
30              
<strong>Output:</strong> 5-&gt;7-&gt;8-&gt;10-&gt;19-&gt;22-&gt;28-&gt;30-&gt;50
<strong>Explanation:</strong>
The resultant linked lists have every
node in a single level.

(<strong>Note: </strong>| represents the bottom pointer.)</span></pre>
<p>&nbsp;</p>
<p><span style="font-size: 18px;"><strong>Your Task:</strong><br>You do not need to read input or print anything. Complete the function <strong>flatten()</strong></span><span style="font-size: 18px;"> that takes the&nbsp;<strong>head </strong>of the linked list as input&nbsp;parameter<strong> </strong>and returns the head of flattened link list.</span></p>
<p><span style="font-size: 18px;"><strong>Expected Time Complexity:</strong>&nbsp;O(N*N*M)<br><strong>Expected Auxiliary Space:</strong> O(N)</span></p>
<p><span style="font-size: 18px;"><strong>Constraints:</strong></span><br><span style="font-size: 18px;">0 &lt;= N &lt;= 50<br>1 &lt;=<strong> M<sub>i</sub> </strong>&lt;= 20<br>1 &lt;= Element of linked list &lt;= 10<sup>3</sup></span></p></div>

### Solution
Approach:

The problem is easier if you have solved "Merge two sorted Linkedlists"

we just created a method similar to it but it will traverse in bottom and sort and then return new head of sorted list.

using that traverse the main list and send two nodes to sorted funtcion and maintain one as main node and traverse another temp2 node and send both as parameteres to function.

then at finally we will get a sorted linkedlist which can be traversed using bottom pointer.

```
class GfG
{
    Node flatten(Node root)
    {
// Your code here
    Node temp1=root;
    Node temp2=root.next;
    Node nxt=temp2;
    while(temp2!=null)
    {
       nxt=temp2.next;
       temp1=sortedMerge(temp1,temp2);
       temp2=nxt;
    }
    return temp1;
    }
    
    public Node sortedMerge(Node head1, Node head2) {
     
     Node temp1=head1;
     Node prev=null;
     Node temp2=head2;
     Node nxt=null;
     while(temp1!=null&&temp2!=null)
     {
         if(temp1.data>=temp2.data)
         {
             if(prev==null)
             {
                 nxt=temp2.bottom;
                 temp2.bottom=temp1;
                 prev=temp2;
                 head1=prev;
                 temp2=nxt;
             }
             else
             {
                 nxt=temp2.bottom;
                 temp2.bottom=prev.bottom;
                 prev.bottom=temp2;
                 prev=temp2;
                 temp2=nxt;
             }
         }
         else
         {
             prev=temp1;
             temp1=temp1.bottom;
         }
     }
     if(temp2!=null && temp1==null)
     {
         prev.bottom=temp2;
     }
     return head1;
   } 
}
```
