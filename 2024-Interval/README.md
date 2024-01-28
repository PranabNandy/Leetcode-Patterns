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
