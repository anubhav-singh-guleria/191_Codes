# ARRAYS-II

## Table of Content
1. [Rotate Image](#arrays---ii-rotate-image)
2. [Merge Intervals](#arrays---ii-merge-intervals)
3. [Merge Two Sorted Arrays Without Extra Space](#arrays---ii-merge-two-sorted-arrays-without-extra-space)
4. [Find the Duplicate in an Array of n+1 Integers](#arrays---ii-find-the-duplicate-in-an-array-of-n1-integers)
5. [Find the Repeating and Missing Numbers](#arrays---ii-find-the-repeating-and-missing-numbers)
6. [Global and Local Inversions](#arrays---ii-global-and-local-inversions)
## Arrays - II Rotate Image
<div class="elfjS" data-track-load="description_content"><p>You are given an <code>n x n</code> 2D <code>matrix</code> representing an image, rotate the image by <strong>90</strong> degrees (clockwise).</p>

<p>You have to rotate the image <a href="https://en.wikipedia.org/wiki/In-place_algorithm" target="_blank"><strong>in-place</strong></a>, which means you have to modify the input 2D matrix directly. <strong>DO NOT</strong> allocate another 2D matrix and do the rotation.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/08/28/mat1.jpg" style="width: 500px; height: 188px;">
<pre><strong>Input:</strong> matrix = [[1,2,3],[4,5,6],[7,8,9]]
<strong>Output:</strong> [[7,4,1],[8,5,2],[9,6,3]]
</pre>

<p><strong class="example">Example 2:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/08/28/mat2.jpg" style="width: 500px; height: 201px;">
<pre><strong>Input:</strong> matrix = [[5,1,9,11],[2,4,8,10],[13,3,6,7],[15,14,12,16]]
<strong>Output:</strong> [[15,13,2,5],[14,3,4,1],[12,6,8,9],[16,7,10,11]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == matrix.length == matrix[i].length</code></li>
	<li><code>1 &lt;= n &lt;= 20</code></li>
	<li><code>-1000 &lt;= matrix[i][j] &lt;= 1000</code></li>
</ul>
</div>
<h3>Solution</h3>
<div class="FN9Jv WRmCx"><p>here give a common method to solve the image rotation problems.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(106, 153, 85);">/*
</span></span><span> * clockwise rotate
</span><span> * first reverse up to down, then swap the symmetry 
</span><span> * 1 2 3     7 8 9     7 4 1
</span><span> * 4 5 6  =&gt; 4 5 6  =&gt; 8 5 2
</span><span> * 7 8 9     1 2 3     9 6 3
</span><span><span class="token" style="color: rgb(106, 153, 85);">*/</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">rotate</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span>matrix</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(220, 220, 170);">reverse</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>matrix</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">begin</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> matrix</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">end</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> matrix</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> matrix</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(220, 220, 170);">swap</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>matrix</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> matrix</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">/*
</span></span><span> * anticlockwise rotate
</span><span> * first reverse left to right, then swap the symmetry
</span><span> * 1 2 3     3 2 1     3 6 9
</span><span> * 4 5 6  =&gt; 6 5 4  =&gt; 2 5 8
</span><span> * 7 8 9     9 8 7     1 4 7
</span><span><span class="token" style="color: rgb(106, 153, 85);">*/</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">anti_rotate</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span>matrix</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">auto</span><span> vi </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> matrix</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">reverse</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vi</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">begin</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> vi</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">end</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> matrix</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> matrix</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(220, 220, 170);">swap</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>matrix</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> matrix</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>

## Go To
[Table of Content](#table-of-content)

## Arrays - II Merge Intervals
<div class="elfjS" data-track-load="description_content"><p>Given an array&nbsp;of <code>intervals</code>&nbsp;where <code>intervals[i] = [start<sub>i</sub>, end<sub>i</sub>]</code>, merge all overlapping intervals, and return <em>an array of the non-overlapping intervals that cover all the intervals in the input</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> intervals = [[1,3],[2,6],[8,10],[15,18]]
<strong>Output:</strong> [[1,6],[8,10],[15,18]]
<strong>Explanation:</strong> Since intervals [1,3] and [2,6] overlap, merge them into [1,6].
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> intervals = [[1,4],[4,5]]
<strong>Output:</strong> [[1,5]]
<strong>Explanation:</strong> Intervals [1,4] and [4,5] are considered overlapping.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= intervals.length &lt;= 10<sup>4</sup></code></li>
	<li><code>intervals[i].length == 2</code></li>
	<li><code>0 &lt;= start<sub>i</sub> &lt;= end<sub>i</sub> &lt;= 10<sup>4</sup></code></li>
</ul>
</div>

### Solution
<div class="break-words"><div><div class="FN9Jv WRmCx"><h4 id="intuition">Intuition</h4>

<p>We can solve this question using Array + Sorting.</p>
<h4 id="approach">Approach</h4>

<p>We can easily understand the approach by seeing the code which is easy to understand with comments.</p>
<h4 id="complexity">Complexity</h4>
<ul>
<li>Time complexity:</li>
</ul>

<p>Time Complexity : O(NlogN), Sorting the array(intervals) costs O(NlogN). Where N is the size of the Vector(intervals).</p>
<ul>
<li>Space complexity:</li>
</ul>

<p>Space Complexity : O(1), Constant Space. Extra space is only allocated for the Vector(output) which can go upto size N , however the output does not count towards the space complexity.</p>
<h4 id="code">Code</h4>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: black; font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent; overflow-wrap: normal;"><code class="language-cpp" style="text-shadow: none; white-space: pre;"><span><span class="token" style="color: slategray;">/*
</span></span><span>
</span><span>    Time Complexity : O(NlogN), Sorting the array(intervals) costs O(NlogN). Where N is the size of
</span><span>    the Vector(intervals).
</span><span>
</span><span>    Space Complexity : O(1), Constant Space. Extra space is only allocated for the Vector(output)
</span><span>    which can go upto size N , however the output does not count towards the space complexity.
</span><span>
</span><span>    Solved using Array + Sorting.
</span><span>
</span><span><span class="token" style="color: slategray;">*/</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(0, 119, 170);">class</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">Solution</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(0, 119, 170);">public</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">:</span><span>
</span></span><span><span>    vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span>vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;&gt;</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">merge</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span>vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;&gt;</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&amp;</span><span> intervals</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> n </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> intervals</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">size</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(221, 74, 104);">sort</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>intervals</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">begin</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> intervals</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">end</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>        vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span>vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;&gt;</span><span> output</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">for</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(0, 119, 170);">auto</span><span> interval </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">:</span><span> intervals</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(0, 119, 170);">if</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>output</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">empty</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">||</span><span> output</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">back</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span> interval</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">0</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>                output</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">push_back</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>interval</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(0, 119, 170);">else</span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>                output</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">back</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">max</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>output</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">back</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> interval</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">return</span><span> output</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(153, 153, 153);">}</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
</div></div></div>

## Go To
[Table of Content](#table-of-content)

## Arrays - II Merge two Sorted Arrays Without Extra Space
<div class="elfjS" data-track-load="description_content"><p>You are given two integer arrays <code>nums1</code> and <code>nums2</code>, sorted in <strong>non-decreasing order</strong>, and two integers <code>m</code> and <code>n</code>, representing the number of elements in <code>nums1</code> and <code>nums2</code> respectively.</p>

<p><strong>Merge</strong> <code>nums1</code> and <code>nums2</code> into a single array sorted in <strong>non-decreasing order</strong>.</p>

<p>The final sorted array should not be returned by the function, but instead be <em>stored inside the array </em><code>nums1</code>. To accommodate this, <code>nums1</code> has a length of <code>m + n</code>, where the first <code>m</code> elements denote the elements that should be merged, and the last <code>n</code> elements are set to <code>0</code> and should be ignored. <code>nums2</code> has a length of <code>n</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums1 = [1,2,3,0,0,0], m = 3, nums2 = [2,5,6], n = 3
<strong>Output:</strong> [1,2,2,3,5,6]
<strong>Explanation:</strong> The arrays we are merging are [1,2,3] and [2,5,6].
The result of the merge is [<u>1</u>,<u>2</u>,2,<u>3</u>,5,6] with the underlined elements coming from nums1.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums1 = [1], m = 1, nums2 = [], n = 0
<strong>Output:</strong> [1]
<strong>Explanation:</strong> The arrays we are merging are [1] and [].
The result of the merge is [1].
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> nums1 = [0], m = 0, nums2 = [1], n = 1
<strong>Output:</strong> [1]
<strong>Explanation:</strong> The arrays we are merging are [] and [1].
The result of the merge is [1].
Note that because m = 0, there are no elements in nums1. The 0 is only there to ensure the merge result can fit in nums1.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>nums1.length == m + n</code></li>
	<li><code>nums2.length == n</code></li>
	<li><code>0 &lt;= m, n &lt;= 200</code></li>
	<li><code>1 &lt;= m + n &lt;= 200</code></li>
	<li><code>-10<sup>9</sup> &lt;= nums1[i], nums2[j] &lt;= 10<sup>9</sup></code></li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up: </strong>Can you come up with an algorithm that runs in <code>O(m + n)</code> time?</p>
</div>

### Solution
<div class="FN9Jv WRmCx"><h4 id="intuition">Intuition</h4>

<p>We are given two sorted arrays nums1 and nums2 of sizes m and n, respectively. We need to merge these two arrays into a single sorted array, and the result should be stored inside nums1. Since nums1 is of size m+n, we can use this extra space to store the merged array. We can iterate through the arrays from the end and place the larger element in the end of nums1.</p>
<hr>
<h4 id="approach--using-stl">Approach : <em><strong>Using STL</strong></em></h4>
<ol>
<li>Traverse through nums2 and append its elements to the end of nums1 starting from index m.</li>
<li>Sort the entire nums1 array using sort() function.</li>
</ol>
<h4 id="complexity">Complexity</h4>
<ul>
<li>Time complexity: O((m+n)log(m+n))</li>
</ul>

<blockquote>
<p><em>due to the sort() function</em></p>
</blockquote>
<ul>
<li>Space complexity: O(1)</li>
</ul>
<blockquote>
<p><em>We are not using any extra space, so the space complexity is O(1).</em></p>
</blockquote>

<h4 id="code">Code</h4>
<div class="border-gray-3 dark:border-dark-gray-3 mb-6 overflow-hidden rounded-lg border"><div class="flex select-none bg-layer-2 dark:bg-dark-layer-2"><div class="relative cursor-pointer px-3 py-3 text-label-1 dark:text-dark-label-1 font-medium EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div></div><div class="px-3 py-2.5 bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: black; font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent; overflow-wrap: normal;"><code class="language-cpp" style="text-shadow: none; white-space: pre;"><span><span class="token" style="color: rgb(0, 119, 170);">class</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">Solution</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(0, 119, 170);">public</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(0, 119, 170);">void</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">merge</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&amp;</span><span> nums1</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> m</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&amp;</span><span> nums2</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> n</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">for</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> j </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">0</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> i </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> m</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span> j</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span>n</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span> j</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">++</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>            nums1</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>i</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> nums2</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>j</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>            i</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">++</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(221, 74, 104);">sort</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>nums1</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">begin</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span>nums1</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">end</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(153, 153, 153);">}</span><span class="token" style="color: rgb(153, 153, 153);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>
<hr>
<h4 id="approach--two-pointer">Approach : <em><strong>Two Pointer</strong></em></h4>

<p>We can start with two pointers i and j, initialized to m-1 and n-1, respectively. We will also have another pointer k initialized to m+n-1, which will be used to keep track of the position in nums1 where we will be placing the larger element. Then we can start iterating from the end of the arrays i and j, and compare the elements at these positions. We will place the larger element in nums1 at position k, and decrement the corresponding pointer i or j accordingly. We will continue doing this until we have iterated through all the elements in nums2. If there are still elements left in nums1, we don't need to do anything because they are already in their correct place.</p>
<h4 id="complexity-1">Complexity</h4>
<ul>
<li>Time complexity: O(m+n)</li>
</ul>

<blockquote>
<p><em>We are iterating through both arrays once, so the time complexity is O(m+n).</em></p>
</blockquote>
<ul>
<li>Space complexity: O(1)</li>
</ul>
<blockquote>
<p><em>We are not using any extra space, so the space complexity is O(1).</em></p>
</blockquote>

<h4 id="code-1">Code</h4>
<div class="border-gray-3 dark:border-dark-gray-3 mb-6 overflow-hidden rounded-lg border"><div class="flex select-none bg-layer-2 dark:bg-dark-layer-2"><div class="relative cursor-pointer px-3 py-3 text-label-1 dark:text-dark-label-1 font-medium EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div></div><div class="px-3 py-2.5 bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: black; font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent; overflow-wrap: normal;"><code class="language-cpp" style="text-shadow: none; white-space: pre;"><span><span class="token" style="color: rgb(0, 119, 170);">class</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">Solution</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(0, 119, 170);">public</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(0, 119, 170);">void</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">merge</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&amp;</span><span> nums1</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> m</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&amp;</span><span> nums2</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> n</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> i </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> m </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">-</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> j </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> n </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">-</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> k </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> m </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">+</span><span> n </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">-</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">while</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>j </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;=</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">0</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(0, 119, 170);">if</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>i </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;=</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">0</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&amp;&amp;</span><span> nums1</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>i</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;</span><span> nums2</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>j</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>                nums1</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>k</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">--</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> nums1</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>i</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">--</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span> </span><span class="token" style="color: rgb(0, 119, 170);">else</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>                nums1</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>k</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">--</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> nums2</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>j</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">--</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(153, 153, 153);">}</span><span class="token" style="color: rgb(153, 153, 153);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## Go To
[Table of Content](#table-of-content)


## Arrays - II Find the duplicate in an array of N+1 integers
<div class="elfjS" data-track-load="description_content"><p>Given an array of integers <code>nums</code> containing&nbsp;<code>n + 1</code> integers where each integer is in the range <code>[1, n]</code> inclusive.</p>

<p>There is only <strong>one repeated number</strong> in <code>nums</code>, return <em>this&nbsp;repeated&nbsp;number</em>.</p>

<p>You must solve the problem <strong>without</strong> modifying the array <code>nums</code>&nbsp;and uses only constant extra space.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,3,4,2,2]
<strong>Output:</strong> 2
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [3,1,3,4,2]
<strong>Output:</strong> 3
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 10<sup>5</sup></code></li>
	<li><code>nums.length == n + 1</code></li>
	<li><code>1 &lt;= nums[i] &lt;= n</code></li>
	<li>All the integers in <code>nums</code> appear only <strong>once</strong> except for <strong>precisely one integer</strong> which appears <strong>two or more</strong> times.</li>
</ul>

<p>&nbsp;</p>
<p><b>Follow up:</b></p>

<ul>
	<li>How can we prove that at least one duplicate number must exist in <code>nums</code>?</li>
	<li>Can you solve the problem in linear runtime complexity?</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><h4 id="problem-understanding">Problem Understanding</h4>
<p>Given an array of N + 1 integers where each element is between 1 and N, the task is to find the duplicate number efficiently.</p>
<h4 id="approach">Approach</h4>
<hr>
<p><strong>I have explored three different approaches to solve this problem, and I am gradually transitioning from a brute-force approach to more optimized ones.</strong></p>
<hr>
<h4 id="solution-1-using-sorting">Solution 1: Using Sorting</h4>
<p><strong>Approach:</strong></p>
<ol>
<li><strong>Sort</strong> the given array in ascending order.</li>
<li><strong>Iterate</strong> through the sorted array.</li>
<li><strong>Check if arr[i] is equal to arr[i+1].</strong> If true, arr[i] is the duplicate number.</li>
</ol>
<p><strong>Intuition:</strong><br>
The <strong>idea</strong> behind this approach is that <strong>if there is a duplicate number in the array, it will be adjacent to another identical number</strong> after sorting. Sorting the array allows us to find duplicates efficiently by comparing adjacent elements.</p>

 <h4 id="code-using-sorting-method">Code Using Sorting Method</h4>
<div class="border-gray-3 dark:border-dark-gray-3 mb-6 overflow-hidden rounded-lg border"><div class="flex select-none bg-layer-2 dark:bg-dark-layer-2"><div class="relative cursor-pointer px-3 py-3 text-label-1 dark:text-dark-label-1 font-medium EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div></div><div class="px-3 py-2.5 bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: black; font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent; overflow-wrap: normal;"><code class="language-cpp" style="text-shadow: none; white-space: pre;"><span><span class="token" style="color: rgb(0, 119, 170);">class</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">Solution</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(0, 119, 170);">public</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">findDuplicate</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&amp;</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(221, 74, 104);">sort</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>nums</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">begin</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">end</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span>
</span><span><span>        </span><span class="token" style="color: slategray;">// Iterate through the sorted array</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">for</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> i </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span> i </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">size</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span> i</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">++</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: slategray;">// Check if adjacent elements are equal</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(0, 119, 170);">if</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>nums</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>i</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">==</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>i </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">-</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(0, 119, 170);">return</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>i</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span> </span><span class="token" style="color: slategray;">// Found the duplicate number</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span>
</span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">return</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">-</span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span> </span><span class="token" style="color: slategray;">// No duplicate found (shouldn't happen for this problem)</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(153, 153, 153);">}</span><span class="token" style="color: rgb(153, 153, 153);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>
<h4 id="solution-2-using-frequency-array">Solution 2: Using Frequency Array</h4>
<p><strong>Approach:</strong></p>
<ol>
<li><strong>Create a frequency array</strong> of size N+1 and initialize it to all zeros.</li>
<li><strong>Traverse</strong> through the given array.</li>
<li><strong>For each element arr[i], increment</strong> the corresponding index in the frequency array by 1.</li>
<li><strong>If you encounter an element with a frequency greater than 1, that element is the duplicate number.</strong></li>
</ol>
<p><strong>Intuition:</strong><br>
<strong>This approach maintains a count of how many times each element appears in the array using a separate data structure</strong> (the frequency array). When we encounter an element with a frequency greater than 1, we have found the duplicate element.</p>
<h4 id="code-using-map-method">Code Using Using Frequency Array</h4>
<div class="border-gray-3 dark:border-dark-gray-3 mb-6 overflow-hidden rounded-lg border"><div class="flex select-none bg-layer-2 dark:bg-dark-layer-2"><div class="relative cursor-pointer px-3 py-3 text-label-1 dark:text-dark-label-1 font-medium EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div></div><div class="px-3 py-2.5 bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: black; font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent; overflow-wrap: normal;"><code class="language-cpp" style="text-shadow: none; white-space: pre;"><span><span class="token" style="color: rgb(0, 119, 170);">class</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">Solution</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(0, 119, 170);">public</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">findDuplicate</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&amp;</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>        unordered_map</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;</span><span> numCount</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span> </span><span class="token" style="color: slategray;">// Map to store the count of each number</span><span>
</span></span><span>
</span><span><span>    </span><span class="token" style="color: slategray;">// Iterate through the array and count the occurrences of each number</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">for</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> num </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">:</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(0, 119, 170);">if</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>numCount</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">find</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>num</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">!=</span><span> numCount</span><span class="token" style="color: rgb(153, 153, 153);">.</span><span class="token" style="color: rgb(221, 74, 104);">end</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(0, 119, 170);">return</span><span> num</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span> </span><span class="token" style="color: slategray;">// Found the duplicate number</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span>            numCount</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>num</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span>
</span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">return</span><span> </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">-</span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span> </span><span class="token" style="color: slategray;">// No duplicate found (shouldn't happen for this problem)  </span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(153, 153, 153);">}</span><span class="token" style="color: rgb(153, 153, 153);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

<h4 id="solution-3-linked-list-cycle-method">Solution 3: Linked List Cycle method</h4>
<p><strong>Step 1 (Phase 1 - Detect the Cycle):</strong></p>

<ul>
<li><strong>Initialize two pointers, slow and fast</strong>, both initially pointing to the first element in the array.</li>
<li><strong>Use a loop to move slow one step at a time and fast two steps at a time.</strong></li>
<li><strong>Continue</strong> this loop until slow and fast meet inside the cycle (i.e., slow == fast).</li>
</ul>
<p><strong>Step 2 (Phase 2 - Find the Entrance to the Cycle):</strong></p>
<ul>
<li><strong>After detecting the cycle,</strong> reset one of the pointers (in this case, we reset fast) to the beginning of the array (i.e., fast = nums[0]).</li>
<li><strong>Now, move both slow and fast one step at a time until they meet again.</strong></li>
<li>The point <strong>where slow and fast meet</strong> for the second time is the entrance to the cycle.</li>
</ul>
<p><strong>Step 3 (Return the Duplicate Number):</strong></p>
<ul>
<li>Return either slow or fast because they both point to the entrance of the cycle, which corresponds to the duplicate number in the array.</li>
</ul>
<h4 id="lets-dry-run-">Let's Dry run-</h4>
<p><strong>Step 1</strong>: Consider the following array where each element's value indicates the next index to jump to.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: black; font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent; overflow-wrap: normal;"><code class="language-csharp" style="text-shadow: none; white-space: pre;"><span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">3</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span class="token" style="color: rgb(153, 0, 85);">3</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span class="token" style="color: rgb(153, 0, 85);">4</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span class="token" style="color: rgb(153, 0, 85);">2</span><span class="token" style="color: rgb(153, 153, 153);">]</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p><strong>Step 2:</strong> Initialize two pointers, slow and fast, both initially at the first element (index 0).</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: black; font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent; overflow-wrap: normal;"><code class="language-csharp" style="text-shadow: none; white-space: pre;"><span><span>slow
</span></span><span>↓
</span><span><span></span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">3</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">3</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">4</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">2</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span>
</span></span><span>↑
</span><span>fast</span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p><strong>Step 3:</strong> Move the pointers. slow moves one step at a time, and fast moves two steps at a time.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: black; font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent; overflow-wrap: normal;"><code class="language-csharp" style="text-shadow: none; white-space: pre;"><span><span>   slow
</span></span><span>    ↓
</span><span><span></span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">3</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">3</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">4</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">2</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span>
</span></span><span>       ↑
</span><span>      fast</span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p><strong>Step 4</strong>: Continue moving the pointers.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: black; font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent; overflow-wrap: normal;"><code class="language-csharp" style="text-shadow: none; white-space: pre;"><span><span>      slow
</span></span><span>       ↓
</span><span><span></span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">3</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">3</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">4</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">2</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span>
</span></span><span>             ↑
</span><span>            fast</span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p><strong>Step 5:</strong> Continue moving the pointers one step at a time until they meet again. This meeting point will be the entrance to the cycle.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: black; font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent; overflow-wrap: normal;"><code class="language-csharp" style="text-shadow: none; white-space: pre;"><span><span>      slow
</span></span><span>       ↓
</span><span><span></span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">3</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">1</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">3</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">4</span><span class="token" style="color: rgb(153, 153, 153);">,</span><span> </span><span class="token" style="color: rgb(153, 0, 85);">2</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span>
</span></span><span>       ↑
</span><span>      fast</span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p><strong>Step 6:</strong> Now Point out to slow at Start, then iterate it one step again. Until it does not meet up with fast. When they meet that's our duplicate Number.</p>
<hr>
<h4 id="time-complexity">Time Complexity</h4>
<ul>
<li>Sorting-O(nlogn)</li>
<li>Map-O(n)</li>
<li>Linked List cycle-O(n)</li>
</ul>
<h4 id="space-complexity">Space Complexity</h4>
<ul>
<li>Sorting-O(1)</li>
<li>Map-O(n)</li>
<li>Linked List cycle-O(1)</li>
</ul>

<h4 id="code-using-linked-list-cycle-method">Code Using Linked-List cycle Method</h4>
<div class="border-gray-3 dark:border-dark-gray-3 mb-6 overflow-hidden rounded-lg border"><div class="flex select-none bg-layer-2 dark:bg-dark-layer-2"><div class="relative cursor-pointer px-3 py-3 text-label-1 dark:text-dark-label-1 font-medium EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div></div><div class="px-3 py-2.5 bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: black; font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent; overflow-wrap: normal;"><code class="language-cpp" style="text-shadow: none; white-space: pre;"><span><span class="token" style="color: rgb(0, 119, 170);">class</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">Solution</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(0, 119, 170);">public</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> </span><span class="token" style="color: rgb(221, 74, 104);">findDuplicate</span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>vector</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&lt;</span><span class="token" style="color: rgb(0, 119, 170);">int</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&gt;</span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">&amp;</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> slow </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">0</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">int</span><span> fast </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">0</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span>
</span><span><span>        </span><span class="token" style="color: slategray;">// Phase 1: Detect the cycle</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">do</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>            slow </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>slow</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>            fast </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>nums</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>fast</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span> </span><span class="token" style="color: rgb(0, 119, 170);">while</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>slow </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">!=</span><span> fast</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span>
</span><span><span>        </span><span class="token" style="color: slategray;">// Phase 2: Find the entrance to the cycle</span><span>
</span></span><span><span>        slow </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span class="token" style="color: rgb(153, 0, 85);">0</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">while</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">(</span><span>slow </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">!=</span><span> fast</span><span class="token" style="color: rgb(153, 153, 153);">)</span><span> </span><span class="token" style="color: rgb(153, 153, 153);">{</span><span>
</span></span><span><span>            slow </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>slow</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>            fast </span><span class="token" style="color: rgb(154, 110, 58); background: rgba(255, 255, 255, 0.5);">=</span><span> nums</span><span class="token" style="color: rgb(153, 153, 153);">[</span><span>fast</span><span class="token" style="color: rgb(153, 153, 153);">]</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span>
</span><span><span>        </span><span class="token" style="color: rgb(0, 119, 170);">return</span><span> slow</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span> </span><span class="token" style="color: slategray;">// or fast, as they both point to the entrance of the cycle</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(153, 153, 153);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(153, 153, 153);">}</span><span class="token" style="color: rgb(153, 153, 153);">;</span><span>
</span></span><span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>
</div>


## Go To
[Table of Content](#table-of-content)


## Arrays - II Find the repeating and missing numbers
<div _ngcontent-serverapp-c178="" disableselect="" class="description pt-8 prevent-select ng-star-inserted"><h4 id="you-are-given-an-array-of-size-n-the-elements-of-the-array-are-in-the-range-from-1-to-n">You are given an array of size ‘N’. The elements of the array are in the range from 1 to ‘N’.</h4>

<h4 id="ideally-the-array-should-contain-elements-from-1-to-n-but-due-to-some-miscalculations-there-is-a-number-r-in-the-range-1-n-which-appears-in-the-array-twice-and-another-number-m-in-the-range-1-n-which-is-missing-from-the-array">Ideally, the array should contain elements from 1 to ‘N’. But due to some miscalculations, there is a number R in the range [1, N] which appears in the array twice and another number M in the range [1, N] which is missing from the array.</h4>

<h4 id="your-task-is-to-find-the-missing-number-m-and-the-repeating-number-r">Your task is to find the missing number (M) and the repeating number (R).</h4>
<pre class="wp-block-preformatted"><code><strong>Example 1:</strong>
<strong>Input Format</strong>:&nbsp; array[] = {3,1,2,5,3}
<strong>Result</strong>: {3,4)
<strong>Explanation</strong>: A = 3 , B = 4&nbsp;
Since 3 is appearing twice and 4 is missing

<strong>Example 2:</strong>
<strong>Input Format</strong>: array[] = {3,1,2,5,4,6,7,5}
<strong>Result</strong>: {5,8)
<strong>Explanation</strong>: A = 5 , B = 8&nbsp;
Since 5 is appearing twice and 8 is missing
</code></pre>


<h5 id="follow-up">Follow Up</h5>

<pre><code>Can you do this in linear time and constant additional space? 
</code></pre>

</div>

### Solution
#### Approach
<!-- Describe your approach to solving the problem. -->
<div _ngcontent-serverapp-c203="" class="content-desc"><p>The approach is to store the frequency of each array element in a 1-D array. Then we can look for the number (index) in the array. The number whose count is 2 is the number that is repeated twice, and the number which is appearing 0 times is the missing number.</p><p>&nbsp;</p><p><strong>The steps are as follows:-</strong></p><p>&nbsp;</p><p><strong>//</strong> Function to find the Missing And Repeating Numbers</p><p><strong>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;function </strong>findMissingRepeatingNumbers<strong>(int[] A, int N):</strong><br>&nbsp;</p><ol><li>Int 'N' be the size of array ‘A’.</li><li>Initialize a 1-D array ‘count’ of size ‘N + 1’, where each index stores the frequency of that number in the array ‘A’.</li><li>Iterate over array ‘A’ from index ‘0’ to index ‘N - 1’ using variable ‘i’:<ul><li>Increment count[A[i]].</li></ul></li><li>Initialize two variables ‘missing’ &amp; ‘repeating’, storing the missing integer and repeating integer, respectively.</li><li>Iterate over array ‘count’ from index ‘1’ to index ‘N’ using variable ‘i’:<ul><li>If count[i] == 2:<ul><li>Assign ‘repeating’ to ‘i’</li></ul></li><li>If count[i] == 0:<ul><li>Assign ‘missing’ to ‘i’</li></ul></li></ul></li><li>Return pair(‘repeating’, ‘missing’)</li></ol></div>

#### Complexity
- Time complexity:
<!-- Add your time complexity here, e.g. $$O(n)$$ -->
            O( N )
- Space complexity:
<!-- Add your space complexity here, e.g. $$O(n)$$ -->
            O( N )

#### Code
```
vector<int> findMissingRepeatingNumbers(vector < int > a) {
    int n = a.size(); // Size of array 'a'
    
    vector<int> count(n + 1, 0); // 'count' array
    for(int i = 0; i < n; ++i) {
        // Incrementing the frequency of current element
        ++count[a[i]];
    }
    int missing, repeating;
    for(int i = 1; i <= n; ++i) {
        if(count[i] == 0) missing = i;
        else if(count[i] == 2) repeating = i;
    }
    vector<int> ans;
    ans.push_back(repeating);
    ans.push_back(missing);
    return ans;
}
```
## Go To
[Table of Content](#table-of-content)


## Arrays - II Global and Local Inversions
<div class="elfjS" data-track-load="description_content"><p>You are given an integer array <code>nums</code> of length <code>n</code> which represents a permutation of all the integers in the range <code>[0, n - 1]</code>.</p>

<p>The number of <strong>global inversions</strong> is the number of the different pairs <code>(i, j)</code> where:</p>

<ul>
	<li><code>0 &lt;= i &lt; j &lt; n</code></li>
	<li><code>nums[i] &gt; nums[j]</code></li>
</ul>

<p>The number of <strong>local inversions</strong> is the number of indices <code>i</code> where:</p>

<ul>
	<li><code>0 &lt;= i &lt; n - 1</code></li>
	<li><code>nums[i] &gt; nums[i + 1]</code></li>
</ul>

<p>Return <code>true</code> <em>if the number of <strong>global inversions</strong> is equal to the number of <strong>local inversions</strong></em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,0,2]
<strong>Output:</strong> true
<strong>Explanation:</strong> There is 1 global inversion and 1 local inversion.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [1,2,0]
<strong>Output:</strong> false
<strong>Explanation:</strong> There are 2 global inversions and 1 local inversion.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>n == nums.length</code></li>
	<li><code>1 &lt;= n &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt; n</code></li>
	<li>All the integers of <code>nums</code> are <strong>unique</strong>.</li>
	<li><code>nums</code> is a permutation of all the numbers in the range <code>[0, n - 1]</code>.</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><h4 id="intuition">Intuition</h4>

<p>We have solve this question using Two Approaches.</p>
<ol>
<li>Solved Using Array(Two Nested Loop). Brute Force Approach.</li>
<li>Solved using Array + Divide and Conquer + Merge Sort. Optimized Approach.</li>
</ol>
<h4 id="approach">Approach</h4>

<p>We can easily understand the All the approaches by seeing the code which is easy to understand with comments.</p>
<h4 id="complexity">Complexity</h4>
<ul>
<li>Time complexity:</li>
</ul>

<p>Time complexity is given in code comment.</p>
<ul>
<li>Space complexity:</li>
</ul>

<p>Space complexity is given in code comment.</p>
<h4 id="code">Code</h4>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(106, 153, 85);">/*
</span></span><span>
</span><span>    Time Complexity : O(N^2), where N is the size of the array. As we check for possible pair which can satisfy
</span><span>    the given condition, and the total number of pairs are : N*(N–1)/2.
</span><span>
</span><span>    Space complexity : O(1), Constant space.
</span><span>
</span><span>    Solved Using Array(Two Nested Loop). Brute Force Approach.
</span><span>
</span><span>    Note : This approach is Giving TLE.
</span><span>
</span><span><span class="token" style="color: rgb(106, 153, 85);">*/</span><span>
</span></span><span>
</span><span>
</span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">/***************************************** Approach 1 *****************************************/</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">reversePairs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> n </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">long</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">long</span><span> reversePairsCount </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">long</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">long</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    reversePairsCount</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> reversePairsCount</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span>
</span><span>
</span><span>
</span><span>
</span><span>
</span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">/*
</span></span><span>
</span><span>    Time Complexity : O(NlogN), Each recursive call to performs two recursive calls on subslices of size N/2 and
</span><span>    One linear scans of length &lt;= N. Therefore, the time complexity of the divide &amp; conquer approach can be
</span><span>    represented by the following recurrence relation: T(N)=2T(N/2)+N. Where N is the size of the Array(nums).
</span><span>
</span><span>    Space Complexity : O(N), Recursion Stack Space O(logN) + Array(temp) space O(N). 
</span><span>
</span><span>    Solved using Array + Divide and Conquer + Merge Sort. Optimized Approach.
</span><span>
</span><span><span class="token" style="color: rgb(106, 153, 85);">*/</span><span>
</span></span><span>
</span><span>
</span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">/***************************************** Approach 2 *****************************************/</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> 
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">merge</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> low</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> mid</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> high</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> reversePairsCount</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> mid</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>low</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span>mid</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span>high </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">long</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">long</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                j</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            reversePairsCount </span><span class="token" style="color: rgb(212, 212, 212);">+=</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>mid</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> size </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> high</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span>low</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">temp</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>size</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> left </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> low</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> right </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> mid</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> k</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span>mid </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> right</span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span>high</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                temp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>k</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                temp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>k</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span>mid</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            temp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>k</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span>high</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            temp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>k</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> m</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>low</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span>high</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> temp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>m</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">mergeSort</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> low</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> high</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> reversePairsCount</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>low </span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span> high</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> mid </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>low </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> high</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">mergeSort</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>nums</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> low</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> mid</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> reversePairsCount</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">mergeSort</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>nums</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> mid</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> high</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> reversePairsCount</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">merge</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>nums</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> low</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> mid</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> high</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> reversePairsCount</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">reversePairs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> reversePairsCount </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">mergeSort</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>nums</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> reversePairsCount</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> reversePairsCount</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
</div>
