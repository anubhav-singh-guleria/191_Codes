## Table of Content
## Maximum Product Subarray
<div class="elfjS" data-track-load="description_content"><p>Given an integer array <code>nums</code>, find a <span data-keyword="subarray-nonempty" class=" cursor-pointer relative text-dark-blue-s text-sm"><div class="popover-wrapper inline-block" data-headlessui-state=""><div><div aria-expanded="false" data-headlessui-state="" id="headlessui-popover-button-:rt:"><div>subarray</div></div><div style="position: fixed; z-index: 40; inset: 0px auto auto 0px; transform: translate(272px, 182px);"></div></div></div></span> that has the largest product, and return <em>the product</em>.</p>

<p>The test cases are generated so that the answer will fit in a <strong>32-bit</strong> integer.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [2,3,-2,4]
<strong>Output:</strong> 6
<strong>Explanation:</strong> [2,3] has the largest product 6.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [-2,0,-1]
<strong>Output:</strong> 0
<strong>Explanation:</strong> The result cannot be 2, because [-2,-1] is not a subarray.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 2 * 10<sup>4</sup></code></li>
	<li><code>-10 &lt;= nums[i] &lt;= 10</code></li>
	<li>The product of any prefix or suffix of <code>nums</code> is <strong>guaranteed</strong> to fit in a <strong>32-bit</strong> integer.</li>
</ul>
</div>

### Solution
<p><strong>Intution:</strong> Since we have to find the contiguous subarray having maximum product then your approach should be combination of following three cases :</p>
<ul>
<li><strong>Case1 :- All the elements are positive :</strong> Then your answer will be product of all the elements in the array.</li>
<li><strong>Case2 :- Array have positive and negative elements both :</strong>
<ol>
<li>If the number of negative elements is even then again your answer will be complete array because on multiplying all the negative numbers it will become positive.</li>
<li>If the number of negative elements is odd then you have to remove just one negative element and for that u need to check your subarrays to get the max product.</li>
</ol>
</li>
<li><strong>Case3 :- Array also contains 0 :</strong> Then there will be not much difference...its just that your array will be divided into subarray around that 0. What u have to so is just as soon as your product becomes 0 make it 1 for the next iteration, now u will be searching new subarray and previous max will already be updated.<br></li>
</ul>
<p><strong>Approach :</strong> For each index i keep updating the max and min. We are also keeping min because on multiplying with any negative number your min will become max and max will become min. So for every index i  we will take max of (i-th element, prevMax * i-th element, prevMin * i-th element).</p>

```
class Solution {
    public int maxProduct(int[] nums) {
        
        int max = nums[0], min = nums[0], ans = nums[0];
        
        for (int i = 1; i < nums.length; i++) {
            
            int temp = max;  // store the max because before updating min your max will already be updated
            
            max = Math.max(Math.max(max * nums[i], min * nums[i]), nums[i]);
            min = Math.min(Math.min(temp * nums[i], min * nums[i]), nums[i]);
            
            if (max > ans) {
                ans = max;
            }
        }
        
        return ans;

    }
}
```

## Longest Increasing Subsequence
<div class="elfjS" data-track-load="description_content"><p>Given an integer array <code>nums</code>, return <em>the length of the longest <strong>strictly increasing </strong></em><span data-keyword="subsequence-array" class=" cursor-pointer relative text-dark-blue-s text-sm"><div class="popover-wrapper inline-block" data-headlessui-state=""><div><div aria-expanded="false" data-headlessui-state="" id="headlessui-popover-button-:rt:"><div><em><strong>subsequence</strong></em></div></div><div style="position: fixed; z-index: 40; inset: 0px auto auto 0px; transform: translate(561px, 182px);"></div></div></div></span>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [10,9,2,5,3,7,101,18]
<strong>Output:</strong> 4
<strong>Explanation:</strong> The longest increasing subsequence is [2,3,7,101], therefore the length is 4.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [0,1,0,3,2,3]
<strong>Output:</strong> 4
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> nums = [7,7,7,7,7,7,7]
<strong>Output:</strong> 1
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 2500</code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
</ul>

<p>&nbsp;</p>
<p><b>Follow up:</b>&nbsp;Can you come up with an algorithm that runs in&nbsp;<code>O(n log(n))</code> time complexity?</p>
</div>

### Solution
<div class="FN9Jv WRmCx"><p><strong>✔️  Solution 1: Dynamic Programming</strong></p>
<ul>
<li>This is a classic Dynamic Programming problem.</li>
<li>Let <code>dp[i]</code> is the longest increase subsequence of <code>nums[0..i]</code> which has <code>nums[i]</code> as the end element of the subsequence.</li>
</ul>

```
class Solution { // 256 ms, faster than 42.84%
public:
    int lengthOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<int> dp(n, 1);
        for (int i = 0; i < n; ++i)
            for (int j = 0; j < i; ++j)
                if (nums[i] > nums[j] && dp[i] < dp[j] + 1)
                    dp[i] = dp[j] + 1;
        return *max_element(dp.begin(), dp.end());
    }
};  
```

