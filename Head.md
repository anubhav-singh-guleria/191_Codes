## Heap - Implementation Of Min Heap and Max Heap
### Implementation
</header>
<div class="entry-content clearfix">
<h3><strong>Binary Heap:</strong></h3>
<p>A Binary Heap is a Binary Tree that satisfies the following conditions.</p>
<ul><li>It should be a Complete Binary Tree.</li><li>It should satisfy the Heap property.</li></ul>
<h3><strong>Complete Binary Tree:&nbsp;</strong></h3>
<p>The tree in Which all the levels are completely filled except the last level and last level is filled in such a way that all the keys are as left as possible.&nbsp;</p>
<figure class="wp-block-image size-full"><img loading="lazy" width="538" height="363" src="https://takeuforward.org/wp-content/uploads/2022/05/image-8.png" data-lazy-type="image" data-src="https://takeuforward.org/wp-content/uploads/2022/05/image-8.png" alt="" class="wp-image-4286 lazy-loaded" srcset="https://takeuforward.org/wp-content/uploads/2022/05/image-8.png 538w, https://takeuforward.org/wp-content/uploads/2022/05/image-8-300x202.png 300w, https://takeuforward.org/wp-content/uploads/2022/05/image-8-120x80.png 120w" data-srcset="" sizes="(max-width: 538px) 100vw, 538px"></figure>
<h3><strong>Heap Property:&nbsp;</strong></h3>
<p>Binary Heap is either a Min Heap or Max Heap. Property of the Binary Heap decides whether it is Min Heap or Max Heap.</p>
<ul><li><strong>Min Heap property: </strong>For every node in a binary heap, if the node value is less than its&nbsp;right and left child’s value then Binary Heap is known as Min Heap. The property of Node’s value less than its children’s value is known as Min Heap property. In Min Heap, the root value is always the Minimum value in Heap.</li></ul>
<figure class="wp-block-image size-full"><img loading="lazy" width="482" height="375" src="https://takeuforward.org/wp-content/uploads/2022/05/image-9.png" data-lazy-type="image" data-src="https://takeuforward.org/wp-content/uploads/2022/05/image-9.png" alt="" class="wp-image-4287 lazy-loaded" srcset="https://takeuforward.org/wp-content/uploads/2022/05/image-9.png 482w, https://takeuforward.org/wp-content/uploads/2022/05/image-9-300x233.png 300w" data-srcset="" sizes="(max-width: 482px) 100vw, 482px"></figure>
<ul><li><strong>Max Heap property:</strong> For every node in a binary heap, if the node value is greater than&nbsp;its right and left child’s value then Binary Heap is known as Max Heap. The property of&nbsp;being Node’s value greater than its children’s value is known as Max Heap property. In Max Heap, the root value is always the maximum value in Heap.</li></ul>
<figure class="wp-block-image size-full"><img loading="lazy" width="506" height="381" src="https://takeuforward.org/wp-content/uploads/2022/05/image-10.png" data-lazy-type="image" data-src="https://takeuforward.org/wp-content/uploads/2022/05/image-10.png" alt="" class="wp-image-4288 lazy-loaded" srcset="https://takeuforward.org/wp-content/uploads/2022/05/image-10.png 506w, https://takeuforward.org/wp-content/uploads/2022/05/image-10-300x226.png 300w" data-srcset="" sizes="(max-width: 506px) 100vw, 506px"></figure>
<p><strong>Representation of the Binary Heap:&nbsp;</strong></p>
<p>A Binary Heap is represented as an array.&nbsp;</p>
<ul><li>The root value is at arr[0]&nbsp;</li></ul>
<p>The below table summarizes how the node and its children are stored in an array.</p>
<figure class="wp-block-table"><table><tbody><tr><td><strong>Node index</strong></td><td><strong>Left child Index</strong></td><td><strong>Right Child Index</strong></td></tr><tr><td>i</td><td>2*i+1</td><td>2*i+2</td></tr></tbody></table></figure>
<p>If the child is at index<strong> i</strong>, then its parent index can be found using the below formula.</p>
<figure class="wp-block-table"><table><tbody><tr><td><strong>Child’s Index</strong></td><td><strong>Parent’s Index</strong></td></tr><tr><td>i</td><td>(i-1)/2</td></tr></tbody></table></figure>
<p><img class="lazy-loaded" loading="lazy" width="409" height="322" src="https://lh5.googleusercontent.com/4r2uUv160SCoj7z6Gw6EK5ID-hHkbLlcD91EiXFBc1jknzFQfgBpLA7HT64yHTnNPtbL9dCDTDGvr0K1w9qVYYVrV5JEW81xGygEtryhHpSEtj4L035fRdVEl6i24dlCgaaptuHeTeq4Kf42vQ" data-lazy-type="image" data-src="https://lh5.googleusercontent.com/4r2uUv160SCoj7z6Gw6EK5ID-hHkbLlcD91EiXFBc1jknzFQfgBpLA7HT64yHTnNPtbL9dCDTDGvr0K1w9qVYYVrV5JEW81xGygEtryhHpSEtj4L035fRdVEl6i24dlCgaaptuHeTeq4Kf42vQ"</p>
<figure class="wp-block-image size-full"><img loading="lazy" width="676" height="163" src="https://takeuforward.org/wp-content/uploads/2022/05/image-11.png" data-lazy-type="image" data-src="https://takeuforward.org/wp-content/uploads/2022/05/image-11.png" alt="" class="wp-image-4289 lazy-loaded" srcset="https://takeuforward.org/wp-content/uploads/2022/05/image-11.png 676w, https://takeuforward.org/wp-content/uploads/2022/05/image-11-300x72.png 300w" data-srcset="" sizes="(max-width: 676px) 100vw, 676px"></figure>
<p><strong>Operations Associated with Min Heap:</strong></p>
<ul><li>Insert()&nbsp;</li><li>Heapify()</li><li>getMin()</li><li>ExtractMin()</li><li>Delete()</li><li>Decreasekey()</li></ul>
<p>Let’s see how these operations are done Using Min Heap.</p>
<p><strong>Note: </strong>The Binary heap should always be a complete binary tree and should satisfy the corresponding heap property (Min / Max). If any of the two conditions are disturbed we should make necessary modifications in a heap to satisfy the two conditions.</p>
<h3><strong>Insert():&nbsp;</strong></h3>
<ul><li>Insert operation inserts a new key in the Binary Heap.</li></ul>
<p><strong>Steps Followed for inserting the key in Binary Heap:&nbsp;</strong></p>
<ul><li>First Insert the key at the first vacant position from the left on the last level of the heap. IF the last level is completely filled, then insert the key as the left-most element in the next level.</li><li>Inserting a new key at the first vacant position in the last level preserves the Complete binary tree property, The Min heap property may get affected we need to check for it.</li><li>If the inserted key parent is less than the key, then the Min heap property is also not violated.&nbsp;</li><li>If the parent is greater than the inserted key value, then swap the values. Now the heap property may get violated at the parent node. So repeat the same process until the heap property is satisfied.&nbsp;</li><li>Inserting an element takes O(logN) Time Complexity. Below shows the animation of how -1 is inserted into a Binary heap by following above described steps.</li></ul>
<p><img class="lazy-loaded" loading="lazy" width="422" height="315" src="https://lh6.googleusercontent.com/fM_FOTNaL_gVvLurkEN0XnyNxr_JxHMU_3ar_aXBgWE7FZtn0BBRZaVPXiEcNgFIxSbcwLzbaPJJZQjRMmRtJJFnlOROArIF1H4_7PVFK_1eagCZenkPA9wMd9_c8U8YoKr6_iPXMzk17iB_GQ" data-lazy-type="image" data-src="https://lh6.googleusercontent.com/fM_FOTNaL_gVvLurkEN0XnyNxr_JxHMU_3ar_aXBgWE7FZtn0BBRZaVPXiEcNgFIxSbcwLzbaPJJZQjRMmRtJJFnlOROArIF1H4_7PVFK_1eagCZenkPA9wMd9_c8U8YoKr6_iPXMzk17iB_GQ"></p>
<h3><strong>Heapify():</strong></h3>
<ul><li>Suppose there exists a Node at some index i, where the Minheap property is Violated.</li><li>We assume that all the subtrees of the tree rooted at index i are valid binary heaps.</li><li>The Heapify function is used to restore the Minheap, by fixing the violation.</li></ul>
<p><strong>Steps to be followed for Heapify:</strong></p>
<ul><li>First find out the Minimum among the Violated Node, left, and right child of Violated Node.</li><li>If the Minimum among them is the left child, then swap the Violated Node value with the&nbsp;Left child value and recursively call the function on the left Child.</li><li>If the Minimum among them is the right child, then swap the Violated Node value with the right child value and recursively call the function right Child.</li><li>Recursive call stops when the heap property is not violated.</li></ul>
<p><img class="lazy-loaded" loading="lazy" width="451" height="338" src="https://lh4.googleusercontent.com/kBHPiugF_QrtkliiXgvbk3dCQgn2YDcZpC69Fg1fxsCSkf94vz5Mz36CNvT54jZLk4mxjvAo63kqT4dOUtkfgkwQz-_NZJ4AUWCX36uhn3hltw-HzNvm2ERqGF66vvdrDtblIDdtXwEh4k_hUg" data-lazy-type="image" data-src="https://lh4.googleusercontent.com/kBHPiugF_QrtkliiXgvbk3dCQgn2YDcZpC69Fg1fxsCSkf94vz5Mz36CNvT54jZLk4mxjvAo63kqT4dOUtkfgkwQz-_NZJ4AUWCX36uhn3hltw-HzNvm2ERqGF66vvdrDtblIDdtXwEh4k_hUg"></p>
<h3><strong>getMin():</strong></h3>
<ul><li>It returns the minimum value in the Binary Heap.</li><li>As we all know, the root Node is the Minimum value in Min Heap. Simply return the arr[0].</li></ul>
<h3><strong>ExtractMin():&nbsp;</strong></h3>
<ul><li>This removes the Minimum element from the heap.</li></ul>
<p><strong>Steps to be followed to Remove Minimum value/root Node:&nbsp;</strong></p>
<ul><li>Copy the last Node value to the Root Node, and decrease the size, this means that the root value is now deleted from the heap, and the size is decreased by 1.</li><li>By doing the above step we ensure that the Complete binary tree property is not violated, as we are copying the last node value to the root node value, the Min Heap property gets violated.</li><li>Call the Heapify function to convert it into a valid heap.</li></ul>
<p><img class="lazy-loaded" loading="lazy" width="478" height="320" src="https://lh3.googleusercontent.com/ik0qVpkax9Svddu_DV5OJdMsH-7MWyPzk4pPwjRy8nUw9BDfr_r96zmEEWargPVrLq3jk7V1fjHMvm4iuQRECGRLNL0mIJ6ekYSuvElyhFHhJvg04QJnJdXrRkGCqmVSF_Xs0BQr-7Jlup_fMg" data-lazy-type="image" data-src="https://lh3.googleusercontent.com/ik0qVpkax9Svddu_DV5OJdMsH-7MWyPzk4pPwjRy8nUw9BDfr_r96zmEEWargPVrLq3jk7V1fjHMvm4iuQRECGRLNL0mIJ6ekYSuvElyhFHhJvg04QJnJdXrRkGCqmVSF_Xs0BQr-7Jlup_fMg"></p>
<h3><strong>Decreasekey():</strong></h3>
<ul><li>Given an index and a value, we need to update the value at the index with the given value.<strong> </strong>We assume that the given value is less than the existing value at that index.</li></ul>
<p><strong>Steps to be followed for Decreasekey():&nbsp;</strong></p>
<ul><li>Let’s the index be <strong>i </strong>and the value be <strong>new_val. </strong>Update existing value at index i with&nbsp;new_val i.e <strong>arr[i] = new_val.&nbsp;</strong></li><li>By performing the above step, the Complete binary tree property is not violated, but the Min heap property may get violated.</li><li>As the new_val we are inserting is less than the previously existing value, the min-heap property is not violated in subtrees of this rooted tree.&nbsp;</li><li>It may get violated in its ancestors, so as we do in insert operation, check the value of a current node with its parent node, if it violates the min-heap property</li></ul>
<p>Swap the nodes and recursively do the same.</p>
<p><img class="lazy-loaded" loading="lazy" width="450" height="326" src="https://lh5.googleusercontent.com/G1LfZQj-F0N3mMyGzvknaPs1-PXtUulpGmAppUL53DIoL7QJ8oIBNdhpp3E0Xsw5UZ9y8WpzmwK7rzxkSWwUXOABsIToFiOApmL9bLcxT1q7dJrCNCzrrFQGyfA4P1UawjuoZFKgMXZsv5DV8A" data-lazy-type="image" data-src="https://lh5.googleusercontent.com/G1LfZQj-F0N3mMyGzvknaPs1-PXtUulpGmAppUL53DIoL7QJ8oIBNdhpp3E0Xsw5UZ9y8WpzmwK7rzxkSWwUXOABsIToFiOApmL9bLcxT1q7dJrCNCzrrFQGyfA4P1UawjuoZFKgMXZsv5DV8A"></p>
<h3><strong>Delete() :&nbsp;</strong></h3>
<ul><li>Given an index, delete the value at that index from the min-heap.</li></ul>
<p><strong>Steps to be followed for Delete operation():&nbsp;</strong></p>
<ul><li>First, update the value at the index that needs to be deleted with INT_MIN.</li><li>Now call the Decreasekey() function at the index which is need to be deleted. As the value at the index is the least, it reaches the top.</li><li>Now call the ExtractMin() operation which deletes the root node in Minheap.</li><li>In this way, the desired index value is deleted from the Minheap.</li></ul>
<p><img class="lazy-loaded" loading="lazy" width="519" height="349" src="https://lh5.googleusercontent.com/_hlmHk-TNz9aZ5D3GO9EK8HPEL05EQp5rIOI7_Al1TQoIjpLVPjsjZhhELlqrrIKBp_JahtYHheuj-z1J-8CvEER2SjLLlEzCbYC8L7Tc9LXWMgif1grznONO9vgSEQEzmgx5D4MHlNLVXPzkQ" data-lazy-type="image" data-src="https://lh5.googleusercontent.com/_hlmHk-TNz9aZ5D3GO9EK8HPEL05EQp5rIOI7_Al1TQoIjpLVPjsjZhhELlqrrIKBp_JahtYHheuj-z1J-8CvEER2SjLLlEzCbYC8L7Tc9LXWMgif1grznONO9vgSEQEzmgx5D4MHlNLVXPzkQ"></p>

