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

## Binary Search - Search in Rotated Sorted Array
