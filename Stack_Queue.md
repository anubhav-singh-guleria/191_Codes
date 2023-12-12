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