```
#include <bits/stdc++.h>

using namespace std;

class BinaryHeap {
  public:
    int capacity; /*Maximum elements that can be stored in heap*/
  int size; /*Current no of elements in heap*/
  int * arr; /*array for storing the keys*/

  BinaryHeap(int cap) {
    capacity = cap; /*Assigning the capacity*/
    size = 0; /*Intailly size of hepa is zero*/
    arr = new int[capacity]; /*Creating a array*/
  }

  /*returns the parent of ith Node*/
  int parent(int i) {
    return (i - 1) / 2;
  }
  /*returns the left child of ith Node*/
  int left(int i) {
    return 2 * i + 1;
  }
  /*Returns the right child of the ith Node*/
  int right(int i) {
    return 2 * i + 2;
  }

  /*Insert a new key x*/
  void Insert(int x) {
    if (size == capacity) {
      cout << "Binary Heap Overflwon" << endl;
      return;
    }
    arr[size] = x; /*Insert new element at end*/
    int k = size; /*store the index ,for checking heap property*/
    size++; /*Increase the size*/

    /*Fix the min heap property*/
    while (k != 0 && arr[parent(k)] > arr[k]) {
      swap( & arr[parent(k)], & arr[k]);
      k = parent(k);
    }
  }

  void Heapify(int ind) {
    int ri = right(ind); /*right child*/
    int li = left(ind); /*left child*/
    int smallest = ind; /*intially assume violated value in Min value*/
    if (li < size && arr[li] < arr[smallest])
      smallest = li;
    if (ri < size && arr[ri] < arr[smallest])
      smallest = ri;
    /*smallest will store the minvalue index*/
    /*If the Minimum among the three nodes is the parent itself,
    that is Heap property satisfied so stop else call function recursively on Minvalue node*/
    if (smallest != ind) {
      swap( & arr[ind], & arr[smallest]);
      Heapify(smallest);
    }
  }
  int getMin() {
    return arr[0];
  }
  int ExtractMin() {
    if (size <= 0)
      return INT_MAX;
    if (size == 1) {
      size--;
      return arr[0];
    }
    int mini = arr[0];
    arr[0] = arr[size - 1]; /*Copy last Node value to root Node value*/
    size--;
    Heapify(0); /*Call heapify on root node*/
    return mini;
  }
  void Decreasekey(int i, int val) {
    arr[i] = val; /*Updating the new_val*/
    while (i != 0 && arr[parent(i)] > arr[i]) /*Fixing the Min heap*/ {
      swap( & arr[parent(i)], & arr[i]);
      i = parent(i);
    }
  }
  void Delete(int i) {
    Decreasekey(i, INT_MIN);
    ExtractMin();
  }
  void swap(int * x, int * y) {
    int temp = * x;
    * x = * y;
    * y = temp;
  }
  void print() {
    for (int i = 0; i < size; i++)
      cout << arr[i] << " ";
    cout << endl;
  }
};
int main()

{
  BinaryHeap h(20);
  h.Insert(4);
  h.Insert(1);
  h.Insert(2);
  h.Insert(6);
  h.Insert(7);
  h.Insert(3);
  h.Insert(8);
  h.Insert(5);
  cout << "Min value is " << h.getMin() << endl;
  h.Insert(-1);
  cout << "Min value is " << h.getMin() << endl;
  h.Decreasekey(3, -2);
  cout << "Min value is " << h.getMin() << endl;
  h.ExtractMin();
  cout << "Min value is " << h.getMin() << endl;
  h.Delete(0);
  cout << "Min value is " << h.getMin() << endl;
  return 0;
}
```
<p><strong>Output:</strong></p>
<p>Min value is 1<br>Min value is -1<br>Min value is -2<br>Min value is -1<br>Min value is 1</p>
<h3><strong>Time Complexities :&nbsp;</strong></h3>
<figure class="wp-block-table"><table><tbody><tr><td><strong>&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp; Function</strong></td><td><strong>Time Complexity</strong></td></tr><tr><td><strong>Insert() :&nbsp;</strong></td><td>O(logN)</td></tr><tr><td><strong>Heapify()</strong></td><td>O(logN)</td></tr><tr><td><strong>getMin()</strong></td><td>O(1)</td></tr><tr><td><strong>ExtractMin()</strong></td><td>O(logN)</td></tr><tr><td><strong>Decreasekey()</strong></td><td>O(logN)</td></tr><tr><td><strong>Delete()</strong></td><td>O(logN)</td></tr></tbody></table></figure>

