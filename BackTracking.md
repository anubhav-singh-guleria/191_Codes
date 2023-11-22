## Table of Content

## Backtracking - Permutations
<div class="elfjS" data-track-load="description_content"><p>Given an array <code>nums</code> of distinct integers, return <em>all the possible permutations</em>. You can return the answer in <strong>any order</strong>.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<pre><strong>Input:</strong> nums = [1,2,3]
<strong>Output:</strong> [[1,2,3],[1,3,2],[2,1,3],[2,3,1],[3,1,2],[3,2,1]]
</pre><p><strong class="example">Example 2:</strong></p>
<pre><strong>Input:</strong> nums = [0,1]
<strong>Output:</strong> [[0,1],[1,0]]
</pre><p><strong class="example">Example 3:</strong></p>
<pre><strong>Input:</strong> nums = [1]
<strong>Output:</strong> [[1]]
</pre>
<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= nums.length &lt;= 6</code></li>
	<li><code>-10 &lt;= nums[i] &lt;= 10</code></li>
	<li>All the integers of <code>nums</code> are <strong>unique</strong>.</li>
</ul>
</div>

### Solution:

```
class Solution {
public:
    vector<vector<int> > permute(vector<int> &num) {
	    vector<vector<int> > result;
	    
	    permuteRecursive(num, 0, result);
	    return result;
    }
    
    // permute num[begin..end]
    // invariant: num[0..begin-1] have been fixed/permuted
	void permuteRecursive(vector<int> &num, int begin, vector<vector<int> > &result)	{
		if (begin >= num.size()) {
		    // one permutation instance
		    result.push_back(num);
		    return;
		}
		
		for (int i = begin; i < num.size(); i++) {
		    swap(num[begin], num[i]);
		    permuteRecursive(num, begin + 1, result);
		    // reset
		    swap(num[begin], num[i]);
		}
    }
};
```

