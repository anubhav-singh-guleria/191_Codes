
## Table of Content

1. [KMP Algorithm - LPS (PI) Array](#kmp-algo--lpspi-array)
2. [Minimum Characters Required to Make a String Palindromic](#minimum-characters-required-to-make-a-string-palindromic)
3. [Valid Anagram](#valid-anagram)
4. [Count and Say](#count-and-say)
5. [Compare Version Numbers](#compare-version-numbers)

## KMP algo / LPS(pi) array	
<div class="elfjS" data-track-load="description_content"><p>Given two strings <code>needle</code> and <code>haystack</code>, return the index of the first occurrence of <code>needle</code> in <code>haystack</code>, or <code>-1</code> if <code>needle</code> is not part of <code>haystack</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> haystack = "sadbutsad", needle = "sad"
<strong>Output:</strong> 0
<strong>Explanation:</strong> "sad" occurs at index 0 and 6.
The first occurrence is at index 0, so we return 0.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> haystack = "leetcode", needle = "leeto"
<strong>Output:</strong> -1
<strong>Explanation:</strong> "leeto" did not occur in "leetcode", so we return -1.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= haystack.length, needle.length &lt;= 10<sup>4</sup></code></li>
	<li><code>haystack</code> and <code>needle</code> consist of only lowercase English characters.</li>
</ul>
</div>

### Solution

```
class Solution {
    public int strStr(String haystack, String needle) {
        if (needle.isEmpty()) return 0;
        int[] lps = buildLPS(needle);
        int n = haystack.length(), m = needle.length();
        for (int i = 0, j = 0; i < n; i++) {
            while (j > 0 && haystack.charAt(i) != needle.charAt(j)) 
                j = lps[j - 1];
            if (haystack.charAt(i) == needle.charAt(j)) {
                if (++j == m) 
                    return i - m + 1; // found solution
            }
        }
        return -1;
    }
    private int[] buildLPS(String pattern) {
        int n = pattern.length();
        int[] lps = new int[n];
        for (int i = 1, j = 0; i < n; i++) {
            while (j > 0 && pattern.charAt(i) != pattern.charAt(j)) 
                j = lps[j - 1];
            if (pattern.charAt(i) == pattern.charAt(j)) 
                lps[i] = ++j;
        }
        return lps;
    }
}
```

## Go To
[Table of Content](#table-of-content)

## Minimum Characters required to make a String Palindromic
<div class="mhGZq BAGeNT"><div type="first" data-hook="rcv-block-first"></div><u class="D-jZk">Minimum Characters required to make a String Palindromic</u></a></span></span></p><div type="paragraph" data-hook="rcv-block1"></div><div id="viewer-1o7ir" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr"><span><br role="presentation"></span></span></div><div type="empty-line" data-hook="rcv-block2"></div><p id="viewer-38ia3" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr" style="padding-top:0px;padding-bottom:0px"><span class="B2EFF public-DraftStyleDefault-ltr"><span><strong>Problem Statement: </strong></span></span></p><div type="paragraph" data-hook="rcv-block3"></div><p id="viewer-3tvos" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr"><span>Given a string <strong>A</strong>. The only operation allowed is to insert characters at the beginning of the string.</span></span></p><div type="paragraph" data-hook="rcv-block4"></div><p id="viewer-7mfos" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr" style="padding-top:0px;padding-bottom:0px"><span class="B2EFF public-DraftStyleDefault-ltr"><span>Find how many minimum characters are needed to be inserted to make the string a palindrome string.</span></span></p><div type="paragraph" data-hook="rcv-block5"></div><div id="viewer-ei51n" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr" style="padding-top:0px;padding-bottom:0px"><span class="B2EFF public-DraftStyleDefault-ltr"><span><br role="presentation"></span></span></div><div type="empty-line" data-hook="rcv-block6"></div><p id="viewer-f7a29" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr" style="padding-top:0px;padding-bottom:0px"><span class="B2EFF public-DraftStyleDefault-ltr"><span><strong>Input Format</strong></span></span></p><div type="paragraph" data-hook="rcv-block7"></div><p id="viewer-8n6bp" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr"><span>The only argument given is string A. </span></span></p><div type="paragraph" data-hook="rcv-block8"></div><div id="viewer-5f1of" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr" style="padding-top:0px;padding-bottom:0px"><span class="B2EFF public-DraftStyleDefault-ltr"><span><br role="presentation"></span></span></div><div type="empty-line" data-hook="rcv-block9"></div><p id="viewer-a5olm" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr" style="padding-top:0px;padding-bottom:0px"><span class="B2EFF public-DraftStyleDefault-ltr"><span><strong>Output Format</strong></span></span></p><div type="paragraph" data-hook="rcv-block10"></div><p id="viewer-656m5" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr"><span>Return the minimum characters that are needed to be inserted to make the string a palindrome string. </span></span></p><div type="paragraph" data-hook="rcv-block11"></div><div id="viewer-3m04m" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr" style="padding-top:0px;padding-bottom:0px"><span class="B2EFF public-DraftStyleDefault-ltr"><span><br role="presentation"></span></span></div><div type="empty-line" data-hook="rcv-block12"></div><p id="viewer-264hd" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr" style="padding-top:0px;padding-bottom:0px"><span class="B2EFF public-DraftStyleDefault-ltr"><span><strong>For Example</strong>  </span></span></p><div type="paragraph" data-hook="rcv-block13"></div><pre id="viewer-a39pf" class="cN6Rd _8ps7N KsFUxO OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr">Input <span class="_3p6CM">1</span><span class="KviDO">:</span>
    <span class="">A</span> <span class="iYKHF">=</span> <span class="qTWn2">"ABC"</span>
Output <span class="_3p6CM">1</span><span class="KviDO">:</span>
    <span class="_3p6CM">2</span>
    Explanation <span class="_3p6CM">1</span><span class="KviDO">:</span>
        Insert <span class="qTWn2">'B'</span> at beginning<span class="KviDO">,</span> string becomes<span class="KviDO">:</span> <span class="qTWn2">"BABC"</span><span class="KviDO">.</span>
        Insert <span class="qTWn2">'C'</span> at beginning<span class="KviDO">,</span> string becomes<span class="KviDO">:</span> <span class="qTWn2">"CBABC"</span><span class="KviDO">.</span>

Input <span class="_3p6CM">2</span><span class="KviDO">:</span>
    <span class="">A</span> <span class="iYKHF">=</span> <span class="qTWn2">"AACECAAAA"</span>
Output <span class="_3p6CM">2</span><span class="KviDO">:</span>
    <span class="_3p6CM">2</span>
    Explanation <span class="_3p6CM">2</span><span class="KviDO">:</span>
        Insert <span class="qTWn2">'A'</span> at beginning<span class="KviDO">,</span> string becomes<span class="KviDO">:</span> <span class="qTWn2">"AAACECAAAA"</span><span class="KviDO">.</span>
        Insert <span class="qTWn2">'A'</span> at beginning<span class="KviDO">,</span> string becomes<span class="KviDO">:</span> <span class="qTWn2">"AAAACECAAAA"</span><span class="KviDO">.</span></span></pre><div type="pre" data-hook="rcv-block14"></div><h2 id="viewer-3qcug" class="qDGi6 Y9Dpf OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr"><span><br role="presentation"></span></span></h2><div type="empty-line" data-hook="rcv-block15"></div><h2 id="viewer-993gq" class="qDGi6 Y9Dpf OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr"><span>Approach: </span></span></h2><div type="h2" data-hook="rcv-block16"></div><p id="viewer-9q0b4" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr"><span><span style="color:#333333"><span style="background-color:#ffffff">Each index of </span></span>the <span style="color:#333333"><span style="background-color:#ffffff">LPS array contains the longest prefix which is also a suffix. Now take the string and reverse of a string and combine them with a sentinel character in between them and compute the LPS array of this combined string. Now take the last value of the LPS array and subtract it with the length of the original string, This will give us the minimum number of insertions required </span></span>at<span style="color:#333333"><span style="background-color:#ffffff"> the </span></span>beginning<span style="color:#333333"><span style="background-color:#ffffff"> of the string.</span></span></span></span></p><div type="paragraph" data-hook="rcv-block17"></div><div id="viewer-ch1ul" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr"><span><br role="presentation"></span></span></div><div type="empty-line" data-hook="rcv-block18"></div><div id="viewer-a7nag" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr"><span><br role="presentation"></span></span></div><div type="empty-line" data-hook="rcv-block19"></div><h2 id="viewer-54nmf" class="qDGi6 Y9Dpf OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr"><span><span style="color:#333333"><span style="background-color:#ffffff">Time &amp; Space Complexity:</span></span></span></span></h2><div type="h2" data-hook="rcv-block20"></div><pre id="viewer-cif0s" class="cN6Rd _8ps7N KsFUxO OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr"><span style="color:#333333"><span style="background-color:#ffffff">Time Complexity</span></span><span class="KviDO"><span style="color:#333333"><span style="background-color:#ffffff">:</span></span></span><span style="color:#333333"><span style="background-color:#ffffff"> </span></span><span class=""><span style="color:#333333"><span style="background-color:#ffffff">O</span></span></span><span class="KviDO"><span style="color:#333333"><span style="background-color:#ffffff">(</span></span></span><span class=""><span style="color:#333333"><span style="background-color:#ffffff">N</span></span></span><span class="KviDO"><span style="color:#333333"><span style="background-color:#ffffff">)</span></span></span></span></pre><div type="pre" data-hook="rcv-block21"></div><div id="viewer-cg3mu" class="xVISr Y9Dpf bCMSCT OZy-3 lnyWN yMZv8w bCMSCT public-DraftStyleDefault-block-depth0 fixed-tab-size public-DraftStyleDefault-text-ltr"><span class="B2EFF public-DraftStyleDefault-ltr"><span><br role="presentation"></span></span></div><div type="empty-line" data-hook="rcv-block22"></div><div id="viewer-65cht" class="QHjDE rzoRKE"><div class="gO6aa y8JqQg y8JqQg" style="width:740px"><div class="_9lBLQ usqJ7F" style="width: 740px; height: 184px; max-height: 184px;" data-hook="HtmlComponent">

```
int computeLPS(string &B){
    int n = B.size(), j = 0;
    int lps[n]; 
    lps[0] = 0;
    
    int i = 1; 
    while(i < n){
        if(B[i] == B[j]){
            j++;
            lps[i] = j;
            i++;
        }
        else{
            if(j!=0){
                j = lps[j-1];
            }
            else{
                lps[i] = 0;
                i++;
            }
        }
    }
    return n/2 - lps[n-1];
}

int Solution::solve(string A) {
    string B = A; 
    reverse(A.begin(), A.end());
    B += "$" + A;
    return computeLPS(B);
}
```
## Go To
[Table of Content](#table-of-content)

## Valid Anagram
<div class="elfjS" data-track-load="description_content"><p>Given two strings <code>s</code> and <code>t</code>, return <code>true</code> <em>if</em> <code>t</code> <em>is an anagram of</em> <code>s</code><em>, and</em> <code>false</code> <em>otherwise</em>.</p>

<p>An <strong>Anagram</strong> is a word or phrase formed by rearranging the letters of a different word or phrase, typically using all the original letters exactly once.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> s = "anagram", t = "nagaram"
<strong>Output:</strong> true
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> s = "rat", t = "car"
<strong>Output:</strong> false
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= s.length, t.length &lt;= 5 * 10<sup>4</sup></code></li>
	<li><code>s</code> and <code>t</code> consist of lowercase English letters.</li>
</ul>

<p>&nbsp;</p>
<p><strong>Follow up:</strong> What if the inputs contain Unicode characters? How would you adapt your solution to such a case?</p>
</div>

### Solution

```
public class Solution {
    public boolean isAnagram(String s, String t) {
        int[] alphabet = new int[26];
        for (int i = 0; i < s.length(); i++) alphabet[s.charAt(i) - 'a']++;
        for (int i = 0; i < t.length(); i++) alphabet[t.charAt(i) - 'a']--;
        for (int i : alphabet) if (i != 0) return false;
        return true;
    }
}
```
## Go To
[Table of Content](#table-of-content)

## Count and Say
<div class="elfjS" data-track-load="description_content"><p>The <strong>count-and-say</strong> sequence is a sequence of digit strings defined by the recursive formula:</p>

<ul>
	<li><code>countAndSay(1) = "1"</code></li>
	<li><code>countAndSay(n)</code> is the way you would "say" the digit string from <code>countAndSay(n-1)</code>, which is then converted into a different digit string.</li>
</ul>

<p>To determine how you "say" a digit string, split it into the <strong>minimal</strong> number of substrings such that each substring contains exactly <strong>one</strong> unique digit. Then for each substring, say the number of digits, then say the digit. Finally, concatenate every said digit.</p>

<p>For example, the saying and conversion for digit string <code>"3322251"</code>:</p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/10/23/countandsay.jpg" style="width: 581px; height: 172px;">
<p>Given a positive integer <code>n</code>, return <em>the </em><code>n<sup>th</sup></code><em> term of the <strong>count-and-say</strong> sequence</em>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> n = 1
<strong>Output:</strong> "1"
<strong>Explanation:</strong> This is the base case.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> n = 4
<strong>Output:</strong> "1211"
<strong>Explanation:</strong>
countAndSay(1) = "1"
countAndSay(2) = say "1" = one 1 = "11"
countAndSay(3) = say "11" = two 1's = "21"
countAndSay(4) = say "21" = one 2 + one 1 = "12" + "11" = "1211"
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 30</code></li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>This function makes <code>n</code> recursive calls, since we start from <code>n</code> and end at <code>1</code> (base case)</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-csharp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token return-type" style="color: rgb(86, 156, 214);">string</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">countAndSay</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">string</span><span> s </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">"1"</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// initial value of the string is "1"</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// base case, when n recursive calls are finished</span><span>
</span></span><span>	
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> len </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">size</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// 'len' is the length of the string 's'</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">string</span><span> res </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">""</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// result after we 'say' the string 's'</span><span>
</span></span><span>	
</span><span><span>	</span><span class="token" style="color: rgb(106, 153, 85);">// 'i' starts from index 0</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>len</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        j</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">// fix 'j' as the current position (i)</span><span>
</span></span><span>		
</span><span><span>		</span><span class="token" style="color: rgb(106, 153, 85);">// increment the value of 'i' till valid position</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">while</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span>len </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">==</span><span>s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> i</span><span class="token" style="color: rgb(212, 212, 212);">++</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>		
</span><span><span>		</span><span class="token" style="color: rgb(106, 153, 85);">// substring with same values as s[j] is [j,i-1] &amp; "i-j" is the count of that value</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(106, 153, 85);">// add the concatenation of (count + s[j]) to the result </span><span>
</span></span><span><span>        res </span><span class="token" style="color: rgb(212, 212, 212);">+=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">to_string</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>i</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">+</span><span> s</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>	
</span><span><span>	</span><span class="token" style="color: rgb(106, 153, 85);">// recursively, call the same function by decrementing the count</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(106, 153, 85);">// and update the result 'res', which will be the next string 's'</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">countAndSay</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">-</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> res</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="h-4 w-4 cursor-pointer fill-gray-6 hover:fill-gray-7 dark:fill-dark-gray-6 dark:hover:fill-dark-gray-7 absolute right-0 top-0" data-state="closed"><div class="opacity-100"><svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" width="1em" height="1em" fill="currentColor" class="h-4 w-4 text-gray-6 hover:text-gray-7 dark:text-dark-gray-6 dark:hover:text-dark-gray-7 hidden group-hover:block"><path fill-rule="evenodd" d="M11.3 8.3H19a3 3 0 013 3V19a3 3 0 01-3 3h-7.7a3 3 0 01-3-3v-7.7a3 3 0 013-3zm0 2a1 1 0 00-1 1V19a1 1 0 001 1H19a1 1 0 001-1v-7.7a1 1 0 00-1-1h-7.7zm-5.6 3.4a1 1 0 110 2h-.9A2.8 2.8 0 012 12.9V4.8A2.8 2.8 0 014.8 2h8.1a2.8 2.8 0 012.8 2.8v.9a1 1 0 11-2 0v-.9a.8.8 0 00-.8-.8H4.8a.8.8 0 00-.8.8v8.1a.8.8 0 00.8.8h.9z" clip-rule="evenodd"></path></svg></div></div></div></div></div>

## Go To
[Table of Content](#table-of-content)


## Compare Version Numbers
<div class="elfjS" data-track-load="description_content"><p>Given two version numbers,&nbsp;<code>version1</code> and <code>version2</code>, compare them.</p>

<ul>
</ul>

<p>Version numbers consist of <strong>one or more revisions</strong> joined by a dot&nbsp;<code>'.'</code>. Each revision&nbsp;consists of <strong>digits</strong>&nbsp;and may contain leading <strong>zeros</strong>. Every revision contains <strong>at least one character</strong>. Revisions are <strong>0-indexed from left to right</strong>, with the leftmost revision being revision 0, the next revision being revision 1, and so on. For example&nbsp;<code>2.5.33</code>&nbsp;and&nbsp;<code>0.1</code>&nbsp;are valid version numbers.</p>

<p>To compare version numbers, compare their revisions in <strong>left-to-right order</strong>. Revisions are compared using their&nbsp;<strong>integer value ignoring any leading zeros</strong>. This means that revisions&nbsp;<code>1</code>&nbsp;and&nbsp;<code>001</code>&nbsp;are considered&nbsp;<strong>equal</strong>. If a version number does not specify a revision at an index, then&nbsp;<strong>treat the revision as&nbsp;<code>0</code></strong>. For example, version&nbsp;<code>1.0</code> is less than version&nbsp;<code>1.1</code>&nbsp;because their revision 0s are the same, but their revision 1s are&nbsp;<code>0</code>&nbsp;and&nbsp;<code>1</code>&nbsp;respectively, and&nbsp;<code>0 &lt; 1</code>.</p>

<p><em>Return the following:</em></p>

<ul>
	<li>If <code>version1 &lt; version2</code>, return <code>-1</code>.</li>
	<li>If <code>version1 &gt; version2</code>, return <code>1</code>.</li>
	<li>Otherwise, return <code>0</code>.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> version1 = "1.01", version2 = "1.001"
<strong>Output:</strong> 0
<strong>Explanation:</strong> Ignoring leading zeroes, both "01" and "001" represent the same integer "1".
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> version1 = "1.0", version2 = "1.0.0"
<strong>Output:</strong> 0
<strong>Explanation:</strong> version1 does not specify revision 2, which means it is treated as "0".
</pre>

<p><strong class="example">Example 3:</strong></p>

<pre><strong>Input:</strong> version1 = "0.1", version2 = "1.1"
<strong>Output:</strong> -1
<strong>Explanation:</strong> version1's revision 0 is "0", while version2's revision 0 is "1". 0 &lt; 1, so version1 &lt; version2.
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= version1.length, version2.length &lt;= 500</code></li>
	<li><code>version1</code> and <code>version2</code>&nbsp;only contain digits and <code>'.'</code>.</li>
	<li><code>version1</code> and <code>version2</code>&nbsp;<strong>are valid version numbers</strong>.</li>
	<li>All the given revisions in&nbsp;<code>version1</code> and <code>version2</code>&nbsp;can be stored in&nbsp;a&nbsp;<strong>32-bit integer</strong>.</li>
</ul>
</div>

### Solution

```
public int compareVersion(String version1, String version2) {
    
    String[] v1 = version1.split("\\.");
    String[] v2 = version2.split("\\.");
    
    for ( int i = 0; i < Math.max(v1.length, v2.length); i++ ) {
        int num1 = i < v1.length ? Integer.parseInt( v1[i] ) : 0;
        int num2 = i < v2.length ? Integer.parseInt( v2[i] ) : 0;
        if ( num1 < num2 ) {
            return -1;
        } else if ( num1 > num2 ) {
            return +1;
        }
    } 
    
    return 0;
}
```

## Go To
[Table of Content](#table-of-content)
