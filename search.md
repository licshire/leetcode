## 搜索
- 深度优先遍历
- 广度优先遍历
- Union Find
---

#### 130. Surrounded Regions
###### 题目描述：

Given a 2D board containing 'X' and 'O' (the letter O), capture all regions surrounded by 'X'.
A region is captured by flipping all 'O's into 'X's in that surrounded region.

For example,
```
X X X X
X O O X
X X O X
X O X X
```

After running your function, the board should be:
```
X X X X
X X X X
X X X X
X O X X
```

###### 思路：

未被包围的区域一定和四周的O相连，以边界O且未被标记的位置为起点深度或广度遍历，标记所有相连的O。最后没有被标记的O替换为X。 

###### 代码：
```
class Solution {
    
    int row;
    int col;
    public void solve(char[][] board) {
        
        if (board.length == 0)
            return;
        
        row = board.length;
        col = board[0].length;
        
        int[][] labled = new int[row][col];
        
        for (int i = 0; i < row; i++){
            
            for (int j = 0; j < col; j++){
                
                if (board[i][j] == 'O' && (i == 0 || i == row-1 || j == 0 || j == col-1) && labled[i][j] == 0){
                    
                    fill(i, j, board, labled);
                }
            }
        }
        
         for (int i = 0; i < row; i++){
            
            for (int j = 0; j < col; j++){
                
                if (board[i][j] == 'O' && labled[i][j] != 1){
                    board[i][j] = 'X';
                }
            }
        }
        
    }
    
    public void fill(int i, int j, char[][] board, int[][] labeled){
        
        if (i < 0 || j < 0 || i >= row || j >= col || board[i][j] == 'X' || labeled[i][j] == 1)
            return;
        
        labeled[i][j] = 1;
        
        fill(i-1, j, board, labeled);
        fill(i+1, j, board, labeled);
        fill(i, j-1, board, labeled);
        fill(i, j+1, board, labeled);
    }
}

```

---
#### 200. Number of Islands

###### 题目描述：
Given a 2d grid map of '1's (land) and '0's (water), count the number of islands. An island is surrounded by water and is formed by connecting adjacent lands horizontally or vertically. You may assume all four edges of the grid are all surrounded by water.

Example 1:
```
11110
11010
11000
00000
```
Answer: 1

Example 2:
```
11000
11000
00100
00011
```
Answer: 3

###### 思路：
同上题，遍历所有位置，遇到未被标记的1,计数加1,，并进行深度或广度遍历，遍历到的1进行标记。
###### 代码：
```

class Solution {
    
    int row;
    int col;
    public int numIslands(char[][] grid) {
        
        int count = 0;
        
        if (grid.length == 0)
            return count;
        
        row = grid.length;
        col = grid[0].length;
        
        int[][] labled = new int[row][col];
        
        for (int i = 0; i < row; i++){
            for (int j = 0; j < col; j++){
                if (grid[i][j] == '1' && labled[i][j] == 0){
                    count++;
                    fill(i, j, grid, labled);
                }
            }
        }   
        
        return count;
        
    }
    
    public void fill(int i, int j, char[][] board, int[][] labeled){
        
        if (i < 0 || j < 0 || i >= row || j >= col || board[i][j] == '0' || labeled[i][j] == 1)
            return;
        
        labeled[i][j] = 1;
        
        fill(i-1, j, board, labeled);
        fill(i+1, j, board, labeled);
        fill(i, j-1, board, labeled);
        fill(i, j+1, board, labeled);
    }
}
```

---

#### 695. Max Area of Island
###### 题目描述：
Given a non-empty 2D array grid of 0's and 1's, an island is a group of 1's (representing land) connected 4-directionally (horizontal or vertical.) You may assume all four edges of the grid are surrounded by water.

Find the maximum area of an island in the given 2D array. (If there is no island, the maximum area is 0.)

Example 1:
```
[[0,0,1,0,0,0,0,1,0,0,0,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,1,1,0,1,0,0,0,0,0,0,0,0],
 [0,1,0,0,1,1,0,0,1,0,1,0,0],
 [0,1,0,0,1,1,0,0,1,1,1,0,0],
 [0,0,0,0,0,0,0,0,0,0,1,0,0],
 [0,0,0,0,0,0,0,1,1,1,0,0,0],
 [0,0,0,0,0,0,0,1,1,0,0,0,0]]
```
Given the above grid, return 6. Note the answer is not 11, because the island must be connected 4-directionally.
Example 2:
[[0,0,0,0,0,0,0,0]]
Given the above grid, return 0.
Note: The length of each dimension in the given grid does not exceed 50.

###### 思路：
同上，边标记边计数，并记录当前最大值。
###### 代码：

```
class Solution {
    
    int row;
    int col;
    public int maxAreaOfIsland(int[][] grid) {
        
        int max = 0;
        if (grid.length == 0)
            return max;
        row = grid.length;
        col = grid[0].length;
        
        int[][] labled = new int[row][col];
        
        for (int i = 0; i < row; i++){
            for (int j = 0; j < col; j++){
                if (grid[i][j] == 1 && labled[i][j] == 0){
                    int cur = fill(i, j, grid, labled);
                    if (cur > max){
                        max = cur;
                    }
                }
            }
        }   
        
        return max;
    }
    
    public int fill(int i, int j, int[][] board, int[][] labeled){
        
        if (i < 0 || j < 0 || i >= row || j >= col || board[i][j] == 0 || labeled[i][j] == 1)
            return 0;
        
        labeled[i][j] = 1;
        
        return 1 + fill(i-1, j, board, labeled) + fill(i+1, j, board, labeled) + fill(i, j-1, board, labeled) + fill(i, j+1, board, labeled);     
    }
}
```

---
## 215. Kth Largest Element in an Array

###### 题目描述：
Find the kth largest element in an unsorted array. Note that it is the kth largest element in the sorted order, not the kth distinct element.
For example,
Given [3,2,1,5,6,4] and k = 2, return 5.

Note: 
You may assume k is always valid, 1 ≤ k ≤ array's length.

###### 思路
1、参考快速排，进行快速搜索，平均复杂度O（n）,最差O（N×N）
2、堆，保持k个元素的大根堆
###### 代码
S1：
```
class Solution {
    public int findKthLargest(int[] nums, int k) {
            
        int n = nums.length;
        int loc = quickSearch(0, nums.length-1,  n-k+1, nums);
        return nums[loc];
    }
    
    public int quickSearch(int start, int end, int k, int[] nums){
        
        
        int i = start, j = end, pov = nums[end];

        while (i < j){
            if (nums[i++] > pov)
                swap(nums, --i, --j);
        }
        swap(nums, i, end);
        
        int loc = i - start + 1;
        
        if (loc == k)
            return i;
        if (loc > k)// res in left
            return quickSearch(start, i-1, k, nums);
        else // res in right
            return quickSearch(i+1, end, k-loc, nums);
            
    }
    
    public void swap(int[] nums, int i, int j){
        
        int tmp = nums[i];
        nums[i] = nums[j];
        nums[j] = tmp;
    }
}
```
S2：
```
//         PriorityQueue<Integer> q = new PriorityQueue(new Comparator<Integer>() {
//                     public int compare(Integer i1, Integer i2) {
//                         return i2 - i1;
//                     }
//                 });
//         for (int i = 0; i < nums.length; i++){
//             q.add(nums[i]);
//         }
//         int res = 0;
//         while (k != 0){
//             res = q.poll();
//             k--;
//         }
        
//         return res;        
```