## Go To
[Table of Content](#table-of-content)

## Backtracking - N-Queens

<div class="elfjS" data-track-load="description_content"><p>The <strong>n-queens</strong> puzzle is the problem of placing <code>n</code> queens on an <code>n x n</code> chessboard such that no two queens attack each other.</p>

<p>Given an integer <code>n</code>, return <em>all distinct solutions to the <strong>n-queens puzzle</strong></em>. You may return the answer in <strong>any order</strong>.</p>

<p>Each solution contains a distinct board configuration of the n-queens' placement, where <code>'Q'</code> and <code>'.'</code> both indicate a queen and an empty space, respectively.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img alt="" src="https://assets.leetcode.com/uploads/2020/11/13/queens.jpg" style="width: 600px; height: 268px;">
<pre><strong>Input:</strong> n = 4
<strong>Output:</strong> [[".Q..","...Q","Q...","..Q."],["..Q.","Q...","...Q",".Q.."]]
<strong>Explanation:</strong> There exist two distinct solutions to the 4-queens puzzle as shown above
</pre>

<p><strong class="example">Example 2:</strong></p>

<pre><strong>Input:</strong> n = 1
<strong>Output:</strong> [["Q"]]
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>1 &lt;= n &lt;= 9</code></li>
</ul>
</div>

### Solution:

```
class Solution {
public:
    vector<vector<string>> ret;
    bool is_valid(vector<string> &board, int row, int col){
        // check col
        for(int i=row;i>=0;--i)
            if(board[i][col] == 'Q') return false;
        // check left diagonal
        for(int i=row,j=col;i>=0&&j>=0;--i,--j)
            if(board[i][j] == 'Q') return false;
        //check right diagonal
        for(int i=row,j=col;i>=0&&j<board.size();--i,++j)
            if(board[i][j] == 'Q') return false;
        return true;
    }
    void dfs(vector<string> &board, int row){
        // exit condition
        if(row == board.size()){
            ret.push_back(board);
            return;
        }
        // iterate every possible position
        for(int i=0;i<board.size();++i){
            if(is_valid(board,row,i)){
                // make decision
                board[row][i] = 'Q';
                // next iteration
                dfs(board,row+1);
                // back-tracking
                board[row][i] = '.';
            }
        }
    }
    vector<vector<string>> solveNQueens(int n) {
		// return empty if n <= 0
        if(n <= 0) return {{}};
        vector<string> board(n,string(n,'.'));
        dfs(board,0);
        return ret;
    }
};
```

## Go To
[Table of Content](#table-of-content)

## Backtracking - Sudoku Solver
<div class="elfjS" data-track-load="description_content"><p>Write a program to solve a Sudoku puzzle by filling the empty cells.</p>

<p>A sudoku solution must satisfy <strong>all of the following rules</strong>:</p>

<ol>
	<li>Each of the digits <code>1-9</code> must occur exactly once in each row.</li>
	<li>Each of the digits <code>1-9</code> must occur exactly once in each column.</li>
	<li>Each of the digits <code>1-9</code> must occur exactly once in each of the 9 <code>3x3</code> sub-boxes of the grid.</li>
</ol>

<p>The <code>'.'</code> character indicates empty cells.</p>

<p>&nbsp;</p>
<p><strong class="example">Example 1:</strong></p>
<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/f/ff/Sudoku-by-L2G-20050714.svg/250px-Sudoku-by-L2G-20050714.svg.png" style="height: 250px; width: 250px;">
<pre><strong>Input:</strong> board = [["5","3",".",".","7",".",".",".","."],["6",".",".","1","9","5",".",".","."],[".","9","8",".",".",".",".","6","."],["8",".",".",".","6",".",".",".","3"],["4",".",".","8",".","3",".",".","1"],["7",".",".",".","2",".",".",".","6"],[".","6",".",".",".",".","2","8","."],[".",".",".","4","1","9",".",".","5"],[".",".",".",".","8",".",".","7","9"]]
<strong>Output:</strong> [["5","3","4","6","7","8","9","1","2"],["6","7","2","1","9","5","3","4","8"],["1","9","8","3","4","2","5","6","7"],["8","5","9","7","6","1","4","2","3"],["4","2","6","8","5","3","7","9","1"],["7","1","3","9","2","4","8","5","6"],["9","6","1","5","3","7","2","8","4"],["2","8","7","4","1","9","6","3","5"],["3","4","5","2","8","6","1","7","9"]]
<strong>Explanation:</strong>&nbsp;The input board is shown above and the only valid solution is shown below:

<img src="https://upload.wikimedia.org/wikipedia/commons/thumb/3/31/Sudoku-by-L2G-20050714_solution.svg/250px-Sudoku-by-L2G-20050714_solution.svg.png" style="height: 250px; width: 250px;">
</pre>

<p>&nbsp;</p>
<p><strong>Constraints:</strong></p>

<ul>
	<li><code>board.length == 9</code></li>
	<li><code>board[i].length == 9</code></li>
	<li><code>board[i][j]</code> is a digit or <code>'.'</code>.</li>
	<li>It is <strong>guaranteed</strong> that the input board has only one solution.</li>
</ul>
</div>

### Solution: 

```
public class Solution {
    public void solveSudoku(char[][] board) {
        if(board == null || board.length == 0)
            return;
        solve(board);
    }
    
    public boolean solve(char[][] board){
        for(int i = 0; i < board.length; i++){
            for(int j = 0; j < board[0].length; j++){
                if(board[i][j] == '.'){
                    for(char c = '1'; c <= '9'; c++){//trial. Try 1 through 9
                        if(isValid(board, i, j, c)){
                            board[i][j] = c; //Put c for this cell
                            
                            if(solve(board))
                                return true; //If it's the solution return true
                            else
                                board[i][j] = '.'; //Otherwise go back
                        }
                    }
                    
                    return false;
                }
            }
        }
        return true;
    }
    
    private boolean isValid(char[][] board, int row, int col, char c){
        for(int i = 0; i < 9; i++) {
            if(board[i][col] != '.' && board[i][col] == c) return false; //check row
            if(board[row][i] != '.' && board[row][i] == c) return false; //check column
            if(board[3 * (row / 3) + i / 3][ 3 * (col / 3) + i % 3] != '.' && 
board[3 * (row / 3) + i / 3][3 * (col / 3) + i % 3] == c) return false; //check 3*3 block
        }
        return true;
    }
}
```

## Go To
[Table of Content](#table-of-content)

## Backtracking - M – Coloring Problem
<p><strong>Problem Statement:</strong> Given an undirected graph and a number m, determine if the graph can be colored with at most m colors such that no two adjacent vertices of the graph are colored with the same color.</p>
<p><strong>Examples:</strong></p>
<pre class="wp-block-preformatted"><strong>Example 1:</strong>
<strong>Input: </strong>
N = 4
M = 3
E = 5
Edges[] = {
  (0, 1),
  (1, 2),
  (2, 3),
  (3, 0),
  (0, 2)
}

<strong>Output:</strong> 1

<strong>Explanation:</strong> It is possible to colour the given graph using 3 colours.

<strong>Example 2:</strong>

<strong>Input:</strong> 
N = 3
M = 2
E = 3
Edges[] = {
  (0, 1),
  (1, 2),
  (0, 2)
}

<strong>Output:</strong> 0


<strong>Explanation:</strong> It is not possible to color.</pre>
<h3><strong>Solution</strong></h3>
<p><strong>Approach</strong>: </p>
<p>Basically starting from vertex 0 color one by one the different vertices.&nbsp;</p>
<p><strong>Base condition:</strong></p>
<p>If I have colored all the N nodes return true.</p>
<p><strong>Recursion:</strong></p>
<p>Trying every color from 1 to m with the help of a for a loop.</p>
<p>Is safe function returns true if it is possible to color it with that color i.e none of the adjacent nodes have the same color.<br><br>In case this is an algorithm and follows a certain intuition, please mention it.&nbsp;</p>
<p>Color it with color i then call the recursive function for the next node if it returns true we will return true.</p>
<p>And If it is false then take off the color.</p>
<p><strong>Code:</strong></p>

```
#include<bits/stdc++.h>

using namespace std;
bool isSafe(int node, int color[], bool graph[101][101], int n, int col) {
  for (int k = 0; k < n; k++) {
    if (k != node && graph[k][node] == 1 && color[k] == col) {
      return false;
    }
  }
  return true;
}
bool solve(int node, int color[], int m, int N, bool graph[101][101]) {
  if (node == N) {
    return true;
  }

  for (int i = 1; i <= m; i++) {
    if (isSafe(node, color, graph, N, i)) {
      color[node] = i;
      if (solve(node + 1, color, m, N, graph)) return true;
      color[node] = 0;
    }

  }
  return false;
}

//Function to determine if graph can be coloured with at most M colours such
//that no two adjacent vertices of graph are coloured with same colour.
bool graphColoring(bool graph[101][101], int m, int N) {
  int color[N] = {
    0
  };
  if (solve(0, color, m, N, graph)) return true;
  return false;
}

int main() {
  int N = 4;
  int m = 3;

  bool graph[101][101];
  memset(graph, false, sizeof graph);

  // Edges are (0, 1), (1, 2), (2, 3), (3, 0), (0, 2)
  graph[0][1] = 1; graph[1][0] = 1;
  graph[1][2] = 1; graph[2][1] = 1;
  graph[2][3] = 1; graph[3][2] = 1;
  graph[3][0] = 1; graph[0][3] = 1;
  graph[0][2] = 1; graph[2][0] = 1;
  
  cout << graphColoring(graph, m, N);

}
```

## Go To
[Table of Content](#table-of-content)

## Backtrcking - Rat in a Maze
<p>Consider a rat placed at <strong>(0, 0)</strong> in a square matrix<strong> </strong>of order <strong>N * N</strong>. It has to reach the destination at <strong>(N – 1, N – 1)</strong>. Find all possible paths that the rat can take to reach from source to destination. The directions in which the rat can move are <strong>‘U'(up)</strong>, <strong>‘D'(down)</strong>, <strong>‘L’ (left)</strong>, <strong>‘R’ (right)</strong>. Value 0 at a cell in the matrix represents that it is blocked and the rat cannot move to it while value 1 at a cell in the matrix represents that rat can travel through it.</p>
<p><strong>Note</strong>: In a path, no cell can be visited more than one time.</p>
<p>Print the answer in lexicographical(sorted) order</p>
<p><strong>Examples:</strong></p>
<pre class="wp-block-preformatted"><strong>Example 1:</strong>

<strong>Input:</strong>
N = 4
m[][] = {{1, 0, 0, 0},
        {1, 1, 0, 1}, 
        {1, 1, 0, 0},
        {0, 1, 1, 1}}

<strong>Output:</strong> DDRDRR DRDDRR

<strong>Explanation:</strong>

<img class="lazy-loaded" loading="lazy" width="227" height="227" src="https://lh4.googleusercontent.com/S8inL4fJsNLyNYtmgFbXAx5BEcA0rgKk3-PYWkVYc90hIBhSgMYWBWtNqz82H0zCZvXqYxp1g3kDpTwjKhTYB2NjwgoHgoPU9Bve6aFzbl-mvI4I90NmEvbV0TpiQ3LXeHccBVEC" data-lazy-type="image" data-src="https://lh4.googleusercontent.com/S8inL4fJsNLyNYtmgFbXAx5BEcA0rgKk3-PYWkVYc90hIBhSgMYWBWtNqz82H0zCZvXqYxp1g3kDpTwjKhTYB2NjwgoHgoPU9Bve6aFzbl-mvI4I90NmEvbV0TpiQ3LXeHccBVEC"><noscript><img loading="lazy" width="227" height="227" src="https://lh4.googleusercontent.com/S8inL4fJsNLyNYtmgFbXAx5BEcA0rgKk3-PYWkVYc90hIBhSgMYWBWtNqz82H0zCZvXqYxp1g3kDpTwjKhTYB2NjwgoHgoPU9Bve6aFzbl-mvI4I90NmEvbV0TpiQ3LXeHccBVEC"></noscript>

The rat can reach the destination at (3, 3) from (0, 0) by two paths - DRDDRR and DDRDRR, when printed in sorted order we get DDRDRR DRDDRR.

<strong>Example 2:</strong>

<strong>Input:</strong> N = 2
       m[][] = {{1, 0},
                {1, 0}}

<strong>Output:</strong>
 No path exists and the destination cell is blocked.
</pre>
<h3><strong>Solution</strong></h3>
<p><strong>Intuition:</strong></p>
<p>The best way to solve such problems is using recursion.</p>
<p><strong>Approach</strong>:</p>
<ul><li>Start at the source(0,0) with an empty string and try every possible path i.e upwards<strong>(U)</strong>, downwards<strong>(D)</strong>, leftwards<strong>(L)</strong> and rightwards<strong>(R)</strong>.</li><li>As the <strong>answer </strong>should be in lexicographical order so it’s better to try the <strong>directions </strong>in lexicographical order i.e (D,L,R,U)</li><li>Declare a 2D-array named visited because the question states that a single cell should be included only once in the path,so it’s important to keep track of the visited cells in a particular path.</li><li>If a cell is in path, mark it in the visited array.</li><li>Also keep a check of the<strong> “out of bound” </strong>conditions while going in a particular direction in the matrix.&nbsp;</li><li>Whenever you reach the destination<strong>(n,n)</strong> it’s very important to get back as shown in the recursion tree.</li><li>While getting back, keep on unmarking the visited array for the respective direction.Also check whether there is a different path possible while getting back and if yes, then mark that cell in the visited array.</li></ul>
<p><strong>Recursive tree:</strong></p>
<p><img class="lazy-loaded" loading="lazy" width="624" height="420" src="https://lh5.googleusercontent.com/G8Ix6_osmHr9thVF0o1o5QL-V6-G2wQPM3J1IwCTFcc3rzoGNbwNo9ZuIjLl5BNrx-bj50VxcU1A3qC6EPiKUxxOD2OtsBAGz0jQksI03jn8r9vkGX2QZs31ghpwUZIHLxTMsgRt" data-lazy-type="image" data-src="https://lh5.googleusercontent.com/G8Ix6_osmHr9thVF0o1o5QL-V6-G2wQPM3J1IwCTFcc3rzoGNbwNo9ZuIjLl5BNrx-bj50VxcU1A3qC6EPiKUxxOD2OtsBAGz0jQksI03jn8r9vkGX2QZs31ghpwUZIHLxTMsgRt"><noscript><img loading="lazy" width="624" height="420" src="https://lh5.googleusercontent.com/G8Ix6_osmHr9thVF0o1o5QL-V6-G2wQPM3J1IwCTFcc3rzoGNbwNo9ZuIjLl5BNrx-bj50VxcU1A3qC6EPiKUxxOD2OtsBAGz0jQksI03jn8r9vkGX2QZs31ghpwUZIHLxTMsgRt"></noscript></p>
<p><strong>For&nbsp; “DDRDRR” :</strong></p>
<div class="wp-block-columns">
<div class="wp-block-column" style="flex-basis:50%">
<p><strong><img class="lazy-loaded" loading="lazy" width="288" height="303" src="https://lh4.googleusercontent.com/jHuDgGszsySZjD2RTMQE4DCT_9OC46Red7ulQwP-8ctIP-C8zxYn2NMljOS4E_y6P1ByfQ3F5vabBsAPJIiuhy-4j5GvHgs0wjkdJQSb9KT1zooSxHb9XqwAGjwyDspd30ZBscHF" data-lazy-type="image" data-src="https://lh4.googleusercontent.com/jHuDgGszsySZjD2RTMQE4DCT_9OC46Red7ulQwP-8ctIP-C8zxYn2NMljOS4E_y6P1ByfQ3F5vabBsAPJIiuhy-4j5GvHgs0wjkdJQSb9KT1zooSxHb9XqwAGjwyDspd30ZBscHF"><noscript><img loading="lazy" width="288" height="303" src="https://lh4.googleusercontent.com/jHuDgGszsySZjD2RTMQE4DCT_9OC46Red7ulQwP-8ctIP-C8zxYn2NMljOS4E_y6P1ByfQ3F5vabBsAPJIiuhy-4j5GvHgs0wjkdJQSb9KT1zooSxHb9XqwAGjwyDspd30ZBscHF"></noscript></strong> </p>
</div>



<div class="wp-block-column" style="flex-basis:50%">
<p><strong><img class="lazy-loaded" loading="lazy" src="https://lh5.googleusercontent.com/HRDMA8b1Htmoz-vNJKntjUXhBnmjptURMWkykzEe4jEP2eYVtP6As4Zf_uBX-vVf9r1wK-hBJ2wuGhKKvikRUr5URVTYArEjhE-TQEAd98505_L0M-EqylJxVawURD1Z4lagpyfc" data-lazy-type="image" data-src="https://lh5.googleusercontent.com/HRDMA8b1Htmoz-vNJKntjUXhBnmjptURMWkykzEe4jEP2eYVtP6As4Zf_uBX-vVf9r1wK-hBJ2wuGhKKvikRUr5URVTYArEjhE-TQEAd98505_L0M-EqylJxVawURD1Z4lagpyfc" width="271" height="296"><noscript><img loading="lazy" src="https://lh5.googleusercontent.com/HRDMA8b1Htmoz-vNJKntjUXhBnmjptURMWkykzEe4jEP2eYVtP6As4Zf_uBX-vVf9r1wK-hBJ2wuGhKKvikRUr5URVTYArEjhE-TQEAd98505_L0M-EqylJxVawURD1Z4lagpyfc" width="271" height="296"></noscript></strong></p>
</div>
</div>
<p><strong>Code:</strong></p>

```
#include <bits/stdc++.h>

using namespace std;

class Solution {
  void solve(int i, int j, vector < vector < int >> & a, int n, vector < string > & ans, string move,
    vector < vector < int >> & vis, int di[], int dj[]) {
    if (i == n - 1 && j == n - 1) {
      ans.push_back(move);
      return;
    }
    string dir = "DLRU";
    for (int ind = 0; ind < 4; ind++) {
      int nexti = i + di[ind];
      int nextj = j + dj[ind];
      if (nexti >= 0 && nextj >= 0 && nexti < n && nextj < n && !vis[nexti][nextj] && a[nexti][nextj] == 1) {
        vis[i][j] = 1;
        solve(nexti, nextj, a, n, ans, move + dir[ind], vis, di, dj);
        vis[i][j] = 0;
      }
    }

  }
  public:
    vector < string > findPath(vector < vector < int >> & m, int n) {
      vector < string > ans;
      vector < vector < int >> vis(n, vector < int > (n, 0));
      int di[] = {
        +1,
        0,
        0,
        -1
      };
      int dj[] = {
        0,
        -1,
        1,
        0
      };
      if (m[0][0] == 1) solve(0, 0, m, n, ans, "", vis, di, dj);
      return ans;
    }
};

int main() {
  int n = 4;

 vector < vector < int >> m = {{1,0,0,0},{1,1,0,1},{1,1,0,0},{0,1,1,1}};
   
  Solution obj;
  vector < string > result = obj.findPath(m, n);
  if (result.size() == 0)
    cout << -1;
  else
    for (int i = 0; i < result.size(); i++) cout << result[i] << " ";
  cout << endl;

  return 0;
}
```
<p><strong>Output:</strong></p>
<p>DDRDRR DRDDRR</p>
<p><strong>Time Complexity: O(4^(m*n)), </strong>because<strong> </strong>on every cell we need to try 4 different directions.</p>
<p><strong>Space Complexity:&nbsp; O(m*n), </strong>Maximum Depth of the recursion tree(auxiliary space).</p>


## Go To
[Table of Content](#table-of-content)
