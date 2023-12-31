## Smallest number on left
<div class="problems_problem_content__Xm_eO"><p><span style="font-size:20px">Given an array <strong>a&nbsp;</strong>of integers of length <strong>n</strong>, find the nearest smaller number for every element such that the smaller element is on left side.If no small element present on the left print -1.</span></p>

<p><strong><span style="font-size:20px">Example 1:</span></strong></p>

<pre><span style="font-size:20px"><strong>Input:</strong> n = 3
a = {1, 6, 2}
<strong>Output:</strong> -1 1 1
<strong>Explaination:</strong> There is no number at the 
left of 1. Smaller number than 6 and 2 is 1.</span></pre>

<p><strong><span style="font-size:20px">Example 2:</span></strong></p>

<pre><span style="font-size:20px"><strong>Input:</strong> n = 6
a = {1, 5, 0, 3, 4, 5}
<strong>Output:</strong> -1 1 -1 0 3 4
<strong>Explaination:</strong> Upto 3 it is easy to see 
the smaller numbers. But for 4 the smaller 
numbers are 1, 0 and 3. But among them 3 
is closest. Similary for 5 it is 4.</span></pre>

<p><span style="font-size:20px"><strong>Your Task:</strong><br>
You do not need to read input or print anything. Your task is to complete the function <strong>leftSmaller()</strong> which takes n and a as input parameters and returns the list of smaller numbers.</span></p>

<p><span style="font-size:20px"><strong>Expected Time Complexity:</strong> O(n)<br>
<strong>Expected Auxiliary Space:</strong> O(n)</span></p>

<p><span style="font-size:20px"><strong>Constraints:</strong><br>
1 ≤ n ≤ 10000<br>
0 ≤ a[i] ≤ 10<sup>4</sup>&nbsp;&nbsp;</span></p>
</div>

### Solution

```
class Solution{
public:
    // Function to find the next smaller element to the left of each element
    vector<int> leftSmaller(int n, int a[]){
        stack<int> st;
        vector<int> sol;
        
        // Iterating through the array
        for(int i = 0;i < n;i++){
            // If stack is not empty and current element is greater than the top of stack
            if(st.size() && a[i] > st.top()){
                sol.push_back(st.top()); // Add the top of stack to the solution vector
                st.push(a[i]); // Push the current element to the stack
            }else{
                // Keep popping elements from stack until stack is empty or current element is smaller than top of stack
                while(!st.empty() && a[i] <= st.top())
                    st.pop();
                    
                // If stack is empty, there is no smaller element to the left
                if(st.empty())
                    sol.push_back(-1); // Add -1 to the solution vector
                else
                    sol.push_back(st.top()); // Add the top of stack to the solution vector
                st.push(a[i]); // Push the current element to the stack
            }
        }

        return sol; // Return the solution vector
    }
};
```

## LRU Cache

<div class="elfjS" data-track-load="description_content"><p>Design a data structure that follows the constraints of a <strong><a href="https://en.wikipedia.org/wiki/Cache_replacement_policies#LRU" target="_blank">Least Recently Used (LRU) cache</a></strong>.</p>

<p>Implement the <code>LRUCache</code> class:</p>

<ul>
	<li><code>LRUCache(int capacity)</code> Initialize the LRU cache with <strong>positive</strong> size <code>capacity</code>.</li>
	<li><code>int get(int key)</code> Return the value of the <code>key</code> if the key exists, otherwise return <code>-1</code>.</li>
	<li><code>void put(int key, int value)</code> Update the value of the <code>key</code> if the <code>key</code> exists. Otherwise, add the <code>key-value</code> pair to the cache. If the number of keys exceeds the <code>capacity</code> from this operation, <strong>evict</strong> the least recently used key.</li>
</ul>

<p>The functions <code>get</code> and <code>put</code> must each run in <code>O(1)</code> average time complexity.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input</strong>
["LRUCache", "put", "put", "get", "put", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [4, 4], [1], [3], [4]]
<strong>Output</strong>
[null, null, null, 1, null, -1, null, -1, 3, 4]

<strong>Explanation</strong>
LRUCache lRUCache = new LRUCache(2);
lRUCache.put(1, 1); // cache is {1=1}
lRUCache.put(2, 2); // cache is {1=1, 2=2}
lRUCache.get(1);    // return 1
lRUCache.put(3, 3); // LRU key was 2, evicts key 2, cache is {1=1, 3=3}
lRUCache.get(2);    // returns -1 (not found)
lRUCache.put(4, 4); // LRU key was 1, evicts key 1, cache is {4=4, 3=3}
lRUCache.get(1);    // return -1 (not found)
lRUCache.get(3);    // return 3
lRUCache.get(4);    // return 4
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= capacity &lt;= 3000</code></li>
	<li><code>0 &lt;= key &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= value &lt;= 10<sup>5</sup></code></li>
	<li>At most <code>2 * 10<sup>5</sup></code> calls will be made to <code>get</code> and <code>put</code>.</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>The problem can be solved with a hashtable that keeps track of the keys and its values in the double linked list. One interesting property about double linked list is that the node can remove itself without other reference. In addition, it takes constant time to add and remove nodes from the head or tail.</p>
