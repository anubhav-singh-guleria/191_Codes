## Table of Content

## Reverse Words in a String
<div class="elfjS" data-track-load="description_content"><p>Given an input string <code>s</code>, reverse the order of the <strong>words</strong>.</p>

<p>A <strong>word</strong> is defined as a sequence of non-space characters. The <strong>words</strong> in <code>s</code> will be separated by at least one space.</p>

<p>Return <em>a string of the words in reverse order concatenated by a single space.</em></p>

<p><b>Note</b> that <code>s</code> may contain leading or trailing spaces or multiple spaces between two words. The returned string should only have a single space separating the words. Do not include any extra spaces.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> s = "the sky is blue"
<strong>Output:</strong> "blue is sky the"
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> s = "  hello world  "
<strong>Output:</strong> "world hello"
<strong>Explanation:</strong> Your reversed string should not contain leading or trailing spaces.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> s = "a good   example"
<strong>Output:</strong> "example good a"
<strong>Explanation:</strong> You need to reduce multiple spaces between two words to a single space in the reversed string.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 10<sup>4</sup></code></li>
	<li><code>s</code> contains English letters (upper-case and lower-case), digits, and spaces <code>' '</code>.</li>
	<li>There is <strong>at least one</strong> word in <code>s</code>.</li>
</ul>

<p>&nbsp;</p>
<p><b data-stringify-type="bold">Follow-up:&nbsp;</b>If the string data type is mutable in your language, can&nbsp;you solve it&nbsp;<b data-stringify-type="bold">in-place</b>&nbsp;with&nbsp;<code data-stringify-type="code">O(1)</code>&nbsp;extra space?</p>
</div>

### Solution

```
string reverseWords(string s) {
        if(s.size() == 0) return s;
        stack<string> stack;
        string result;
        for(int i=0; i<s.size(); i++) {
            string word;
            if(s[i]==' ') continue; //skip spaces
            while(i<s.size() && s[i]!=' ' ) { //store continuous letters into word
                word += s[i]; i++;
            }
            stack.push(word); //push word to the stack
        }
        while(!stack.empty()) {
            result += stack.top(); stack.pop();
            if(!stack.empty()) result += " ";
        }
        return result;
    }
};
```

