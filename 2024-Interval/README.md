**1.https://leetcode.com/problems/merge-intervals/description/**

```
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