<p>One particularity about the double linked list that I implemented is that I create a pseudo head and tail to mark the boundary, so that we don't need to check the NULL node during the update. This makes the code more concise and clean, and also it is good for the performance.</p>
<p>Voila, here is the code.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">import</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">java</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(78, 201, 176);">util</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(78, 201, 176);">Hashtable</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span>
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">LRUCache</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> key</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> value</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> pre</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> post</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token doc-comment" style="color: rgb(106, 153, 85);">/**
</span></span><span> * Always add the new node right after head;
</span><span><span class="token doc-comment" style="color: rgb(106, 153, 85);"> */</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">addNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span>    
</span><span><span>  node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>pre </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>post </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>post</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>  head</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>post</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>pre </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  head</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>post </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token doc-comment" style="color: rgb(106, 153, 85);">/**
</span></span><span> * Remove an existing node from the linked list.
</span><span><span class="token doc-comment" style="color: rgb(106, 153, 85);"> */</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">removeNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> pre </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>pre</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> post </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>post</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>  pre</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>post </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> post</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  post</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>pre </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> pre</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token doc-comment" style="color: rgb(106, 153, 85);">/**
</span></span><span> * Move certain node in between to the head.
</span><span><span class="token doc-comment" style="color: rgb(106, 153, 85);"> */</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">moveToHead</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">removeNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">addNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">// pop the current tail. </span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">popTail</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> res </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> tail</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>pre</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">removeNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>res</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> res</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Hashtable</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(78, 201, 176);">Integer</span><span class="token generics" style="color: rgb(212, 212, 212);">,</span><span class="token generics"> </span><span class="token generics" style="color: rgb(78, 201, 176);">DLinkedNode</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span> 
</span></span><span><span>  cache </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Hashtable</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(78, 201, 176);">Integer</span><span class="token generics" style="color: rgb(212, 212, 212);">,</span><span class="token generics"> </span><span class="token generics" style="color: rgb(78, 201, 176);">DLinkedNode</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> count</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> capacity</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> tail</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">LRUCache</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> capacity</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>count </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>capacity </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> capacity</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>  head </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  head</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>pre </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>  tail </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  tail</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>post </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>  head</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>post </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> tail</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  tail</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>pre </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> key</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span>
</span><span><span>  </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> node </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cache</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>key</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// should raise exception here.</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span>  </span><span class="token" style="color: rgb(106, 153, 85);">// move the accessed node to the head;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">moveToHead</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>value</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span>
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">put</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> key</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> value</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> node </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cache</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">get</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>key</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>  </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span>
</span><span><span>    </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> newNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    newNode</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>key </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> key</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    newNode</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>value </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> value</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>cache</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">put</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>key</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> newNode</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">addNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>newNode</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span>count</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>count </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> capacity</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>      </span><span class="token" style="color: rgb(106, 153, 85);">// pop the tail</span><span>
</span></span><span><span>      </span><span class="token" style="color: rgb(78, 201, 176);">DLinkedNode</span><span> tail </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">popTail</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>      </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>cache</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">remove</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>tail</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>key</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>      </span><span class="token" style="color: rgb(212, 212, 212);">--</span><span>count</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(86, 156, 214);">else</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(106, 153, 85);">// update the value.</span><span>
</span></span><span><span>    node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>value </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> value</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">moveToHead</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>  </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3h49a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1h49a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## LFU Cache
<div class="elfjS" data-track-load="description_content"><p>Design and implement a data structure for a <a href="https://en.wikipedia.org/wiki/Least_frequently_used" target="_blank">Least Frequently Used (LFU)</a> cache.</p>

<p>Implement the <code>LFUCache</code> class:</p>

<ul>
	<li><code>LFUCache(int capacity)</code> Initializes the object with the <code>capacity</code> of the data structure.</li>
	<li><code>int get(int key)</code> Gets the value of the <code>key</code> if the <code>key</code> exists in the cache. Otherwise, returns <code>-1</code>.</li>
	<li><code>void put(int key, int value)</code> Update the value of the <code>key</code> if present, or inserts the <code>key</code> if not already present. When the cache reaches its <code>capacity</code>, it should invalidate and remove the <strong>least frequently used</strong> key before inserting a new item. For this problem, when there is a <strong>tie</strong> (i.e., two or more keys with the same frequency), the <strong>least recently used</strong> <code>key</code> would be invalidated.</li>
</ul>

<p>To determine the least frequently used key, a <strong>use counter</strong> is maintained for each key in the cache. The key with the smallest <strong>use counter</strong> is the least frequently used key.</p>

<p>When a key is first inserted into the cache, its <strong>use counter</strong> is set to <code>1</code> (due to the <code>put</code> operation). The <strong>use counter</strong> for a key in the cache is incremented either a <code>get</code> or <code>put</code> operation is called on it.</p>

<p>The functions&nbsp;<code data-stringify-type="code">get</code>&nbsp;and&nbsp;<code data-stringify-type="code">put</code>&nbsp;must each run in <code>O(1)</code> average time complexity.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input</strong>
["LFUCache", "put", "put", "get", "put", "get", "get", "put", "get", "get", "get"]
[[2], [1, 1], [2, 2], [1], [3, 3], [2], [3], [4, 4], [1], [3], [4]]
<strong>Output</strong>
[null, null, null, 1, null, -1, 3, null, -1, 3, 4]

<strong>Explanation</strong>
// cnt(x) = the use counter for key x
// cache=[] will show the last used order for tiebreakers (leftmost element is  most recent)
LFUCache lfu = new LFUCache(2);
lfu.put(1, 1);   // cache=[1,_], cnt(1)=1
lfu.put(2, 2);   // cache=[2,1], cnt(2)=1, cnt(1)=1
lfu.get(1);      // return 1
                 // cache=[1,2], cnt(2)=1, cnt(1)=2
