#
**solution**

use bfs to mark all the islands, count the number of bfs calls

**time complexity**

O(nm) to traverse the 2D array, O(k) for a single call of bfs.

**space complexity**

O(nm).

```cpp

class Solution {
public:
    bool isValid(int index,int border){
        if(index >= 0 && index < border) return true;
        else return false;
    }
    
    void dfs(vector<vector<char>>& grid,int index1,int index2){
        int n = grid.size();int m = grid[index1].size();
        grid[index1][index2] = '0';
        if(isValid(index1-1,n)) 
            if (grid[index1-1][index2] == '1') 
                dfs(grid,index1-1,index2);
        if(isValid(index1+1,n)) 
            if (grid[index1+1][index2] == '1') 
                dfs(grid,index1+1,index2);
        if(isValid(index2-1,m)) 
            if(grid[index1][index2-1] == '1') 
                dfs(grid,index1,index2-1);
        if(isValid(index2+1,m)) 
            if(grid[index1][index2+1] == '1') 
                dfs(grid,index1,index2+1);
        
    }
    
    int numIslands(vector<vector<char>>& grid) {
        int count = 0;
        for(int i = 0;i < grid.size();++ i) {
            for(int j = 0;j < grid[i].size();++ j){
                if(grid[i][j] == '1') {
                    count ++;
                    dfs(grid, i,j);
                    //cout << i << ' ' << j << endl;
                }
            }
        }
        return count;
    }
};
```