<p><strong>Complexity</strong></p>
<ul>
<li>Time: <code>O(N^2)</code>, where <code>N &lt;= 2500</code> is the number of elements in array <code>nums</code>.</li>
<li>Space: <code>O(N)</code></li>
</ul>
<hr>
<p><strong>✔️ Solution 2: Greedy with Binary Search</strong></p>
<ul>
<li>Let's construct the idea from following example.</li>
<li>Consider the example <code>nums = [2, 6, 8, 3, 4, 5, 1]</code>,  let's try to build the increasing subsequences starting with an empty one: <code>sub1 = []</code>.
<ol>
<li>Let pick the first element, <code>sub1 = [2]</code>.</li>
<li><code>6</code> is greater than previous number, <code>sub1 = [2, 6]</code></li>
<li><code>8</code> is greater than previous number, <code>sub1 = [2, 6, 8]</code></li>
<li><code>3</code> is less than previous number, we can't extend the subsequence <code>sub1</code>, but we must keep <code>3</code> because in the future there may have the longest subsequence start with <code>[2, 3]</code>, <code>sub1 = [2, 6, 8], sub2 = [2, 3]</code>.</li>
<li>With <code>4</code>,  we can't extend <code>sub1</code>, but we can extend <code>sub2</code>, so <code>sub1 = [2, 6, 8], sub2 = [2, 3, 4]</code>.</li>
<li>With <code>5</code>, we can't extend <code>sub1</code>, but we can extend <code>sub2</code>, so <code>sub1 = [2, 6, 8], sub2 = [2, 3, 4, 5]</code>.</li>
<li>With <code>1</code>, we can't extend neighter <code>sub1</code> nor <code>sub2</code>, but we need to keep <code>1</code>, so <code>sub1 = [2, 6, 8], sub2 = [2, 3, 4, 5], sub3 = [1]</code>.</li>
<li>Finally, length of longest increase subsequence = <code>len(sub2)</code> = 4.</li>
</ol>
</li>
<li>In the above steps, we need to keep different <code>sub</code> arrays (<code>sub1</code>, <code>sub2</code>..., <code>subk</code>) which causes poor performance. But we notice that we can just keep one <code>sub</code> array, when new number <code>x</code> is not greater than the last element of the subsequence <code>sub</code>, we do binary search to find the smallest element &gt;= <code>x</code> in <code>sub</code>, and replace with number <code>x</code>.</li>
<li>Let's run that example <code>nums = [2, 6, 8, 3, 4, 5, 1]</code> again:
<ol>
<li>Let pick the first element, <code>sub = [2]</code>.</li>
<li><code>6</code> is greater than previous number, <code>sub = [2, 6]</code></li>
<li><code>8</code> is greater than previous number, <code>sub = [2, 6, 8]</code></li>
<li><code>3</code> is less than previous number, so we can't extend the subsequence <code>sub</code>. We need to find the smallest number &gt;= <code>3</code> in <code>sub</code>, it's <code>6</code>. Then we overwrite it, now <code>sub = [2, 3, 8]</code>.</li>
<li><code>4</code> is less than previous number, so we can't extend the subsequence <code>sub</code>. We overwrite <code>8</code> by <code>4</code>, so <code>sub = [2, 3, 4]</code>.</li>
<li><code>5</code> is greater than previous number, <code>sub = [2, 3, 4, 5]</code>.</li>
<li><code>1</code> is less than previous number, so we can't extend the subsequence <code>sub</code>. We overwrite <code>2</code> by <code>1</code>, so <code>sub = [1, 3, 4, 5]</code>.</li>
<li>Finally, length of longest increase subsequence = <code>len(sub)</code> = 4.</li>
</ol>
</li>
</ul>
<p><img src="https://assets.leetcode.com/users/images/737a284c-b0f7-4dea-aa0f-068e768e65f5_1625856915.051443.jpeg" alt="image"></p>

```
class Solution { // 8 ms, faster than 91.61%
public:
    int lengthOfLIS(vector<int>& nums) {
        vector<int> sub;
        for (int x : nums) {
            if (sub.empty() || sub[sub.size() - 1] < x) {
                sub.push_back(x);
            } else {
                auto it = lower_bound(sub.begin(), sub.end(), x); // Find the index of the first element >= x
                *it = x; // Replace that number with x
            }
        }
        return sub.size();
    }
};
```
<p><strong>Complexity</strong></p>
<ul>
<li>Time: <code>O(N * logN)</code>, where <code>N &lt;= 2500</code> is the number of elements in array <code>nums</code>.</li>
<li>Space: <code>O(N)</code>, we can achieve <code>O(1)</code> in space by overwriting values of <code>sub</code> into original <code>nums</code> array.</li>
</ul>
<p><strong>[BONUS CODE] Get Longest Increasing Subsequence Path</strong></p>