lfu.put(3, 3);   // 2 is the LFU key because cnt(2)=1 is the smallest, invalidate 2.
&nbsp;                // cache=[3,1], cnt(3)=1, cnt(1)=2
lfu.get(2);      // return -1 (not found)
lfu.get(3);      // return 3
                 // cache=[3,1], cnt(3)=2, cnt(1)=2
lfu.put(4, 4);   // Both 1 and 3 have the same cnt, but 1 is LRU, invalidate 1.
                 // cache=[4,3], cnt(4)=1, cnt(3)=2
lfu.get(1);      // return -1 (not found)
lfu.get(3);      // return 3
                 // cache=[3,4], cnt(4)=1, cnt(3)=3
lfu.get(4);      // return 4
                 // cache=[4,3], cnt(4)=2, cnt(3)=3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= capacity&nbsp;&lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= key &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= value &lt;= 10<sup>9</sup></code></li>
	<li>At most <code>2 * 10<sup>5</sup></code>&nbsp;calls will be made to <code>get</code> and <code>put</code>.</li>
</ul>

<p>&nbsp;</p>
<span style="display: none;">&nbsp;</span></div>

### Solution

<h3 id="approach-1-maintaining-2-hashmaps">Approach : Maintaining 2 HashMaps</h3>
<h4 id="intuition">Intuition</h4>
<p>We need to maintain all the keys, values and frequencies. Without invalidation (removing from the data structure when it reaches capacity), they can be maintained by a HashMap&lt;Integer, Pair&lt;Integer, Integer&gt;&gt;, keyed by the original <code>key</code> and valued by the <code>frequency</code>-<code>value</code> pair.</p>
<p>With the invalidation, we need to maintain the current minimum frequency and delete particular keys. Hence, we can group the keys with the same frequency together and maintain another HashMap&lt;Integer, Set&gt;, keyed by the frequency and valued by the set of <code>keys</code> that have the same frequency. This way, if we know the minimum frequency, we can access the potential keys to be deleted.</p>
<p>Also note that in the case of a tie, we're required to find the least recently used key and invalidate it, hence we need to keep the frequencies ordered in the Set. Instead of using a TreeSet which adds an extra <span class="math math-inline"><span class="katex"><span class="katex-mathml"></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord mathnormal" style="margin-right: 0.02778em;">O</span><span class="mopen">(</span><span class="mord mathnormal" style="margin-right: 0.01968em;">l</span><span class="mord mathnormal">o</span><span class="mord mathnormal" style="margin-right: 0.03588em;">g</span><span class="mopen">(</span><span class="mord mathnormal" style="margin-right: 0.10903em;">N</span><span class="mclose">))</span></span></span></span></span> time complexity, we can maintain the keys using a LinkedList so that it supports finding both an arbitrary key and the least recently used key in constant time. Fortunately, LinkedHashSet can do the job. Once a <code>key</code> is inserted/updated, we put it to the end of the LinkedHashSet so that we can invalidate the first <code>key</code> in the LinkedHashSet corresponding to the minimum frequency.</p>
<p>The original operations can be transformed into operations on the 2 HashMaps, keeping them in sync and maintaining the minimum frequency.</p>
<p>Since C++ lacks LinkedHashSet, we have to use a workaround like maintaining a list of key and value pairs instead of the LinkedHashSet and keeping the iterator with the frequency in another unordered_map to keep this connection. The idea is similar but a little bit complicated. Another workaround would be to implement your own LRU cache with a doubly linked list.</p>
<h4 id="algorithm">Algorithm</h4>
<p>To make things simpler, assume we have 4 member variables:</p>
<ol>
<li><code>HashMap&lt;Integer, Pair&lt;Integer, Integer&gt;&gt; cache</code>, keyed by the original <code>key</code> and valued by the <code>frequency</code>-<code>value</code> pair.</li>
<li><code>HashMap&lt;Integer, LinkedListHashSet&lt;Integer&gt;&gt; frequencies</code>, keyed by frequency and valued by the set of <code>keys</code> that have the same frequency.</li>
<li><code>int minf</code>, which is the minimum frequency at any given time.</li>
<li><code>int capacity</code>, which is the <code>capacity</code> given in the input.</li>
</ol>
<p>It's also convenient to have a private utility function <code>insert</code> to insert a <code>key</code>-<code>value</code> pair with a given frequency.</p>
<h5 id="void-insertint-key-int-frequency-int-value">void insert(int key, int frequency, int value)</h5>
<ol>
<li>Insert <code>frequency</code>-<code>value</code> pair into <code>cache</code> with the given <code>key</code>.</li>
<li>Get the LinkedHashSet corresponding to the given <code>frequency</code> (default to empty Set) and insert the given <code>key</code>.</li>
</ol>
<h5 id="int-getint-key">int get(int key)</h5>
<ol>
<li>If the given <code>key</code> is not in the <code>cache</code>, return <code>-1</code>, otherwise go to step <code>2</code>.</li>
<li>Get the <code>frequency</code> and <code>value</code> from the <code>cache</code>.</li>
<li>Get the LinkedHashSet associated with <code>frequency</code> from <code>frequencies</code> and remove the given <code>key</code> from it, since the usage of the current key is increased by this function call.</li>
<li>If <code>minf</code> == <code>frequency</code> and the above LinkedHashSet is empty, that means there are no more elements used <code>minf</code> times, so increase <code>minf</code> by 1. To save some space, we can also delete the entry <code>frequency</code> from the <code>frequencies</code> hash map.</li>
<li>Call insert(<code>key</code>, <code>frequency</code> + 1, <code>value</code>), since the current key's usage has increased from this function call.</li>
<li>Return <code>value</code></li>
</ol>
<h5 id="void-putint-key-int-value">void put(int key, int value)</h5>
<ol>
<li>If <code>capacity</code> &lt;= 0, exit.</li>
<li>If the given <code>key</code> exists in <code>cache</code>, update the <code>value</code> in the original <code>frequency</code>-<code>value</code> (don't call insert here), and then increment the frequency by using get(<code>key</code>). Exit the function.</li>
<li>If <code>cache.size()</code> == <code>capacity</code>, get the first (least recently used) value in the LinkedHashSet corresponding to <code>minf</code> in <code>frequencies</code>, and remove it from <code>cache</code> and the LinkedHashSet.</li>
<li>If we didn't exit the function in step 2, it means that this element is a new one, so the minimum frequency cannot possibly be greater than one. Set <code>minf</code> to 1.</li>
<li>Call insert(<code>key</code>, 1, <code>value</code>)</li>
</ol>
<h4 id="implementation">Implementation</h4>

```
class LFUCache {
    // key: original key, value: frequency and original value.
    private Map<Integer, Pair<Integer, Integer>> cache;
    // key: frequency, value: All keys that have the same frequency.
    private Map<Integer, LinkedHashSet<Integer>> frequencies;
    private int minf;
    private int capacity;
    
    private void insert(int key, int frequency, int value) {
        cache.put(key, new Pair<>(frequency, value));
        frequencies.putIfAbsent(frequency, new LinkedHashSet<>());
        frequencies.get(frequency).add(key);
    }

    public LFUCache(int capacity) {
        cache = new HashMap<>();
        frequencies = new HashMap<>();
        minf = 0;
        this.capacity = capacity;
    }
    
    public int get(int key) {
        Pair<Integer, Integer> frequencyAndValue = cache.get(key);
        if (frequencyAndValue == null) {
            return -1;
        }
        final int frequency = frequencyAndValue.getKey();
        final Set<Integer> keys = frequencies.get(frequency);
        keys.remove(key);
        if (keys.isEmpty()) {
            frequencies.remove(frequency);
            
            if (minf == frequency) {
                ++minf;
            }
        }
        final int value = frequencyAndValue.getValue();
        insert(key, frequency + 1, value);   
        return value;
    }
    
    public void put(int key, int value) {
        if (capacity <= 0) {
            return;
        }
        Pair<Integer, Integer> frequencyAndValue = cache.get(key);
        if (frequencyAndValue != null) {
            cache.put(key, new Pair<>(frequencyAndValue.getKey(), value));
            get(key);
            return;
        }
        if (capacity == cache.size()) {
            final Set<Integer> keys = frequencies.get(minf);
            final int keyToDelete = keys.iterator().next();
            cache.remove(keyToDelete);
            keys.remove(keyToDelete);
            if (keys.isEmpty()) {
                frequencies.remove(minf);
            }
        }
        minf = 1;
        insert(key, 1, value);
    }
}
```

<h4 id="complexity-analysis">Complexity Analysis</h4>
<p>Here, <span class="math math-inline"><span class="katex"><span class="katex-mathml">NN</span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 0.6833em;"></span><span class="mord mathnormal" style="margin-right: 0.10903em;">N</span></span></span></span></span> is the total number of operations.</p>
<ul>
<li>Time complexity: <span class="math math-inline"><span class="katex"><span class="katex-mathml"></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord mathnormal" style="margin-right: 0.02778em;">O</span><span class="mopen">(</span><span class="mord">1</span><span class="mclose">)</span></span></span></span></span>, as required by the question.</li>
</ul>
<p>Since we only have basic HashMap/(Linked)HashSet operations. For details,</p>
<p>Our utility function <code>insert</code> puts the <code>key</code>- <code>value</code> pair into the <code>cache</code>, queries and possibly puts an empty LinedHashSet in the <code>frequencies</code>, then queries <code>frequencies</code> again and adds a <code>key</code> into the associated <code>value</code> which is a LinkedHashSet. All the operations are based on the hash calculating for simple type (int or Integer) and the time complexity is constant.</p>
<p>For each <code>get</code> operation, in the worst case, we query the <code>frequencies</code> and remove a <code>key</code> from the associated <code>value</code> which is a LinkedHashSet and call <code>insert</code> function once. All the operations have the constant time complexity based on the hash calculating for simple type.</p>
<p>For each <code>put</code> operation, in the simple case we just insert the new <code>key</code>-<code>value</code> pair into the <code>cache</code> and call <code>get</code> function once. In the worst case, we query the <code>frequencies</code> to get the associated <code>value</code>, namely all the <code>keys</code> with the same frequencies which is a LinkedHashSet. And then we get the first key from the LinkedHashSet, remove it from both <code>cache</code> and <code>frequencies</code>. All the operations have the constant time complexity based on the hash calculating for simple type.</p>
<ul>
<li>
<p>Space complexity: <span class="math math-inline"><span class="katex"><span class="katex-mathml"></span><span class="katex-html" aria-hidden="true"><span class="base"><span class="strut" style="height: 1em; vertical-align: -0.25em;"></span><span class="mord mathnormal" style="margin-right: 0.02778em;">O</span><span class="mopen">(</span><span class="mord mathnormal" style="margin-right: 0.10903em;">N</span><span class="mclose">)</span></span></span></span></span>.</p>
<p>We save all the <code>key</code>-<code>value</code> pairs as well as all the keys with frequencies in the 2 HashMaps (plus a LinkedHashSet), so there are at most $min(N, capacity) <code>keys</code> and <code>values</code> at any given time.</p>
</li>
</ul>
<hr></div>

## Largest Rectangle in Histogram
<div class="elfjS" data-track-load="description_content"><p>Given an array of integers <code>heights</code> representing the histogram's bar height where the width of each bar is <code>1</code>, return <em>the area of the largest rectangle in the histogram</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/04/histogram.jpg" style="width: 522px; height: 242px;">
<pre><strong>Input:</strong> heights = [2,1,5,6,2,3]
<strong>Output:</strong> 10
<strong>Explanation:</strong> The above is a histogram where width of each bar is 1.
The largest rectangle is shown in the red area, which has an area = 10 units.
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2021/01/04/histogram-1.jpg" style="width: 202px; height: 362px;">
<pre><strong>Input:</strong> heights = [2,4]
<strong>Output:</strong> 4
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= heights.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= heights[i] &lt;= 10<sup>4</sup></code></li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><h4 id="intuition">Intuition:</h4>
<p>The intuition behind the solution is to use two arrays, <code>nsr</code> (nearest smaller to the right) and <code>nsl</code> (nearest smaller to the left), to determine the boundaries of the rectangle for each bar in the histogram. By calculating the area for each rectangle and keeping track of the maximum area, we can find the largest rectangle in the histogram.</p>
<h4 id="approach">Approach:</h4>
<ol>
<li>Initialize an empty stack <code>s</code> to store the indices of the histogram bars.</li>
<li>Create two arrays, <code>nsr</code> and <code>nsl</code>, each of size <code>n</code> (where <code>n</code> is the number of elements in the <code>heights</code> vector), and initialize all elements to 0.</li>
<li>Process the histogram bars from right to left:
<ul>
<li>While the stack is not empty and the height of the current bar is less than or equal to the height of the bar at the top of the stack, pop the stack.</li>
<li>If the stack becomes empty, set <code>nsr[i]</code> (the nearest smaller to the right for the current bar) to <code>n</code>.</li>
<li>Otherwise, set <code>nsr[i]</code> to the index at the top of the stack.</li>
<li>Push the current index <code>i</code> onto the stack.</li>
</ul>
</li>
<li>Empty the stack.</li>
<li>Process the histogram bars from left to right:
<ul>
<li>While the stack is not empty and the height of the current bar is less than or equal to the height of the bar at the top of the stack, pop the stack.</li>
<li>If the stack becomes empty, set <code>nsl[i]</code> (the nearest smaller to the left for the current bar) to -1.</li>
<li>Otherwise, set <code>nsl[i]</code> to the index at the top of the stack.</li>
<li>Push the current index <code>i</code> onto the stack.</li>
</ul>
</li>
<li>Initialize a variable <code>ans</code> to 0. This variable will store the maximum rectangle area.</li>
<li>Iterate over the histogram bars:
<ul>
<li>Calculate the area of the rectangle for the current bar using the formula: <code>heights[i] * (nsr[i] - nsl[i] - 1)</code>.</li>
<li>Update <code>ans</code> with the maximum of <code>ans</code> and the calculated area.</li>
</ul>
</li>
<li>Return <code>ans</code> as the largest rectangle area in the histogram.</li>
</ol>
<h4 id="complexity">Complexity:</h4>
<ul>
<li>The time complexity of this solution is O(n), where n is the number of elements in the <code>heights</code> vector. This is because each bar is processed only once.</li>
<li>The space complexity is O(n) as well because we use two additional arrays of size n, <code>nsr</code> and <code>nsl</code>, and a stack to store indices.</li>
</ul>
<hr>
<h4 id="c">C++</h4>

```
class Solution {
public:
    int largestRectangleArea(vector<int>& heights){
        int n=heights.size();
        vector<int> nsr(n,0);
        vector<int> nsl(n,0);

        stack<int> s;

        for(int i=n-1;i>=0;i--){
            while(!s.empty() && heights[i]<=heights[s.top()]){
                s.pop();
            }
            if(s.empty()) nsr[i]=n;
            else nsr[i]=s.top();
            s.push(i);
        }

        while(!s.empty()) s.pop();

        for(int i=0;i<n;i++){
            while(!s.empty() && heights[i]<=heights[s.top()]){
                s.pop();
            }
            if(s.empty()) nsl[i]=-1;
            else nsl[i]=s.top();
            s.push(i);
        }

        int ans=0;

        for(int i=0;i<n;i++){
            ans=max(ans, heights[i]*(nsr[i]-nsl[i]-1));
        }
        return ans;        
    }
};
```

## Sliding Window Maximum
<div class="elfjS" data-track-load="description_content"><p>You are given an array of integers&nbsp;<code>nums</code>, there is a sliding window of size <code>k</code> which is moving from the very left of the array to the very right. You can only see the <code>k</code> numbers in the window. Each time the sliding window moves right by one position.</p>

<p>Return <em>the max sliding window</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,3,-1,-3,5,3,6,7], k = 3
<strong>Output:</strong> [3,3,5,5,6,7]
<strong>Explanation:</strong> 
Window position                Max
---------------               -----
[1  3  -1] -3  5  3  6  7       <strong>3</strong>
 1 [3  -1  -3] 5  3  6  7       <strong>3</strong>
 1  3 [-1  -3  5] 3  6  7      <strong> 5</strong>
 1  3  -1 [-3  5  3] 6  7       <strong>5</strong>
 1  3  -1  -3 [5  3  6] 7       <strong>6</strong>
 1  3  -1  -3  5 [3  6  7]      <strong>7</strong>
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [1], k = 1
<strong>Output:</strong> [1]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li><code>1 &lt;= k &lt;= nums.length</code></li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>We scan the array from 0 to n-1, keep "promising" elements in the deque. The algorithm is amortized O(n) as each element is put and polled once.</p>
<p>At each i, we keep "promising" elements, which are potentially max number in window [i-(k-1),i] or any subsequent window. This means</p>
<ol>
<li>
<p>If an element in the deque and it is out of i-(k-1), we discard them. We just need to poll from the head, as we are using a deque and elements are ordered as the sequence in the array</p>
</li>
<li>
<p>Now only those elements within [i-(k-1),i]  are in the deque. We then discard elements smaller than a[i] from the tail. This is because if a[x] &lt;a[i] and x&lt;i, then a[x] has no chance to be the "max" in [i-(k-1),i], or any other subsequent window: a[i] would always be a better candidate.</p>
</li>
<li>
<p>As a result elements in the deque are ordered in both sequence in array and their value. At each step the head of the deque is the max element in [i-(k-1),i]</p>
</li>
</ol>
<hr>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-csharp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(86, 156, 214);">int</span><span class="token return-type" style="color: rgb(212, 212, 212);">[</span><span class="token return-type" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">maxSlidingWindow</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> a</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> k</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>		
</span></span><span><span>		</span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>a </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">||</span><span> k </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> n </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> a</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>length</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> r </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span>k</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> ri </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(106, 153, 85);">// store index</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(78, 201, 176);">Deque</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> q </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">ArrayDeque</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> a</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>length</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(106, 153, 85);">// remove numbers out of range k</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">peek</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> k </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>				q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(106, 153, 85);">// remove smaller numbers in k range as they are useless</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> a</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">peekLast</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> a</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>				q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">pollLast</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(106, 153, 85);">// q contains index... r contains content</span><span>
</span></span><span><span>			q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">offer</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span> k </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>				r</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>ri</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> a</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">peek</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> r</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## Min Stack
<div class="elfjS" data-track-load="description_content"><p>Design a stack that supports push, pop, top, and retrieving the minimum element in constant time.</p>

