## Table of Content

## Implement Trie (Prefix Tree)
<div class="elfjS" data-track-load="description_content"><p>A <a href="https://en.wikipedia.org/wiki/Trie" target="_blank"><strong>trie</strong></a> (pronounced as "try") or <strong>prefix tree</strong> is a tree data structure used to efficiently store and retrieve keys in a dataset of strings. There are various applications of this data structure, such as autocomplete and spellchecker.</p>

<p>Implement the Trie class:</p>

<ul>
	<li><code>Trie()</code> Initializes the trie object.</li>
	<li><code>void insert(String word)</code> Inserts the string <code>word</code> into the trie.</li>
	<li><code>boolean search(String word)</code> Returns <code>true</code> if the string <code>word</code> is in the trie (i.e., was inserted before), and <code>false</code> otherwise.</li>
	<li><code>boolean startsWith(String prefix)</code> Returns <code>true</code> if there is a previously inserted string <code>word</code> that has the prefix <code>prefix</code>, and <code>false</code> otherwise.</li>
</ul>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input</strong>
["Trie", "insert", "search", "search", "startsWith", "insert", "search"]
[[], ["apple"], ["apple"], ["app"], ["app"], ["app"], ["app"]]
<strong>Output</strong>
[null, null, true, false, true, null, true]

<strong>Explanation</strong>
Trie trie = new Trie();
trie.insert("apple");
trie.search("apple");   // return True
trie.search("app");     // return False
trie.startsWith("app"); // return True
trie.insert("app");
trie.search("app");     // return True
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= word.length, prefix.length &lt;= 2000</code></li>
	<li><code>word</code> and <code>prefix</code> consist only of lowercase English letters.</li>
	<li>At most <code>3 * 10<sup>4</sup></code> calls <strong>in total</strong> will be made to <code>insert</code>, <code>search</code>, and <code>startsWith</code>.</li>
</ul>
</div>

### Solution

```
class TrieNode {
public:
    TrieNode *child[26];
    bool isWord;
    TrieNode() {
        isWord = false;
        for (auto &a : child) a = nullptr;
    }
};
class Trie {
    TrieNode* root;
public:
    Trie() {
        root = new TrieNode();
    }
    void insert(string s) {
        TrieNode *p = root;
        for (auto &a : s) {
            int i = a - 'a';
            if (!p->child[i]) p->child[i] = new TrieNode();
            p = p->child[i];
        }
        p->isWord = true;
    }
    bool search(string key, bool prefix=false) {
        TrieNode *p = root;
        for (auto &a : key) {
            int i = a - 'a';
            if (!p->child[i]) return false;
            p = p->child[i];
        }
        if (prefix==false) return p->isWord;
        return true;
    }
    bool startsWith(string prefix) {
        return search(prefix, true);
    }
};
```

## Longest Word in Dictionary
<div class="elfjS" data-track-load="description_content"><p>Given an array of strings <code>words</code> representing an English Dictionary, return <em>the longest word in</em> <code>words</code> <em>that can be built one character at a time by other words in</em> <code>words</code>.</p>

<p>If there is more than one possible answer, return the longest word with the smallest lexicographical order. If there is no answer, return the empty string.</p>

<p>Note that the word should be built from left to right with each additional character being added to the end of a previous word.&nbsp;</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> words = ["w","wo","wor","worl","world"]
<strong>Output:</strong> "world"
<strong>Explanation:</strong> The word "world" can be built one character at a time by "w", "wo", "wor", and "worl".
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> words = ["a","banana","app","appl","ap","apply","apple"]
<strong>Output:</strong> "apple"
<strong>Explanation:</strong> Both "apply" and "apple" can be built from other words in the dictionary. However, "apple" is lexicographically smaller than "apply".
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= words.length &lt;= 1000</code></li>
	<li><code>1 &lt;= words[i].length &lt;= 30</code></li>
	<li><code>words[i]</code> consists of lowercase English letters.</li>
