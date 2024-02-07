## Table of Content
1. [Maximum Number of Non-Overlapping Substrings](#maximum-number-of-non-overlapping-substrings)
2. [Dijkstra's Algorithm](#dijkstras-algorithm)
3. [Bellman-Ford Algorithm](#bellman-ford-algorithm)
4. [Floyd-Warshall Algorithm](#floyd-warshall)


## KOSARAJU'S ALGORITHM FOR STRONGLY CONNECTED COMPONENTS
<p><a href="https://www.topcoder.com/thrive/articles/kosarajus-algorithm-for-strongly-connected-components" target="blank">Read Here</a>
</p>

## Maximum Number of Non-Overlapping Substrings
<div class="elfjS" data-track-load="description_content"><p>Given a string <code>s</code> of lowercase letters, you need to find the maximum number of <strong>non-empty</strong> substrings of <code>s</code> that meet the following conditions:</p>

<ol>
	<li>The substrings do not overlap, that is for any two substrings <code>s[i..j]</code> and <code>s[x..y]</code>, either <code>j &lt; x</code> or <code>i &gt; y</code> is true.</li>
	<li>A substring that contains a certain character <code>c</code> must also contain all occurrences of <code>c</code>.</li>
</ol>

<p>Find <em>the maximum number of substrings that meet the above conditions</em>. If there are multiple solutions with the same number of substrings, <em>return the one with minimum total length. </em>It can be shown that there exists a unique solution of minimum total length.</p>

<p>Notice that you can return the substrings in <strong>any</strong> order.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> s = "adefaddaccc"
<strong>Output:</strong> ["e","f","ccc"]
<b>Explanation:</b>&nbsp;The following are all the possible substrings that meet the conditions:
[
&nbsp; "adefaddaccc"
&nbsp; "adefadda",
&nbsp; "ef",
&nbsp; "e",
  "f",
&nbsp; "ccc",
]
If we choose the first string, we cannot choose anything else and we'd get only 1. If we choose "adefadda", we are left with "ccc" which is the only one that doesn't overlap, thus obtaining 2 substrings. Notice also, that it's not optimal to choose "ef" since it can be split into two. Therefore, the optimal way is to choose ["e","f","ccc"] which gives us 3 substrings. No other solution of the same number of substrings exist.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> s = "abbaccd"
<strong>Output:</strong> ["d","bb","cc"]
<b>Explanation: </b>Notice that while the set of substrings ["d","abba","cc"] also has length 3, it's considered incorrect since it has larger total length.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>5</sup></code></li>
	<li><code>s</code> contains only lowercase English letters.</li>
</ul>
</div>

### Solution
<div class="break-words"><div><div class="FN9Jv WRmCx"><p>Model this question as graph problem</p>
<p>If there is a character 'b' between the first and last occurrence of character 'a', then it means we must include 'b' in the substring if we want to include 'a', so we can create an edge from 'a' to 'b'.</p>
<p>So we can convert the input string into a directed graph, which has at most 26 vertex 'a' to 'z'.</p>
<p>Within this graph, each SCC (Strongly Connected Components) much be included in a substring together. Additionaly, 'downstream' SCCs of a chosen SCC must also be included in the same substring.</p>
<p>Thus, its easy to see that we just need to find all the SCC with 0 out-degree. Characters in each SCC are characters we must include in each substring. And it is guaranteed to be minimal total length.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">List</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(78, 201, 176);">String</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">maxNumOfSubstrings</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">String</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">S</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>	    </span><span class="token" style="color: rgb(106, 153, 85);">// some nasty pre-compute in order to build the graph in O(N) time</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> mins </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> maxs </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">Arrays</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">fill</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>mins</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>MAX_VALUE</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">Arrays</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">fill</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>maxs</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">boolean</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> exists </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">boolean</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> prefixSum </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(78, 201, 176);">S</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">S</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(78, 201, 176);">System</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">arraycopy</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>prefixSum</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> prefixSum</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>            prefixSum</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(78, 201, 176);">S</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'a'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>            mins</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(78, 201, 176);">S</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'a'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Math</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">min</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>mins</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(78, 201, 176);">S</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'a'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>            maxs</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(78, 201, 176);">S</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'a'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Math</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">max</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>maxs</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(78, 201, 176);">S</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'a'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>            exists</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(78, 201, 176);">S</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'a'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">true</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// build graph, using adjacency matrix</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">boolean</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> graph </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">boolean</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>exists</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>prefixSum</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>maxs</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> prefixSum</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>mins</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                        graph</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">true</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>                    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// kosaraju algorithm to find scc</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">Stack</span><span> stack </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Stack</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">boolean</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> visited </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">boolean</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>exists</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>visited</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(220, 220, 170);">dfs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> graph</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> stack</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> visited</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> batch </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// 'id' of each SCC</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> batches </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> degree </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>  </span><span class="token" style="color: rgb(106, 153, 85);">// out-degree of each SCC</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">Arrays</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">fill</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>batches</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>stack</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> v </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> stack</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>batches</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>v</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(220, 220, 170);">dfs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>v</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> graph</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> batches</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> batch</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> degree</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                batch </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">List</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(78, 201, 176);">String</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span> res </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">ArrayList</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> batch </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">--</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>degree</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> min </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>MAX_VALUE</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> max </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>batches</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                        min </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Math</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">min</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>mins</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> min</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>                        max </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Math</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">max</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>maxs</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> max</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>                    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>                res</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">S</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">substring</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>min</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> max </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> res</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">dfs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> v</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">boolean</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> graph</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Stack</span><span> stack</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">boolean</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> visited</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>visited</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>v</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            visited</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>v</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">true</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>graph</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>v</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>visited</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(220, 220, 170);">dfs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> graph</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> stack</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> visited</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            stack</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>v</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">dfs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> v</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">boolean</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> graph</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> batches</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> batch</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> degree</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>batches</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>v</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            batches</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>v</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> batch</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>graph</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>v</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(220, 220, 170);">dfs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> graph</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> batches</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> batch</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> degree</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>  
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>batches</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>v</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> batch</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                degree</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>batches</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>v</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">static</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">final</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Stack</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> values </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> top </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            values</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>top </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> val</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            top </span><span class="token" style="color: rgb(212, 212, 212);">--</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> values</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>top</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">boolean</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> top </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>        
</span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div></div></div></div>

## Go To
[Table of Content](#table-of-content)

## Dijkstra's Algorithm
<p id="ember63" class="ember-view reader-content-blocks__paragraph">
      <!---->Dijkstra's algorithm is a fundamental and widely used algorithm for solving the single-source shortest path problem in graphs. It was developed by computer scientist Edsger W. Dijkstra and has since become one of the most important algorithms in graph theory and network analysis.<!---->
<!---->    </p>      
 <img src="https://media.licdn.com/dms/image/D5612AQFWVDOjXX4FMg/article-inline_image-shrink_1500_2232/0/1685397234242?e=1712793600&amp;v=beta&amp;t=BHZnO9yKL8_znruPxeVTy1L14hVdt_uMHPbtXYoHHIQ" loading="lazy" alt="No alt text provided for this image" id="ember64" class="ivm-view-attr__img--centered  reader-image-block__img evi-image lazy-image ember-view">
<p id="ember65" class="ember-view reader-content-blocks__paragraph">
      <!---->The<span class="white-space-pre"> </span><strong><!---->single-source shortest path problem<!----></strong><span class="white-space-pre"> </span>involves finding the shortest path from a specific source vertex to all other vertices in a graph.<span class="white-space-pre"> </span><strong><!---->Dijkstra's algorithm uses a greedy approach<!----></strong><span class="white-space-pre"> </span>to explore the graph iteratively, incrementally building the shortest path tree.<!---->
<!---->    </p><p id="ember66" class="ember-view reader-content-blocks__paragraph">
      <!---->The key idea behind Dijkstra's algorithm is that the shortest path to a vertex is known once it has been visited, ensuring the optimality of the paths discovered. This property is achieved by selecting the vertex with the smallest tentative distance in each iteration, ensuring that the algorithm considers the most promising paths first.<!---->
<!---->    </p><p id="ember67" class="ember-view reader-content-blocks__paragraph">
      <!---->The greedy aspect of Dijkstra's algorithm is important because it ensures that the algorithm considers the most promising paths first. By always choosing the vertex with the smallest tentative distance, Dijkstra's algorithm explores the graph in a manner that prioritizes immediate gains in terms of finding shorter paths.<!---->
<!---->    </p>
<p id="ember68" class="ember-view reader-content-blocks__paragraph">
            <ul><li><!---->However, it is worth noting that the greedy choice made by Dijkstra's algorithm can only guarantee optimality if the graph has<span class="white-space-pre"> </span><strong><!---->non-negative edge weights<!----></strong><!---->. Negative weights may violate the optimality assumption, leading to incorrect shortest paths. However, for larger graphs or graphs with negative edge weights, more specialized algorithms like the<span class="white-space-pre"> </span><a class="app-aware-link " target="_self" href="https://www.linkedin.com/pulse/single-source-shortest-path-problem-shubham-shankar/?trackingId=zn91EThvYs5NQW%2FWHaEruA%3D%3D" data-test-app-aware-link=""><strong><!---->Bellman-Ford algorithm<!----></strong></a><span class="white-space-pre"> </span>or the<span class="white-space-pre"> </span><strong><!---->A* algorithm<!----></strong><span class="white-space-pre"> </span>may be more suitable.<!----></li></ul>

<!---->    </p>
<p id="ember69" class="ember-view reader-content-blocks__paragraph">
      <!---->Nevertheless, Dijkstra's algorithm remains a fundamental and widely employed tool in graph theory, network analysis, and various real-world applications that involve finding the shortest path in graphs.<!---->
<!---->    </p>
<h3 id="ember70" class="ember-view">
      <strong><!---->A step-by-step explanation of how Dijkstra's algorithm works:<!----></strong>
<!---->    </h3>
<p id="ember71" class="ember-view reader-content-blocks__paragraph">
      <!---->1.<span class="white-space-pre"> </span><strong><span class="white-space-pre"> </span>Initialize the algorithm<!----></strong><!---->:<!---->
<!---->    </p>
<p id="ember72" class="ember-view reader-content-blocks__paragraph">
            <ul><li><!---->Set the distance of the source vertex to 0 and the distances of all other vertices to infinity.<!----></li><li><!---->Set the distance of the source vertex as the current distance.<!----></li><li><!---->Create an empty set to store visited vertices.<!----></li></ul>

<!---->    </p>
<p id="ember73" class="ember-view reader-content-blocks__paragraph">
      <!---->2.<span class="white-space-pre"> </span><strong><!---->Find the vertex with the smallest tentative distance<!----></strong><!---->:<!---->
<!---->    </p>
<p id="ember74" class="ember-view reader-content-blocks__paragraph">
            <ul><li><!---->Choose the vertex with the smallest current distance (initially, this will be the source vertex).<!----></li><li><span class="white-space-pre"> </span>Mark it as visited and add it to the set of visited vertices.<!----></li></ul>

<!---->    </p>
<p id="ember75" class="ember-view reader-content-blocks__paragraph">
      <!---->3.<span class="white-space-pre"> </span><strong><!---->Update tentative distances<!----></strong><!---->:<!---->
<!---->    </p>
<p id="ember76" class="ember-view reader-content-blocks__paragraph">
            <ul><li><!---->For each neighbor of the current vertex:<!----></li></ul>

<!---->    </p>
<p id="ember77" class="ember-view reader-content-blocks__paragraph">
      <span class="white-space-pre"> </span>o Calculate the distance to reach that neighbor from the source by summing the current distance and the weight of the edge connecting the current vertex to its neighbor.<!---->
<!---->    </p>
<p id="ember78" class="ember-view reader-content-blocks__paragraph">
      <span class="white-space-pre"> </span>o If the calculated distance is smaller than the neighbor's current distance, update it.<!---->
<!---->    </p>
<p id="ember79" class="ember-view reader-content-blocks__paragraph">
      <!---->4.<span class="white-space-pre"> </span><strong><!---->Repeat steps 2 and 3 until all vertices have been visited<!----></strong><!---->:<!---->
<!---->    </p>
<p id="ember80" class="ember-view reader-content-blocks__paragraph">
            <ul><li><!---->Choose the unvisited vertex with the smallest tentative distance.<!----></li><li><!---->Mark it as visited and update the tentative distances of its neighbors.<!----></li></ul>

<!---->    </p>
<p id="ember81" class="ember-view reader-content-blocks__paragraph">
      <!---->5.&nbsp;&nbsp;&nbsp;&nbsp;Once<span class="white-space-pre"> </span><strong><!---->all vertices have been visited<!----></strong><span class="white-space-pre"> </span>or the destination vertex has been reached, the algorithm terminates.<!---->
<!---->    </p>
<p id="ember82" class="ember-view reader-content-blocks__paragraph">
      <!---->6.<span class="white-space-pre"> </span><strong><!---->Extract the shortest path<!----></strong><!---->:<!---->
<!---->    </p>
<p id="ember83" class="ember-view reader-content-blocks__paragraph">
            <ul><li><!---->To obtain the shortest path from the source vertex to any other vertex, follow the predecessor pointers starting from the destination vertex and working backward until the source vertex is reached.<!----></li></ul>

<!---->    </p>
 <img src="https://media.licdn.com/dms/image/D5612AQEUoLUm69JGLw/article-inline_image-shrink_1500_2232/0/1685397873594?e=1712793600&amp;v=beta&amp;t=c96vADPR6nCXggk7YAPGeBu-CMj--ivkN8UxGTUt1Yk" loading="lazy" alt="No alt text provided for this image" id="ember85" class="ivm-view-attr__img--centered  reader-image-block__img evi-image lazy-image ember-view">

### Code:

```
#include <iostream>
#include <vector>
#include <queue>
#include <climits> // For INT_MAX

using namespace std;

class Solution {
public:
    vector<int> dijkstra(int V, vector<vector<pair<int, int>>>& adj, int S) {
        // Initialize distances to infinity
        vector<int> distance(V, INT_MAX);
        distance[S] = 0; // Distance to source is 0
        
        // Min heap to store vertices by distance
        priority_queue<pair<int, int>, vector<pair<int, int>>, greater<pair<int, int>>> minHeap;
        minHeap.push({0, S}); // Push source vertex with distance 0
        
        // Dijkstra's Algorithm
        while (!minHeap.empty()) {
            int dist = minHeap.top().first;
            int node = minHeap.top().second;
            minHeap.pop();
            
            // Check neighbors of current node
            for (auto& nei : adj[node]) {
                int adj_nei = nei.first;
                int weight = nei.second;
                
                // Update distance if shorter path found
                int update_dist = dist + weight;
                if (update_dist < distance[adj_nei]) {
                    distance[adj_nei] = update_dist;
                    minHeap.push({update_dist, adj_nei});
                }
            }
        }
        
        return distance;
    }
};

int main() {
    Solution sol;
    
    int V = 5; // Number of vertices
    vector<vector<pair<int, int>>> adj(V); // Adjacency list representation of graph
    
    // Add edges to the graph
    adj[0].push_back({1, 2}); // Edge from vertex 0 to vertex 1 with weight 2
    adj[0].push_back({2, 4}); // Edge from vertex 0 to vertex 2 with weight 4
    adj[1].push_back({2, 1}); // Edge from vertex 1 to vertex 2 with weight 1
    adj[1].push_back({3, 7}); // Edge from vertex 1 to vertex 3 with weight 7
    adj[2].push_back({3, 3}); // Edge from vertex 2 to vertex 3 with weight 3
    adj[2].push_back({4, 2}); // Edge from vertex 2 to vertex 4 with weight 2
    adj[3].push_back({4, 5}); // Edge from vertex 3 to vertex 4 with weight 5
    
    int source = 0; // Source vertex
    
    // Run Dijkstra's Algorithm
    vector<int> distances = sol.dijkstra(V, adj, source);
    
    // Print shortest distances from source vertex to all other vertices
    cout << "Shortest distances from vertex " << source << ":\n";
    for (int i = 0; i < V; ++i) {
        cout << "Vertex " << i << ": " << distances[i] << "\n";
    }
    
    return 0;
}
```
## Go To
[Table of Content](#table-of-content)
## Bellman-Ford Algorithm
<p>Consider a scenario where you are presented with a weighted graph. Your objective is to determine the shortest path from a given source vertex to all other vertices. Initially, you might consider implementing Dijkstra’s algorithm for this task. However, if the graph contains negative weights, Dijkstra’s algorithm cannot be used. Therefore, we need a different algorithm that can handle such situations. The Bellman-Ford algorithm is a suitable alternative to Dijkstra’s algorithm as it accommodates negative edge weights.<br>
This article provides a comprehensive discussion of the Bellman-Ford algorithm. It covers its functionality, complexity, highlights the disparities between Dijkstra’s and Bellman-Ford algorithms, and presents various applications of the Bellman-Ford algorithm. Before delving into the details of the Bellman-Ford algorithm, it is important to understand why negative weights in a graph pose a challenge and warrant caution.</p>
<h3>Why Should We Be Cautious Of Negative Weights?</h3>
<p>It is important to exercise caution when dealing with negative weight edges in a graph due to the possibility of generating negative weight cycles. Negative weight cycles are cycles that have the same vertex at the beginning and end, and their total sum of edge weights is negative. These cycles pose a challenge for shortest path algorithms as they cannot accurately detect them, leading to incorrect results. Even the Bellman-Ford algorithm is unable to overcome this limitation. To grasp this concept more clearly, please refer to the illustration provided below.</p>
<p><img decoding="async" src="https://prepbytes-misc-images.s3.ap-south-1.amazonaws.com/assets/1679578791206-1-01%20%2829%29.png" alt=""></p>
<p>The vertices B, C, and D in this illustration form a cycle with B as the starting and ending nodes. This cycle also behaves as a negative cycle because the total value is -1.</p>
<h3>How Bellman-Ford Algorithm Works</h3>
<p>The Bellman-Ford algorithm is a single-source shortest-path algorithm that can handle negative weight edges. It works by iteratively relaxing all edges in the graph, reducing the estimated distance from the source vertex to all other vertices until the actual shortest path is found.</p>
<p>Here are the steps involved in the Bellman-Ford algorithm:</p>
<ul>
<li><strong>Step – 1</strong> Initialize the distance to the source vertex as 0, and the distance to all other vertices as infinity.</li>
<li><strong>Step – 2</strong> Relax all edges in the graph |V| – 1 times, where |V| is the number of vertices in the graph. For each edge (u, v) with weight w, check if the distance from the source vertex to v can be reduced by going through u. If so, update the distance to v to the new, shorter distance.</li>
<li><strong>Step – 3</strong> Check for negative weight cycles. If there is a negative weight cycle in the graph, the algorithm will never converge and will keep reducing the distance to some vertices with each iteration. To detect such cycles, repeat step 2 one more time. If any distance is updated in this extra iteration, there must be a negative weight cycle in the graph.</li>
<li><strong>Step – 4</strong> If there is no negative weight cycle, the shortest distance to each vertex from the source vertex has been found.</li>
</ul>

```
#include <bits/stdc++.h>
using namespace std;

struct Edge {
    int src, dest, weight;
};

struct Graph {
    int V, E;
    struct Edge* edge;
};

struct Graph* createGraph(int V, int E)
{
    struct Graph* graph = new Graph;
    graph->V = V;
    graph->E = E;
    graph->edge = new Edge[E];
    return graph;
}

void printArr(int dist[], int n)
{
    printf("Vertex   Distance from Source\n");
    for (int i = 0; i < n; ++i)
        printf("%d \t\t %d\n", i, dist[i]);
}

void BellmanFord(struct Graph* graph, int src)
{
    int V = graph->V;
    int E = graph->E;
    int dist[V];
    for (int i = 0; i < V; i++)
        dist[i] = INT_MAX;
    dist[src] = 0;
    for (int i = 1; i <= V - 1; i++) {
        for (int j = 0; j < E; j++) {
            int u = graph->edge[j].src;
            int v = graph->edge[j].dest;
            int weight = graph->edge[j].weight;
            if (dist[u] != INT_MAX
                && dist[u] + weight < dist[v])
                dist[v] = dist[u] + weight;
        }
    }
    for (int i = 0; i < E; i++) {
        int u = graph->edge[i].src;
        int v = graph->edge[i].dest;
        int weight = graph->edge[i].weight;
        if (dist[u] != INT_MAX
            && dist[u] + weight < dist[v]) {
            printf("Graph contains negative weight cycle");
            return;
        }
    }
    printArr(dist, V);
    return;
}

int main()
{
    int V = 5;
    int E = 8;
    struct Graph* graph = createGraph(V, E);

    // adding edge 0-1 (or A-B in above dry run)
    graph->edge[0].src = 0;
    graph->edge[0].dest = 1;
    graph->edge[0].weight = -1;

    // adding edge 0-2 (or A-C in above dry run)
    graph->edge[1].src = 0;
    graph->edge[1].dest = 2;
    graph->edge[1].weight = 4;

    // adding edge 1-2 (or B-C in above dry run)
    graph->edge[2].src = 1;
    graph->edge[2].dest = 2;
    graph->edge[2].weight = 3;

    // adding edge 1-3 (or B-D in above dry run)
    graph->edge[3].src = 1;
    graph->edge[3].dest = 3;
    graph->edge[3].weight = 2;

    // adding edge 1-4 (or B-E in above dry run)
    graph->edge[4].src = 1;
    graph->edge[4].dest = 4;
    graph->edge[4].weight = 2;

    // adding edge 3-2 (or D-C in above dry run)
    graph->edge[5].src = 3;
    graph->edge[5].dest = 2;
    graph->edge[5].weight = 5;

    // adding edge 3-1 (or D-B in above dry run)
    graph->edge[6].src = 3;
    graph->edge[6].dest = 1;
    graph->edge[6].weight = 1;

    // adding edge 4-3 (or E-D in above dry run)
    graph->edge[7].src = 4;
    graph->edge[7].dest = 3;
    graph->edge[7].weight = -3;
    
    BellmanFord(graph, 0);
    return 0;
}
```
## Go To
[Table of Content](#table-of-content)
## Floyd Warshall
<h3>What is the Floyd Warshall Algorithm in C?</h3>
<p>Floyd-Warshall Algorithm is an algorithm which follows dynamic programming approach to find the shortest path between all the pairs of vertices in a weighted graph. This algorithm works well for both the directed and undirected weighted graphs. But, it does not work for graphs that contain negative weight cycles.</p>
<p>If you’re looking for an algorithm for scenarios like finding the shortest path between every pair of cities in a state or in a country, then the best man at work is our polynomial-time Floyd-Warshall algorithm.</p>
<p>In other words, the Floyd-Warshall algorithm is the best choice for finding the shortest path across every pair of vertex in a graph.</p>
<p>One restriction we have to follow is that the graph shouldn’t contain any negative weight cycles.</p>
<p>You see, the Floyd-Warshall algorithm does support negative weight edges in a directed graph so long the weighted sum of such edges forming a cycle isn’t negative.</p>
<p>And that’s what here means by a negative weight cycle.</p>
<p>If there exists at least one such negative weight cycle, we can always just keep traversing this cycle over and over while making the length of the path smaller and smaller. Keep repeating it, and the length at some point reaches negative infinity which is wildly unreasonable.</p>
<p><img decoding="async" src="https://prepbytes-misc-images.s3.ap-south-1.amazonaws.com/assets/1675334232295-Floyd%20Warshall%20Algorithm1.png" alt=""></p>
<p>Also if we notice, the algorithm cannot support negative weight edges in an undirected graph at all. Such an edge forms a negative cycle in and of itself since we can traverse back and forth along that edge infinitely as it’s an undirected graph.</p>
<p>Well, you may suspect why we are learning another algorithm when we can solve the same thing by expanding the Bellman-Ford or Dijkstra’s shortest path algorithm on every vertex in the graph.</p>
<p>Yes, you can, but the main reason why we are not using Bellman-Ford or Dijkstra’s shortest path algorithm is their Time complexity which we will discuss later in this article.</p>
<p>Now that we have developed a fair understanding as to what is and why we use the Floyd-Warshall algorithm, let’s take our discussion ahead and see how it actually works.</p>
<p><strong>Points to Remember:</strong></p>
<ul>
<li>Negative weight cycle graphs are graphs where the sum of the weights of edges in a cycle is negative).</li>
<li>A weighted graph is a graph in which each edge has some weight(numerical value) associated with it.</li>
</ul>
<h3>How does Floyd Warshall Algorithm in C Work?</h3>
<p><img decoding="async" src="https://prepbytes-misc-images.s3.ap-south-1.amazonaws.com/assets/1675334232295-Floyd%20Warshall%20Algorithm2.png" alt=""></p>
<p>Follow the steps mentioned below to find the shortest path between all the pairs of vertices:</p>
<ul>
<li>
<p><strong>Step 1:</strong><br>
Create a matrix A0 of dimension V*V, where V is the number of vertices. The row and column are indexed as i and j, respectively. i and j are the graph’s vertices.<br>
The value of cell A[i][j] means the distance from the ith vertex to the jth vertex. If there is no path between the ith vertex and the jth vertex, the cell is left with infinity.</p>
<p><img decoding="async" src="https://prepbytes-misc-images.s3.ap-south-1.amazonaws.com/assets/1675334232333-Floyd%20Warshall%20Algorithm3.png" alt=""></p>
</li>
<li>
<p><strong>Step 2:</strong><br>
Now, using matrix A0, construct matrix A1. The elements in the first column and row stay unchanged. The remaining cells are filled out as follows.</p>
<p>Let k be the intermediate vertex on the shortest path from source to destination. k is the 0th vertex (i.e k = 0) in this stage. If (A[i][j] &gt; A[i][k] + A[k][j]), A[i][j] is filled with (A[i][k] + A[k][j]).</p>
<p>In other words, if the direct distance between the source and the destination is larger than the path through the vertex k, the cell is filled with A[i][k] + A[k][j].</p>
<p><img decoding="async" src="https://prepbytes-misc-images.s3.ap-south-1.amazonaws.com/assets/1675334232334-Floyd%20Warshall%20Algorithm4.png" alt=""></p>
<p>This vertex k is used to compute the distance from the source vertex to the destination vertex.</p>
</li>
<li>
<p><strong>Step 3:</strong><br>
Similarly, A2 is derived from A1. The elements in the second column and second row remain unchanged.</p>
<p>k is the 1st vertex in this stage (i.e. k = 1). The remaining steps are similar to those in step 2.</p>
<p><img decoding="async" src="https://prepbytes-misc-images.s3.ap-south-1.amazonaws.com/assets/1675334232338-Floyd%20Warshall%20Algorithm5.png" alt=""></p>
<p>For example: For A2[3,2], the direct distance from vertex 3 to 2 is infinity and the sum of the distance from vertex 3 to 2 through vertex k(i.e. from vertex 3 to vertex 1 and from vertex 1 to vertex 2) is 0. Since 0 is less than infinity, A2[3,2] is filled with 0.</p>
</li>
<li>
<p><strong>Step 4:</strong><br>
Similarly, A3 and A4 matrices are also constructed.<br>
When generating A3, k is a second vertex(i.e. K = 2) and k is a third vertex(i.e. K = 3) during the construction of A4.</p>
</li>
</ul>
<p><img decoding="async" src="https://prepbytes-misc-images.s3.ap-south-1.amazonaws.com/assets/1675334232338-Floyd%20Warshall%20Algorithm6.png" alt=""></p>
<p><img decoding="async" src="https://prepbytes-misc-images.s3.ap-south-1.amazonaws.com/assets/1675334232339-Floyd%20Warshall%20Algorithm7.png" alt=""></p>
<ul>
<li>
<p><strong>Step 5:</strong><br>
A4 displays the shortest path between any pair of vertices.</p>
<p><img decoding="async" src="https://prepbytes-misc-images.s3.ap-south-1.amazonaws.com/assets/1675334232372-Floyd%20Warshall%20Algorithm8.png" alt=""></p>
</li>
</ul>

```
// Implementation of Floyd-Warshall Algorithm in C++
#include <iostream>
using namespace std;

// defining the number of vertices
#define V 4

#define INF 9999

void printMatrix(int matrix[][V]);

// Implementing floyd warshall algorithm
void floydWarshall(int graph[][V]) {
  int matrix[V][V], i, j, k;
  for (i = 0; i < V; i++)
    for (j = 0; j < V; j++)
      matrix[i][j] = graph[i][j];

  // Adding vertices individually
  for (k = 0; k < V; k++) {
    for (i = 0; i < V; i++) {
      for (j = 0; j < V; j++) {
        if (matrix[i][k] + matrix[k][j] < matrix[i][j])
          matrix[i][j] = matrix[i][k] + matrix[k][j];
      }
    }
  }
  printMatrix(matrix);
}

void printMatrix(int matrix[][V]) {
  for (int i = 0; i < V; i++) {
    for (int j = 0; j < V; j++) {
        if(i==j){
            continue;
        }
        else if (matrix[i][j] == INF){
            cout<<"no path exist between "<<i<<" and "<<j<<endl;
        }
        else{
            cout<<"shortest path from "<<i<<" to "<<j<<" is "<<matrix[i][j]<<endl;
        }
    }
  }
}

int main() {
  int graph[V][V] = {{0,INF,-3,INF},
                     {5,0,4,INF},
                     {INF,INF,0,3},
                     {INF,-2,INF,0}};
  floydWarshall(graph);
  return 0;
  // End of Program
}
```
## Go To
[Table of Content](#table-of-content)
## Prims Algorithm + Minimum Spanning Tree
<a href="https://www.interviewkickstart.com/learn/prims-spanning-tree-algorithm" target="_blank">Prim's Spanning Tree Algorithm</a>


## Kruskals Algo
<a href="https://www.thealgorist.com/Algo/GraphTheory/Kruskal" target="_blank">Kruskal's Algorithm</a>
## Go To
[Table of Content](#table-of-content)