<p>Implement the <code>MinStack</code> class:</p>

<ul>
	<li><code>MinStack()</code> initializes the stack object.</li>
	<li><code>void push(int val)</code> pushes the element <code>val</code> onto the stack.</li>
	<li><code>void pop()</code> removes the element on the top of the stack.</li>
	<li><code>int top()</code> gets the top element of the stack.</li>
	<li><code>int getMin()</code> retrieves the minimum element in the stack.</li>
</ul>

<p>You must implement a solution with <code>O(1)</code> time complexity for each function.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input</strong>
["MinStack","push","push","push","getMin","pop","top","getMin"]
[[],[-2],[0],[-3],[],[],[],[]]

<strong>Output</strong>
[null,null,null,null,-3,null,0,-2]

<strong>Explanation</strong>
MinStack minStack = new MinStack();
minStack.push(-2);
minStack.push(0);
minStack.push(-3);
minStack.getMin(); // return -3
minStack.pop();
minStack.top();    // return 0
minStack.getMin(); // return -2
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>-2<sup>31</sup> &lt;= val &lt;= 2<sup>31</sup> - 1</code></li>
	<li>Methods <code>pop</code>, <code>top</code> and <code>getMin</code> operations will always be called on <strong>non-empty</strong> stacks.</li>
	<li>At most <code>3 * 10<sup>4</sup></code> calls will be made to <code>push</code>, <code>pop</code>, <code>top</code>, and <code>getMin</code>.</li>