```
class Solution {
public:
    vector<int> pathOfLIS(vector<int>& nums) {
        int n = nums.size();
        vector<int> sub, subIndex; // Store index instead of value for tracing path purpose
        vector<int> trace(n, -1); // trace[i] point to the index of previous number in LIS
        for (int i = 0; i < n; ++i) {
            if (sub.empty() || sub[sub.size() - 1] < nums[i]) {
                if (!sub.empty()) 
                    trace[i] = subIndex[sub.size() - 1];
                sub.push_back(nums[i]);
                subIndex.push_back(i);
            } else {
                int idx = lower_bound(sub.begin(), sub.end(), nums[i]) - sub.begin();
                if (idx > 0)
                    trace[i] = subIndex[idx - 1];
                sub[idx] = nums[i];
                subIndex[idx] = i;
            }
        }
        vector<int> path;
        int t = subIndex[subIndex.size() - 1];
        while (t != -1) {
            path.push_back(nums[t]);
            t = trace[t];
        }
        reverse(path.begin(), path.end());
        return path;
    }
};

int main() {
    vector<int> nums = {2, 6, 8, 3, 4, 5, 1};
    vector<int> res = Solution().pathOfLIS(nums); // [2, 3, 4, 5]
    for (int x : res) cout << x << " "; 
    return 0;
}
```

<p>Complexity:</p>
<ul>
<li>Time: <code>O(N * logN)</code></li>
<li>Space: <code>O(N)</code></li>
</ul>
<p><strong>REFERENCE</strong></p>
<ul>
<li><a href="https://www.cs.princeton.edu/courses/archive/spring13/cos423/lectures/LongestIncreasingSubsequence.pdf" target="_blank">Princeton lecture</a></li>
</ul>
<hr>
<p><strong>✔️  Solution 3: Binary Indexed Tree (Increase BASE of <code>nums</code> into one-base indexing)</strong></p>
<ul>
<li>Let <code>f[x]</code> is the length of longest increase subsequence , where all number in the subsequence &lt;= <code>x</code>. This is the max element in indices <code>[1..x]</code> if we build the <strong>Binary Indexed Tree (BIT)</strong></li>
<li>Since <code>-10^4 &lt;= nums[i] &lt;= 10^4</code>, we can convert nums into <code>1 &lt;= nums[i] &lt;= 2*10^4+1</code> by plus <code>BASE=10001</code> to store into the BIT.</li>
<li>We build <strong>Max BIT</strong>, which has 2 operators:
<ul>
<li><code>get(idx)</code>: Return the maximum value of indices in range <code>[1..idx]</code>.</li>
<li><code>update(idx, val)</code>: Update a value <code>val</code> into BIT at index <code>idx</code>.</li>
</ul>
</li>
<li>Iterate numbers <code>i</code> in range <code>[0..n-1]</code>:
<ul>
<li>subLongest = bit.get(nums[i] - 1) // Get longest increasing subsequence so far, which <code>idx &lt; nums[i]</code>, or <code>idx &lt;= nums[i] - 1</code>.</li>
<li>bit.update(nums[i], subLongest + 1) // Update latest longest to the BIT.</li>
</ul>
</li>
<li>The answer is <code>bit.get(20001)</code> // Maximum of all elements in the BIT</li>
</ul>

```
class MaxBIT { // One-based indexing
    vector<int> bit;
public:
    MaxBIT(int size) {
        bit.resize(size + 1);
    }
    int get(int idx) {
        int ans = 0;
        for (; idx > 0; idx -= idx & -idx)
            ans = max(ans, bit[idx]);
        return ans;
    }
    void update(int idx, int val) {
        for (; idx < bit.size(); idx += idx & -idx)
            bit[idx] = max(bit[idx], val);
    }
};
class Solution { // 16 ms, faster than 72.16%
public:
    int lengthOfLIS(vector<int>& nums) {
        int BASE = 10001;
        MaxBIT bit(20001);
        for (int x : nums) {
            int subLongest = bit.get(BASE + x - 1);
            bit.update(BASE + x, subLongest + 1);
        }
        return bit.get(20001);
    }
};
```

<p><strong>Complexity</strong></p>
<ul>
<li>Time: <code>O(N * logMAX)</code>, where <code>MAX = 20000</code> is the difference between minimum and maximum elements in <code>nums</code>, <code>N &lt;= 2500</code> is the number of elements in array <code>nums</code>.</li>
<li>Space: <code>O(MAX)</code></li>
</ul>
<hr>
<p><strong>✔️  Solution 4: Binary Indexed Tree (Compress <code>nums</code> into values in <code>[1...N]</code>)</strong></p>
<ul>
<li>In solution 3, <code>-10^4 &lt;= nums[i] &lt;= 10^4</code> is small enough, so we can store in our <strong>Binary Indexed Tree (BIT)</strong>.</li>
<li>Can we store when <code>-10^9 &lt;= nums[i] &lt;= 10^9</code> is very big? In that case, we can <strong>compress</strong> our <code>nums</code> array while <strong>keeping the relative comparation order</strong> between numbers.</li>
<li><strong>How to compress?</strong>
<ul>
<li>In the <code>nums</code> array length <code>N</code>, where <code>N &lt;= 2500</code>, there are maximum <code>N</code> different numbers.</li>
<li>We can get the <strong>unique values</strong> of numbers in <code>nums</code>, and sort those values in increasing order, let name it <code>uniqueSorted</code>.</li>
<li>Then we traverse <code>i</code> in range <code>[0..n-1]</code>, we get the compressed value of <code>nums[i]</code> by looking the index in <code>uniqueSorted</code>.</li>
<li>As the result, elemenents in <code>nums</code> is compressed into values in range <code>[1...N]</code>.</li>
</ul>
</li>
</ul>