</div>
</article>


## Heap - Kth Largest Element in an Array
<div class="elfjS" data-track-load="description_content"><p>Given an integer array <code>nums</code> and an integer <code>k</code>, return <em>the</em> <code>k<sup>th</sup></code> <em>largest element in the array</em>.</p>

<p>Note that it is the <code>k<sup>th</sup></code> largest element in the sorted order, not the <code>k<sup>th</sup></code> distinct element.</p>

<p>Can you solve it without sorting?</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [3,2,1,5,6,4], k = 2
<strong>Output:</strong> 5
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [3,2,3,1,2,4,5,5,6], k = 4
<strong>Output:</strong> 4
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= k &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><H3 id="intuition">Intuition:</H3>
<p>The problem asks to find the kth largest element in an array. One way to solve this problem is to sort the array and return the kth element from the end (i.e., kth largest element). However, the time complexity of this approach would be O(nlogn) due to the sorting process.</p>
<H3 id="approach">Approach:</H3>
<p>We can use a heap data structure to efficiently find the kth largest element in the array. There are two types of heaps we can use for this problem: a min heap and a max heap.</p>
<ul>
<li>
<p>Min Heap:<br>
We can use a min heap to keep track of the k largest elements seen so far. We iterate over the array, and for each element, we insert it into the heap. If the size of the heap becomes larger than k, we remove the minimum element from the heap. At the end, the top element of the heap will be the kth largest element in the array.</p>
</li>
<li>
<p>Max Heap:<br>
We can also use a max heap to keep track of the k largest elements seen so far. We initialize the heap with all the elements in the array. We then pop the top element from the heap k-1 times to get the kth largest element in the array.</p>
</li>
</ul>
<H3 id="complexity">Complexity:</H3>
<ul>
<li>
<H3 id="time-complexity">Time complexity:</H3>
<ul>
<li>
<p>Min Heap: The time complexity of this approach is O(nlogk), where n is the size of the array and k is the number of largest elements we need to keep track of in the heap. We iterate over n elements and each heap operation takes logk time.</p>
</li>
<li>
<p>Max Heap: The time complexity of this approach is O(nlogn), where n is the size of the array. We initialize the heap with n elements, and each heap operation takes logn time.</p>
</li>
</ul>
</li>
<li>
<H3 id="space-complexity">Space complexity:</H3>
<ul>
<li>
<p>Min Heap: The space complexity of this approach is O(k), where k is the number of largest elements we need to keep track of in the heap.</p>
</li>
<li>
<p>Max Heap: The space complexity of this approach is O(n), where n is the size of the array as we need to store all the elements in the heap.</p>
</li>
</ul>
</li>
</ul>
<H3 id="c">C++</H3>
<h4 id="min-heap">Min Heap</h4>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">findKthLargest</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> k</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        priority_queue</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> greater</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;&gt;</span><span> min_heap</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> num </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            min_heap</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>num</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>min_heap</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> k</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                min_heap</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> min_heap</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">top</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H39a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H39a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<h2 id="max-heap">Max Heap</h2>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">findKthLargest</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> k</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        priority_queue</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">max_heap</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>nums</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">begin</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">end</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> k </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            max_heap</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> max_heap</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">top</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H39a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H39a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>

