## 
1. [Implement Stack Using Array](#implement-stack-using-array)
2. [Implement Queue Using Array](#implement-queue-using-array)
3. [Implement Stack Using Queues](#implement-stack-using-queues)
4. [Implement Queue Using Stacks](#implement-queue-using-stacks)
5. [Valid Parentheses](#valid-parentheses)
6. [Next Greater Element I](#next-greater-element-i)
7. [Sort a Stack](#sort-a-stack)

## Implement Stack using Array

<p><strong>Problem statement:</strong> Implement a stack using an array.</p>
<p><strong>Note:</strong> Stack is a data structure that follows the <strong>Last In First Out (LIFO)</strong> rule.</p>
<p><strong>Example:</strong> </p>
<p><img class="lazy-loaded" loading="lazy" width="508" height="376" src="https://lh5.googleusercontent.com/38iOcYEofTjzGa7IlFmJVWv_2SJ5eCsdcqqNqLSur4JOk3t7X7elCFdP95KWzyr0JpyFrys8i9_QiGpdntURNzVZA3m79cc7GnWViG2-FpUwpxThzb_OCFeXqiGIMyaKgBA96RQm" data-lazy-type="image" data-src="https://lh5.googleusercontent.com/38iOcYEofTjzGa7IlFmJVWv_2SJ5eCsdcqqNqLSur4JOk3t7X7elCFdP95KWzyr0JpyFrys8i9_QiGpdntURNzVZA3m79cc7GnWViG2-FpUwpxThzb_OCFeXqiGIMyaKgBA96RQm"><noscript><img loading="lazy" width="508" height="376" src="https://lh5.googleusercontent.com/38iOcYEofTjzGa7IlFmJVWv_2SJ5eCsdcqqNqLSur4JOk3t7X7elCFdP95KWzyr0JpyFrys8i9_QiGpdntURNzVZA3m79cc7GnWViG2-FpUwpxThzb_OCFeXqiGIMyaKgBA96RQm"></noscript></p>
<p><strong>Explanation</strong>:&nbsp;</p>
<p>push(): Insert the element in the stack.</p>
<p>pop(): Remove and return the topmost element of the stack.</p>
<p>top(): Return the topmost element of the stack</p>
<p>size(): Return the number of remaining elements in the stack.</p>
<h3><strong>Solution</strong></h3>
<p class="has-vivid-red-color has-text-color"><em>Disclaimer</em>: <em>Don’t jump directly to the solution, try it out yourself first.</em></p>
<p><strong>Intuition</strong>: As we know stack works on the principle of last in first out, so we have to put elements in an array such that it keeps track of the most recently inserted element. Hence we can think of using a Top variable which will help in keeping track of recent elements inserted in the array.</p>
<p><strong>Approach</strong>:</p>
<ul><li>Declare an array of particular size.</li><li>Define a variable “Top” and initialize it as -1.</li><li>push(x): insert element is the array by increasing top by one.</li><li>pop(): check whether top is not equal to -1 if it is so, return top and decrease its value by one.</li><li>size(): return top+1.</li></ul>
<p><img class="lazy-loaded" loading="lazy" width="536" height="341" src="https://lh5.googleusercontent.com/Tf5F14Aod0nLRLP3iZtOf3VwFCOUSKaGusVMfpbtUU4pU9zb9QRbqQ8s_Uvue2RGpmsBlI4cgQALk08_7cVrxx1UW_RrULS-sPnCyriqnD8jXdFRZbU6nDP1GOgm6dCFgceVUhpq" data-lazy-type="image" data-src="https://lh5.googleusercontent.com/Tf5F14Aod0nLRLP3iZtOf3VwFCOUSKaGusVMfpbtUU4pU9zb9QRbqQ8s_Uvue2RGpmsBlI4cgQALk08_7cVrxx1UW_RrULS-sPnCyriqnD8jXdFRZbU6nDP1GOgm6dCFgceVUhpq"><noscript><img loading="lazy" width="536" height="341" src="https://lh5.googleusercontent.com/Tf5F14Aod0nLRLP3iZtOf3VwFCOUSKaGusVMfpbtUU4pU9zb9QRbqQ8s_Uvue2RGpmsBlI4cgQALk08_7cVrxx1UW_RrULS-sPnCyriqnD8jXdFRZbU6nDP1GOgm6dCFgceVUhpq"></noscript></p>

```
#include<bits/stdc++.h>

using namespace std;
class Stack {
  int size;
  int * arr;
  int top;
  public:
    Stack() {
      top = -1;
      size = 1000;
      arr = new int[size];
    }
  void push(int x) {
    top++;
    arr[top] = x;
  }
  int pop() {
    int x = arr[top];
    top--;
    return x;
  }
  int Top() {
    return arr[top];
  }
  int Size() {
    return top + 1;
  }
};
int main() {

  Stack s;
  s.push(6);
  s.push(3);
  s.push(7);
  cout << "Top of stack is before deleting any element " << s.Top() << endl;
  cout << "Size of stack before deleting any element " << s.Size() << endl;
  cout << "The element deleted is " << s.pop() << endl;
  cout << "Size of stack after deleting an element " << s.Size() << endl;
  cout << "Top of stack after deleting an element " << s.Top() << endl;
  return 0;
}
```

<p><strong>Output:</strong></p>
<p>Top of stack is before deleting any element 7<br>Size of stack before deleting any element 3<br>The element deleted is 7<br>Size of stack after deleting an element 2<br>Top of stack after deleting an element 3</p>
<p><strong>Time Complexity:</strong> O(N)</p>
<p><strong>Space Complexity:</strong> O(N)</p>
</div></div></div>
</div>
</article>

## Implement Queue Using Array

<p><strong>Problem Statement:</strong>&nbsp;Implement Queue Data Structure using Array with all functions like pop, push, top, size, etc.</p>
<p><strong>Example:</strong></p>
<pre class="wp-block-preformatted"><strong>Input</strong>: push(4)
       push(14)
       push(24)
       push(34)
       top()
       size()
       pop()

<strong>Output: </strong>

The element pushed is 4
The element pushed is 14
The element pushed is 24
The element pushed is 34
The peek of the queue before deleting any element 4
The size of the queue before deletion 4
The first element to be deleted 4
The peek of the queue after deleting an element 14
The size of the queue after deleting an element 3

</pre>
<h3><strong>Solution</strong></h3>
<p>The intuition is to fill the array in a circular manner, (ie) after popping from the front, rather than moving all the elements towards the front. We can have 2 variables to keep track of the start and end indexes of the sequence. Mod addition is done to handle boundary conditions.</p>
<p><strong>Approach</strong>:&nbsp;</p>
<p>The basic approach is to maintain two variables to point to the START and END of the filled elements in the array. START pointer is used to point to the starting index of the elements and the same case for the END pointer(ending index). Initially, both have value -1(indicating empty queue).&nbsp;</p>
<p>First, let’s see the implementation of the push function. Push basically inserts a new element at the end. So only the END variable is going to be incremented. </p>
<p><strong>Corner case 1:</strong> What if we have no empty places in the array? So, first check that, if we don’t have we exit, in the other case we increment the START variable and put the new element. </p>
<p><strong>Corner case 2:</strong> What if END reaches the last index? We are doing mod with addition. So, END goes back to index 0([0-(n-1)] will always be the range for END).</p>
<p>Second, let us see the pop function. In Queue pop removes and returns the front element. So, START needs to be modified. The general approach is to copy the current element pointed by START and increase the START variable to the next index. </p>
<p><strong>Corner case 3:</strong> What if the Queue is empty? That’s why we are checking the START variable. If it is -1, then the queue is empty, we just exit. </p>
<p><strong>Corner case 4:</strong> What if START goes out of bound? As done for END, mod addition comes to the rescue. </p>
<p><strong>Corner case 5:</strong> What happens after popping the last element? We check this state with the currSize variable. Queue returns to the initial state, both START and END are set to -1.</p>
<p>Third, let’s see the top function. It behaves more like a pop function. We need to return the element pointed by the START variable. Since we are not actually removing any element, it’s fine to ignore corner cases 4 and 5.</p>
<p>That’s all about the Queue class implementation. In the main function, we just initialize the Queue class to check all corner cases.</p>
<p><strong>Code:</strong></p>

```
#include<bits/stdc++.h>

using namespace std;
class Queue {
  int * arr;
  int start, end, currSize, maxSize;
  public:
    Queue() {
      arr = new int[16];
      start = -1;
      end = -1;
      currSize = 0;
    }

  Queue(int maxSize) {
    ( * this).maxSize = maxSize;
    arr = new int[maxSize];
    start = -1;
    end = -1;
    currSize = 0;
  }
  void push(int newElement) {
    if (currSize == maxSize) {
      cout << "Queue is full\nExiting..." << endl;
      exit(1);
    }
    if (end == -1) {
      start = 0;
      end = 0;
    } else
      end = (end + 1) % maxSize;
    arr[end] = newElement;
    cout << "The element pushed is " << newElement << endl;
    currSize++;
  }
  int pop() {
    if (start == -1) {
      cout << "Queue Empty\nExiting..." << endl;
    }
    int popped = arr[start];
    if (currSize == 1) {
      start = -1;
      end = -1;
    } else
      start = (start + 1) % maxSize;
    currSize--;
    return popped;
  }
  int top() {
    if (start == -1) {
      cout << "Queue is Empty" << endl;
      exit(1);
    }
    return arr[start];
  }
  int size() {
    return currSize;
  }

};

int main() {
  Queue q(6);
  q.push(4);
  q.push(14);
  q.push(24);
  q.push(34);
  cout << "The peek of the queue before deleting any element " << q.top() << endl;
  cout << "The size of the queue before deletion " << q.size() << endl;
  cout << "The first element to be deleted " << q.pop() << endl;
  cout << "The peek of the queue after deleting an element " << q.top() << endl;
  cout << "The size of the queue after deleting an element " << q.size() << endl;

  return 0;
}
```

<p><strong>Output:</strong></p>
<p>The element pushed is 4<br>The element pushed is 14<br>The element pushed is 24<br>The element pushed is 34<br>The peek of the queue before deleting any element 4<br>The size of the queue before deletion 4<br>The first element to be deleted 4<br>The peek of the queue after deleting an element 14<br>The size of the queue after deleting an element 3</p>
<p><strong>Time Complexity:</strong></p>
<p><strong></strong>pop function: O(1)</p>
<p>push function: O(1)</p>
<p>top function: O(1)</p>
<p>size function: O(1)</p>
<p><strong>Space Complexity:</strong></p>
<p>Whole Queue: O(n)</p>

## Implement Stack using Queues
<div class="elfjS" data-track-load="description_content"><p>Implement a last-in-first-out (LIFO) stack using only two queues. The implemented stack should support all the functions of a normal stack (<code>push</code>, <code>top</code>, <code>pop</code>, and <code>empty</code>).</p>

<p>Implement the <code>MyStack</code> class:</p>

<ul>
	<li><code>void push(int x)</code> Pushes element x to the top of the stack.</li>
	<li><code>int pop()</code> Removes the element on the top of the stack and returns it.</li>
	<li><code>int top()</code> Returns the element on the top of the stack.</li>
	<li><code>boolean empty()</code> Returns <code>true</code> if the stack is empty, <code>false</code> otherwise.</li>
</ul>

<p><b>Notes:</b></p>

<ul>
	<li>You must use <strong>only</strong> standard operations of a queue, which means that only <code>push to back</code>, <code>peek/pop from front</code>, <code>size</code> and <code>is empty</code> operations are valid.</li>
	<li>Depending on your language, the queue may not be supported natively. You may simulate a queue using a list or deque (double-ended queue) as long as you use only a queue's standard operations.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input</strong>
["MyStack", "push", "push", "top", "pop", "empty"]
[[], [1], [2], [], [], []]
<strong>Output</strong>
[null, null, null, 2, 2, false]

<strong>Explanation</strong>
MyStack myStack = new MyStack();
myStack.push(1);
myStack.push(2);
myStack.top(); // return 2
myStack.pop(); // return 2
myStack.empty(); // return False
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= x &lt;= 9</code></li>
	<li>At most <code>100</code> calls will be made to <code>push</code>, <code>pop</code>, <code>top</code>, and <code>empty</code>.</li>
	<li>All the calls to <code>pop</code> and <code>top</code> are valid.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow-up:</strong> Can you implement the stack using only one queue?</p>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>First, let's see the most easiest way: one queue.<br>
In this method,  the point is that after you add one element to the queue, rotate the queue to make the tail be the head.</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-csharp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">MyStack</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">//one Queue solution</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Queue</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> q </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">LinkedList</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">Integer</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">// Push element x onto stack.</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//rotate the queue to make the tail be the head</span><span>
</span></span><span><span>        q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">// Removes the element on top of the stack.</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">// Get the top element.</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">top</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">peek</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>        
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">// Return whether the stack is empty.</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(78, 201, 176);">boolean</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">empty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> q</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>Then, two queue ways.</p>
<p>1  Push method is inefficient.</p>
<p>when you push an element, choose one empty queue(whichever when both are empty) to add this element, and then push all elements of the other queue into the chosen queue. After that, the newest element is at the head of the chosen queue so that whenever you want to do pop() or top(), you always get the newest element.</p>
<p>For example,</p>
<p>push(1):</p>
<p>[ , ,1]    [ , , ]</p>
<p>push(2):</p>
<p>[ , , ]   [ ,1,2]</p>
<p>push(3):</p>
<p>[ 1, 2,3 ] [ , , ]</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-csharp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">MyStack</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">//using two queue. The push is inefficient.</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Queue</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> q1 </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">LinkedList</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">Integer</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Queue</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> q2 </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">LinkedList</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">Integer</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> 
</span></span><span><span>        q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span>
</span></span><span><span>        q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">top</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">?</span><span> q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">peek</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">peek</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(78, 201, 176);">boolean</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">empty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>2 pop() and top() are inefficient</p>
<p>When you push elements, choose a queue which is not empty(whichever when both are empty).<br>
When you do pop() or top(), first pop all elements of the queue except the tail into another empty queue, and then pop the tail which is your want.</p>
<p>For example:</p>
<p>push(1):</p>
<p>[ , , 1] [ , , ]</p>
<p>push(2):</p>
<p>[ ,2,1] [ , , ]</p>
<p>top();</p>
<p>[ , , 2] [ , ,1] -&gt; [ , , ] [ ,2,1]</p>
<p>pop():</p>
<p>[ , , 1] [ , ,2]  -&gt; [ , ,1] [ , , ]</p>
<p>push(3) :</p>
<p>[ ,3,1] [ , , ]</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-csharp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">MyStack</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(106, 153, 85);">//using two queue. The pop and top are inefficient.</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Queue</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> q1 </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">LinkedList</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">Integer</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Queue</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(78, 201, 176);">Integer</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> q2 </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">LinkedList</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&lt;</span><span class="token constructor-invocation" style="color: rgb(78, 201, 176);">Integer</span><span class="token constructor-invocation" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> 
</span></span><span><span>        q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span>
</span></span><span><span>        q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> size </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> size</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> size </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> size</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">top</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> res</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> size </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> size</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        res </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>res</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> size </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> size</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        res </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">poll</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(86, 156, 214);">add</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>res</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> res</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token return-type" style="color: rgb(78, 201, 176);">boolean</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">empty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> q1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> q2</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## Implement Queue using Stacks
<div class="elfjS" data-track-load="description_content"><p>Implement a first in first out (FIFO) queue using only two stacks. The implemented queue should support all the functions of a normal queue (<code>push</code>, <code>peek</code>, <code>pop</code>, and <code>empty</code>).</p>

<p>Implement the <code>MyQueue</code> class:</p>

<ul>
	<li><code>void push(int x)</code> Pushes element x to the back of the queue.</li>
	<li><code>int pop()</code> Removes the element from the front of the queue and returns it.</li>
	<li><code>int peek()</code> Returns the element at the front of the queue.</li>
	<li><code>boolean empty()</code> Returns <code>true</code> if the queue is empty, <code>false</code> otherwise.</li>
</ul>

<p><strong>Notes:</strong></p>

<ul>
	<li>You must use <strong>only</strong> standard operations of a stack, which means only <code>push to top</code>, <code>peek/pop from top</code>, <code>size</code>, and <code>is empty</code> operations are valid.</li>
	<li>Depending on your language, the stack may not be supported natively. You may simulate a stack using a list or deque (double-ended queue) as long as you use only a stack's standard operations.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input</strong>
["MyQueue", "push", "push", "peek", "pop", "empty"]
[[], [1], [2], [], [], []]
<strong>Output</strong>
[null, null, null, 1, 1, false]

<strong>Explanation</strong>
MyQueue myQueue = new MyQueue();
myQueue.push(1); // queue is: [1]
myQueue.push(2); // queue is: [1, 2] (leftmost is front of the queue)
myQueue.peek(); // return 1
myQueue.pop(); // return 1, queue is [2]
myQueue.empty(); // return false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= x &lt;= 9</code></li>
	<li>At most <code>100</code>&nbsp;calls will be made to <code>push</code>, <code>pop</code>, <code>peek</code>, and <code>empty</code>.</li>
	<li>All the calls to <code>pop</code> and <code>peek</code> are valid.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow-up:</strong> Can you implement the queue such that each operation is <strong><a href="https://en.wikipedia.org/wiki/Amortized_analysis" target="_blank">amortized</a></strong> <code>O(1)</code> time complexity? In other words, performing <code>n</code> operations will take overall <code>O(n)</code> time even if one of those operations may take longer.</p>
</div>

### Solution

```

import java.util.Stack;

//############## FIRST SOLUTION ###############
//This first solution is remove (pop) efficient as removing (popping) an element from the queue
//is taking constant amount of time, while inserting (pushing) an element in the queue is taking
//linear amount of time.
//
//Time complexity:
//
//Pop() = O(1)
//Push() = O(N)
//Peek() = O(1)

class MyQueue {

    Stack<Integer> stack1 = new Stack<>();
    Stack<Integer> stack2 = new Stack<>();

    public MyQueue() {

    }

    public void push(int x) {

        while (!stack1.isEmpty()) {
            stack2.push(stack1.pop());
        }
        stack1.push(x);

        while (!stack2.empty()) {
            stack1.push(stack2.pop());
        }
    }

    public int pop() {

        int removed = stack1.pop();
        return removed;
    }

    public int peek() {

        int top = stack1.peek();
        return top;
    }

    public boolean empty() {

        return stack1.isEmpty();
    }
}


//############## SECOND SOLUTION ###############
//This second solution is insert (push) efficient as inserting (pushing) an element into the queue
//is taking constant amount of time, while removing (popping) an element from the queue is taking
//linear amount of time.
//
//Time complexity:
//
//Pop() = O(N)
//Push() = O(1)
//Peek() = O(N)

//Note : In this peek() also has O(N) time complexity.

class MyQueue {

    Stack<Integer> stack1;
    Stack<Integer> stack2;

    public MyQueue() {

        stack1 = new Stack<>();
        stack2 = new Stack<>();
    }

    public void push(int x) {

        stack1.push(x);
    }

    public int pop() {

        while (!stack1.isEmpty()) {
            stack2.push(stack1.pop());
        }

        int removed = stack2.pop();

        while (!stack2.empty()) {
            stack1.push(stack2.pop());
        }

        return removed;
    }

    public int peek() {

        while (!stack1.isEmpty()) {
            stack2.push(stack1.pop());
        }

        int peeked = stack2.peek();

        while (!stack2.empty()) {
            stack1.push(stack2.pop());
        }

        return peeked;
    }

    public boolean empty() {

        return stack1.isEmpty();
    }
}



/**
 * Your MyQueue object will be instantiated and called as such:
 * MyQueue obj = new MyQueue();
 * obj.push(x);
 * int param_2 = obj.pop();
 * int param_3 = obj.peek();
 * boolean param_4 = obj.empty();
 */
```

## Valid Parentheses
<div class="elfjS" data-track-load="description_content"><p>Given a string <code>s</code> containing just the characters <code>'('</code>, <code>')'</code>, <code>'{'</code>, <code>'}'</code>, <code>'['</code> and <code>']'</code>, determine if the input string is valid.</p>

<p>An input string is valid if:</p>

<ol>
	<li>Open brackets must be closed by the same type of brackets.</li>
	<li>Open brackets must be closed in the correct order.</li>
	<li>Every close bracket has a corresponding open bracket of the same type.</li>
</ol>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> s = "()"
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> s = "()[]{}"
<strong>Output:</strong> true
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> s = "(]"
<strong>Output:</strong> false
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>4</sup></code></li>
	<li><code>s</code> consists of parentheses only <code>'()[]{}'</code>.</li>
</ul>
</div>

###  Solution

```
class Solution {
public:
    bool isValid(string s) {
        stack<char> st; // create an empty stack to store opening brackets
        for (char c : s) { // loop through each character in the string
            if (c == '(' || c == '{' || c == '[') { // if the character is an opening bracket
                st.push(c); // push it onto the stack
            } else { // if the character is a closing bracket
                if (st.empty() || // if the stack is empty or 
                    (c == ')' && st.top() != '(') || // the closing bracket doesn't match the corresponding opening bracket at the top of the stack
                    (c == '}' && st.top() != '{') ||
                    (c == ']' && st.top() != '[')) {
                    return false; // the string is not valid, so return false
                }
                st.pop(); // otherwise, pop the opening bracket from the stack
            }
        }
        return st.empty(); // if the stack is empty, all opening brackets have been matched with their corresponding closing brackets,
                           // so the string is valid, otherwise, there are unmatched opening brackets, so return false
    }
};
```

## Next Greater Element I
<div class="elfjS" data-track-load="description_content"><p>The <strong>next greater element</strong> of some element <code>x</code> in an array is the <strong>first greater</strong> element that is <strong>to the right</strong> of <code>x</code> in the same array.</p>

<p>You are given two <strong>distinct 0-indexed</strong> integer arrays <code>nums1</code> and <code>nums2</code>, where <code>nums1</code> is a subset of <code>nums2</code>.</p>

<p>For each <code>0 &lt;= i &lt; nums1.length</code>, find the index <code>j</code> such that <code>nums1[i] == nums2[j]</code> and determine the <strong>next greater element</strong> of <code>nums2[j]</code> in <code>nums2</code>. If there is no next greater element, then the answer for this query is <code>-1</code>.</p>

<p>Return <em>an array </em><code>ans</code><em> of length </em><code>nums1.length</code><em> such that </em><code>ans[i]</code><em> is the <strong>next greater element</strong> as described above.</em></p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums1 = [4,1,2], nums2 = [1,3,4,2]
<strong>Output:</strong> [-1,3,-1]
<strong>Explanation:</strong> The next greater element for each value of nums1 is as follows:
- 4 is underlined in nums2 = [1,3,<u>4</u>,2]. There is no next greater element, so the answer is -1.
- 1 is underlined in nums2 = [<u>1</u>,3,4,2]. The next greater element is 3.
- 2 is underlined in nums2 = [1,3,4,<u>2</u>]. There is no next greater element, so the answer is -1.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums1 = [2,4], nums2 = [1,2,3,4]
<strong>Output:</strong> [3,-1]
<strong>Explanation:</strong> The next greater element for each value of nums1 is as follows:
- 2 is underlined in nums2 = [1,<u>2</u>,3,4]. The next greater element is 3.
- 4 is underlined in nums2 = [1,2,3,<u>4</u>]. There is no next greater element, so the answer is -1.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums1.length &lt;= nums2.length &lt;= 1000</code></li>
	<li><code>0 &lt;= nums1[i], nums2[i] &lt;= 10<sup>4</sup></code></li>
	<li>All integers in <code>nums1</code> and <code>nums2</code> are <strong>unique</strong>.</li>
	<li>All the integers of <code>nums1</code> also appear in <code>nums2</code>.</li>
</ul>

<p>&nbsp;</p>
<strong>Follow up:</strong> Could you find an <code>O(nums1.length + nums2.length)</code> solution?</div>

### Solution
<div class="FN9Jv WRmCx"><h4 id="approach">Approach:</h4>
<p>The idea here is to create a map which will have the mapping of each element from the bigger array (<code>nums2[]</code>) and its corresponding greater element. In order to do that we are using a monotone stack in increasing order (top element is smaller than the element below in the stack).</p>
<h4 id="algorithm">Algorithm:</h4>
<ul>
<li>We iterate through <code>nums2[]</code> and push each element into a stack.</li>
<li>If the current element in the iteration is greater than the top most element in the stack, then we pop it out and add the popped out element as key and the current element as the value (next greater number).</li>
<li>We repeat this process as long as the current element is greater than the top most element in the stack or the stack is empty.</li>
<li>The current element is also added to the stack.</li>
<li>The last element in the <code>nums2[]</code> will not have a next element. Hence we are not adding that to the map.</li>
<li>Similarly if there are elements in the stack which does not have a next greater element, remains in the stack and is not moved to the map as the requirement for these elements is to default it to  -1, which is being taken care while fetching values from the map.</li>
</ul>
<h4 id="code">Code:</h4>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-dart" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    public int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">nextGreaterElement</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> nums1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> nums2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> result </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> int</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>nums1</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>length</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">Stack</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(78, 201, 176);">Integer</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span> stack</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Stack</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(78, 201, 176);">Map</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(78, 201, 176);">Integer</span><span class="token generics" style="color: rgb(212, 212, 212);">,</span><span class="token generics"> </span><span class="token generics" style="color: rgb(78, 201, 176);">Integer</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span> map </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">HashMap</span><span class="token generics" style="color: rgb(212, 212, 212);">&lt;</span><span class="token generics" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>int num</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> nums2</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>            
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>stack</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">isEmpty</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> num </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> stack</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">peek</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>                map</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">put</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>stack</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">pop</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> num</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            stack</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">push</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>num</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>            
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>        
</span><span><span>        int i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>        
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>int num </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> nums1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>            result</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> map</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">getOrDefault</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>num</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> result</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## Sort a Stack	
<h4><strong>Solution idea</strong></h4>
<p>This idea is similar to the recursive insertion sort, where we pop the top element from the stack and sort the remaining (n - 1) size stack recursively using the same function. After sorting the (n - 1) size stack, we use another helper function&nbsp;<strong>insertTop(s, topElement)</strong>, to insert the top element into the current position of the sorted stack.</p>
<p>Implementation of the&nbsp;<strong>insertTop(s, topElement)</strong>&nbsp;function</p>
<ul>
<li>If the stack is empty or topElement is less than the top, we push it into the stack and return.</li>
<li>Otherwise, we insert the topElement into the correct position of the sorted stack. For this, we recursively pop out each stack element and call the same function to insert the elements again in the stack in sorted order.</li>
</ul>

<pre class="language-cpp"><code class="language-cpp"><span class="token keyword">void</span> <span class="token function">insertTop</span><span class="token punctuation">(</span>stack<span class="token operator">&lt;</span><span class="token keyword">int</span><span class="token operator">&gt;</span><span class="token operator">&amp;</span> s<span class="token punctuation">,</span> <span class="token keyword">int</span> topElement<span class="token punctuation">)</span>
<span class="token punctuation">{</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span>s<span class="token punctuation">.</span><span class="token function">empty</span><span class="token punctuation">(</span><span class="token punctuation">)</span> <span class="token operator">||</span> topElement <span class="token operator">&lt;</span> s<span class="token punctuation">.</span><span class="token function">top</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span>
    <span class="token punctuation">{</span>
        s<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>topElement<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token keyword">return</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
    
    <span class="token keyword">int</span> temp <span class="token operator">=</span> s<span class="token punctuation">.</span><span class="token function">top</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    s<span class="token punctuation">.</span><span class="token function">pop</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token function">insertTop</span><span class="token punctuation">(</span>s<span class="token punctuation">,</span> topElement<span class="token punctuation">)</span><span class="token punctuation">;</span>
    s<span class="token punctuation">.</span><span class="token function">push</span><span class="token punctuation">(</span>temp<span class="token punctuation">)</span><span class="token punctuation">;</span>
<span class="token punctuation">}</span>

<span class="token keyword">void</span> <span class="token function">sortStack</span><span class="token punctuation">(</span>stack<span class="token operator">&lt;</span><span class="token keyword">int</span><span class="token operator">&gt;</span><span class="token operator">&amp;</span> s<span class="token punctuation">)</span>
<span class="token punctuation">{</span>
    <span class="token keyword">if</span> <span class="token punctuation">(</span><span class="token operator">!</span>s<span class="token punctuation">.</span><span class="token function">empty</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">)</span> 
    <span class="token punctuation">{</span>
        <span class="token keyword">int</span> topElement <span class="token operator">=</span> s<span class="token punctuation">.</span><span class="token function">top</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        s<span class="token punctuation">.</span><span class="token function">pop</span><span class="token punctuation">(</span><span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token function">sortStack</span><span class="token punctuation">(</span>s<span class="token punctuation">)</span><span class="token punctuation">;</span>
        <span class="token function">insertTop</span><span class="token punctuation">(</span>s<span class="token punctuation">,</span> topElement<span class="token punctuation">)</span><span class="token punctuation">;</span>
    <span class="token punctuation">}</span>
<span class="token punctuation">}</span></code></pre>