```
class MaxBIT {
    vector<int> bit;
public:
    MaxBIT(int size) {
        bit.resize(size + 1);
    }
    int get(int idx) {
        int ans = 0;
        for (; idx > 0; idx -= idx & -idx)
            ans = max(ans, bit[idx]);
        return ans;
    }
    void update(int idx, int val) {
        for (; idx < bit.size(); idx += idx & -idx)
            bit[idx] = max(bit[idx], val);
    }
};
class Solution { // 12 ms, faster than 75.90%
public:
    int lengthOfLIS(vector<int>& nums) {
        int nUnique = compress(nums);
        MaxBIT bit(nUnique);
        for (int x : nums) {
            int subLongest = bit.get(x - 1);
            bit.update(x, subLongest + 1);
        }
        return bit.get(nUnique);
    }
    int compress(vector<int>& arr) {
        vector<int> uniqueSorted(arr);
        sort(uniqueSorted.begin(), uniqueSorted.end());
        uniqueSorted.erase(unique(uniqueSorted.begin(), uniqueSorted.end()), uniqueSorted.end()); // Remove duplicated values
        for (int& x : arr) x = lower_bound(uniqueSorted.begin(), uniqueSorted.end(), x) - uniqueSorted.begin() + 1;
        return uniqueSorted.size();
    }
};
```

<p>Complexity:</p>
<ul>
<li>Time: <code>O(N*logN)</code>, where <code>N &lt;= 2500</code> is the number of elements in array <code>nums</code>.</li>
<li>Space: <code>O(N)</code></li>
</ul>

## Longest Common Subsequence
<div class="elfjS" data-track-load="description_content"><p>Given two strings <code>text1</code> and <code>text2</code>, return <em>the length of their longest <strong>common subsequence</strong>. </em>If there is no <strong>common subsequence</strong>, return <code>0</code>.</p>

<p>A <strong>subsequence</strong> of a string is a new string generated from the original string with some characters (can be none) deleted without changing the relative order of the remaining characters.</p>

<ul>
	<li>For example, <code>"ace"</code> is a subsequence of <code>"abcde"</code>.</li>
</ul>

<p>A <strong>common subsequence</strong> of two strings is a subsequence that is common to both strings.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> text1 = "abcde", text2 = "ace" 
<strong>Output:</strong> 3  
<strong>Explanation:</strong> The longest common subsequence is "ace" and its length is 3.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> text1 = "abc", text2 = "abc"
<strong>Output:</strong> 3
<strong>Explanation:</strong> The longest common subsequence is "abc" and its length is 3.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> text1 = "abc", text2 = "def"
<strong>Output:</strong> 0
<strong>Explanation:</strong> There is no such common subsequence, so the result is 0.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= text1.length, text2.length &lt;= 1000</code></li>
	<li><code>text1</code> and <code>text2</code> consist of only lowercase English characters.</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><h2 id="brute-force">Brute Force</h2>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-typescript" style="color: rgb(156, 220, 254); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> int </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> int </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> int i</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> int j</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> text1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">||</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(197, 134, 192);">else</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> </span><span class="token known-class-name" style="color: rgb(78, 201, 176);">Math</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">max</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<h2 id="top-down-dp">Top-down DP</h2>
<p>We might use memoization to overcome overlapping subproblems.<br>
Since there are two changing values, i.e. <code>i</code> and <code>j</code> in the recursive function <code>longestCommonSubsequence</code>, we might apply a two-dimensional array.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-typescript" style="color: rgb(156, 220, 254); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> int </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        dp </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>text2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> int </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> int i</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> int j</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> text1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">||</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token null nil" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>            
</span><span><span>        </span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(197, 134, 192);">else</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token known-class-name" style="color: rgb(78, 201, 176);">Math</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">max</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<h2 id="bottom-up-dp">Bottom-up DP</h2>
<p>For every <code>i</code> in text1, <code>j</code> in text2, we will choose one of the following two options:</p>
<ul>
<li>if two characters match, length of the common subsequence would be 1 plus the length of the common subsequence till the <code>i-1</code> and<code> j-1</code> indexes</li>
<li>if two characters doesn't match, we will take the longer by either skipping <code>i</code> or <code>j</code> indexes</li>
</ul>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">longestCommonSubsequence</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>String text1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> String text2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> dp </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>text2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> text1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> text2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>                    dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span>
</span></span><span><span>                    dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> Math</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">max</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>text1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>text2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div></div>

## 0-1 knapsack problem
<a href="https://www.enjoyalgorithms.com/blog/zero-one-knapsack-problem" target="_blank">0-1 Knapsack Problem</a>

## Edit Distance
<div class="elfjS" data-track-load="description_content"><p>Given two strings <code>word1</code> and <code>word2</code>, return <em>the minimum number of operations required to convert <code>word1</code> to <code>word2</code></em>.</p>