## Heap - Maximum Sum Combinations
<div class="p-html-content__container"><p><strong>Problem Description</strong><br> 
 </p><div id="problem_description_markdown_content_value" style="background-color: #f9f9f9; padding: 5px 10px; "><p>Given two equally sized 1-D arrays <strong>A, B</strong> containing <strong>N</strong> integers each.</p><p></p><p></p><p></p><p></p><p></p><p></p><p></p>
<p>A <strong>sum combination</strong> is made by adding one element from array <strong>A</strong> and another element of array <strong>B</strong>.</p>
<p>Return the <strong>maximum C valid sum combinations</strong> from all the possible sum combinations.</p>

<p></p></div><br><br><strong>Problem Constraints</strong><br> 
 <div id="problem_constraints_markdown_content_value" style="background-color: #f9f9f9; padding: 5px 10px; "><p>1 &lt;= N &lt;= 10<sup>5</sup></p> 
<p>1 &lt;= A[i] &lt;= 10<sup>5</sup></p>
<p>1 &lt;= C &lt;= N</p> </div><br><br><strong>Input Format</strong><br> 
 <div id="input_format_markdown_content_value" style="background-color: #f9f9f9; padding: 5px 10px; "><p>First argument is an one-dimensional integer array <strong>A</strong> of size <strong>N</strong>.</p><p></p><p></p><p></p><p></p><p></p><p></p><p></p>
<p>Second argument is an one-dimensional integer array <strong>B</strong> of size <strong>N</strong>.</p>
<p>Third argument is an integer <strong>C</strong>.</p>

<p></p></div><br><br><strong>Output Format</strong><br> 
 <div id="output_format_markdown_content_value" style="background-color: #f9f9f9; padding: 5px 10px; "><p>Return a one-dimensional integer array of size <strong>C</strong> denoting the top C maximum sum combinations.</p><p></p><p></p><p></p><p></p><p></p><p></p><p></p>
<p><strong>NOTE:</strong></p>
<p>The returned array must be sorted in non-increasing order.</p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p></div><br><br><strong>Example Input</strong><br> 
 <div id="example_input_markdown_content_value" style="background-color: #f9f9f9; padding: 5px 10px; "><p>Input 1:</p><p></p><p></p><p></p><p></p><p></p><p></p><p></p>
<pre> A = [3, 2]
 B = [1, 4]
 C = 2
</pre>
<p>Input 2:</p>
<pre> A = [1, 4, 2, 3]
 B = [2, 5, 1, 6]
 C = 4
</pre>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p></div><br><br><strong>Example Output</strong><br> 
 <div id="example_output_markdown_content_value" style="background-color: #f9f9f9; padding: 5px 10px; "><p>Output 1:</p><p></p><p></p><p></p><p></p><p></p><p></p><p></p>
<pre> [7, 6]
</pre>
<p>Output 1:</p>
<pre> [10, 9, 9, 8]
</pre>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p>
<p></p></div><br><br><strong>Example Explanation</strong><br> 
 <div id="example_explanation_markdown_content_value" style="background-color: #f9f9f9; padding: 5px 10px; "><p>Explanation 1:</p><p></p><p></p><p></p><p></p><p></p><p></p><p></p>