</ul>
</div>

### solution

```
	class MinStack {
	public:
		stack<int>s;
		int minElement = INT_MAX;//initalize with max value

		void push(int val) {
			if(minElement>=val){// whenever val is lesser than current minElement, store current minElement in stack and make val as current minElement
				s.push(minElement);
				 minElement = val;
			}
			  s.push(val);
		}

		void pop() {
			if(minElement==s.top()){//top is minElement then previous element will be previous minElement, so pop and store current top as current MinElement
				s.pop();
				minElement = s.top();
			}
			s.pop();
		}

		int top() {// return stack top
			return s.top();
		}

		int getMin() {//return minElement
			return minElement;
		}
	};
```

## Rotting Oranges
<div class="elfjS" data-track-load="description_content"><p>You are given an <code>m x n</code> <code>grid</code> where each cell can have one of three values:</p>

<ul>
	<li><code>0</code> representing an empty cell,</li>
	<li><code>1</code> representing a fresh orange, or</li>
	<li><code>2</code> representing a rotten orange.</li>
</ul>

<p>Every minute, any fresh orange that is <strong>4-directionally adjacent</strong> to a rotten orange becomes rotten.</p>

<p>Return <em>the minimum number of minutes that must elapse until no cell has a fresh orange</em>. If <em>this is impossible, return</em> <code>-1</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2019/02/16/oranges.png" style="width: 650px; height: 137px;">
<pre><strong>Input:</strong> grid = [[2,1,1],[1,1,0],[0,1,1]]
<strong>Output:</strong> 4
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> grid = [[2,1,1],[0,1,1],[1,0,1]]
<strong>Output:</strong> -1
<strong>Explanation:</strong> The orange in the bottom left corner (row 2, column 0) is never rotten, because rotting only happens 4-directionally.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> grid = [[0,2]]
<strong>Output:</strong> 0
<strong>Explanation:</strong> Since there are already no fresh oranges at minute 0, the answer is just 0.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 10</code></li>
	<li><code>grid[i][j]</code> is <code>0</code>, <code>1</code>, or <code>2</code>.</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>The trick is to start bfs from all initial rotten oranges simultaneously to get minimum time, this way any oranges that can get rotten due to more than 1 initially rotten oranges will be covered by the nearest one.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">orangesRotting</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> grid</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> 
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span>        
</span><span><span>        vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> dir</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//used for finding all 4 adjacent coordinates</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> m</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>grid</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>grid</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        queue</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>pair</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;&gt;</span><span> q</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> fresh</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//To keep track of all fresh oranges left</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>m</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>grid</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>                    q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>grid</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>                    fresh</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> ans</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//initialised to -1 since after each step we increment the time by 1 and initially all rotten oranges started at 0.</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">empty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> sz</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>sz</span><span class="token" style="color: rgb(212, 212, 212);">--</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                pair</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> p</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">front</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(181, 206, 168);">4</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> r</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>p</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>first</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span>dir</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> c</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>p</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span>dir</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>r</span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> r</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>m </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> c</span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> c</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>n </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span>grid</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>r</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>c</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                        grid</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>r</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>c</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                        q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>r</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>c</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                        fresh</span><span class="token" style="color: rgb(212, 212, 212);">--</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// decrement by 1 foreach fresh orange that now is rotten</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>                    
</span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            ans</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//incremented after each minute passes</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>fresh</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//if fresh&gt;0 that means there are fresh oranges left</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>ans</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//we initialised with -1, so if there were no oranges it'd take 0 mins.</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> ans</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>