<p>You have the following three operations permitted on a word:</p>

<ul>
	<li>Insert a character</li>
	<li>Delete a character</li>
	<li>Replace a character</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> word1 = "horse", word2 = "ros"
<strong>Output:</strong> 3
<strong>Explanation:</strong> 
horse -&gt; rorse (replace 'h' with 'r')
rorse -&gt; rose (remove 'r')
rose -&gt; ros (remove 'e')
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> word1 = "intention", word2 = "execution"
<strong>Output:</strong> 5
<strong>Explanation:</strong> 
intention -&gt; inention (remove 't')
inention -&gt; enention (replace 'i' with 'e')
enention -&gt; exention (replace 'n' with 'x')
exention -&gt; exection (replace 'n' with 'c')
exection -&gt; execution (insert 'u')
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= word1.length, word2.length &lt;= 500</code></li>
	<li><code>word1</code> and <code>word2</code> consist of lowercase English letters.</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>To apply DP, we define the state <code>dp[i][j]</code> to be the minimum number of operations to convert <code>word1[0..i)</code> to <code>word2[0..j)</code>.</p>
<p>For the base case, that is, to convert a string to an empty string, the mininum number of operations (deletions) is just the length of the string. So we have <code>dp[i][0] = i</code> and <code>dp[0][j] = j</code>.</p>
<p>For the general case to convert <code>word1[0..i)</code> to <code>word2[0..j)</code>, we break this problem down into sub-problems. Suppose we have already known how to convert <code>word1[0..i - 1)</code> to <code>word2[0..j - 1)</code> (<code>dp[i - 1][j - 1]</code>), if  <code>word1[i - 1] == word2[j - 1]</code>, then no more operation is needed and <code>dp[i][j] = dp[i - 1][j - 1]</code>.</p>
<p>If <code>word1[i - 1] != word2[j - 1]</code>, we need to consider three cases.</p>
<ol>
<li><strong>Replace</strong> <code>word1[i - 1]</code> by <code>word2[j - 1]</code> (<code>dp[i][j] = dp[i - 1][j - 1] + 1</code>);</li>
<li>If <code>word1[0..i - 1) = word2[0..j)</code> then <strong>delete</strong> <code>word1[i - 1]</code> (<code>dp[i][j] = dp[i - 1][j] + 1</code>);</li>
<li>If <code>word1[0..i) + word2[j - 1] = word2[0..j)</code> then <strong>insert</strong> <code>word2[j - 1]</code> to <code>word1[0..i)</code> (<code>dp[i][j] = dp[i][j - 1] + 1</code>).</li>
</ol>
<p>So when <code>word1[i - 1] != word2[j - 1]</code>, <code>dp[i][j]</code> will just be the minimum of the above three cases.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">minDistance</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>string word1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> string word2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> m </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> word1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> n </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> word2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">dp</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>m </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token generic-function" style="color: rgb(220, 220, 170);">vector</span><span class="token generic-function generic" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generic-function generic" style="color: rgb(86, 156, 214);">int</span><span class="token generic-function generic" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>n </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> m</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> m</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>word1</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> word2</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">min</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">min</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>m</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>Note that each time when we update <code>dp[i][j]</code>, we only need <code>dp[i - 1][j - 1]</code>, <code>dp[i][j - 1]</code> and <code>dp[i - 1][j]</code>. We may optimize the space of the code to use only two vectors.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">minDistance</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>string word1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> string word2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> m </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> word1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> n </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> word2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">pre</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>n </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">cur</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>n </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            pre</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> m</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>word1</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> word2</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> pre</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">min</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>pre</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">min</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> pre</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(220, 220, 170);">fill</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>pre</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">begin</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> pre</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">end</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(220, 220, 170);">swap</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>pre</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> pre</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>Or even just one vector.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">minDistance</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>string word1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> string word2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> m </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> word1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> n </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> word2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> pre</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">cur</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>n </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> m</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            pre </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> temp </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>word1</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> word2</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> pre</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">min</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>pre</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">min</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>                pre </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> temp</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> cur</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div></div>

## Best Team With No Conflicts
<div class="elfjS" data-track-load="description_content"><p>You are the manager of a basketball team. For the upcoming tournament, you want to choose the team with the highest overall score. The score of the team is the <strong>sum</strong> of scores of all the players in the team.</p>

<p>However, the basketball team is not allowed to have <strong>conflicts</strong>. A <strong>conflict</strong> exists if a younger player has a <strong>strictly higher</strong> score than an older player. A conflict does <strong>not</strong> occur between players of the same age.</p>