<pre> 7     (A : 3) + (B : 4)
 6     (A : 2) + (B : 4)
</pre>
<p>Explanation 2:</p>
<pre> 10   (A : 4) + (B : 6)
 9   (A : 4) + (B : 5)
 9   (A : 3) + (B : 6)
 8   (A : 3) + (B : 5)
</pre>
<p></p></div><br><br><p></p>
</div>

### Solution
<ol>
<li value="1"><span>Sort both arrays array A and array B.</span></li>
<li value="2"><span>Create a max heap i.e </span><a href="https://www.geeksforgeeks.org/priority-queue-in-cpp-stl/" class="GFGEditorTheme__link"><span>priority_queue in C++</span></a><span> to store the sum combinations along with the indices of elements from both arrays A and B which make up the sum. Heap is ordered by the sum.</span></li>
<li value="3"><span>Initialize the heap with the maximum possible sum combination i.e (A[N – 1] + B[N – 1] where N is the size of array) and with the indices of elements from both arrays (N – 1, N – 1). The tuple inside max heap will be (A[N-1] + B[N – 1], N – 1, N – 1). Heap is ordered by first value i.e sum of both elements.</span></li>
<li value="4"><span>Pop the heap to get the current largest sum and along with the indices of the element that make up the sum. Let the tuple be (sum, i, j).</span>
<ol>
<li value="1"><span>Next insert (A[i – 1] + B[j], i – 1, j) and (A[i] + B[j – 1], i, j – 1) into the max heap but make sure that the pair of indices i.e (i – 1, j) and (i, j – 1) are not&nbsp;</span><br><span>already present in the max heap. To check this we can use </span><a href="https://www.geeksforgeeks.org/set-in-cpp-stl/" class="GFGEditorTheme__link"><span>set in C++</span></a><span>.</span></li>
<li value="2"><span>Go back to 4 until K times.</span></li>
</ol>
</li>
</ol>

```
// An efficient C++ program to find top K elements
// from two arrays.
#include <bits/stdc++.h>
using namespace std;

// Function prints k maximum possible combinations
void KMaxCombinations(vector<int>& A, 
					vector<int>& B, int K)
{
	// sort both arrays A and B
	sort(A.begin(), A.end());
	sort(B.begin(), B.end());

	int N = A.size();

	// Max heap which contains tuple of the format
	// (sum, (i, j)) i and j are the indices
	// of the elements from array A
	// and array B which make up the sum.
	priority_queue<pair<int, pair<int, int> > > pq;

	// my_set is used to store the indices of
	// the pair(i, j) we use my_set to make sure
	// the indices does not repeat inside max heap.
	set<pair<int, int> > my_set;

	// initialize the heap with the maximum sum
	// combination ie (A[N - 1] + B[N - 1])
	// and also push indices (N - 1, N - 1) along
	// with sum.
	pq.push(make_pair(A[N - 1] + B[N - 1],
					make_pair(N - 1, N - 1)));

	my_set.insert(make_pair(N - 1, N - 1));

	// iterate upto K
	for (int count = 0; count < K; count++)
	{
		// tuple format (sum, (i, j)).
		pair<int, pair<int, int> > temp = pq.top();
		pq.pop();

		cout << temp.first << endl;

		int i = temp.second.first;
		int j = temp.second.second;

		int sum = A[i - 1] + B[j];

		// insert (A[i - 1] + B[j], (i - 1, j))
		// into max heap.
		pair<int, int> temp1 = make_pair(i - 1, j);

		// insert only if the pair (i - 1, j) is
		// not already present inside the map i.e.
		// no repeating pair should be present inside
		// the heap.
		if (my_set.find(temp1) == my_set.end()) 
		{
			pq.push(make_pair(sum, temp1));
			my_set.insert(temp1);
		}

		// insert (A[i] + B[j - 1], (i, j - 1))
		// into max heap.
		sum = A[i] + B[j - 1];
		temp1 = make_pair(i, j - 1);

		// insert only if the pair (i, j - 1)
		// is not present inside the heap.
		if (my_set.find(temp1) == my_set.end())
		{
			pq.push(make_pair(sum, temp1));
			my_set.insert(temp1);
		}
	}
}

// Driver Code.
int main()
{
	vector<int> A = { 1, 4, 2, 3 };
	vector<int> B = { 2, 5, 1, 6 };
	int K = 4;

	// Function call
	KMaxCombinations(A, B, K);
	return 0;
}
```
<div class="code-output"><strong>Output</strong><p></p>
<pre>10
9
9
8

</pre>
</div>

## Heap - Find Median from Data Stream
<div class="elfjS" data-track-load="description_content"><p>The <strong>median</strong> is the middle value in an ordered integer list. If the size of the list is even, there is no middle value, and the median is the mean of the two middle values.</p>

<ul>
	<li>For example, for <code>arr = [2,3,4]</code>, the median is <code>3</code>.</li>
	<li>For example, for <code>arr = [2,3]</code>, the median is <code>(2 + 3) / 2 = 2.5</code>.</li>
</ul>

<p>Implement the MedianFinder class:</p>

<ul>
	<li><code>MedianFinder()</code> initializes the <code>MedianFinder</code> object.</li>
	<li><code>void addNum(int num)</code> adds the integer <code>num</code> from the data stream to the data structure.</li>
	<li><code>double findMedian()</code> returns the median of all elements so far. Answers within <code>10<sup>-5</sup></code> of the actual answer will be accepted.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input</strong>
["MedianFinder", "addNum", "addNum", "findMedian", "addNum", "findMedian"]
[[], [1], [2], [], [3], []]
<strong>Output</strong>
[null, null, null, 1.5, null, 2.0]

<strong>Explanation</strong>
MedianFinder medianFinder = new MedianFinder();
medianFinder.addNum(1);    // arr = [1]
medianFinder.addNum(2);    // arr = [1, 2]
medianFinder.findMedian(); // return 1.5 (i.e., (1 + 2) / 2)
medianFinder.addNum(3);    // arr[1, 2, 3]
medianFinder.findMedian(); // return 2.0
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>-10<sup>5</sup> &lt;= num &lt;= 10<sup>5</sup></code></li>
	<li>There will be at least one element in the data structure before calling <code>findMedian</code>.</li>
	<li>At most <code>5 * 10<sup>4</sup></code> calls will be made to <code>addNum</code> and <code>findMedian</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong></p>