## Go To
[Table of Content](#table-of-content)
## Longest Palindromic Substring
<div class="elfjS" data-track-load="description_content"><p>Given a string <code>s</code>, return <em>the longest</em> <span data-keyword="palindromic-string" class=" cursor-pointer relative text-dark-blue-s text-sm"><div class="popover-wrapper inline-block" data-headlessui-state=""><div><div aria-expanded="false" data-headlessui-state="" id="headlessui-popover-button-:rr:"><div><em>palindromic</em></div></div><div style="position: fixed; z-index: 40; inset: 0px auto auto 0px; transform: translate(282px, 182px);"></div></div></div></span> <span data-keyword="substring-nonempty" class=" cursor-pointer relative text-dark-blue-s text-sm"><div class="popover-wrapper inline-block" data-headlessui-state=""><div><div aria-expanded="false" data-headlessui-state="" id="headlessui-popover-button-:rt:"><div><em>substring</em></div></div><div style="position: fixed; z-index: 40; inset: 0px auto auto 0px; transform: translate(350px, 182px);"></div></div></div></span> in <code>s</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> s = "babad"
<strong>Output:</strong> "bab"
<strong>Explanation:</strong> "aba" is also a valid answer.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> s = "cbbd"
<strong>Output:</strong> "bb"
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 1000</code></li>
	<li><code>s</code> consist of only digits and English letters.</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>I had trouble understanding this question, as I am not much good when it comes to DP, and also because no solution offered enough explanation for DP newbies, so here I am going to try my best to explain it in detail.</p>
<p><strong>Question Interpretation:</strong> To solve a question , we first have to understand it!<br>
Here we are being asked to calculate longest substring which is a Palindrome(Palindrome is a string which is read same forwards and backwards), among all the Palindromes that exist!!</p>
<p><strong>Intuition:</strong> Now, we can solve this question in two ways that come at first glance:</p>
<ul>
<li>Use <code>Brute Force</code> : Check for every corresponding element in string the longest palindrome possible and do it till the end.</li>
<li><code>DP</code>: Since we are essentially looping over every element in <code>Brute Force</code>, maybe we can somehow use the result from our previous iteration to simplify the current one, right?? This gives us a nudge to look for a pattern and hence we go for DP.</li>
</ul>
<p><strong>Analysis:</strong><br>
Lets see both the approaches one by one !!!</p>
<p>1.)<code>Brute Force:</code> Instead of directly going to code and finding a problem later, lets stop and think about the concept we intend to use here .</p>
<p><em>Concept:</em> We will go through <strong>all</strong> possible element in string and find the longest palindrome amongst them.</p>
<p><em>Review:</em> To calculate <strong>all</strong> the possible substrings in a string of length <code>n</code> ,number of combinations generated are:<br>
<code>1+2+3+4+..........n</code>=<code>n(n-1)/2</code>.<br>
<code>==&gt;</code> To check all the substrings for Palindrome, we will have to go through <strong>all the <code>n</code> characters</strong><br>
<code>==&gt;</code> <strong>Total</strong> Combinations: <code>n*n(n-1)/2</code>= <code>O(n^3)</code></p>
<p><em>Conclusion:</em> Since the time complexity is <code>O(n^3)</code>, hence we will not discuss on this approach, and our energy would be better spent looking at <code>DP</code> solution .</p>
<p>2.)<code>DP:</code> Instead of going through all the previous Palindromes again and again, how about we save them somewhere and calculate the new ones based on them, but how do we d that? Lets see it below</p>
<p><em>Concept:</em> To check a Palindrome of length ,say <code>l</code>,  we just have to check if<br>
i.) <code>s[first character]==s[last character]</code><br>
ii.) <code>s[first character+1, last charcter -1]</code> is a Palindrome</p>
<p>For example : say s=" balab"<br>
Now, to check , if "s" is Palindrome or not, we just have to look at<br>
i.) <code>s[first character]==s[last character]</code> -&gt; b==b -&gt; True<br>
ii.)<code>s[first character+1, last charcter -1]</code> is a Palindrome --&gt; "aba" is a Palindrome??<br>
To check for "aba", a==a--&gt; True , and "b" is a Palindrome(of length 1)<br>
==&gt; <code>s</code> is a Plaindrome</p>
<p><em>Review:</em> We will make a table <code>dp</code> containing if the string from <code>left</code> to <code>right</code> is a Pal. or not, and to do that, we will fill in the table with <code>1</code> or <code>0</code>.<br>
Lets look at an example of how the table looks like for <code>s:"geeks"</code><br>
<img src="https://assets.leetcode.com/users/images/cccbc507-96ac-45d8-a3fb-9658fc007fc7_1616569419.1798341.png" alt="image"></p>
<p>For <code>s:geeks:</code><br>
<code>dp[i][i]</code>=1, as single letters are always Palindromes<br>
<code>dp[1][2]</code> : string from starting position 1 to ending position 2 are Pal. or not (since "ee" is, hence we fill the table with "1")<br>
and likewise for others.</p>
<p>This reduces our time from <code>O(n^3)</code> to <code>O(n^2)</code> as we dont have to check every possible combination now, instead we can directly check the value being 1 or 0.</p>
<p><strong>Code:</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-go" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>class Solution </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>     </span><span class="token" style="color: rgb(206, 145, 120);">string</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">longestPalindrome</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(206, 145, 120);">string</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> 
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>   
</span></span><span><span>    </span><span class="token" style="color: rgb(206, 145, 120);">int</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">len</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(206, 145, 120);">int</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(206, 145, 120);">len</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(206, 145, 120);">len</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(220, 220, 170);">memset</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>dp</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span class="token" style="color: rgb(220, 220, 170);">sizeof</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>dp</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(206, 145, 120);">int</span><span> end</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(206, 145, 120);">int</span><span> start</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>	
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(206, 145, 120);">int</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(206, 145, 120);">len</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(206, 145, 120);">int</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(206, 145, 120);">len</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span> dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>start</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>end</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(206, 145, 120);">int</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(206, 145, 120);">len</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(206, 145, 120);">int</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">len</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>  
</span></span><span><span>            </span><span class="token" style="color: rgb(206, 145, 120);">int</span><span> left</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//start point</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(206, 145, 120);">int</span><span> right </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>  </span><span class="token" style="color: rgb(106, 153, 85);">//ending point</span><span>
</span></span><span>            
</span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> 
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                dp</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>left</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>right</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> start</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> end</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>        
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>   </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">substr</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>start</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> end</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
	
