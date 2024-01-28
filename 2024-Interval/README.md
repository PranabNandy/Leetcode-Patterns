![Screenshot from 2024-01-28 12-18-00](https://github.com/PranabNandy/Leetcode-Patterns/assets/34576104/1e20e934-cef7-4fb9-a3c5-5b04e00d394a)
**1.https://leetcode.com/problems/merge-intervals/description/**

```cpp
class Solution {
public:

    static bool comp(vector<int> &v1,vector<int> &v2);
! ---------------------------------------------------------------- !
    vector<vector<int>> merge(vector<vector<int>>& arr) {
        int n=arr.size();
        sort(arr.begin(),arr.end(),comp);
        vector<vector<int>> ans;
        ans.push_back(arr[0]);
        for(int i=1;i<n;i++){
            if(ans.back()[1]<arr[i][0]) ans.push_back(arr[i]);
            else ans.back()[1]=max(ans.back()[1],arr[i][1]);
        }
        return ans;
    }
};

! ---------------------------------------------------------------- !
bool Solution::comp(vector<int> &v1, vector<int> &v2){
    if(v1[0]<v2[0]) return true;
    else return false;
}
```
**2.https://leetcode.com/problems/interval-list-intersections/description/**
![Screenshot from 2024-01-27 15-27-55](https://github.com/PranabNandy/Leetcode-Patterns/assets/34576104/75cbbcc8-7f27-4a0e-8db0-ffc281ab44f1)
```cpp
class Solution {
public:
    vector<vector<int>> intervalIntersection(vector<vector<int>>& first, vector<vector<int>>& second) {
        int n=first.size();
        int m=second.size();
        int i=0,j=0;
        vector<vector<int>> merge;
        while(i<n && j<m){
            int s1=first[i][0], e1=first[i][1];
            int s2=second[j][0], e2=second[j][1];
            if(s1<=e2 && s2<=e1){
                int x=max(s1,s2);
                int y=min(e1,e2);
                merge.push_back({x,y});
            }      
            if(e1<e2) i++;
            else j++;
        }
        return merge;
    }

};
```
**3.https://leetcode.com/problems/non-overlapping-intervals/**
### Greedy Approach
- Based on sorting of **any of the points**(`start point or end point`)
```cpp
class Solution {
private:
public:
    int eraseOverlapIntervals(vector<vector<int>>& arr) {
        // Considering end point during sorting
      /*sort(arr.begin(),arr.end(),[](vector<int> &a,vector<int> &b){
            if(a[1]<b[1]) return true;
            else if(a[1]>b[1]) return false;
            else return a[0]<b[0];
        });*/
        // Considering start point during sorting
        sort(arr.begin(),arr.end(),[](vector<int> &a,vector<int> &b){
            if(a[0]<b[0]) return true;
            else if(a[0]>b[0]) return false;
            else return a[1]<b[1];
        });
        
        int cnt=0;
        int global_end=arr[0][1];
        int n=arr.size();
        for(int i=1;i<n;i++){
            int start=arr[i][0];
            int end=arr[i][1];
            if(global_end<=start){
                global_end=end;
            }
            else{
                global_end=min(end,global_end);
                cnt++;
            }
        }
        return cnt;
    }
};
```
### Top Down Approach => DP ( Recursion + Memorization)

```cpp
class Solution {
private:
    vector<int> dp;
    int solve(vector<vector<int>> &arr,int global_end, int index){
        if(index>=arr.size())
            return 0;
        
        int pick=0,not_pick;
        if(dp[index]!=-1) return dp[index];
        if(global_end<=arr[index][0]){
            pick=1+solve(arr,arr[index][1],index+1);
        }
        not_pick=solve(arr,global_end,index+1);
        return dp[index]=max(pick,not_pick);
    }
public:
    int eraseOverlapIntervals(vector<vector<int>>& arr) {
        // Considering end point during sorting
        sort(arr.begin(),arr.end(),[](vector<int> &a,vector<int> &b){
            if(a[1]<b[1]) return true;
            else if(a[1]>b[1]) return false;
            else return a[0]<b[0];
        });
        int n=arr.size();
        dp.clear();
        dp.resize(n,-1);
        int global_end=INT_MIN, index=0;
        int cnt=solve(arr,global_end,index);
        return n-cnt;
    }
};
```