<ul>
	<li>If all integer numbers from the stream are in the range <code>[0, 100]</code>, how would you optimize your solution?</li>
	<li>If <code>99%</code> of all integer numbers from the stream are in the range <code>[0, 100]</code>, how would you optimize your solution?</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p><strong>✔️ Solution 1: MaxHeap to store a half of low numbers, MinHeap to store a half of high numbers</strong></p>
<ul>
<li>The idea is to divide numbers into 2 balanced halves, one half <code>low</code> stores low numbers, the other half <code>high</code> stores high numbers. To access the median in <code>O(1)</code>, we need a data structure that give us the maximum of <code>low</code> half and the minimum of <code>high</code> half in <code>O(1)</code>. That's where <code>maxHeap</code> and <code>minHeap</code> come into play.</li>
<li>We use <code>maxHeap</code> to store a half of <strong>low numbers</strong>, top of the maxHeap is the highest number among low numbers.</li>
<li>We use <code>minHeap</code> to store a half of <strong>high numbers</strong>, top of the minHeap is the lowest number among high numbers.</li>
<li>We need to balance the size between <code>maxHeap</code> and <code>minHeap</code> while processing. Hence after adding <code>k</code> elements,
<ul>
<li>If <code>k = 2 * i</code> then <code>maxHeap.size = minHeap.size = i</code></li>
<li>If <code>k = 2 * i + 1</code>, let <code>maxHeap</code> store 1 element more than <code>minHeap</code>, then <code>maxHeap.size = minHeap.size + 1</code>.</li>
</ul>
</li>
<li>When adding a new number <code>num</code> into our  <code>MedianFinder</code>:
<ul>
<li>Firstly, add <code>num</code> to the <code>maxHeap</code>, now <code>maxHeap</code> may contain the big element (which should belong to <code>minHeap</code>). So we need to balance, by removing the highest element from <code>maxHeap</code>, and offer it to <code>minHeap</code>.</li>
<li>Now, the <code>minHeap</code> might hold more elements than <code>maxHeap</code>, in that case, we need to balance the size, by removing the lowest element from <code>minHeap</code> and offer it back to <code>maxHeap</code>.</li>
</ul>
</li>
<li>When doing <code>findMedian()</code>:
<ul>
<li>If <code>maxHeap.size &gt; minHeap.size</code> return top of the <code>maxHeap</code>, which is the highest number amongs low numbers.</li>
<li>Else if <code>maxHeap.size == minHeap</code> return the <code>(maxHeap.top() + minHeap.top()) / 2</code>.</li>
</ul>
</li>
</ul>
<p><img src="https://assets.leetcode.com/users/images/0eb8feba-cbfa-4f73-8d26-9aad226bdbc5_1626016093.9717174.png" alt="image"></p>

```
class MedianFinder {
public:
    priority_queue<int> maxHeap;
    priority_queue<int, vector<int>, greater<int>> minHeap;
    
    MedianFinder() {
    }
    void addNum(int num) {
        maxHeap.push(num);
        minHeap.push(maxHeap.top());
        maxHeap.pop();
        if (minHeap.size() > maxHeap.size()) {
            maxHeap.push(minHeap.top());
            minHeap.pop();
        }
    }
    double findMedian() {
        if (maxHeap.size() > minHeap.size()) return maxHeap.top();
        return (maxHeap.top() + minHeap.top()) / 2.0;
    }
};
```

<p><strong>Complexity</strong></p>
<ul>
<li>Time:
<ul>
<li>Constructor: <code>O(1)</code></li>
<li>addNum: <code>O(logN)</code></li>
<li>findMedian: <code>O(1)</code></li>
</ul>
</li>
<li>Space: <code>O(N)</code></li>
</ul>

## Heap - Merge k Sorted Lists
<div class="elfjS" data-track-load="description_content"><p>You are given an array of <code>k</code> linked-lists <code>lists</code>, each linked-list is sorted in ascending order.</p>

<p><em>Merge all the linked-lists into one sorted linked-list and return it.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> lists = [[1,4,5],[1,3,4],[2,6]]
<strong>Output:</strong> [1,1,2,3,4,4,5,6]
<strong>Explanation:</strong> The linked-lists are:
[
  1-&gt;4-&gt;5,
  1-&gt;3-&gt;4,
  2-&gt;6
]
merging them into one sorted list:
1-&gt;1-&gt;2-&gt;3-&gt;4-&gt;4-&gt;5-&gt;6
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> lists = []
<strong>Output:</strong> []
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> lists = [[]]
<strong>Output:</strong> []
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>k == lists.length</code></li>
	<li><code>0 &lt;= k &lt;= 10<sup>4</sup></code></li>
	<li><code>0 &lt;= lists[i].length &lt;= 500</code></li>
	<li><code>-10<sup>4</sup> &lt;= lists[i][j] &lt;= 10<sup>4</sup></code></li>
	<li><code>lists[i]</code> is sorted in <strong>ascending order</strong>.</li>
	<li>The sum of <code>lists[i].length</code> will not exceed <code>10<sup>4</sup></code>.</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p><em><strong>Brief note about Question-</strong></em></p>