## Online Stock Span
<div class="elfjS" data-track-load="description_content"><p>Design an algorithm that collects daily price quotes for some stock and returns <strong>the span</strong> of that stock's price for the current day.</p>

<p>The <strong>span</strong> of the stock's price in one day is the maximum number of consecutive days (starting from that day and going backward) for which the stock price was less than or equal to the price of that day.</p>

<ul>
	<li>For example, if the prices of the stock in the last four days is <code>[7,2,1,2]</code> and the price of the stock today is <code>2</code>, then the span of today is <code>4</code> because starting from today, the price of the stock was less than or equal <code>2</code> for <code>4</code> consecutive days.</li>
	<li>Also, if the prices of the stock in the last four days is <code>[7,34,1,2]</code> and the price of the stock today is <code>8</code>, then the span of today is <code>3</code> because starting from today, the price of the stock was less than or equal <code>8</code> for <code>3</code> consecutive days.</li>
</ul>

<p>Implement the <code>StockSpanner</code> class:</p>

<ul>
	<li><code>StockSpanner()</code> Initializes the object of the class.</li>
	<li><code>int next(int price)</code> Returns the <strong>span</strong> of the stock's price given that today's price is <code>price</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input</strong>
["StockSpanner", "next", "next", "next", "next", "next", "next", "next"]
[[], [100], [80], [60], [70], [60], [75], [85]]
<strong>Output</strong>
[null, 1, 1, 1, 2, 1, 4, 6]