<p>Given two lists, <code>scores</code> and <code>ages</code>, where each <code>scores[i]</code> and <code>ages[i]</code> represents the score and age of the <code>i<sup>th</sup></code> player, respectively, return <em>the highest overall score of all possible basketball teams</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> scores = [1,3,5,10,15], ages = [1,2,3,4,5]
<strong>Output:</strong> 34
<strong>Explanation:</strong>&nbsp;You can choose all the players.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> scores = [4,5,6,5], ages = [2,1,2,1]
<strong>Output:</strong> 16
<strong>Explanation:</strong>&nbsp;It is best to choose the last 3 players. Notice that you are allowed to choose multiple people of the same age.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> scores = [1,2,3,5], ages = [8,9,10,1]
<strong>Output:</strong> 6
<strong>Explanation:</strong>&nbsp;It is best to choose the first 3 players. 
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= scores.length, ages.length &lt;= 1000</code></li>
	<li><code>scores.length == ages.length</code></li>
	<li><code>1 &lt;= scores[i] &lt;= 10<sup>6</sup></code></li>
	<li><code>1 &lt;= ages[i] &lt;= 1000</code></li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>Actually, this problem is to find the maximum sum of increasing subsequence.<br>
Very similiar with <a href="https://leetcode.com/problems/longest-increasing-subsequence/" target="_blank">300.Longest Increasing Subsequence</a></p>
<p>This problem want both age and score are increasing.<br>
We can sort by <code>age</code> and do DP for <code>scores</code>.<br>
Sum up, 3 key points:</p>
<ul>
<li>Create another <code>arr</code> by <code>{age[i], socres[i]}</code> and sorted by age.</li>
<li>For each loop, goes back and find maximum for current DP value to it maintain a increasing subsequence.</li>
<li>The answer could in any place of the dp array.</li>
</ul>
<p>Time complexity: O(n * n), space complexity: O(n)</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">bestTeamScore</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> scores</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> ages</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">const</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> n </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> scores</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">dp</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// first: age</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// second: scores</span><span>
</span></span><span><span>        vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>pair</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">arr</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>first </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> ages</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> scores</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">sort</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>arr</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">begin</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> arr</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">end</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> team_score </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j </span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">--</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(106, 153, 85);">// arr sorted by age, latter element has to have high score to maintain increasing susequence</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second </span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span> arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    </span><span class="token" style="color: rgb(106, 153, 85);">// update each status</span><span>
</span></span><span><span>                    dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">max</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(106, 153, 85);">// maximum value could in any place</span><span>
</span></span><span><span>            team_score </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">max</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>team_score</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> team_score</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div></div>


## Matrix Chain Multiplication
<div class="discuss-markdown-container"><p><strong>Question</strong> : <em>If a chain of matrices is given, we have to find the minimum number of the correct sequence of matrices to multiply</em>.</p><p>
</p><ul>
<li>The problem is not actually to perform the multiplications, but merely to decide in which order to perform the multiplications.</li>
<li>Note:no  matter how we parenthesize the product, the result will be the same. For example, if we had four matrices A, B, C, and D, we would have:</li>
</ul>
<pre><code>(ABC)D = (AB)(CD) = A(BCD) = ....
</code></pre>
<ul>
<li>However, the order in which we parenthesize the product affects the number of simple arithmetic operations needed to compute the product, or the efficiency. For example, suppose A is a 10 × 30 matrix, B is a 30 × 5 matrix, and C is a 5 × 60 matrix. Then,</li>
</ul>
<pre><code>(AB)C = (<span class="hljs-number">10</span>×<span class="hljs-number">30</span>×<span class="hljs-number">5</span>) + (<span class="hljs-number">10</span>×<span class="hljs-number">5</span>×<span class="hljs-number">60</span>) = <span class="hljs-number">1500</span> + <span class="hljs-number">3000</span> = <span class="hljs-number">4500</span> <span class="hljs-function">operations
<span class="hljs-title">A</span><span class="hljs-params">(BC)</span> </span>= (<span class="hljs-number">30</span>×<span class="hljs-number">5</span>×<span class="hljs-number">60</span>) + (<span class="hljs-number">10</span>×<span class="hljs-number">30</span>×<span class="hljs-number">60</span>) = <span class="hljs-number">9000</span> + <span class="hljs-number">18000</span> = <span class="hljs-number">27000</span> operations.
</code></pre>
<ul>
<li><strong>Clearly the first parenthesization requires less number of operations.</strong></li>
<li><strong>Note</strong> ; We'll be given an array arr[ ] which represents the chain of matrices such that the ith matrix arr[i] is of dimension arr[i-1] x arr[i].</li>
<li>That's why we start out 'k' i.e partition from  'i' =1 so that arr[ 1] is of dimentions arr[1-1] * arr[1] else we'll get index out of bound error Eg arr[0-1] * arr[0] is not possible</li>
<li>So first half of the array is from i to k &amp; other half is from k+1 to j</li>
<li>Also we need to find the cost of multiplication of these 2 resultant matrixes (first half &amp; second half) which is nothing but <strong>arr[i-1] * arr[k] * arr[j]</strong></li>
</ul>
<h3>Recursion</h3>
<h4>Here is the recursive algo :</h4>
<p></p><p><img src="https://assets.leetcode.com/users/images/f9f88962-750c-4689-bc87-13863f4a9452_1623912914.131823.png" alt="image"></p><p>
</p><h3>Code</h3>