</ul>
</div>

### Solution
<div class="FN9Jv WRmCx"><p>We will use <code>Trie</code>, also called <code>Prefix tree</code>, structure to solve the problem.<br>
If you don't know what the <code>Trie</code> is, then complete this problem first <a href="https://leetcode.com/problems/implement-trie-prefix-tree/" target="_blank">https://leetcode.com/problems/implement-trie-prefix-tree/</a></p>
<p>First of all, let's define our node of tree:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-javascript" style="color: rgb(156, 220, 254); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> children </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>	</span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> word</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>	</span><span class="token" style="color: rgb(220, 220, 170);">TreeNode</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>As said in constraints, words contains lowercase letters only; That's why we can simply use array <code>TreeNode[26]</code> to store node children. To compute the index we will use next trick - <code>index = character - 'a'</code>.<br>
We need to, somehow, check is the node represents a word. So, let's store in each <code>TreeNode</code> field <code>word</code>. If node is representing the word, then value of word will be in the field <code>word</code>, otherwise field will be empty.</p>
<p>How to insert a word into our <code>Trie</code>? - Using <code>current</code> as pointer of node. If <code>current</code> don't have <code>character</code> in his children, just put new <code>TreeNode</code> to <code>current</code> children.<br>
We have to put word character by character into Tree. There are 2 cases:</p>
<ul>
<li>
<ol>
<li>We already have the character -  just set <code>current</code> to <code>current.children[c - 'a']</code></li>
</ol>
</li>
<li>
<ol start="2">
<li>We don't have the character yet - put it into <code>current.children</code> and then set <code>current</code> to <code>current.children[c - 'a']</code></li>
</ol>
</li>
</ul>
<p>At the end of inserting operation we need to take node, represanting the last character of a word, and set it <code>word</code> field to whole word.</p>
<p>The code below insert word into our <code>Trie</code>:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-java" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">insert</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">String</span><span> word</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> current </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(86, 156, 214);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">char</span><span> c </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> word</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token" style="color: rgb(220, 220, 170);">toCharArray</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(86, 156, 214);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>current</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>children</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>c </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'a'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>			current</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>children</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>c </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'a'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		current </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> current</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>children</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>c </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'a'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>	current</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span>word </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> word</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>As we defined our <code>TreeNode</code> and <code>insert</code> function, let's fill it by all words, we have in input:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-lisp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span>for </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token car">String</span><span> w : words</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>			insert</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token car">w</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(106, 153, 85);">;</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>Now we have all words in our <code>Trie</code> and just have to iterate over the whole tree and find the longest word.<br>
We will use <code>Depth-First Search</code> to iterate over it.<br>
As said in the problem defenition, we should build each word <code>character by character</code>. It means, if we have character, which isn't word - we should stop <code>DFS</code> for this branch of our <code>Trie</code>.<br>
If current <code>TreeNode</code> have word - then check is it the longest word, we are looking for.</p>
<p>Next code describes <code>DFS</code>, looking for the longest word:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-typescript" style="color: rgb(156, 220, 254); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">dfs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token null nil" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(197, 134, 192);">return</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>	</span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token null nil" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> result</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>			result </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(197, 134, 192);">else</span><span> </span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> result</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">compareTo</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>result</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>			result </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span>	</span><span class="token" style="color: rgb(197, 134, 192);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> child </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">children</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>child </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token null nil" style="color: rgb(86, 156, 214);">null</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> child</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token null nil" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(220, 220, 170);">dfs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>child</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
<p>Enjoy ;)<br>
The whole solution:</p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-typescript" style="color: rgb(156, 220, 254); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> result </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">""</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>	</span><span class="token" style="color: rgb(86, 156, 214);">public</span><span> </span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">longestWord</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> words</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>		root </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>		</span><span class="token" style="color: rgb(197, 134, 192);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> w </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> words</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(220, 220, 170);">insert</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>w</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>		</span><span class="token" style="color: rgb(220, 220, 170);">dfs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>root</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>		</span><span class="token" style="color: rgb(197, 134, 192);">return</span><span> result</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span>	</span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">dfs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token null nil" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(197, 134, 192);">return</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>		</span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token null nil" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> result</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>				result </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(197, 134, 192);">else</span><span> </span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> result</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">length</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">compareTo</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>result</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span> </span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>				result </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span>		</span><span class="token" style="color: rgb(197, 134, 192);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> child </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> node</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">children</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>child </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token null nil" style="color: rgb(86, 156, 214);">null</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;&amp;</span><span> child</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">!=</span><span> </span><span class="token null nil" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>				</span><span class="token" style="color: rgb(220, 220, 170);">dfs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>child</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span>	</span><span class="token" style="color: rgb(86, 156, 214);">private</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">insert</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> word</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> current </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> root</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(197, 134, 192);">for</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>char c </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> word</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token method property-access" style="color: rgb(220, 220, 170);">toCharArray</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>			</span><span class="token" style="color: rgb(197, 134, 192);">if</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>current</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">children</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>c </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'a'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">==</span><span> </span><span class="token null nil" style="color: rgb(86, 156, 214);">null</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span>
</span></span><span><span>				current</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">children</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>c </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'a'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>			current </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> current</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">children</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>c </span><span class="token" style="color: rgb(212, 212, 212);">-</span><span> </span><span class="token" style="color: rgb(206, 145, 120);">'a'</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>		</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>		current</span><span class="token" style="color: rgb(212, 212, 212);">.</span><span class="token property-access">word</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> word</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>	</span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> children </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">TreeNode</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">26</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>	</span><span class="token known-class-name" style="color: rgb(78, 201, 176);">String</span><span> word</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>
</span><span><span>	</span><span class="token" style="color: rgb(220, 220, 170);">TreeNode</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div></div>

