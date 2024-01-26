**1.https://leetcode.com/problems/number-of-islands/description/**
![Screenshot from 2024-01-26 18-18-39](https://github.com/PranabNandy/Leetcode-Patterns/assets/34576104/26f63e51-6c3f-44ff-b64f-8b4c43f943dd)

```
class Solution {
private:
    vector<int> parent;
    int islands;
    vector<pair<int,int>> adj={{-1,0},{0,-1},{1,0},{0,1}};
    int find(int node){
        if(node==parent[node]) return parent[node];
        else return find(parent[node]);
    }
    void Union(int a, int b){
        int par_a=find(a);
        int par_b=find(b);
        if( par_b != par_a){
             parent[par_a]=par_b;
             islands--;   
        }
    }
    void init_union(vector<vector<char>>& grid){
        int n=grid.size();
        int m=grid[0].size();
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(grid[i][j]=='1'){
                    islands++;
                    int index=i*m+j;
                    parent[index]=index;
                } 
            }
        }
    }
public:
    int numIslands(vector<vector<char>>& grid) {
        islands=0;
        parent.clear();
        int n=grid.size();
        int m=grid[0].size();
        parent.resize(n*m);
        init_union(grid);
         for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(grid[i][j]=='1'){
                    for(auto k:adj){
                        int x=i+k.first;
                        int y=j+k.second;
                        if(x>=0 && x<n && y>=0 && y<m && grid[x][y]=='1'){
                            int element1=i*m+j;
                            int element2=x*m+y;
                            Union(element1,element2);
                        }
                    }
                }
            }
        }
        return islands;
    }
};
```