```
int solve(int i, int j,int arr[])
    {
        if(i>=j)return 0;

        int ans=INT_MAX;
        for(int k=i;k<=j-1;k++)
        {
            int tempAns = solve(i,k,arr) + solve(k+1,j,arr)
                          + arr[i-1]*arr[k]*arr[j];
            
            ans=min(ans,tempAns);                        
        }
        return ans;
    }
    int matrixMultiplication(int N, int arr[])
    {
        return solve(1,N-1,arr);
    }
```

<ul>
<li>
<p></p><p>The time complexity of the above naive recursive approach is exponential. Observe that the above function computes the same subproblems again and again.</p><p>
</p></li>
<li>
<p></p><p>Let us saywe are given an array of 5 elements that means we are given N-1 i.e 4 matrixes .See the following recursion tree for a matrix chain of size 4.<br>
<img src="https://assets.leetcode.com/users/images/c89a32af-1eb7-4d37-ac62-8b5b45eec22a_1623913557.5356348.png" alt="image"></p><p>
</p></li>
<li>
<p></p><p>There are so many <strong>overlapping subproblems</strong> . Let's optimize it using DP !!</p><p>
</p></li>
</ul>
<h3>Memoization</h3>
<ul>
<li>Just adding a few lines to the above code, we can reduce time complexity from exponential to cubic</li>
</ul>

```
int dp[501][501];
    
    int solve(int i, int j,int arr[])
    {
        if(i>=j)return 0;
        
        if(dp[i][j]!=-1)
        return dp[i][j];

        int ans=INT_MAX;
        for(int k=i;k<=j-1;k++)
        {
            int tempAns = solve(i,k,arr) + solve(k+1,j,arr)
                          + arr[i-1]*arr[k]*arr[j];
            
            ans=min(ans,tempAns);
                          
        }
        return dp[i][j] = ans;
    }
    int matrixMultiplication(int N, int arr[])
    {
        memset(dp,-1,sizeof(dp));
        return solve(1,N-1,arr);
    }
```

<h3>Bottom Up DP</h3>
<ul>
<li>It's a bit tricky but if you got the above logic then you woudn't face any issues. I stil, prefer the Momoization</li>
</ul>

```
int MatrixChainOrder(int arr[], int n)
{
 
    /* For simplicity of the program, one
    extra row and one extra column are
    allocated in arr[][]. 0th row and 0th
    column of arr[][] are not used */
    int dp[n][n];
 
    int i, j, k, L, q;
 
    /* dp[i, j] = Minimum number of scalar
    multiplications needed to compute the
    matrix A[i]A[i+1]...A[j] = A[i..j] where
    dimension of A[i] is arr[i-1] x arr[i] */
 
    // cost is zero when multiplying
    // one matrix.
    for (i = 1; i < n; i++)
        dp[i][i] = 0;
 
    // L is chain length.
    for (L = 2; L < n; L++)
    {
        for (i = 1; i < n - L + 1; i++)
        {
            j = i + L - 1;
            dp[i][j] = INT_MAX;
            for (k = i; k <= j - 1; k++)
            {
                // q = cost/scalar multiplications
                q = dp[i][k] + dp[k + 1][j]
                    + arr[i - 1] * arr[k] * arr[j];
                if (q < dp[i][j])
                    dp[i][j] = q;
            }
        }
    }
 
    return dp[1][n - 1];
}
```

<p></p></div>


## Minimum Path Sum
<div class="elfjS" data-track-load="description_content"><p>Given a <code>m x n</code> <code>grid</code> filled with non-negative numbers, find a path from top left to bottom right, which minimizes the sum of all numbers along its path.</p>

<p><strong>Note:</strong> You can only move either down or right at any point in time.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/05/minpath.jpg" style="width: 242px; height: 242px;">
<pre><strong>Input:</strong> grid = [[1,3,1],[1,5,1],[4,2,1]]
<strong>Output:</strong> 7
<strong>Explanation:</strong> Because the path 1 → 3 → 1 → 1 → 1 minimizes the sum.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> grid = [[1,2,3],[4,5,6]]
<strong>Output:</strong> 12
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>m == grid.length</code></li>
	<li><code>n == grid[i].length</code></li>
	<li><code>1 &lt;= m, n &lt;= 200</code></li>
	<li><code>0 &lt;= grid[i][j] &lt;= 200</code></li>
</ul>
</div>

### Solution

```
class Solution {
public:
    int minPathSum(vector<vector<int>>& grid) {
        int m = grid.size();
        int n = grid[0].size();
        
        for (int i = 1; i < m; i++) {
            grid[i][0] += grid[i-1][0];
        }
        
        for (int j = 1; j < n; j++) {
            grid[0][j] += grid[0][j-1];
        }
        
        for (int i = 1; i < m; i++) {
            for (int j = 1; j < n; j++) {
                grid[i][j] += min(grid[i-1][j], grid[i][j-1]);
            }
        }
        
        return grid[m-1][n-1];
    }
};
```

## Coin Change
<div class="elfjS" data-track-load="description_content"><p>You are given an integer array <code>coins</code> representing coins of different denominations and an integer <code>amount</code> representing a total amount of money.</p>

<p>Return <em>the fewest number of coins that you need to make up that amount</em>. If that amount of money cannot be made up by any combination of the coins, return <code>-1</code>.</p>