<p>We have to <em><strong>Merge all the linked-lists into one sorted linked-list and return it.</strong></em></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-rust" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(78, 201, 176);">Take</span><span> an example </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(78, 201, 176);">Given</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> k number of sorted linked list </span><span class="token" style="color: rgb(86, 156, 214);">in</span><span> ascending order</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(78, 201, 176);">Aim</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Merge</span><span> them into a single sorted linked list</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(78, 201, 176);">Take</span><span> anthor example which is not given </span><span class="token" style="color: rgb(86, 156, 214);">in</span><span> question</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(156, 220, 254);">L1</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">5</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">7</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">9</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">N</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(156, 220, 254);">L2</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">4</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">8</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">N</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(156, 220, 254);">L3</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">3</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">6</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">N</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(78, 201, 176);">So</span><span> our answer should like this</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">2</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">3</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">4</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">5</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">6</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">7</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">8</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">9</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">N</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<p><em><strong>Solution - I (Most basic approach, Accepted)-</strong></em></p>
<ul>
<li>Okay, so the most basic approach we can think of is, we are obedient person, and not to do anything extra from ourself,</li>
<li>We will simply do what the question wants us to do, we create an array which store all the elements of all 'k' linked list present in the array.</li>
<li>After storing all elements, we sort them a/c to their vaules.</li>
<li>Now, the only task which is left is to link them, so we start linking them.</li>
</ul>
<p><strong>Okay, I got the approach, but how i will implement this or code these words-</strong></p>
<ol>
<li>We take help of a <code>vector pair</code> which of value and Node type.</li>
<li>But why vector pair?</li>
<li>See,  <em>Here we have k different linked list na and each linked list contain some elements so to observe that we need a vector pair.</em></li>
<li>Okay good, I take a vector pair,so now what i have to do?</li>
<li>Now we start storing each value in this vector pair.</li>
<li>After this, by using <code>sort function</code> (present in STL) we sort this vectorAnd at last, i start linking them, it can be done simply by putting next pointer i.e <code>arr[i].second -&gt; next = arr[i + 1].second</code>.</li>
</ol>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-sql" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>Suppose </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> total number </span><span class="token" style="color: rgb(86, 156, 214);">of</span><span> nodes present </span><span class="token" style="color: rgb(212, 212, 212);">in</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">all</span><span> linked list </span><span class="token" style="color: rgb(212, 212, 212);">is</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'n'</span><span> 
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">Time</span><span> Complexity </span><span class="token" style="color: rgb(106, 153, 85);">--&gt; O(n log n) // as sorting takes (n log n) time</span><span>
</span></span><span><span>Space Complexity </span><span class="token" style="color: rgb(106, 153, 85);">--&gt; O(n) // to store nodes of the all linked list</span><span>
</span></span><span><span>It paases </span><span class="token" style="color: rgb(212, 212, 212);">[</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">133</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">/</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">133</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">in</span><span> built test cases</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p><strong>Code (C++)</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(106, 153, 85);">/**
</span></span><span> * Definition for singly-linked list.
</span><span> * struct ListNode {
</span><span> *     int val;
</span><span> *     ListNode *next;
</span><span> *     ListNode() : val(0), next(nullptr) {}
</span><span> *     ListNode(int x) : val(x), next(nullptr) {}
</span><span> *     ListNode(int x, ListNode *next) : val(x), next(next) {}
</span><span> * };
</span><span><span class="token" style="color: rgb(106, 153, 85);"> */</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">mergeKLists</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> lists</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> k </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> lists</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// taking size of the list</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>k </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// if size is zero</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// simply return NULL</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// making a vector pair where first contain value and second contain node</span><span>
</span></span><span><span>        vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>pair</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span class="token" style="color: rgb(212, 212, 212);">&gt;&gt;</span><span> arr</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> k</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// traverse all over the list</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> curr_list </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> lists</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// extracting current linked list</span><span>
</span></span><span>            
</span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>curr_list </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// while current linked list is NOT NULL</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                arr</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push_back</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>curr_list </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> val</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> curr_list</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// push into vector</span><span>
</span></span><span><span>                curr_list </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> curr_list </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// this does not gurantee that k is zero, </span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// suppose an array like this [[],[],[],],here k = 3 and size of array is 0</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>arr</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// if their is no element i.e zero element</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(220, 220, 170);">sort</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>arr</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">begin</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> arr</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">end</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// sort the vector on the basis of values</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// start making links b/w the elements of vector</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> arr</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// in the next of last node put NULL</span><span>
</span></span><span><span>        arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>arr</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// return first node of the vector</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<p><em><strong>Solution - II (Further optimization in time as well as in space, Using priority queue, Accepted)-</strong></em></p>
<ul>
<li>Now, we want to become a good programmer and anyhow we want to optimize our soloution.</li>
<li>The main point is to observe here is that <em><strong>every linked list is already sorted</strong></em> and our task is just to merge them.</li>
<li>Our approach to merge linked list is same as about merge function of merge sort.</li>
<li>In merge sort, we have just two arrays / linked list but here we have 'k' linked list.</li>
<li>So by using <code>min heap</code> we compare k node values and add the smallest one to the final list.</li>
<li>One property of min heap we have to remember here is that, <em><strong>it keeps smallest element always on the top,</strong></em> so using that property we merge our k sorted linked list.</li>
</ul>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-sql" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>Suppose </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> total number </span><span class="token" style="color: rgb(86, 156, 214);">of</span><span> nodes present </span><span class="token" style="color: rgb(212, 212, 212);">in</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">all</span><span> linked list </span><span class="token" style="color: rgb(212, 212, 212);">is</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'n'</span><span> 
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">Time</span><span> Complexity </span><span class="token" style="color: rgb(106, 153, 85);">--&gt; O(n log k) // as we are using min heap</span><span>
</span></span><span><span>Space Complexity </span><span class="token" style="color: rgb(106, 153, 85);">--&gt; O(k) // at a single point of time min heap always handle the k elements</span><span>
</span></span><span><span>It paases </span><span class="token" style="color: rgb(212, 212, 212);">[</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">133</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">/</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">133</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">in</span><span> built test cases</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p><strong>Code (C++)</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(106, 153, 85);">/**
</span></span><span> * Definition for singly-linked list.
</span><span> * struct ListNode {
</span><span> *     int val;
</span><span> *     ListNode *next;
</span><span> *     ListNode() : val(0), next(nullptr) {}
</span><span> *     ListNode(int x) : val(x), next(nullptr) {}
</span><span> *     ListNode(int x, ListNode *next) : val(x), next(next) {}
</span><span> * };
</span><span><span class="token" style="color: rgb(106, 153, 85);"> */</span><span>
</span></span><span>
</span><span>
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(106, 153, 85);">// we define pair as pi</span><span>
</span></span><span><span>    </span><span class="token macro directive-hash" style="color: rgb(156, 220, 254);">#</span><span class="token macro directive" style="color: rgb(86, 156, 214);">define</span><span class="token macro" style="color: rgb(156, 220, 254);"> </span><span class="token macro macro-name" style="color: rgb(156, 220, 254);">pi</span><span class="token macro" style="color: rgb(156, 220, 254);"> </span><span class="token macro expression" style="color: rgb(156, 220, 254);">pair</span><span class="token macro expression" style="color: rgb(212, 212, 212);">&lt;</span><span class="token macro expression" style="color: rgb(86, 156, 214);">int</span><span class="token macro expression" style="color: rgb(212, 212, 212);">,</span><span class="token macro expression" style="color: rgb(156, 220, 254);"> ListNode</span><span class="token macro expression" style="color: rgb(212, 212, 212);">*</span><span class="token macro expression" style="color: rgb(156, 220, 254);"> </span><span class="token macro expression" style="color: rgb(212, 212, 212);">&gt;</span><span>
</span></span><span>    
</span><span><span>    ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">mergeKLists</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> lists</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> k </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> lists</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// taking the size of the linked list</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>k </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// if no linked list is present</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// simply return null</span><span>
</span></span><span>        
</span><span><span>        priority_queue</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>pi</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>pi</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> greater</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>pi</span><span class="token" style="color: rgb(212, 212, 212);">&gt;&gt;</span><span> minh</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// making priority queue</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> k</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// traverse from the whole array </span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> curr_list </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> lists</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// extracting current linked list</span><span>
</span></span><span>            
</span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>curr_list </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// if element present in the linked list</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                minh</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>curr_list </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> val</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> curr_list</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// push into min heap</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// this does not gurantee that k is zero, </span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// suppose an array like this [[],[],[],],here k = 3 and size of array is 0</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>minh</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// if their is no element i.e zero element</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> head </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">ListNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// can also be called as dummy</span><span>
</span></span><span><span>        ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> curr </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// make a pointer pointing to head</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>minh</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">empty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">false</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// adding further most elements to min heap</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            pair</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> temp </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> minh</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">top</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// extracting top pair</span><span>
</span></span><span><span>            minh</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// pop that pair</span><span>
</span></span><span>            
</span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>temp</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// if elements still remaining in the linked list then push them</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                minh</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>temp</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> val</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> temp</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>            
</span><span><span>            curr </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> temp</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>second</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            curr </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> curr </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>        
</span><span><span>        curr </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        head </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> head </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// move head, which is actually containg the list</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> head</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// return head</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<hr>
<p><em><strong>Solution - III (Further optimization in space, Accepted)-</strong></em></p>
<ul>
<li>Okay, the question arises, if we just have to merge k linked list,</li>
<li>Is the use of priority queue is necesssary? Can't we do it without using the priority queue?</li>
<li>The answer is <em><strong>YES</strong></em>, we can do further optimization in space complexity as well.</li>
<li>We use <code>two pointers</code> for doing this.</li>
<li>First we put start pointer to zero index and last pointer to last index and after that we start merging them thinking of as two sorted linked list.</li>
<li>And again we will continue this task until we get a single linked list.</li>
<li>See commented code, you will get it easily.</li>
</ul>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-sql" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>Suppose </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> total number </span><span class="token" style="color: rgb(86, 156, 214);">of</span><span> nodes present </span><span class="token" style="color: rgb(212, 212, 212);">in</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">all</span><span> linked list </span><span class="token" style="color: rgb(212, 212, 212);">is</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'n'</span><span> 
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">Time</span><span> Complexity </span><span class="token" style="color: rgb(106, 153, 85);">--&gt; O(n log k)</span><span>
</span></span><span><span>Space Complexity </span><span class="token" style="color: rgb(106, 153, 85);">--&gt; O(1) </span><span>
</span></span><span><span>It paases </span><span class="token" style="color: rgb(212, 212, 212);">[</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">133</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">/</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">133</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">in</span><span> built test cases</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p><strong>Code (C++)</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(106, 153, 85);">/**
</span></span><span> * Definition for singly-linked list.
</span><span> * struct ListNode {
</span><span> *     int val;
</span><span> *     ListNode *next;
</span><span> *     ListNode() : val(0), next(nullptr) {}
</span><span> *     ListNode(int x) : val(x), next(nullptr) {}
</span><span> *     ListNode(int x, ListNode *next) : val(x), next(next) {}
</span><span> * };
</span><span><span class="token" style="color: rgb(106, 153, 85);"> */</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(106, 153, 85);">// this do the same work as merge function of merging two values</span><span>
</span></span><span><span>    ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">merge</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> first</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> second</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> result </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>first </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">nullptr</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> second</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>second </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">nullptr</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> first</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>first </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> val </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> second </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> val</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            result </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> first</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            result </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">merge</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>first </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> second</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            result </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> second</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            result </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">merge</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>first</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> second </span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span> next</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> result</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">mergeKLists</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>ListNode</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> arr</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> k </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> arr</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// extracting size of array</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>k </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// if size of array is value</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> start </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// start pointer</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> last </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> k </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// last pointer</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> temp</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>last </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// if last pointer not becomes zero</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            start </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            temp </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> last</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>start </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> temp</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(106, 153, 85);">// merge them and store in one of the linked list</span><span>
</span></span><span><span>                arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>start</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">merge</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>start</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span>arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>temp</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                start</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// increment start</span><span>
</span></span><span><span>                temp</span><span class="token" style="color: rgb(212, 212, 212);">--</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// decrese start</span><span>
</span></span><span>                
</span><span><span>                </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>start </span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span> temp</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// if at any point start passes the temp</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                    last </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> temp</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>                </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> arr</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// return first linked list of the aray as now it contains the all nodes in the sorted order.</span><span>
</span></span><span>        
</span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
</div>

## Heap - Top K Frequent Elements
<div class="elfjS" data-track-load="description_content"><p>Given an integer array <code>nums</code> and an integer <code>k</code>, return <em>the</em> <code>k</code> <em>most frequent elements</em>. You may return the answer in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [1,1,1,2,2,3], k = 2
<strong>Output:</strong> [1,2]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [1], k = 1
<strong>Output:</strong> [1]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10<sup>5</sup></code></li>
	<li><code>-10<sup>4</sup> &lt;= nums[i] &lt;= 10<sup>4</sup></code></li>
	<li><code>k</code> is in the range <code>[1, the number of unique elements in the array]</code>.</li>
	<li>It is <strong>guaranteed</strong> that the answer is <strong>unique</strong>.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> Your algorithm's time complexity must be better than <code>O(n log n)</code>, where n is the array's size.</p>
</div>

### Solution

```
class Solution {
public:
    vector<int> topKFrequent(vector<int>& nums, int k) {
        unordered_map<int,int> map;
        for(int num : nums){
            map[num]++;
        }
        
        vector<int> res;
        // pair<first, second>: first is frequency,  second is number
        priority_queue<pair<int,int>> pq; 
        for(auto it = map.begin(); it != map.end(); it++){
            pq.push(make_pair(it->second, it->first));
            if(pq.size() > (int)map.size() - k){
                res.push_back(pq.top().second);
                pq.pop();
            }
        }
        return res;
    }
};
```
