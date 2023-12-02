## Table of Content
1. [Nth Root of a Number using Binary Search](#binary-search---nth-root-of-a-number-using-binary-search)
2. [Median of Row-Wise Sorted Matrix](#binary-search---median-of-row-wise-sorted-matrix)
3. [Single Element in a Sorted Array](#binary-search---single-element-in-a-sorted-array)
4. [Search in Rotated Sorted Array](#binary-search---search-in-rotated-sorted-array)
5. [Median of Two Sorted Arrays](#binary-search---median-of-two-sorted-arrays)
6. [K-th Element of Two Arrays](#binary-search---k-th-element-of-two-arrays)
7. [Allocate Minimum Number of Pages](#binary-search---allocate-minimum-number-of-pages)
8. [Aggressive Cows](#binary-search---aggressive-cows)

## Binary Search - Nth Root of a Number using Binary Search
<p><strong>Problem Statement:</strong> Given two numbers N and M, find the Nth root of M. The nth root of a number M is defined as a number X when raised to the power N equals M. If the ‘nth root is not an integer, return -1.</p>

### Solution
<p><strong>Problem Statement:</strong> Given two numbers N and M, find the Nth root of M. The nth root of a number M is defined as a number X when raised to the power N equals M. If the ‘nth root is not an integer, return -1.</p>
<p>We are going to use the Binary Search algorithm to optimize the approach.</p>
<p><em>The primary objective of the Binary Search algorithm is to efficiently determine the appropriate half to eliminate, thereby reducing the search space by half. It does this by determining a specific condition that ensures that the target is not present in that half.</em></p>
<p>Now, we are not given any sorted array on which we can apply binary search. But, if we observe closely, we can notice that our answer space i.e. [1, n] is sorted. So, we will apply binary search on the answer space.</p>
<p><strong>Edge case: How to eliminate the halves:</strong></p>
<p>Our first approach should be the following:</p>
<ul><li>After placing low at 1 and high m, we will calculate the value of ‘mid’.</li><li>Now, based on the value of ‘mid’ raised to the power n, we will check if ‘mid’ can be our answer, and based on this value we will also eliminate the halves. If the value is smaller than m, we will eliminate the left half and if greater we will eliminate the right half.</li></ul>
<p>But, if the given numbers m and n are big enough, we cannot store the value mid<sup>n</sup> in a variable. So to resolve this problem, we will implement a function like the following:</p>
<p><strong>func(n, m, mid):</strong></p>
<ul><li>We will first declare a variable ‘ans’ to store the value mid<sup>n</sup>.</li><li>Now, we will run a loop for n times to multiply the ‘mid’ n times with ‘ans’.&nbsp;</li><li>Inside the loop, <strong>if at any point ‘ans’ becomes greater than m, we will return 2</strong>.</li><li>Once the loop is completed, if the ‘ans’ is equ<strong>al to m, we will return 1</strong>.</li><li><strong>If the value is smaller, we will return 0</strong>.</li></ul>
<p>Now, based on the output of the above function, we will check if ‘mid’ is our possible answer or we will eliminate the halves. Thus we can avoid the integer overflow case.</p>
<p><strong>Algorithm:</strong></p>
<ol><li><strong>Place the 2 pointers i.e. low and high: </strong>Initially, we will place the pointers. The pointer low will point to 1 and the high will point to m.<br></li><li><strong>Calculate the ‘mid’: </strong>Now, inside a loop, we will calculate the value of ‘mid’ using the following formula:<br><strong>mid = (low+high) // 2 ( ‘//’ refers to integer division)<br></strong></li><li><strong>Eliminate the halves accordingly:&nbsp;</strong><ol><li><strong>If func(n, m, mid) == 1: </strong>On satisfying this condition, we can conclude that the number ‘mid’ is our answer. So, we will return to ‘mid’.</li><li><strong>If func(n, m, mid) == 0: </strong>On satisfying this condition, we can conclude that the number ‘mid’ is smaller than our answer. So, we will eliminate the left half and consider the right half(i.e. low = mid+1).</li><li><strong>If func(n, m, mid) == 2: </strong>the value mid is larger than the number we want. This means the numbers greater than ‘mid’ will not be our answers and the right half of ‘mid’ consists of such numbers. So, we will eliminate the right half and consider the left half(i.e. high = mid-1).</li></ol></li><li>Finally,&nbsp; if we are outside the loop, this means no answer exists. So, we will return -1.</li></ol>
<p>The steps from 2-3 will be inside a loop and the loop will continue until low crosses high.</p>

<p>Code:</p>

```



#include <bits/stdc++.h>
using namespace std;

//return 1, if == m:
//return 0, if < m:
//return 2, if > m:
int func(int mid, int n, int m) {
    long long ans = 1;
    for (int i = 1; i <= n; i++) {
        ans = ans * mid;
        if (ans > m) return 2;
    }
    if (ans == m) return 1;
    return 0;
}

int NthRoot(int n, int m) {
    //Use Binary search on the answer space:
    int low = 1, high = m;
    while (low <= high) {
        int mid = (low + high) / 2;
        int midN = func(mid, n, m);
        if (midN == 1) {
            return mid;
        }
        else if (midN == 0) low = mid + 1;
        else high = mid - 1;
    }
    return -1;
}

int main()
{
    int n = 3, m = 27;
    int ans = NthRoot(n, m);
    cout << "The answer is: " << ans << "\n";
    return 0;
}
```
<details class="secondary-details" open="">
<summary class="secondary-summary">
<span>
Complexity Analysis
</span>
<svg class="arrow-svg opacity-75" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 20 20">
<path d="M12.95 10.707l.707-.707L8 4.343 6.586 5.757 10.828 10l-4.242 4.243L8 15.657l4.95-4.95z">
</path>
</svg>
</summary>
<p>

</p><p><strong>Time Complexity: </strong>O(logN), N = size of the given array.<strong><br>Reason: </strong>We are basically using binary search to find the minimum.</p>
<p><strong>Space Complexity: </strong>O(1)<strong><br>Reason: </strong>We have not used any extra data structures, this makes space complexity, even in the worst case as O(1).</p>
<p></p>
</details>

## Go To
[Table of Content](#table-of-content)

## Binary Search - Median of Row Wise Sorted Matrix
<div class="entry-content clearfix">
<p><strong>Problem Statement:</strong> Given a row-wise sorted matrix of size r*c, where r is no. of rows and c is no. of columns, find the median in the given matrix.</p>
<p><strong>Assume </strong>– r*c is odd</p>
<p><strong>Examples:</strong></p>
<pre class="wp-block-preformatted"><strong>Example 1:</strong>
<strong>Input:</strong> 
r = 3 , c = 3
1 4 9 
2 5 6
3 8 7
<strong>Output:</strong> Median = 5
<strong>Explanation:</strong> If we find the linear sorted array, the array becomes 1 2 3 4 5 6 7 8 9
So, median = 5

<strong>Example 2:</strong>
<strong>Input:</strong> 
r = 3 , c = 3
1 3 8
2 3 4
1 2 5
<strong>Output:</strong> Median = 3
<strong>Explanation:</strong> If we find the linear sorted array, the array becomes 1 1 2 2 3 3 4 5 7 8
So, median = 3
</pre>
<h3><strong>Solution</strong></h3>

<p><strong>Step 1: </strong>Find the minimum and maximum element in the given array. By just traversing the first column, we find the minimum element and by just traversing the last column, we find the maximum element.</p>
<p><strong>Step 2: </strong>Now find the middle element of the array one by one and check in the matrix how many elements are present in the matrix.</p>
<p><strong>Three cases can occur:-</strong></p>
<ul><li>If count ==&nbsp; (r*c+1)/2 , so it may be the answer still we mark max as mid since we are not referring indices , we are referring the elements and 5 elements can be smaller than 6 also and 7 also , so to confirm we mark max as mid.</li><li>If count&lt;(r*c+1)/2 , we mark&nbsp; min as mid+1 since curr element or elements before it cannot be the answer.</li><li>If count&gt;(r*c+1)/2 , we mark max as mid , since elements after this can only be the&nbsp; answer now.</li></ul>
<p>Let’s discuss the approach with an example</p>
<p>For eg, the given array is</p>
<p><img class="lazy-loaded" loading="lazy" width="624" height="349" src="https://lh6.googleusercontent.com/4TXWnuiVcUQEaQUiomnn_gwquL9qfAT4O38Qls6Sdz_ZNnnxt5txhGiiJLsYAL5OR9zAvchqsVwQmkGlLfro3CVDqieinu3VgyFba1tbmzxt9cFUpeky5ufzZ-clfJmGlbkRGkic" data-lazy-type="image" data-src="https://lh6.googleusercontent.com/4TXWnuiVcUQEaQUiomnn_gwquL9qfAT4O38Qls6Sdz_ZNnnxt5txhGiiJLsYAL5OR9zAvchqsVwQmkGlLfro3CVDqieinu3VgyFba1tbmzxt9cFUpeky5ufzZ-clfJmGlbkRGkic"><noscript><img loading="lazy" width="624" height="349" src="https://lh6.googleusercontent.com/4TXWnuiVcUQEaQUiomnn_gwquL9qfAT4O38Qls6Sdz_ZNnnxt5txhGiiJLsYAL5OR9zAvchqsVwQmkGlLfro3CVDqieinu3VgyFba1tbmzxt9cFUpeky5ufzZ-clfJmGlbkRGkic"></noscript></p>
<p><img class="lazy-loaded" loading="lazy" width="624" height="352" src="https://lh5.googleusercontent.com/3Aozu7SCX0Tq2Jf0W8TEGeeQSSX6KeRzGK2AblElAuhYPELxbZmtRQ0EK3H3hIVH_XfXR1Fd4EekyiitASB1g1D5qucGDdaWBDJW2BTmAELKBMqbwtW4i9zCszBynrKE7kpldAtk" data-lazy-type="image" data-src="https://lh5.googleusercontent.com/3Aozu7SCX0Tq2Jf0W8TEGeeQSSX6KeRzGK2AblElAuhYPELxbZmtRQ0EK3H3hIVH_XfXR1Fd4EekyiitASB1g1D5qucGDdaWBDJW2BTmAELKBMqbwtW4i9zCszBynrKE7kpldAtk"><noscript><img loading="lazy" width="624" height="352" src="https://lh5.googleusercontent.com/3Aozu7SCX0Tq2Jf0W8TEGeeQSSX6KeRzGK2AblElAuhYPELxbZmtRQ0EK3H3hIVH_XfXR1Fd4EekyiitASB1g1D5qucGDdaWBDJW2BTmAELKBMqbwtW4i9zCszBynrKE7kpldAtk"></noscript></p>
<p><strong>Code:</strong></p>

```
#include <bits/stdc++.h>
using namespace std;
// Function to find median  of row wise sorted matrix
int Findmedian(int arr[3][3], int row, int col)
{
  int median[row * col];
  int index = 0;
  for (int i = 0; i < row; i++)
  {
    for (int j = 0; j < col; j++)
    {
      median[index] = arr[i][j];
      index++;
    }
  }
 
  return median[(row * col) / 2];
}
int main()
{
  int row = 3, col = 3;
  int arr[3][3] = {{1, 3, 8},
                   {2, 3, 4},
                   {1, 2, 5}};
  cout <<"The median of the row-wise sorted matrix is: "<<Findmedian
  (arr, row, col) << endl;
  return 0;
}
```
<p><strong>Output:</strong> The median of the row-wise sorted matrix is: 3</p>
<p><strong>Time Complexity: </strong>O<strong>(</strong>row*col log(row*col)) for sorting the array where r*c denotes the number of elements in the linear array.</p>
<p><strong>Space Complexity: </strong>O<strong>(</strong>row*col)&nbsp; for storing elements in the linear array</p>


</div>

## Go To
[Table of Content](#table-of-content)


## Binary Search - Single Element in a Sorted Array
<div class="elfjS" data-track-load="description_content"><p>You are given a sorted array consisting of only integers where every element appears exactly twice, except for one element which appears exactly once.</p>

<p>Return <em>the single element that appears only once</em>.</p>

<p>Your solution must run in <code>O(log n)</code> time and <code>O(1)</code> space.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [1,1,2,3,3,4,4,8,8]
<strong>Output:</strong> 2
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [3,3,7,7,10,11,11]
<strong>Output:</strong> 10
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= 10<sup>5</sup></code></li>
</ul>
</div>

### Solution 

```
EXPLANATION:-
Suppose array is [1, 1, 2, 2, 3, 3, 4, 5, 5]
we can observe that for each pair, 
first element takes even position and second element takes odd position
for example, 1 is appeared as a pair,
so it takes 0 and 1 positions. similarly for all the pairs also.

this pattern will be missed when single element is appeared in the array.

From these points, we can implement algorithm.
1. Take left and right pointers . 
    left points to start of list. right points to end of the list.
2. find mid.
    if mid is even, then it's duplicate should be in next index.
	or if mid is odd, then it's duplicate  should be in previous index.
	check these two conditions, 
	if any of the conditions is satisfied,
	then pattern is not missed, 
	so check in next half of the array. i.e, left = mid + 1
	if condition is not satisfied, then the pattern is missed.
	so, single number must be before mid.
	so, update end to mid.
3. At last return the nums[left]

Time: -  O(logN)
space:-  O(1)

IF YOU  HAVE ANY DOUBTS, FEEL FREE TO ASK
IF YOU UNDERSTAND, DON'T FORGET TO UPVOTE.
```

```
Java:-
class Solution {
    public int singleNonDuplicate(int[] nums) {
        int left = 0, right = nums.length-1;
        while(left < right){
            int mid = (left + right)/2;
            if( (mid % 2 == 0 && nums[mid] == nums[mid +1]) || (mid %2 == 1 && nums[mid] == nums[mid - 1]) )
                left = mid + 1;
            else
                right = mid;
        }
        return nums[left];
    }   
}

Python3:-
class Solution:
    def singleNonDuplicate(self, nums: List[int]) -> int:
        left, right = 0, len(nums)-1
        while left < right:
            mid = int((left + right)/2)
            if (mid % 2 == 1 and nums[mid - 1] == nums[mid]) or (mid%2 == 0 and nums[mid] == nums[mid + 1]):
                left = mid + 1
            else:
                right = mid
        return nums[left]
		
C++:-
class Solution {
public:
    int singleNonDuplicate(vector<int>& nums) {
        int left = 0, right = nums.size() - 1;
        while(left < right){
            int mid = (left + right)/2;
            if((mid % 2 == 0 && nums[mid] == nums[mid + 1]) || (mid % 2 == 1 && nums[mid] == nums[mid - 1]))
                left = mid + 1;
            else
                right = mid;
        }
        
        return nums[left];
    }
};
```
## Go To
[Table of Content](#table-of-content)

## Binary Search - Search in Rotated Sorted Array
<div class="elfjS" data-track-load="description_content"><p>There is an integer array <code>nums</code> sorted in ascending order (with <strong>distinct</strong> values).</p>

<p>Prior to being passed to your function, <code>nums</code> is <strong>possibly rotated</strong> at an unknown pivot index <code>k</code> (<code>1 &lt;= k &lt; nums.length</code>) such that the resulting array is <code>[nums[k], nums[k+1], ..., nums[n-1], nums[0], nums[1], ..., nums[k-1]]</code> (<strong>0-indexed</strong>). For example, <code>[0,1,2,4,5,6,7]</code> might be rotated at pivot index <code>3</code> and become <code>[4,5,6,7,0,1,2]</code>.</p>

<p>Given the array <code>nums</code> <strong>after</strong> the possible rotation and an integer <code>target</code>, return <em>the index of </em><code>target</code><em> if it is in </em><code>nums</code><em>, or </em><code>-1</code><em> if it is not in </em><code>nums</code>.</p>

<p>You must write an algorithm with <code>O(log n)</code> runtime complexity.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [4,5,6,7,0,1,2], target = 0
<strong>Output:</strong> 4
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [4,5,6,7,0,1,2], target = 3
<strong>Output:</strong> -1
</pre><p><strong class="example">Example 3:</strong></p>
<pre><strong>Input:</strong> nums = [1], target = 0
<strong>Output:</strong> -1
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 5000</code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li>All values of <code>nums</code> are <strong>unique</strong>.</li>
	<li><code>nums</code> is an ascending array that is possibly rotated.</li>
	<li><code>-10<sup>4</sup> &lt;= target &lt;= 10<sup>4</sup></code></li>
</ul>
</div>

### Solution
<strong>Explanation</strong><br>
Think of the problem in this. We cannot do regular binary search because of the rotation.</p>
<ul>
<li>Example: <code>nums</code>: [12, 13, 14, 15, 16, 17, 0, 1, 2, 3, 4, 5, 6, 7]</li>
<li>Ideally this would have looked as [0, 1, 2, 3, 4, 5, 6, 7, <strong>12</strong>, 13, 14, 15, 16, 17]<br>
But it is rotated at a pivot number: 12. This is <code>nums[0]</code>. Let's call it  pivot number for this explanation.</li>
</ul>
<p>Let's call the left increasing sub sequence as <strong>left half</strong> and right increasing subsequence as <strong>right half</strong>.</p>
<p><strong>HERE'S THE GIST OF THE SOLUTION LOGIC: THE PROBLEM IN NOT BEING ABLE TO DO REGULAR BINARY SEARCH IS: WHEN YOUR MID POINT AND TARGET END UP BEING IN DIFFERENT HALVES (ONE IS IN LEFT AND OTHER IN RIGHT OR VICE VERSA). IF THEY ARE BOTH IN SAME HALF, IT'S JUST LIKE REGULAR BINARY SEARCH BECAUSE YOU WILL CONVERGE TOWARDS THE TARGET ON THAT STEP OF THE BINARY SEARCH. IF YOU ENDED UP IN SEPARATE HALVES, WE CAN CONVERGE TOWARDS THE TARGET BY MAKING IT -INF OR INF LIKE SHOWN BELOW.</strong><br>
Here's the trick:</p>
<ul>
<li>If <code>target</code> is say in the left half, then when searching we need to make the numbers as
<ul>
<li>[12, 13, 14, 15, 16, 17, inf, inf, inf, inf, inf, inf, inf, inf]</li>
</ul>
</li>
<li>if <code>target</code> is in right half then we need to make it as
<ul>
<li>[-inf, -inf, -inf, -inf, -inf, -inf, 0, 1, 2, 3, 4, 5, 6, 7]</li>
</ul>
</li>
</ul>
<p>We don't need to edit the actual array like that, we just need to make the comparator number(in regular case, the mid point that we select) to INF or -INF based on which side the <code>target</code> is and which side the mid point number is.</p>
<p>Okay, but we don't need to always use the comparator as -inf or inf. Think of the case when that is possible?<br>
That's when your <code>target</code> and <code>nums[mid]</code> are on the same half side (left or right half). THis means that your mid point and target are on the same half and you are converging towards the target. So then just keep doing regular binary for that step and let the comparator be <code>nums[mid]</code>.</p>
<ul>
<li>How do we check if they both (<code>nums[mid]</code> and <code>target</code>) are on the same half? We have to check if they are both greater than the pivot number or both smaller than pivot number
<ul>
<li><code>if (((nums[mid] &gt; nums[0]) &amp;&amp; (target &gt; nums[0])) || ((nums[mid] &lt;= nums[0]) &amp;&amp; (target &lt;= nums[0])))</code>.</li>
<li>This can also be done as <code>if ((target &gt; nums[0]) == (nums[mid] &gt; nums[0]))</code>.</li>
<li>Ok, so if they both are on the same half let our comparator be <code>nums[mid]</code>, because we are converging towards the target and are on the same half at the moment of comparision.</li>
<li><code>comparator = nums[mid]</code></li>
<li>proceed with comparing how you do regular binary search comparision.</li>
</ul>
</li>
</ul>
<p>But, what if <code>nums[mid]</code> and <code>target</code> are on different halves? Then we have to not use the <code>nums[mid]</code> as comparator. We have to use -INF or INF. How can we decide whether to make comparator as  -INF or INF instead of <code>nums[mid]</code>?</p>
<ul>
<li>target and <code>nums[mid]</code> are on different halves. we have to change <code>nums[mid]</code> to -INF or INF.</li>
<li>Let's find out which side <code>nums[mid]</code> is. If we know which half (left or right) it is in, we know whether to select -INF or INF.</li>
<li>Compare target to <code>nums[0]</code>. (Why compare <code>target</code> and not <code>nums[mid]</code> because we want to make the numbers on <code>nums[mid]</code> 's side as -INF or INF when comparing, not on <code>target</code>'s side, so we use target as the reference)</li>
<li>if <code>target</code> is greater than <code>nums[0]</code>, target is on the <strong>left half</strong>. Look at the example above and you can see this.
<ul>
<li>For example: <code>target</code> is 14, it is greater than 12 so it belongs in <strong>left half</strong></li>
<li>This means that <code>nums[mid]</code> is on the other half: <strong>right half</strong>. Make comparator as INF.</li>
</ul>
</li>
<li>if <code>target</code> is less than nums[0], target is on the <strong>right half</strong>. Look at the example above:
<ul>
<li>For example if <code>target</code> is 5, it is less than 12 so it belongs in <strong>right half</strong></li>
<li>This means that <code>nums[mid]</code> is on the other half. <strong>left half</strong>. make comparator as -INF.</li>
</ul>
</li>
</ul>
<p>Now you can go ahead and do binary search</p>
<hr>
<p><strong>CODE:</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">search</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> target</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> 
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> l </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> r </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>l </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> r</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> mid </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>r </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> l</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">/</span><span class="token" style="color: rgb(181, 206, 168);">2</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> l</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> comparator </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>mid</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(106, 153, 85);">// Checking if both target and nums[mid] are on same side.</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>target </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>mid</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">||</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>target </span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>mid</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>                    comparator </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>mid</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(106, 153, 85);">// Trying to figure out where nums[mid] is and making comparator as -INF or INF</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>target </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>nums</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>                        comparator </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span>INFINITY</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> 
</span></span><span><span>                        comparator </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> INFINITY</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>target </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> comparator</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> mid</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>target </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> comparator</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>            
</span></span><span><span>                    l </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> mid</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>            
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span>
</span></span><span><span>                    r </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> mid</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## Go To
[Table of Content](#table-of-content)

## Binary Search - Median of Two Sorted Arrays
<div class="elfjS" data-track-load="description_content"><p>Given two sorted arrays <code>nums1</code> and <code>nums2</code> of size <code>m</code> and <code>n</code> respectively, return <strong>the median</strong> of the two sorted arrays.</p>

<p>The overall run time complexity should be <code>O(log (m+n))</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums1 = [1,3], nums2 = [2]
<strong>Output:</strong> 2.00000
<strong>Explanation:</strong> merged array = [1,2,3] and median is 2.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums1 = [1,2], nums2 = [3,4]
<strong>Output:</strong> 2.50000
<strong>Explanation:</strong> merged array = [1,2,3,4] and median is (2 + 3) / 2 = 2.5.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>nums1.length == m</code></li>
	<li><code>nums2.length == n</code></li>
	<li><code>0 &lt;= m &lt;= 1000</code></li>
	<li><code>0 &lt;= n &lt;= 1000</code></li>
	<li><code>1 &lt;= m + n &lt;= 2000</code></li>
	<li><code>-10<sup>6</sup> &lt;= nums1[i], nums2[i] &lt;= 10<sup>6</sup></code></li>
</ul>
</div>

### Solution 
<div class="FN9Jv WRmCx"><p>This problem is notoriously hard to implement due to all the corner cases. Most implementations consider odd-lengthed and even-lengthed arrays as two different cases and treat them separately. As a matter of fact, with a little mind twist. These two cases can be combined as one, leading to a very simple solution where (almost) no special treatment is needed.</p>
<p>First, let's see the concept of 'MEDIAN' in a slightly unconventional way. That is:</p>
<blockquote>
<p>"<strong>if we cut the sorted array to two halves of EQUAL LENGTHS, then<br>
median is the AVERAGE OF Max(lower_half) and Min(upper_half), i.e. the<br>
two numbers immediately next to the cut</strong>".</p>
</blockquote>
<p>For example, for [2 3 5 7], we make the cut between 3 and 5:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-csharp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">2</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">3</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">/</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">5</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">7</span><span class="token" style="color: rgb(212, 212, 212);">]</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>then the median = (3+5)/2. <strong>Note that I'll use '/' to represent a cut, and (number / number) to represent a cut made through a number in this article</strong>.</p>
<p>for [2 3 4 5 6], we make the cut right through 4 like this:</p>
<p>[2 3 (4/4) 5 7]</p>
<p>Since we split 4 into two halves, we say now both the lower and upper subarray contain 4. This notion also leads to the correct answer: (4 + 4) / 2 = 4;</p>
<p>For convenience, let's use L to represent the number immediately left to the cut, and R the right counterpart. In [2 3 5 7], for instance, we have L = 3 and R = 5, respectively.</p>
<p>We observe the index of L and R have the following relationship with the length of the array N:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>N        Index of L / R
</span></span><span>1               0 / 0
</span><span>2               0 / 1
</span><span>3               1 / 1  
</span><span>4               1 / 2      
</span><span>5               2 / 2
</span><span>6               2 / 3
</span><span>7               3 / 3
</span><span>8               3 / 4</span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>It is not hard to conclude that index of L = (N-1)/2, and R is at N/2. Thus, the median can be represented as</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-lisp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token car">L</span><span> + R</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>/2 = </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token car">A</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token car">N-1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>/2</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> + A</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>N/2</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>/2</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<p>To get ready for the two array situation, let's add a few imaginary 'positions' (represented as #'s) in between numbers, and treat numbers as 'positions' as well.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-csharp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">6</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">9</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">13</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">18</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span>  </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>   </span><span class="token" style="color: rgb(212, 212, 212);">[</span><span># </span><span class="token" style="color: rgb(181, 206, 168);">6</span><span> # </span><span class="token" style="color: rgb(181, 206, 168);">9</span><span> # </span><span class="token" style="color: rgb(181, 206, 168);">13</span><span> # </span><span class="token" style="color: rgb(181, 206, 168);">18</span><span> #</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>N </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">4</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>position index     </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">3</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">4</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">5</span><span>  </span><span class="token" style="color: rgb(181, 206, 168);">6</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">7</span><span>  </span><span class="token" style="color: rgb(181, 206, 168);">8</span><span>     </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>N_Position </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">9</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span>		  
</span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">6</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">9</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">11</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">13</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">18</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>   </span><span class="token" style="color: rgb(212, 212, 212);">[</span><span># </span><span class="token" style="color: rgb(181, 206, 168);">6</span><span> # </span><span class="token" style="color: rgb(181, 206, 168);">9</span><span> # </span><span class="token" style="color: rgb(181, 206, 168);">11</span><span> # </span><span class="token" style="color: rgb(181, 206, 168);">13</span><span> # </span><span class="token" style="color: rgb(181, 206, 168);">18</span><span> #</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span>   </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>N </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">5</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>position index      </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">3</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">4</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">5</span><span>  </span><span class="token" style="color: rgb(181, 206, 168);">6</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">7</span><span>  </span><span class="token" style="color: rgb(181, 206, 168);">8</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">9</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">10</span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>N_Position </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">11</span><span class="token" style="color: rgb(212, 212, 212);">)</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>As you can see, there are always exactly 2*N+1 'positions' regardless of length N. Therefore, the middle cut should always be made on the Nth position (0-based). Since index(L) = (N-1)/2 and index(R) = N/2 in this situation, we can infer that <strong>index(L) = (CutPosition-1)/2, index(R) = (CutPosition)/2</strong>.</p>
<hr>
<p>Now for the two-array case:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-python" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>A1</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(106, 153, 85);"># 1 # 2 # 3 # 4 # 5 #]    (N1 = 5, N1_positions = 11)</span><span>
</span></span><span>
</span><span><span>A2</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(106, 153, 85);"># 1 # 1 # 1 # 1 #]     (N2 = 4, N2_positions = 9)</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>Similar to the one-array problem, we need to find a cut that divides the two arrays each into two halves such that</p>
<blockquote>
<p>"any number in the two left halves" &lt;= "any number in the two right<br>
halves".</p>
</blockquote>
<p>We can also make the following observations：</p>
<ol>
<li>
<p>There are 2<em>N1 + 2</em>N2 + 2 position altogether. Therefore, there must be exactly N1 + N2 positions on each side of the cut, and 2 positions directly on the cut.</p>
</li>
<li>
<p>Therefore, when we cut at position C2 = K in A2, then the cut position in A1 must be C1 = N1 + N2 - k. For instance, if C2 = 2, then we must have C1 = 4 + 5 - C2 = 7.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-python" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span> </span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(106, 153, 85);"># 1 # 2 # 3 # (4/4) # 5 #]    </span><span>
</span></span><span>
</span><span><span> </span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(106, 153, 85);"># 1 / 1 # 1 # 1 #]   </span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
</li>
<li>
<p>When the cuts are made, we'd have two L's and two R's. They are</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span> L1 = A1[(C1-1)/2]; R1 = A1[C1/2];
</span></span><span> L2 = A2[(C2-1)/2]; R2 = A2[C2/2];</span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
</li>
</ol>
<p>In the above example,</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>    L1 = A1[(7-1)/2] = A1[3] = 4; R1 = A1[7/2] = A1[3] = 4;
</span></span><span>    L2 = A2[(2-1)/2] = A2[0] = 1; R2 = A1[2/2] = A1[1] = 1;</span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>Now how do we decide if this cut is the cut we want? Because L1, L2 are the greatest numbers on the left halves and R1, R2 are the smallest numbers on the right, we only need</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>L1 &lt;= R1 &amp;&amp; L1 &lt;= R2 &amp;&amp; L2 &lt;= R1 &amp;&amp; L2 &lt;= R2</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>to make sure that any number in lower halves &lt;= any number in upper halves. As a matter of fact, since<br>
L1 &lt;= R1 and L2 &lt;= R2 are naturally guaranteed because A1 and A2 are sorted, we only need to make sure:</p>
<p>L1 &lt;= R2 and L2 &lt;= R1.</p>
<p>Now we can use simple binary search to find out the result.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-sql" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">If</span><span> we have L1 </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> R2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> it means there are too many large numbers </span><span class="token" style="color: rgb(86, 156, 214);">on</span><span> the </span><span class="token" style="color: rgb(86, 156, 214);">left</span><span> half </span><span class="token" style="color: rgb(86, 156, 214);">of</span><span> A1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">then</span><span> we must move C1 </span><span class="token" style="color: rgb(86, 156, 214);">to</span><span> the </span><span class="token" style="color: rgb(86, 156, 214);">left</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>e</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span> move C2 </span><span class="token" style="color: rgb(86, 156, 214);">to</span><span> the </span><span class="token" style="color: rgb(86, 156, 214);">right</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">If</span><span> L2 </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> R1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">then</span><span> there are too many large numbers </span><span class="token" style="color: rgb(86, 156, 214);">on</span><span> the </span><span class="token" style="color: rgb(86, 156, 214);">left</span><span> half </span><span class="token" style="color: rgb(86, 156, 214);">of</span><span> A2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">and</span><span> we must move C2 </span><span class="token" style="color: rgb(86, 156, 214);">to</span><span> the </span><span class="token" style="color: rgb(86, 156, 214);">left</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>
</span></span><span><span>Otherwise</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> this cut </span><span class="token" style="color: rgb(212, 212, 212);">is</span><span> the </span><span class="token" style="color: rgb(86, 156, 214);">right</span><span> one</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span> 
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">After</span><span> we find the cut</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> the medium can be computed </span><span class="token" style="color: rgb(86, 156, 214);">as</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(220, 220, 170);">max</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>L1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> L2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">min</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>R1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> R2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">/</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>Two side notes:</p>
<p>A. Since C1 and C2 can be mutually determined from each other, we can just move one of them first, then calculate the other accordingly. However, it is much more practical to move C2 (the one on the shorter array) first. The reason is that on the shorter array, all positions are possible cut locations for median, but on the longer array, the positions that are too far left or right are simply impossible for a legitimate cut. For instance, [1], [2 3 4 5 6 7 8]. Clearly the cut between 2 and 3 is impossible, because the shorter array does not have that many elements to balance out the [3 4 5 6 7 8] part if you make the cut this way. Therefore, for the longer array to be used as the basis for the first cut, a range check must be performed. It would be just easier to do it on the shorter array, which requires no checks whatsoever. Also, moving only on the shorter array gives a run-time complexity of O(log(min(N1, N2))) (edited as suggested by @baselRus)</p>
<p>B. The only edge case is when a cut falls on the 0th(first) or the 2<em>Nth(last) position. For instance, if C2 = 2</em>N2, then R2 = A2[2*N2/2] = A2[N2], which exceeds the boundary of the array. To solve this problem, we can imagine that both A1 and A2 actually have two extra elements, INT_MAX at A[-1] and INT_MAX at A[N]. These additions don't change the result, but make the implementation easier: If any L falls out of the left boundary of the array, then L = INT_MIN, and if any R falls out of the right boundary, then R = INT_MAX.</p>
<hr>
<p>I know that was not very easy to understand, but all the above reasoning eventually boils down to the following concise code:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span> </span><span class="token" style="color: rgb(86, 156, 214);">double</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">findMedianSortedArrays</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> nums1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> nums2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> N1 </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nums1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> N2 </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> nums2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>N1 </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> N2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">findMedianSortedArrays</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>nums2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> nums1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>	</span><span class="token" style="color: rgb(106, 153, 85);">// Make sure A2 is the shorter one.</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> lo </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> hi </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> N2 </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>lo </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> hi</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> mid2 </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>lo </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> hi</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">/</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>   </span><span class="token" style="color: rgb(106, 153, 85);">// Try Cut 2 </span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> mid1 </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> N1 </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> N2 </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> mid2</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>  </span><span class="token" style="color: rgb(106, 153, 85);">// Calculate Cut 1 accordingly</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">double</span><span> L1 </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>mid1 </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> INT_MIN </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> nums1</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>mid1</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">/</span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>	</span><span class="token" style="color: rgb(106, 153, 85);">// Get L1, R1, L2, R2 respectively</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">double</span><span> L2 </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>mid2 </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> INT_MIN </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> nums2</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>mid2</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">/</span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">double</span><span> R1 </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>mid1 </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> N1 </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> INT_MAX </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> nums1</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>mid1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">/</span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">double</span><span> R2 </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>mid2 </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> N2 </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> INT_MAX </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> nums2</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>mid2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">/</span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>L1 </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> R2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> lo </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> mid2 </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>		</span><span class="token" style="color: rgb(106, 153, 85);">// A1's lower half is too big; need to move C1 left (C2 right)</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>L2 </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> R1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> hi </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> mid2 </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>	</span><span class="token" style="color: rgb(106, 153, 85);">// A2's lower half too big; need to move C2 left.</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(220, 220, 170);">max</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>L1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>L2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">min</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>R1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> R2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">/</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>	</span><span class="token" style="color: rgb(106, 153, 85);">// Otherwise, that's the right cut.</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span> </span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>

## Go To
[Table of Content](#table-of-content)


## Binary Search - K-th element of two Arrays
<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">Given two arrays <strong>arr1</strong> and <strong>arr2</strong> of size <strong>N</strong>&nbsp;and <strong>M</strong>&nbsp;respectively and an element <strong>K</strong>. The task is to find the element that would be at the kth position of the final sorted array.</span><br>&nbsp;</p>
<p><span style="font-size: 18px;"><strong>Example 1:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input:</strong>
arr1[] = {2, 3, 6, 7, 9}
arr2[] = {1, 4, 8, 10}
k = 5
<strong>Output:</strong>
6
<strong>Explanation:</strong>
The final sorted array would be -
1, 2, 3, 4, 6, 7, 8, 9, 10
The 5th element of this array is 6.
</span></pre>
<div><span style="font-size: 18px;"><strong>Example 2:</strong></span></div>
<pre><span style="font-size: 18px;"><strong>Input:</strong>
arr1[] = {100, 112, 256, 349, 770}
arr2[] = {72, 86, 113, 119, 265, 445, 892}
k = 7
<strong>Output:</strong>
256
<strong>Explanation:</strong>
Final sorted array is - 72, 86, 100, 112,
113, 119, 256, 265, 349, 445, 770, 892
7th element of this array is 256.</span></pre>
<p><br><span style="font-size: 18px;"><strong>Your Task:&nbsp;&nbsp;</strong><br>You don't need to read input or print anything. Your task is to complete the function&nbsp;<strong>kthElement()</strong>&nbsp;which takes the arrays <strong>arr1[]</strong>,&nbsp;<strong>arr2[]</strong>, its size <strong>N </strong>and <strong>M </strong>respectively and an integer <strong>K </strong>as inputs and returns the element at the Kth position.</span></p>
<p><br><span style="font-size: 18px;"><strong>Expected Time Complexity:</strong> O(Log(N) + Log(M))<br><strong>Expected Auxiliary Space:</strong> O(Log (N))</span></p>
<p><br><span style="font-size: 18px;"><strong>Constraints:</strong><br>1 &lt;= N, M &lt;= 10<sup>6</sup><br>0 &lt;= arr1<sub>i</sub>, arr2<sub>i</sub> &lt;&nbsp;INT_MAX<br>1 &lt;= K &lt;= N+M</span></p></div>

### Solution
<p>Given two sorted arrays of size m and n respectively, you are tasked with finding the element that would be at the k’th position of the final sorted array.</p>
<p><strong>Examples :</strong></p>
<blockquote><p>Input : Array 1 - 2 3 6 7 9</p><p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Array 2 - 1 4 8 10</p><p>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; k = 5</p><p>Output : 6</p><p>Explanation: The final sorted array would be -</p><p>1, 2, 3, 4, 6, 7, 8, 9, 10</p><p>The 5th element of this array is 6, The 1st element of this array is 1. The thing to notice here is upper_bound(6) gives 5, upper_bound(4) gives 4 that is number of element equal to or less than the number we are giving as input to upper_bound().</p><p>Here is another example</p><p>Input : Array 1 - 100 112 256 349 770</p><p>&nbsp; &nbsp; &nbsp; Array 2 - 72 86 113 119 265 445 892</p><p>&nbsp; &nbsp; &nbsp; k = 7</p><p>Output : 256</p><p>Explanation: Final sorted array is -</p><p>72, 86, 100, 112, 113, 119, 256, 265, 349, 445, 770, 892</p><p>7th element of this array is 256.</p></blockquote>
<p><strong>Observation required :</strong></p>
<p>The simplest method to solve this question is using upper_bound to check what is the position of a element in the sorted array. The upper_bound function return the pointer to element which is greater than the element we searched.</p>
<p>So to find the kth element we need to just find the element whose upper_bound() is 4. So again now we now what upper_bound() gives us we need 1 last observation to solve this question. If we have been given 2 arrays, We just need to the sum of upper_bound for the 2 arrays</p>
<blockquote><p>Input : Array 1 - 2 3 6 7 9</p><p>&nbsp; &nbsp; &nbsp;Array 2 - 1 4 8 10</p><p>&nbsp; &nbsp; &nbsp;k = 5</p><p>Value of upper_bound for value(6) in array1 is 3 and for array 2 is 2. This give us a total of 5. which is the answer.</p></blockquote>
<p><strong>Algorithm :</strong></p>
<ul><li>We take a mid between [L,R] using the formula mid = (L+R)/2.</li><li>Check if the middle can be the kth element using upper_bound() function</li><li>Find the sum of upper_bound() for both the arrays and if the sum is &gt;= K, It's a possible value of kth element.</li><li>If sum is &gt;= K then we assign R = mid - 1.</li><li>else if sum &lt;k then the current mid is too small and we assign L = mid+1.</li><li>Repeat from top</li><li>Return the smallest value found.</li></ul>
<p><strong>Here is the implementation for the optimized method :</strong></p>

```
// C++ program to find the kth element
#include <bits/stdc++.h>
using namespace std;

long long int maxN
    = 1e10; // the maximum value in the array possible.

long long int kthElement(int arr1[], int arr2[], int n,
                         int m, int k)
{
    long long int left = 1,
                  right
                  = maxN; // The range of where ans can lie.
    long long int ans = 1e15; // We have to find min of all
                              // the ans so take .

    // using binary search to check all possible values of
    // kth element
    while (left <= right) {
        long long int mid = (left + right) / 2;
        long long int up_cnt
            = upper_bound(arr1, arr1 + n, mid) - arr1;
        up_cnt += upper_bound(arr2, arr2 + m, mid) - arr2;

        if (up_cnt >= k) {
            ans = min(ans,
                      mid); // find the min of all answers.
            right
                = mid - 1; // Try to find a smaller answer.
        }
        else
            left = mid + 1; // Current mid is too small so
                            // shift right.
    }

    return ans;
}

// Driver code
int main()
{
    // Example 1
    int n = 5, m = 7, k = 7;
    int arr1[n] = { 100, 112, 256, 349, 770 };
    int arr2[m] = { 72, 86, 113, 119, 265, 445, 892 };
    cout << kthElement(arr1, arr2, n, m, k) << endl;
    return 0;
}
```

<div class="code-output ck-widget"><br><strong>Output</strong><pre>256
</pre></div>
<p><strong>Time Complexity :</strong> O( Log( maxN ).log( N+M ) )<br><strong>Auxiliary Space :</strong> O( 1 )</p>

## Go To
[Table of Content](#table-of-content)

## Binary Search - Allocate minimum number of pages
<div class="problems_problem_content__Xm_eO"><p><span style="font-size: 18px;">You have <strong>N</strong> books, each with <strong>A[i]</strong> number of pages. <strong>M</strong> students need to be allocated contiguous books, with each student getting at least one book. <br>Out of all the permutations, the goal is to find the permutation where the student with the most <strong>books </strong>allocated to him gets the minimum number of pages, out of all possible permutations.</span></p>
<p><span style="font-size: 18px;"><strong>Note</strong>: Return <strong>-1</strong> if a valid assignment is not possible, and allotment should be in contiguous order (see the explanation for better understanding).</span></p>
<p>&nbsp;</p>
<p><span style="font-size: 18px;"><strong>Example 1:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input:
</strong>N = 4
A[] = {12,34,67,90}
M = 2
<strong>Output:</strong>113
<strong>Explanation:</strong>Allocation can be done in 
following ways:
{12} and {34, 67, 90} Maximum Pages = 191
{12, 34} and {67, 90} Maximum Pages = 157
{12, 34, 67} and {90} Maximum Pages =113.
Therefore, the minimum of these cases is 113,
which is selected as the output.</span></pre>
<p><br><span style="font-size: 18px;"><strong>Example 2:</strong></span></p>
<pre><span style="font-size: 18px;"><strong>Input:
</strong>N = 3
A[] = {15,17,20}
M = 2
<strong>Output:</strong>32
<strong>Explanation: </strong>Allocation is done as
{15,17} and {20}</span></pre>
<p><span style="font-size: 18px;"><strong>Your Task:</strong><br>You don't need to read input or print anything. Your task is to complete the function findPages() which takes 2 Integers <strong>N</strong>, and m and an array <strong>A[]</strong> of length <strong>N</strong> as input and returns the expected answer.</span></p>
<p><br><span style="font-size: 18px;"><strong>Expected Time Complexity</strong>: O(NlogN)<br><strong>Expected Auxilliary Space:</strong> O(1)</span></p>
<p><br><span style="font-size: 18px;"><strong>Constraints:</strong><br>1 &lt;= N &lt;= 10<sup>5</sup><br>1 &lt;= A [ i ] &lt;= 10<sup>6</sup><br>1 &lt;= M &lt;= 10<sup>5</sup></span></p>
<p>&nbsp;</p></div>

### Solution
<p dir="ltr"><span>The idea is to use </span><b><strong>binary search on answer</strong></b><span>.</span><br><span>There can be 2 cases:</span></p>
<ol><li value="1"><span>When </span><b><strong>no valid answer</strong></b><span> exists:</span><br><span>If the number of students is greater than the number of books (i.e, </span><b><strong>M &gt; N</strong></b><span>), In this case at least 1 student will be left to which no book has been assigned.</span></li><li value="2"><span>When a </span><b><strong>valid answer exists</strong></b><span>.</span><br><span>The </span><b><strong>maximum possible answer</strong></b><span> could be when there is only one student. So, all the book will be assigned to him and the result would be the </span><b><strong>sum of pages of all the books</strong></b><span>.</span><br><span>The </span><b><strong>minimum possible answer</strong></b><span> could be when number of student is equal to the number of book (i.e, M == N) , In this case all the students will get at most one book. So, the result would be the maximum number of pages among them (i.e, </span><b><strong>maximum(pages[])</strong></b><span>).</span><br><span>Hence, we can apply binary search in this given range and each time we can consider the mid value as the maximum limit of pages one can get. And check for the limit if answer is valid then update the limit accordingly.</span></li></ol>
<h3><span>Example:</span></h3>
<blockquote><p dir="ltr"><b><strong>Input: n = 3, arr[] = {3, 2, 4}, m = 2</strong></b><br><span>start=4, end=9, mid=6 &nbsp;-&gt; mid is valid so ans=6 and make end = mid-1 to look for better answer.</span><br><span>start=4, end=5, mid=4 &nbsp;-&gt; mid is not valid so make start = mid+1</span><br><span>start=5, end=5, mid=5 &nbsp;-&gt; mid is valid and we found a better ans as 5.</span><br><span>Search space finished, return 5 as the answer.</span></p></blockquote>
<h3><span>Implementation</span></h3>
<p dir="ltr"><b><strong>Implementation of findPages(int arr[], int n, int m) function:</strong></b></p>
<ul><li value="1"><span>Check if answer exists or not, if m&gt;n then return -1.</span></li><li value="2"><span>Declare a variable sum and store sum of all elements of arr into it.</span></li><li value="3"><span>Initialize the start to maximum(pages[]) or 0, and end to sum of pages[] or some higher limit like 10</span><sup><span>15</span></sup><span> and ans as some non-valid result.</span></li><li value="4"><span>Do while start &lt;= end:&nbsp;</span><ul><li value="1"><span>mid = (start+end)/2.</span></li><li value="2"><span>If mid is valid(To check the validity of mid call the function isPossible) then, update the result (ans=mid) and move the end = mid – 1.</span></li><li value="3"><span>Else move the start = mid + 1.</span></li></ul></li><li value="5"><span>Return ans.</span></li></ul>
<p dir="ltr"><b><strong>Implementation of isPossible(int arr[], int n, int m, long long int curMin)</strong></b><span> to check if curMin will be valid or not:</span><br><span>We need to check if curMin number of pages can assign any student by satisfying the given condition such that all students will get at least one book. Follow the steps to check for validity:</span></p>
<ul><li value="1"><span>Initialise the studentsRequired = 1 and curr_sum = 0 for sum of consecutive pages of book.</span></li><li value="2"><span>Iterate over all books or say pages[] or arr[]</span><ul><li value="1"><span>&nbsp;Add the pages to curr_sum and check curr_sum &gt; curr_min then increment the count of studentRequired by 1.</span></li><li value="2"><span>Check if the studentRequired &gt; m, return false.</span></li></ul></li><li value="3"><span>Return true as studentRequired are less than or equal to m.</span></li></ul>
<h3><span>Code</span></h3>

```
class Solution 
{
    public:
    //Function to check if current minimum value is feasible or not.
    bool isPossible(int arr[], int n, int m, long long int curMin) 
    {
        int studentsRequired = 1;
        int curSum = 0;
        
        //iterating over all the books.
        for (int i = 0; i < n; i++) 
        {
            //if current number of pages are greater than curMin, return false
            if (arr[i] > curMin) 
                return false;
            
            //counting number of students required to distribute curMin pages
            if (curSum + arr[i] > curMin) 
            {
                //incrementing student count and updating curSum.
                studentsRequired++;
                curSum = arr[i];

                //if students required becomes greater than given number 
                //of students, we return false.
                if (studentsRequired > m) return false;
            }
            //else updating curSum
            else 
            {
                curSum += arr[i];
            }
        }
        return true;
    }

    //Function to find minimum number of pages.
    int findPages(int arr[], int n, int m) 
    {
        long long sum = 0;

        //returning -1 if no. of books is less than no. of students.
        if(n < m) return -1;
        
        //counting total number of pages.
        for(int i = 0; i < n; ++i) sum += arr[i];
        
        //initializing start as 0 pages and end as total pages.
        long long start = 0;
        long long end = sum, mid;
        long long int ans = int(1e15);
        
        while(start <= end) 
        {
            mid = (start + end) / 2;
            
            //checking if it is possible to distribute books 
            //by using mid as current minimum.
            if (isPossible(arr, n, m, mid))
            {
                //if yes, then we find the minimum distribution.
                ans = ans<mid? ans:mid;
                
                //as we are finding minimum and books are sorted 
                //so reducing end as end = mid -1. 
                end = mid - 1;
            }
            //if not possible means pages should be increased so
            //updating start = mid + 1.
            else {
                start = mid + 1;
            }
        }
        //returning minimum number of pages.
        return ans;
    }
};
```
<p dir="ltr"><b><strong>Time Complexity: O(n*log (M - max))</strong></b><span>, as isPossible function took O(n) time complexity, and we are applying binary search on search space having (M-max) size. where M is sum(arr[]) and max is max(arr[]).</span><br><b><strong>Auxiliary Space: O(1)</strong></b><span> as we are not using any extra space.</span></p>

## Go To
[Table of Content](#table-of-content)

## Binary Search - Aggressive Cows

<h4>Question</h4>
<p></p><p>Given an array of length ‘N’, where each element denotes the position of a stall. Now you have ‘N’ stalls and an integer ‘K’ which denotes the number of cows that are aggressive. To prevent the cows from hurting each other, you need to assign the cows to the stalls, such that the minimum distance between any two of them is as large as possible. Return the largest minimum distance.<br>
Eg</p><p>
</p><pre><code><span class="hljs-built_in">array</span>: <span class="hljs-number">1</span>,<span class="hljs-number">2</span>,<span class="hljs-number">4</span>,<span class="hljs-number">8</span>,<span class="hljs-number">9</span>  &amp;  k=<span class="hljs-number">3</span>
O/P: <span class="hljs-number">3</span>
Explaination: <span class="hljs-number">1</span>st cow at stall <span class="hljs-number">1</span> , <span class="hljs-number">2</span>nd cow at stall <span class="hljs-number">4</span> <span class="hljs-keyword">and</span> <span class="hljs-number">3</span>rd cow at stall <span class="hljs-number">8</span>
</code></pre>

</p><h3>Logic:</h3>
<ul>
<li>We need to define a isPossible() function that checks if a distance x is possible between each of the cows. We can use a <strong>greedy</strong> approach here by placing cows at the <strong>leftmost</strong> possible stalls such that they are at least x distance away from the last-placed cow.</li>
<li>We need to sort the given array/list so once we have our sorted array  to do the greedy task then we can apply the <strong>Binary</strong> <strong>Search</strong> algorithm on the sorted input, and use our function isPossible( ) to find the largest distance possible.</li>
</ul>
<h3>Steps are as follows :</h3>
<ul>
<li>First of all, consider low and high values for the starting and ending positions of the given array/list or just take low=0 and high = ending position (anything it really does not matter ...you can eve take low=0 and high=100000 any large no ...eventually binary search will eliminate the extra range by removing their left half or right half)</li>
<li>Let mid be the minimum distance. Check in the sorted array how many positions are available so that the minimum distance between them is this mid.</li>
</ul>
<h3>Now how to do that?</h3>
<ol>
<li>Start with the least value in the array and keep ignoring all the elements until you get a difference between the lower element and the current element &gt;= mid or you run out of elements.</li>
<li>Use this idea to find the count of such possible positions. Now if this count is &gt;= c then we already have a possible solution so store it and we now eliminate it from our search space by making low as mid+1, otherwise, we don't store the result as it is not our solution and eliminate it from our search space by making high as mid-1.</li>
</ol>
<ul>
<li>. Now our only objective is to find the maximum from all the results we have stored until our search space has exhausted.</li>
<li></li>
</ul>
<p></p><p><img src="https://assets.leetcode.com/users/images/50352ec0-218a-4e97-b68b-89d6ffa14be1_1624871057.5222998.png" alt="image"></p><p>
</p><h3>Basically :</h3>
<ul>
<li>If you placed all cows with min dist 'mid' this means we can try to further increase this min dist so we do low=mid+1</li>
<li>But if all the cows could not be placed wihtin the 'mid' dist WKT that increasing the dist further would n=be of no use since we could not ensure even the min distance of 'mid' b/w cows ...how can we think of a greater distance than 'mid' ...SO We know for sure that the dist has to be less than mid so we do high=mid-1</li>
</ul>
<h3>Suppose we take 1,2,4,8,9 and cows=3 (given)</h3>
<p></p><p>So initially low=1, high=8 and therefore mid(1+8)/2 = 4<br>
<img src="https://assets.leetcode.com/users/images/7b64fc6d-8303-4697-87ee-af367fef8482_1624869585.3251574.png" alt="image"><br>
We could only place 2 cows not 3 so return false as '4' dist bw cows is not possible it has to be less than that<br>
So we do high=mid-1 = 4-1= 3<br>
so now low=1, high=3 and so mid becomes average of 1 &amp; 3 i.e 2<br>
<img src="https://assets.leetcode.com/users/images/cef5decf-ed9f-4998-ac81-eaf2b9b069ef_1624870042.4218912.png" alt="image"><br>
Now we know one possible ans is 2 ..since we need to maximise this min ans so lets try for a dist &gt; 2<br>
so we do low=mid + 1 i.e 2 + 1 = 3<br>
so low=3 &amp; high = 3 so mid becomes 3<br>
<img src="https://assets.leetcode.com/users/images/24fa094b-dcc3-418a-8244-a9e93a88db5b_1624870167.751106.png" alt="image"><br>
Now we got 3 as ans WOW lets try for more dist<br>
low=mid + 1 i.e low=3 + 1=4<br>
low = 4 and high = 3 OOPS low crosses high so STOP<br>
3 is the  only ans !!</p><p>
</p><h3>lets get our hands dirty</h3>
<h3>Code</h3>
<pre><code><span class="hljs-function"><span class="hljs-keyword">bool</span> <span class="hljs-title">isPossible</span><span class="hljs-params">(<span class="hljs-built_in">vector</span>&lt;<span class="hljs-keyword">int</span>&gt; &amp;stalls, <span class="hljs-keyword">int</span> minDist, <span class="hljs-keyword">int</span> k)</span>
</span>{
    <span class="hljs-keyword">int</span> cows=<span class="hljs-number">1</span>;               <span class="hljs-comment">// we already place it at the first available slot i.e stalls[0]  ( GREEDY )</span>
    <span class="hljs-keyword">int</span> lastCowPosition=stalls[<span class="hljs-number">0</span>];
    <span class="hljs-keyword">for</span>(<span class="hljs-keyword">int</span> i=<span class="hljs-number">1</span>;i&lt;stalls.size();i++)
    {
        <span class="hljs-keyword">if</span>(stalls[i]-lastCowPosition&gt;=minDist)
        {
            cows++;
            lastCowPosition=stalls[i];
            <span class="hljs-keyword">if</span>(cows&gt;=k) <span class="hljs-keyword">return</span> <span class="hljs-literal">true</span>;
        }
    }
    <span class="hljs-keyword">return</span> <span class="hljs-literal">false</span>;
}

<span class="hljs-function"><span class="hljs-keyword">int</span> <span class="hljs-title">aggressiveCows</span><span class="hljs-params">(<span class="hljs-built_in">vector</span>&lt;<span class="hljs-keyword">int</span>&gt; &amp;stalls, <span class="hljs-keyword">int</span> k)</span>
</span>{
    <span class="hljs-keyword">int</span> n=stalls.size();
    sort(stalls.begin(),stalls.end());
    <span class="hljs-keyword">int</span> low=<span class="hljs-number">1</span>,high=stalls[n<span class="hljs-number">-1</span>]-stalls[<span class="hljs-number">0</span>];              <span class="hljs-comment">// just take low=0 and high = 1000000 any large number if this seems tricky</span>
    <span class="hljs-keyword">int</span> res;
    <span class="hljs-keyword">while</span>(low&lt;=high)
    {
        <span class="hljs-keyword">int</span> mid=(low+high)/<span class="hljs-number">2</span>;
        <span class="hljs-keyword">if</span>(isPossible(stalls,mid,k))
        {
            res=mid;
            low=mid+<span class="hljs-number">1</span>;
        }
        <span class="hljs-keyword">else</span> high=mid<span class="hljs-number">-1</span>;
    }
    <span class="hljs-keyword">return</span> res;
}
</code></pre><p></p></div>

## Go To
[Table of Content](#table-of-content)