<strong>Explanation</strong>
StockSpanner stockSpanner = new StockSpanner();
stockSpanner.next(100); // return 1
stockSpanner.next(80);  // return 1
stockSpanner.next(60);  // return 1
stockSpanner.next(70);  // return 2
stockSpanner.next(60);  // return 1
stockSpanner.next(75);  // return 4, because the last 4 prices (including today's price of 75) were less than or equal to today's price.
stockSpanner.next(85);  // return 6
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= price &lt;= 10<sup>5</sup></code></li>
	<li>At most <code>10<sup>4</sup></code> calls will be made to <code>next</code>.</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p><strong>Let's start with code, then we move to visualization!</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-csharp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">StockSpanner</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(106, 153, 85);">/*
</span></span><span>        We should have a stack of a pair of (current  price, maximum number of consecutive days)
</span><span>        Since we don't have an access to the indicies.
</span><span><span class="token" style="color: rgb(106, 153, 85);">    */</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(78, 201, 176);">Stack</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">StockSpanner</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        s </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">Stack</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span>   </span><span class="token" style="color: rgb(106, 153, 85);">/*
</span></span><span>   Let's trace the algorithm together on [100, 80, 60, 70, 60, 75, 85]
</span><span>   1. calling StockSpanner.next(100) should result in first element in our stack will be (100, 1) (s.size() == 1)
</span><span>   2. calling StockSpanner.next(80) should result in second element in our stack will be (80, 1) (s.size() == 2)
</span><span>   3. calling StockSpanner.next(60) should result in third element in our stack will be (60, 1) (s.size() == 3)
</span><span>   4. Now on calling StockSpanner.next(70) we should add span of (60) + 1 {the current day}
</span><span>   and remove it from stack (70, 2) (s.size() == 3)
</span><span>   5. Now on calling StockSpanner.next(60) result in fourth element in our stack will be (60, 1) (s.size() == 4)
</span><span>   6. Now on calling StockSpanner.next(75) we should add span of (60) and (70) + 1 {the current day}
</span><span>   and remove it from stack : (75, 4) (s.size() == 3)
</span><span>   7. Now on calling StockSpanner.next(85) we should add span of (75) and (80) + 1 {the current day}
</span><span>   and remove it from stack : (85, 6) (s.size() == 2)
</span><span><span class="token" style="color: rgb(106, 153, 85);">   */</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">next</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> price</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> span </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> price </span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">peek</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// If the current price is greater than stack peek.</span><span>
</span></span><span><span>            span </span><span class="token" style="color: rgb(212, 212, 212);">+=</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">peek</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(86, 156, 214);">int</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">[</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>price</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> span</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> span</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p><img src="https://assets.leetcode.com/users/el-seoudy/image_1589879595.png" alt="image"></p>
<p><strong>Please upvote if you liked it.</strong> &lt;3</p></div>