## Go To
[Table of Content](#table-of-content)
	
## Roman to Integer
<div class="elfjS" data-track-load="description_content"><p>Roman numerals are represented by seven different symbols:&nbsp;<code>I</code>, <code>V</code>, <code>X</code>, <code>L</code>, <code>C</code>, <code>D</code> and <code>M</code>.</p>

<pre><strong>Symbol</strong>       <strong>Value</strong>
I             1
V             5
X             10
L             50
C             100
D             500
M             1000</pre>

<p>For example,&nbsp;<code>2</code> is written as <code>II</code>&nbsp;in Roman numeral, just two ones added together. <code>12</code> is written as&nbsp;<code>XII</code>, which is simply <code>X + II</code>. The number <code>27</code> is written as <code>XXVII</code>, which is <code>XX + V + II</code>.</p>

<p>Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not <code>IIII</code>. Instead, the number four is written as <code>IV</code>. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as <code>IX</code>. There are six instances where subtraction is used:</p>

<ul>
	<li><code>I</code> can be placed before <code>V</code> (5) and <code>X</code> (10) to make 4 and 9.&nbsp;</li>
	<li><code>X</code> can be placed before <code>L</code> (50) and <code>C</code> (100) to make 40 and 90.&nbsp;</li>
	<li><code>C</code> can be placed before <code>D</code> (500) and <code>M</code> (1000) to make 400 and 900.</li>
</ul>

<p>Given a roman numeral, convert it to an integer.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> s = "III"
<strong>Output:</strong> 3
<strong>Explanation:</strong> III = 3.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> s = "LVIII"
<strong>Output:</strong> 58
<strong>Explanation:</strong> L = 50, V= 5, III = 3.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> s = "MCMXCIV"
<strong>Output:</strong> 1994
<strong>Explanation:</strong> M = 1000, CM = 900, XC = 90 and IV = 4.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length &lt;= 15</code></li>
	<li><code>s</code> contains only&nbsp;the characters <code>('I', 'V', 'X', 'L', 'C', 'D', 'M')</code>.</li>
	<li>It is <strong>guaranteed</strong>&nbsp;that <code>s</code> is a valid roman numeral in the range <code>[1, 3999]</code>.</li>
</ul>
</div>

### Solution 
<div class="FN9Jv WRmCx"><p><strong>Certainly! Let's break down the code and provide a clear intuition and explanation, using the examples "IX" and "XI" to demonstrate its functionality.</strong></p>
<h1 id="intuition">Intuition:</h1>
<p>The key intuition lies in the fact that in Roman numerals, when a smaller value appears before a larger value, it represents subtraction, while when a smaller value appears after or equal to a larger value, it represents addition.</p>
<h1 id="explanation">Explanation:</h1>
<ol>
<li>
<p>The unordered map <code>m</code> is created and initialized with mappings between Roman numeral characters and their corresponding integer values. For example, 'I' is mapped to 1, 'V' to 5, 'X' to 10, and so on.</p>
</li>
<li>
<p>The variable <code>ans</code> is initialized to 0. This variable will accumulate the final integer value of the Roman numeral string.</p>
</li>
<li>
<p>The for loop iterates over each character in the input string <code>s</code>.<br>
<strong>For the example "IX":</strong></p>
<ul>
<li>
<p>When <code>i</code> is 0, the current character <code>s[i]</code> is 'I'. Since there is a next character ('X'), and the value of 'I' (1) is less than the value of 'X' (10), the condition <code>m[s[i]] &lt; m[s[i+1]]</code> is true. In this case, we subtract the value of the current character from <code>ans</code>.</p>
<p><code>ans -= m[s[i]];</code><br>
<code>ans -= m['I'];</code><br>
<code>ans -= 1;</code><br>
<code>ans</code> becomes -1.</p>
</li>
<li>
<p>When <code>i</code> is 1, the current character <code>s[i]</code> is 'X'. This is the last character in the string, so there is no next character to compare. Since there is no next character, we don't need to evaluate the condition. In this case, we add the value of the current character to <code>ans</code>.</p>
<p><code>ans += m[s[i]];</code><br>
<code>ans += m['X'];</code><br>
<code>ans += 10;</code><br>
<code>ans</code> becomes 9.</p>
</li>
</ul>
<p><strong>For the example "XI":</strong></p>
<ul>
<li>
<p>When <code>i</code> is 0, the current character <code>s[i]</code> is 'X'. Since there is a next character ('I'), and the value of 'X' (10) is greater than the value of 'I' (1), the condition <code>m[s[i]] &lt; m[s[i+1]]</code> is false. In this case, we add the value of the current character to <code>ans</code>.</p>
<p><code>ans += m[s[i]];</code><br>
<code>ans += m['X'];</code><br>
<code>ans += 10;</code><br>
<code>ans</code> becomes 10.</p>
</li>
<li>
<p>When <code>i</code> is 1, the current character <code>s[i]</code> is 'I'. This is the last character in the string, so there is no next character to compare. Since there is no next character, we don't need to evaluate the condition. In this case, we add the value of the current character to <code>ans</code>.</p>
<p><code>ans += m[s[i]];</code><br>
<code>ans += m['I'];</code><br>
<code>ans += 1;</code><br>
<code>ans</code> becomes 11.</p>
</li>
</ul>
</li>
<li>
<p>After the for loop, the accumulated value in <code>ans</code> represents the integer conversion of the Roman numeral string, and it is returned as the result.</p>
</li>
</ol>
<h1 id="code">Code</h1>
<div class="border-gray-3 dark:border-dark-gray-3 mb-6 overflow-hidden rounded-lg border"><div class="flex select-none bg-layer-2 dark:bg-dark-layer-2"><div class="relative cursor-pointer px-3 py-3 text-label-1 dark:text-dark-label-1 font-medium EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div><div class="relative cursor-pointer px-3 py-3 text-label-4 dark:text-dark-label-4 hover:text-label-1 dark:hover:text-dark-label-1 EoHqa"></div></div><div class="px-3 py-2.5 bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">romanToInt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>string s</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        unordered_map</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">char</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> m</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        m</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(206, 145, 120);">'I'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        m</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(206, 145, 120);">'V'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">5</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        m</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(206, 145, 120);">'X'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">10</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        m</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(206, 145, 120);">'L'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">50</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        m</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(206, 145, 120);">'C'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">100</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        m</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(206, 145, 120);">'D'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">500</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        m</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(206, 145, 120);">'M'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1000</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> ans </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>m</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> m</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                ans </span><span class="token" style="color: rgb(212, 212, 212);">-=</span><span> m</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>                ans </span><span class="token" style="color: rgb(212, 212, 212);">+=</span><span> m</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> ans</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## Go To
[Table of Content](#table-of-content)

## Integer to Roman 
<div class="elfjS" data-track-load="description_content"><p>Roman numerals are represented by seven different symbols:&nbsp;<code>I</code>, <code>V</code>, <code>X</code>, <code>L</code>, <code>C</code>, <code>D</code> and <code>M</code>.</p>

<pre><strong>Symbol</strong>       <strong>Value</strong>
I             1
V             5
X             10
L             50
C             100
D             500
M             1000</pre>

<p>For example,&nbsp;<code>2</code> is written as <code>II</code>&nbsp;in Roman numeral, just two one's added together. <code>12</code> is written as&nbsp;<code>XII</code>, which is simply <code>X + II</code>. The number <code>27</code> is written as <code>XXVII</code>, which is <code>XX + V + II</code>.</p>

<p>Roman numerals are usually written largest to smallest from left to right. However, the numeral for four is not <code>IIII</code>. Instead, the number four is written as <code>IV</code>. Because the one is before the five we subtract it making four. The same principle applies to the number nine, which is written as <code>IX</code>. There are six instances where subtraction is used:</p>

<ul>
	<li><code>I</code> can be placed before <code>V</code> (5) and <code>X</code> (10) to make 4 and 9.&nbsp;</li>
	<li><code>X</code> can be placed before <code>L</code> (50) and <code>C</code> (100) to make 40 and 90.&nbsp;</li>
	<li><code>C</code> can be placed before <code>D</code> (500) and <code>M</code> (1000) to make 400 and 900.</li>
</ul>

<p>Given an integer, convert it to a roman numeral.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> num = 3
<strong>Output:</strong> "III"
<strong>Explanation:</strong> 3 is represented as 3 ones.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> num = 58
<strong>Output:</strong> "LVIII"
<strong>Explanation:</strong> L = 50, V = 5, III = 3.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> num = 1994
<strong>Output:</strong> "MCMXCIV"
<strong>Explanation:</strong> M = 1000, CM = 900, XC = 90 and IV = 4.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= num &lt;= 3999</code></li>
</ul>
</div>

### Solution

```
class Solution {
public:
    const int val[13] = {1000,900,500,400,100,90,50,40,10,9,5,4,1};
    const string rom[13] = {"M","CM","D","CD","C","XC","L","XL","X","IX","V","IV","I"};

    string intToRoman(int N) {
        string ans = "";
        for (int i = 0; N; i++)
            while (N >= val[i]) ans += rom[i], N -= val[i];
        return ans;
    }
};
```
## Go To
[Table of Content](#table-of-content)

## String to Integer (atoi)
<div class="elfjS" data-track-load="description_content"><p>Implement the <code>myAtoi(string s)</code> function, which converts a string to a 32-bit signed integer (similar to C/C++'s <code>atoi</code> function).</p>

<p>The algorithm for <code>myAtoi(string s)</code> is as follows:</p>

<ol>
	<li>Read in and ignore any leading whitespace.</li>
	<li>Check if the next character (if not already at the end of the string) is <code>'-'</code> or <code>'+'</code>. Read this character in if it is either. This determines if the final result is negative or positive respectively. Assume the result is positive if neither is present.</li>
	<li>Read in next the characters until the next non-digit character or the end of the input is reached. The rest of the string is ignored.</li>
	<li>Convert these digits into an integer (i.e. <code>"123" -&gt; 123</code>, <code>"0032" -&gt; 32</code>). If no digits were read, then the integer is <code>0</code>. Change the sign as necessary (from step 2).</li>
	<li>If the integer is out of the 32-bit signed integer range <code>[-2<sup>31</sup>, 2<sup>31</sup> - 1]</code>, then clamp the integer so that it remains in the range. Specifically, integers less than <code>-2<sup>31</sup></code> should be clamped to <code>-2<sup>31</sup></code>, and integers greater than <code>2<sup>31</sup> - 1</code> should be clamped to <code>2<sup>31</sup> - 1</code>.</li>
	<li>Return the integer as the final result.</li>
</ol>

<p><strong>Note:</strong></p>

<ul>
	<li>Only the space character <code>' '</code> is considered a whitespace character.</li>
	<li><strong>Do not ignore</strong> any characters other than the leading whitespace or the rest of the string after the digits.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> s = "42"
<strong>Output:</strong> 42
<strong>Explanation:</strong> The underlined characters are what is read in, the caret is the current reader position.
Step 1: "42" (no characters read because there is no leading whitespace)
         ^
Step 2: "42" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "<u>42</u>" ("42" is read in)
           ^
The parsed integer is 42.
Since 42 is in the range [-2<sup>31</sup>, 2<sup>31</sup> - 1], the final result is 42.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> s = "   -42"
<strong>Output:</strong> -42
<strong>Explanation:</strong>
Step 1: "<u>   </u>-42" (leading whitespace is read and ignored)
            ^
Step 2: "   <u>-</u>42" ('-' is read, so the result should be negative)
             ^
Step 3: "   -<u>42</u>" ("42" is read in)
               ^
The parsed integer is -42.
Since -42 is in the range [-2<sup>31</sup>, 2<sup>31</sup> - 1], the final result is -42.
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> s = "4193 with words"
<strong>Output:</strong> 4193
<strong>Explanation:</strong>
Step 1: "4193 with words" (no characters read because there is no leading whitespace)
         ^
Step 2: "4193 with words" (no characters read because there is neither a '-' nor '+')
         ^
Step 3: "<u>4193</u> with words" ("4193" is read in; reading stops because the next character is a non-digit)
             ^
The parsed integer is 4193.
Since 4193 is in the range [-2<sup>31</sup>, 2<sup>31</sup> - 1], the final result is 4193.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>0 &lt;= s.length &lt;= 200</code></li>
	<li><code>s</code> consists of English letters (lower-case and upper-case), digits (<code>0-9</code>), <code>' '</code>, <code>'+'</code>, <code>'-'</code>, and <code>'.'</code>.</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p><strong>Let's understand this problem with all possible testcases.</strong><br>
<img src="https://assets.leetcode.com/users/images/c6a8113d-c9cc-44be-8ccc-9d2a33770d22_1642121693.8403566.png" alt="image"></p>
<ol>
<li>If we look at <strong>1st testcase</strong>. We have Given a string with numerical values &amp; we will simply return in Integral value and <strong>return 42</strong>.</li>
<li>If we look at <strong>2nd testcase</strong>. First we see we have some space "and it's clearly mentioned in question, we need to <strong>discard whitespace</strong>", then we <strong>takecare of sign</strong> &amp; use sign as it is &amp; finally use numerical value <strong>return -42</strong>.</li>
<li>If we look at <strong>3rd testcase</strong>. We look for <strong>whitespace</strong>, but we <strong>dont have</strong> it. Then we will see wether it have a <strong>sign</strong> or not. Then we will see wether the <strong>1st value numerical</strong> or not. So, we found it is and simply go for <strong>4193</strong>, again we will check after this numerical value do we have more numerical value &amp; <strong>states No</strong>. then we simply <strong>return 4193</strong></li>
<li>Coming to <strong>4th testcase</strong>. We see that it dont have whitespace, dont have any sign. And very first sequence is non-numerical and simply <strong>return 0</strong></li>
<li>Coming to <strong>5th testcase</strong>. We clearly see that no is <strong>out of range</strong>, we simply <strong>return -2^31</strong>.</li>
</ol>
<p><strong>What rules we can get from these testcases are:</strong><br>
<img src="https://assets.leetcode.com/users/images/ce10b71e-950a-4ee4-8caf-255c2d87c5f2_1642122439.133612.png" alt="image"></p>
<p><code>By keeping these condition's in mind we can simply write up our code:</code></p>
<p><strong>Java</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-kotlin" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> Solution </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> int </span><span class="token" style="color: rgb(220, 220, 170);">myAtoi</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>String s</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">equals</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token string-literal singleline" style="color: rgb(206, 145, 120);">""</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>		
</span><span><span>		</span><span class="token" style="color: rgb(106, 153, 85);">// helper variables</span><span>
</span></span><span><span>		int res </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> i </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> sign </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>		
</span><span><span>		</span><span class="token" style="color: rgb(106, 153, 85);">// get rid of whitespace</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">' '</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>			i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>		
</span><span><span>		</span><span class="token" style="color: rgb(106, 153, 85);">// check for sign</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'+'</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">||</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'-'</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(106, 153, 85);">// change if negative, iterate</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'-'</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>				sign </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>		
</span><span><span>		</span><span class="token" style="color: rgb(106, 153, 85);">// now iterate across digits if any</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(106, 153, 85);">// should only be in range 0-9</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(86, 156, 214);">while</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'0'</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'9'</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(106, 153, 85);">// check if we will go over the max</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>res </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> Integer</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>MAX_VALUE </span><span class="token" style="color: rgb(212, 212, 212);">/</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">10</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">||</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>res </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> Integer</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>MAX_VALUE </span><span class="token" style="color: rgb(212, 212, 212);">/</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">10</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'0'</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">7</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>				</span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>sign </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>					</span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> Integer</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>MIN_VALUE</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>				</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>				</span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> Integer</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>MAX_VALUE</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>			
</span><span><span>			</span><span class="token" style="color: rgb(106, 153, 85);">// update res</span><span>
</span></span><span><span>			res </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> res </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">10</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">charAt</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'0'</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> sign </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span> res</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p><strong>C++</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-csharp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token return-type" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">myAtoi</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">string</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// helper variables</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> res</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> sign</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>		
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(206, 145, 120);">' '</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>  </span><span class="token" style="color: rgb(106, 153, 85);">//ignore leading white space</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(206, 145, 120);">'-'</span><span class="token" style="color: rgb(212, 212, 212);">||</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(206, 145, 120);">'+'</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>          </span><span class="token" style="color: rgb(106, 153, 85);">//check if number positve or negative</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            sign</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(206, 145, 120);">'-'</span><span class="token" style="color: rgb(212, 212, 212);">?</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(106, 153, 85);">// now iterate across digits if any</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(106, 153, 85);">// should only be in range 0-9</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span class="token" style="color: rgb(206, 145, 120);">'0'</span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">&lt;=</span><span class="token" style="color: rgb(206, 145, 120);">'9'</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>  </span><span class="token" style="color: rgb(106, 153, 85);">//traverse string till nondigit not found or string ends</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> digit</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(206, 145, 120);">'0'</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>sign</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>sign</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>res</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span>INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">/</span><span class="token" style="color: rgb(181, 206, 168);">10</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">||</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>res</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span>INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">/</span><span class="token" style="color: rgb(181, 206, 168);">10</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> digit</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span>INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">%</span><span class="token" style="color: rgb(181, 206, 168);">10</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> INT_MAX</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//check for overflow</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>sign</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>res</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>INT_MIN</span><span class="token" style="color: rgb(212, 212, 212);">/</span><span class="token" style="color: rgb(181, 206, 168);">10</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">||</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>res</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span>INT_MIN</span><span class="token" style="color: rgb(212, 212, 212);">/</span><span class="token" style="color: rgb(181, 206, 168);">10</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> digit</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>INT_MIN</span><span class="token" style="color: rgb(212, 212, 212);">%</span><span class="token" style="color: rgb(181, 206, 168);">10</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> INT_MIN</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//check for underflow</span><span>
</span></span><span>            
</span><span><span>            res</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>res</span><span class="token" style="color: rgb(212, 212, 212);">*</span><span class="token" style="color: rgb(181, 206, 168);">10</span><span class="token" style="color: rgb(212, 212, 212);">+</span><span>digit</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// update res</span><span>
</span></span><span><span>            i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> res</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div>
<p>ANALYSIS :-</p>
<ul>
<li>
<p><strong>Time Complexity :-</strong> BigO(N) where N is string length;</p>
</li>
<li>
<p><strong>Space Complexity :-</strong> BigO(1) as not using extra memory</p>
</li>
</ul></div>

## Go To
[Table of Content](#table-of-content)

## Longest Common Prefix
<div class="elfjS" data-track-load="description_content"><p>Write a function to find the longest common prefix string amongst an array of strings.</p>

<p>If there is no common prefix, return an empty string <code>""</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> strs = ["flower","flow","flight"]
<strong>Output:</strong> "fl"
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> strs = ["dog","racecar","car"]
<strong>Output:</strong> ""
<strong>Explanation:</strong> There is no common prefix among the input strings.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= strs.length &lt;= 200</code></li>
	<li><code>0 &lt;= strs[i].length &lt;= 200</code></li>
	<li><code>strs[i]</code> consists of only lowercase English letters.</li>
</ul>
</div>

### Solution

```
class Solution {
public:
    string longestCommonPrefix(vector<string>& v) {
        string ans="";
        sort(v.begin(),v.end());
        int n=v.size();
        string first=v[0],last=v[n-1];
        for(int i=0;i<min(first.size(),last.size());i++){
            if(first[i]!=last[i]){
                return ans;
            }
            ans+=first[i];
        }
        return ans;
    }
};
```
## Go To
[Table of Content](#table-of-content)

## Rabin-Karp algorithm (Repeated String Match)
<div class="elfjS" data-track-load="description_content"><p>Given two strings <code>a</code> and <code>b</code>, return <em>the minimum number of times you should repeat string </em><code>a</code><em> so that string</em> <code>b</code> <em>is a substring of it</em>. If it is impossible for <code>b</code>​​​​​​ to be a substring of <code>a</code> after repeating it, return <code>-1</code>.</p>

<p><strong>Notice:</strong> string <code>"abc"</code> repeated 0 times is <code>""</code>, repeated 1 time is <code>"abc"</code> and repeated 2 times is <code>"abcabc"</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> a = "abcd", b = "cdabcdab"
<strong>Output:</strong> 3
<strong>Explanation:</strong> We return 3 because by repeating a three times "ab<strong>cdabcdab</strong>cd", b is a substring of it.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> a = "a", b = "aa"
<strong>Output:</strong> 2
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= a.length, b.length &lt;= 10<sup>4</sup></code></li>
	<li><code>a</code> and <code>b</code> consist of lowercase English letters.</li>
</ul>
</div>

### Solution
#### How does Rabin Karp Algorithm Works
<ol><li>Calculate hash value of <em>pattern</em></li><li>Calculate hash value of first <em>M</em> characters of <em>text</em></li><li>Compare both hash values</li><li>If they are unequal, calculate hash value for next <em>M</em> characters of <em>text</em> and compare again.</li><li>If they are equal, perform a brute force comparison.</li></ol>
<p>This technique results in only one comparison per text sub-sequence and brute force is only required when the hash values match.</p>

<p>The task is to determine how many times we need to repeat string <code>a</code> such that string <code>b</code> becomes a substring of the repeated string <code>a</code>.</p>
<p>Here are important things to note from the problem:</p>
<ul>
<li>If it is not possible for <code>b</code> to be a substring of <code>a</code> no matter how many times <code>a</code> is repeated, we should return <code>-1</code>.</li>
<li>A string repeated 0 times is an empty string, repeated once remains the same, and so on.</li>
</ul>
<p>The challenge lies in finding the minimum number of repetitions needed.</p>

```
class Solution {
private:
    int BASE = 1000000;
public:
    int repeatedStringMatch(string A, string B) {
        if(A == B) return 1;
        int count = 1;
        string source = A;
        while(source.size() < B.size()){
            count++;
            source+=A;
        }
        if(source == B) return count;
        if(Rabin_Karp(source,B) != -1) return count;
        if(Rabin_Karp(source+A,B) != -1) return count+1;
        return -1;
    }
    int Rabin_Karp(string source, string target){
        if(source == "" or target == "") return -1;
        int m = target.size();
        int power = 1;
        for(int i = 0;i<m;i++){
            power = (power*31)%BASE;
        }
        int targetCode = 0;
        for(int i = 0;i<m;i++){
            targetCode = (targetCode*31+target[i])%BASE;
        }
        int hashCode = 0;
        for(int i = 0;i<source.size();i++){
            hashCode = (hashCode*31 + source[i])%BASE;
            if(i<m-1) continue;
            if(i>=m){
                hashCode = (hashCode-source[i-m]*power)%BASE;
            }
            if(hashCode<0)
                hashCode+=BASE;
            if(hashCode == targetCode){
                if(source.substr(i-m+1,m) == target)
                    return i-m+1;
            }
        }
        return -1;
    }
};
```

## Go To
[Table of Content](#table-of-content)
