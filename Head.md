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

## Heap - 