## Find the Celebrity
<p>Suppose you are at a party with <code>n</code> people labeled from <code>0</code> to <code>n - 1</code> and among them, there may exist one celebrity. The definition of a celebrity is that all the other <code>n - 1</code> people know the celebrity, but the celebrity does not know any of them.</p>
<p>Now you want to find out who the celebrity is or verify that there is not one. You are only allowed to ask questions like: "Hi, A. Do you know B?" to get information about whether A knows B. You need to find out the celebrity (or verify there is not one) by asking as few questions as possible (in the asymptotic sense).</p>
<p>You are given a helper function <code>bool knows(a, b)</code> that tells you whether <code>a</code> knows <code>b</code>. Implement a function <code>int findCelebrity(n)</code>. There will be exactly one celebrity if they are at the party.</p>
<p>Return <em>the celebrity's label if there is a celebrity at the party</em>. If there is no celebrity, return <code>-1</code>.</p>
<p><strong class="example">Example 1:</strong></p>
<p><img alt="" src="https://fastly.jsdelivr.net/gh/doocs/leetcode@main/solution/0200-0299/0277.Find%20the%20Celebrity/images/g1.jpg" style="width: 224px; height: 145px;"></p>
<pre><strong>Input:</strong> graph = [[1,1,0],[0,1,0],[1,1,1]]
<strong>Output:</strong> 1
<strong>Explanation:</strong> There are three persons labeled with 0, 1 and 2. graph[i][j] = 1 means person i knows person j, otherwise graph[i][j] = 0 means person i does not know person j. The celebrity is the person labeled as 1 because both 0 and 2 know him but 1 does not know anybody.
</pre>
<p><strong class="example">Example 2:</strong></p>
<p><img alt="" src="https://fastly.jsdelivr.net/gh/doocs/leetcode@main/solution/0200-0299/0277.Find%20the%20Celebrity/images/g2.jpg" style="width: 224px; height: 145px;"></p>
<pre><strong>Input:</strong> graph = [[1,0,1],[1,1,0],[0,1,1]]
<strong>Output:</strong> -1
<strong>Explanation:</strong> There is no celebrity.
</pre>
<p><strong>Constraints:</strong></p>
<ul>
	<li><code>n == graph.length == graph[i].length</code></li>
	<li><code>2 &lt;= n &lt;= 100</code></li>
	<li><code>graph[i][j]</code> is <code>0</code> or <code>1</code>.</li>
	<li><code>graph[i][i] == 1</code></li>
</ul>

### Solution
<h2>Intuition</h2>
<p>To solve this problem, we take advantage of the unique characteristics of the celebrity:</p>
<ol>
<li>Every person other than the celebrity must know the celebrity, which means if <code>knows(a, b)</code> is <code>true</code>, <code>a</code> cannot be the celebrity.</li>
<li>The celebrity does not know anyone else, which implies if <code>knows(a, b)</code> is <code>false</code>, <code>b</code> cannot be the celebrity.</li>
</ol>
<p>Based on these points, we can iterate through the list of people at the party and use the <code>knows</code> function to determine potential candidates for being the celebrity. One way to find the celebrity is to assume the first person (labeled <code>0</code>) is the celebrity and then check this assumption against every other person using <code>knows</code>. If the assumed celebrity knows another person, then the assumption is wrong, and the other person becomes the new candidate for the celebrity. This process continues until we finish checking everybody.</p>
<p>After we find a candidate through the first iteration, we need to verify two conditions to confirm the candidate is indeed the celebrity:</p>
<ul>
<li>The candidate does not know any person. If the candidate knows any person, then the candidate cannot be the celebrity.</li>
<li>Every person knows the candidate. If there is any person who does not know the candidate, then the candidate cannot be the celebrity.</li>
</ul>
<p>The iteration for verification ensures that these conditions are met. If both conditions are satisfied for the candidate, then the candidate is the celebrity. Otherwise, there is no celebrity at the party.</p>
<p>The solution capitalizes on these ideas, using the intuition that knowing a person instantly disqualifies one from being a celebrity and not being known by at least one person also leads to a disqualification.</p></div>

```
/* The knows API is defined for you.
      bool knows(int a, int b); */

class Solution {
public:
    // This method is to find the celebrity within 'n' people. 
    // A celebrity is defined as somebody who everyone knows but who knows nobody themselves.
    int findCelebrity(int n) {
        // Initialize the candidate for celebrity to 0
        int candidate = 0;

        // The first loop is to find a candidate who might be the celebrity.
        for (int i = 1; i < n; ++i) {
            // If the candidate knows 'i', then 'candidate' can't be a celebrity.
            // 'i' might be the celebrity.
            if (knows(candidate, i)) {
                candidate = i;
            }
        }

        // The second loop is to confirm whether the candidate is the celebrity.
        for (int i = 0; i < n; ++i) {
            // The candidate should not know any other person,
            // and all other people should know the candidate.
            // If these conditions are not met, return -1 indicating no celebrity.
            if (candidate != i && (knows(candidate, i) || !knows(i, candidate))) {
                return -1;
            }
        }

        // If all conditions are met, return the candidate as the celebrity.
        return candidate;
    }
};
```