## Number of Distinct Substrings in a String
<p>Given a string <code>s</code>, return <em>the number of <strong>distinct</strong> substrings of</em>&nbsp;<code>s</code>.</p>
<p>A <strong>substring</strong> of a string is obtained by deleting any number of characters (possibly zero) from the front of the string and any number (possibly zero) from the back of the string.</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> s = "aabbaba"
<strong>Output:</strong> 21
<strong>Explanation:</strong> The set of distinct strings is ["a","b","aa","bb","ab","ba","aab","abb","bab","bba","aba","aabb","abba","bbab","baba","aabba","abbab","bbaba","aabbab","abbaba","aabbaba"]
</pre>
<p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> s = "abcdefg"
<strong>Output:</strong> 28
</pre>
<p><strong>Constraints:</strong></p>
<ul>
	<li><code>1 &lt;= s.length &lt;= 500</code></li>
	<li><code>s</code> consists of lowercase English letters.</li>
<p><strong>Constraints:</strong></p></ul>

<p><strong>Follow up:</strong> Can you solve this problem in <code>O(n)</code> time complexity?</p>


### Solution
Use a <code class="language-plaintext highlighter-rouge">Trie</code>, and every time a new <code class="language-plaintext highlighter-rouge">Trie</code> node created, meaning a new substring.</p>
<p>If <code class="language-plaintext highlighter-rouge">O(n)</code> time complexity, then we need some <code class="language-plaintext highlighter-rouge">extra space</code> to store for de-dup check, like a <code class="language-plaintext highlighter-rouge">Set</code>.</p>

```
public class Solution {
    class Trie {
        Trie[] children = new Trie[26];
    }

    public int countDistinct(String s) {
        Trie root = new Trie();
        Trie current;
        int count = 0;
        for (int i = 0; i < s.length(); i++) {
            current = root;
            for (int j = i; j < s.length(); j++) {

                if (current.children[s.charAt(j) - 'a'] == null) {
                    current.children[s.charAt(j) - 'a'] = new Trie();
                    count++;
                }

                current = current.children[s.charAt(j) - 'a'];
            }
        }

        return count;
    }
}
```