<p>You may assume that you have an infinite number of each kind of coin.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> coins = [1,2,5], amount = 11
<strong>Output:</strong> 3
<strong>Explanation:</strong> 11 = 5 + 5 + 1
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> coins = [2], amount = 3
<strong>Output:</strong> -1
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> coins = [1], amount = 0
<strong>Output:</strong> 0
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= coins.length &lt;= 12</code></li>
	<li><code>1 &lt;= coins[i] &lt;= 2<sup>31</sup> - 1</code></li>
	<li><code>0 &lt;= amount &lt;= 10<sup>4</sup></code></li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>Okay, this is probably the second most famous classic problem introducing the concepts of dynamic programming, second only to Fibonacci numbers generation.</p>
<p>And in order to proceed, we really need to lay down the result step by step.</p>
<p>I opted to do so using an array instead of a vector and the differences in both speed and consumed memory were relevant, but I invite you to experiment with it and see with your own eyes how this works.</p>
<p>That said, the core logic: let's assume we have a series of memory cells storing how many coins are needed as a minimum to get there, safely considering that for the first, matching the amount of <code>0</code>, we actually have <code>0</code> options, while the initial value of all the others is going to be <code>INT_MAX</code>. Since we want to compute up to <code>amount</code>, and we have a <code>0</code> value for simplicity <code>amount + 1</code> cells are how many we need.</p>
<p>It is much easier to go with an example and I am confident most people will find it more understandable as they proceed reading.</p>
<p>So, for our aforementioned example, let's assume having as coins <code>[1, 2, 5]</code> and wishing to get up to the amount of <code>6</code> with the required mininum numbers of coins, we will have this starting situation for our array:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(212, 212, 212);">{</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>And we move then with our loop to the second cell, with index <code>i == 1</code>, our first <code>INT_MAX</code> to parse: we loop through the coins and we see we can go back only with the first coin (<code>c == 1</code>, since in order to get there, we can make one move, plus what it took to get to <code>i - c</code> positions before. This is definitely less than <code>INT_MAX</code>, so we update our array, which now is:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(212, 212, 212);">{</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>Not too clear? Okay, let's move to index <code>i == 2</code> and things should possibly simplify a bit: this time we have two coins that are <code>&lt;= i</code>, <code>1</code> and <code>2</code>: we know that to get to a total of two coins, we can take either what is needed to make one coin (the cell we just computed to have value <code>1</code> in the previous iteration) plus one with <code>c == 1</code> or what is needed to make zero coins (initially set to <code>0</code>) plus one with <code>c == 2</code>. Again, we will not use <code>c == 5</code> because, for now, we cannot go back 5 positions. Updated situation:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(212, 212, 212);">{</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>Now, what happens with <code>i == 3</code>? Well, whether we go back one cell or two, the value is the same and we add one (ie: we can make <code>3</code> either as <code>1 + 2</code> or <code>2 + 1</code>: it doesn't matter), so we have:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(212, 212, 212);">{</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>Now: <code>i == 4</code>: we can go back again only by one cell or two, and we quickly notice that going back by two is more conveient (ie: <code>2 + 2</code> uses less coins than <code>1 + 2 + 1</code>, the latter being an option if we went back by only one step):</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(212, 212, 212);">{</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>Finally with <code>i == 5</code> we can also use the last and more "powerful" coin, going back up to five slots; if you followed me up to here, you will see probably soon that using this very coin is the most convenient option: to have a value of <code>5</code>, we just need one coin (with the same value) plus the coins we needed to have a value of <code>0</code> (zero coins, indeed); definitely better than having a coin more than the one necessary to get either a value of <code>3</code> or <code>4</code> (that would be <code>3</code> coins in both cases), so we have now:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(212, 212, 212);">{</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>Last step, with <code>i == 6</code>, we can quickly compute that while going back by two cells would cost us a grand total of <code>3</code> coins, either going back by one or five will cost us only two (ie: we can get to <code>6</code> either as <code>5 + 1</code> or <code>1 + 5</code>, respectively), so we have:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(212, 212, 212);">{</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>And we can return the value of the last cell as the correct result.</p>
<p>My code below does the same with an extra bit of logic: when I backtrack and encounter a cell with value still equal to <code>INT_MAX</code> it means that the same cell was never reached before, so I skip it.</p>
<p>If in the end my final cell has a value of <code>INT_MAX</code>, I replace it with <code>-1</code> as required in the specs, otherwise I return its properly computed value.</p>
<p>The code:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">coinChange</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> coins</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// creating the base dp array, with first value set to 0</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// more convenient to have the coins sorted</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">sort</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(220, 220, 170);">begin</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>coins</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">end</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>coins</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// populating our dp array</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(106, 153, 85);">// setting dp[0] base value to 1, 0 for all the rest</span><span>
</span></span><span><span>            dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> c</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> coins</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> c </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">break</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(106, 153, 85);">// if it was a previously not reached cell, we do not add use it</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> c</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">min</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> c</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">--</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> INT_MAX </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div></div>

## 























































































































































































































































































































































