## Subsets
<div class="elfjS" data-track-load="description_content"><p>Given an integer array <code>nums</code> of <strong>unique</strong> elements, return <em>all possible</em> <span data-keyword="subset" class=" cursor-pointer relative text-dark-blue-s text-sm"><div class="popover-wrapper inline-block" data-headlessui-state=""><div><div aria-expanded="false" data-headlessui-state="" id="headlessui-popover-button-:rt:"><div><em>subsets</em></div></div><div style="position: fixed; z-index: 40; inset: 0px auto auto 0px; transform: translate(466px, 182px);"></div></div></div></span> <em>(the power set)</em>.</p>

<p>The solution set <strong>must not</strong> contain duplicate subsets. Return the solution in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [1,2,3]
<strong>Output:</strong> [[],[1],[2],[1,2],[3],[1,3],[2,3],[1,2,3]]
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [0]
<strong>Output:</strong> [[],[0]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 10</code></li>
	<li><code>-10 &lt;= nums[i] &lt;= 10</code></li>
	<li>All the numbers of&nbsp;<code>nums</code> are <strong>unique</strong>.</li>
</ul>
</div>

### Solution
<p>Let's start from an empty subset in the output list. At each step, one takes a new integer into consideration and generates new subsets from the existing ones.</p>
<p><img src="https://leetcode.com/problems/subsets/Figures/78/combinations.png" alt="diff"></p>

```
class Solution {
  public List<List<Integer>> subsets(int[] nums) {
    List<List<Integer>> output = new ArrayList();
    output.add(new ArrayList<Integer>());

    for (int num : nums) {
      List<List<Integer>> newSubsets = new ArrayList();
      for (List<Integer> curr : output) {
        newSubsets.add(new ArrayList<Integer>(curr){{add(num);}});
      }
      for (List<Integer> curr : newSubsets) {
        output.add(curr);
      }
    }
    return output;
  }
}
```

## Maximum XOR of Two Numbers in an Array
<div class="elfjS" data-track-load="description_content"><p>Given an integer array <code>nums</code>, return <em>the maximum result of </em><code>nums[i] XOR nums[j]</code>, where <code>0 &lt;= i &lt;= j &lt; n</code>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>

<pre><strong>Input:</strong> nums = [3,10,5,25,2,8]
<strong>Output:</strong> 28
<strong>Explanation:</strong> The maximum result is 5 XOR 25 = 28.
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> nums = [14,70,53,83,49,91,36,80,92,51,66,70]
<strong>Output:</strong> 127
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 2 * 10<sup>5</sup></code></li>
	<li><code>0 &lt;= nums[i] &lt;= 2<sup>31</sup> - 1</code></li>
</ul>
</div>

### Soliution
<div class="FN9Jv WRmCx"><p><strong>APPROACH :</strong></p>
<ul>
<li>We need a data structure through which we can do the following 2 jobs easily :<br>
1. Insert all the elements of the array into the data structure.<br>
2. Given a Y, find maximum XOR of Y with all numbers that have been inserted.</li>
<li>So, we can use trie.</li>
<li>Every bit in a number has 2 possibilities : <code>0</code> &amp; <code>1</code>.</li>
<li>So, we have 2 pointers in every Trie Node : child[0] ---&gt; pointing to <code>0</code> bit &amp; child[1] ---&gt; pointing to <code>1</code> bit.</li>
<li>We insert all the elements into the Trie :<br>
1. We use a bitset of size 32 (<code>bitset&lt;32&gt; bs</code>), go from the most significant bit (MSB) to the least significant bit (LSB).<br>
2. We start at the root of the Trie &amp; check if it's child[0] or child[1] is present (not <code>NULL</code>), depending upon the current bit <code>bs[j]</code> at each bit of the number.<br>
3. If it's present, we go to it's child, if not, we create a new Node at that child (0 bit or 1 bit) and move to it's child.</li>
<li>We traverse the array &amp; for each element we find the maximum <code>XOR</code> possible with any other element in the array using the Trie :<br>
1. We start at the root of the Trie and at the MSB of the number &amp; we initialize <code>ans = 0</code>.<br>
2. If the current bit is set, we go to <code>child[0]</code> to check if it's not NULL. If it's not NULL, we add <code>1&lt;&lt;i</code> to <code>ans</code>.<br>
3. If it's not set, we go to <code>child[1]</code> to see it's not NULL, if it's not NULL, we add <code>1&lt;&lt;i</code> to <code>ans</code>.</li>
<li>After checking the maximum XOR possible (with any other element) at each element of the array, we update the result to maximum of previous result &amp; the current result.</li>
<li>Finally return the maximum possible XOR.</li>
</ul>
<p><em>I tried my best to explain the approavh here, please refer to the code for better clarity</em></p>
<p><strong>Time Complexity :</strong> O(n<em>x</em>logm) - <code>n = nums.size()</code>, <code>m = *max_element(nums.begin(), nums.end())</code>.</p>
<p><strong>Code :</strong></p>
<div class="mb-6 rounded-lg px-3 py-2.5 font-menlo text-sm bg-fill-3 dark:bg-dark-fill-3"><div class="group relative" translate="no"><pre style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none; padding: 0px; margin: 0px; overflow: auto; background: transparent;"><code class="language-cpp" style="color: rgb(212, 212, 212); font-size: 13px; text-shadow: none; font-family: Menlo, Monaco, Consolas, &quot;Andale Mono&quot;, &quot;Ubuntu Mono&quot;, &quot;Courier New&quot;, monospace; direction: ltr; text-align: left; white-space: pre; word-spacing: normal; word-break: normal; line-height: 1.5; tab-size: 4; hyphens: none;"><span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">TrieNode</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    TrieNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>child</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">2</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(220, 220, 170);">TrieNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>child</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//for 0 bit </span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">this</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>child</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(156, 220, 254);">NULL</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//for 1 bit</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">class</span><span> </span><span class="token" style="color: rgb(78, 201, 176);">Solution</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>    TrieNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>newNode</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">void</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">insert</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>   </span><span class="token" style="color: rgb(106, 153, 85);">//to insert each element into the Trie</span><span>
</span></span><span><span>        TrieNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>t </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> newNode</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        bitset</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(181, 206, 168);">32</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">bs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>x</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">31</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">--</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>t</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>child</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>bs</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> t</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>child</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>bs</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">TrieNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//start from the MSB =, move to LSB using bitset</span><span>
</span></span><span><span>            t </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> t</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>child</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>bs</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>    
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span></span><span class="token" style="color: rgb(86, 156, 214);">public</span><span class="token" style="color: rgb(212, 212, 212);">:</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">findMaximumXOR</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>vector</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        newNode </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(86, 156, 214);">new</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">TrieNode</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">auto</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">&amp;</span><span>n </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">insert</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//insert all the elements into the Trie</span><span>
</span></span><span>        
</span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> ans</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//Stores the maximum XOR possible so far</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">auto</span><span> n </span><span class="token" style="color: rgb(212, 212, 212);">:</span><span> nums</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            ans </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">max</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>ans</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">maxXOR</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>  </span><span class="token" style="color: rgb(106, 153, 85);">//updates the ans as we traverse the array &amp; compute max XORs at each element.</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> ans</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span>    
</span><span><span>    </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">maxXOR</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> n</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>        TrieNode </span><span class="token" style="color: rgb(212, 212, 212);">*</span><span>t </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> newNode</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        bitset</span><span class="token" style="color: rgb(212, 212, 212);">&lt;</span><span class="token" style="color: rgb(181, 206, 168);">32</span><span class="token" style="color: rgb(212, 212, 212);">&gt;</span><span> </span><span class="token" style="color: rgb(220, 220, 170);">bs</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>n</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> ans</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> 
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">for</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(86, 156, 214);">int</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">=</span><span class="token" style="color: rgb(181, 206, 168);">31</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">&gt;=</span><span class="token" style="color: rgb(181, 206, 168);">0</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> j</span><span class="token" style="color: rgb(212, 212, 212);">--</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">{</span><span>
</span></span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">if</span><span class="token" style="color: rgb(212, 212, 212);">(</span><span>t</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>child</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>bs</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span> ans </span><span class="token" style="color: rgb(212, 212, 212);">+=</span><span> </span><span class="token" style="color: rgb(212, 212, 212);">(</span><span class="token" style="color: rgb(181, 206, 168);">1</span><span class="token" style="color: rgb(212, 212, 212);">&lt;&lt;</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">)</span><span class="token" style="color: rgb(212, 212, 212);">,</span><span> t </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> t</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>child</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span class="token" style="color: rgb(212, 212, 212);">!</span><span>bs</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span> </span><span class="token" style="color: rgb(106, 153, 85);">//Since 1^0 = 1 &amp; 1^1 = 0, 0^0 = 0</span><span>
</span></span><span>           
</span><span><span>            </span><span class="token" style="color: rgb(86, 156, 214);">else</span><span> t </span><span class="token" style="color: rgb(212, 212, 212);">=</span><span> t</span><span class="token" style="color: rgb(212, 212, 212);">-&gt;</span><span>child</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>bs</span><span class="token" style="color: rgb(212, 212, 212);">[</span><span>j</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">]</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span>        </span><span class="token" style="color: rgb(86, 156, 214);">return</span><span> ans</span><span class="token" style="color: rgb(212, 212, 212);">;</span><span>
</span></span><span><span>    </span><span class="token" style="color: rgb(212, 212, 212);">}</span><span>
</span></span><span><span></span><span class="token" style="color: rgb(212, 212, 212);">}</span><span class="token" style="color: rgb(212, 212, 212);">;</span></span></code></pre><div class="z-base-1 hidden rounded border group-hover:block border-border-quaternary dark:border-border-quaternary bg-layer-02 dark:bg-layer-02 absolute -right-1.5 -top-0.5"><div class="relative cursor-pointer flex h-[22px] w-[22px] items-center justify-center bg-layer-02 dark:bg-layer-02 hover:bg-fill-tertiary dark:hover:bg-fill-tertiary rounded-[4px]" data-state="closed"><div><div data-state="closed"><div class="relative text-[12px] leading-[normal] p-[1px] before:block before:h-3 before:w-3 h-3.5 w-3.5 text-text-primary dark:text-text-primary"><svg aria-hidden="true" focusable="false" data-prefix="far" data-icon="clone" class="svg-inline--fa fa-clone absolute left-1/2 top-1/2 -translate-x-1/2 -translate-y-1/2" role="img" xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"><path fill="currentColor" d="M64 464H288c8.8 0 16-7.2 16-16V384h48v64c0 35.3-28.7 64-64 64H64c-35.3 0-64-28.7-64-64V224c0-35.3 28.7-64 64-64h64v48H64c-8.8 0-16 7.2-16 16V448c0 8.8 7.2 16 16 16zM224 304H448c8.8 0 16-7.2 16-16V64c0-8.8-7.2-16-16-16H224c-8.8 0-16 7.2-16 16V288c0 8.8 7.2 16 16 16zm-64-16V64c0-35.3 28.7-64 64-64H448c35.3 0 64 28.7 64 64V288c0 35.3-28.7 64-64 64H224c-35.3 0-64-28.7-64-64z"></path></svg></div></div></div></div></div></div></div>
</div>
