
**1. https://leetcode.com/problems/missing-number/description/**
- Special Case:
- **Using bitset:**
```
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n=nums.size();
        bitset<10001> arr;    // it takes constant arguments
        for(int i=0;i<n;i++)
            arr.set(nums[i]);
        for(int i=0;i<=n;i++){
            if(arr[i]==0) return i;
        }
        return 0;
    }
};
```
`**arr.to_string()  && arr.to_ulong()**` 


- **Using sum of N numbers**:
```
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n = nums.size();
        int total_sum = (n*(n+1))/2;
        for(auto x: nums){
            total_sum -=x;
        }
        return total_sum;
    }
};
```
- **Using x-or logic**:
```
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int ans=0;
        int n=nums.size();
        for(int i=0;i<=n;i++)
            ans=ans^i;
        for(int i=0;i<n;i++)
            ans=ans^nums[i];
        return ans;
    }
};
```
- **Using set**:
```
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        unordered_set<int> s;
        int n=nums.size();
        for(int i=0;i<n;i++){
            s.insert(nums[i]);     // These are the 2 important functions
        }
        for(int i=0;i<=n;i++){
            if(s.end()==s.find(i)) return i;   // These are 2 important functions
        }
        return 0;

    }
};
```
### https://www.linkedin.com/in/prantikmukherjee/
- **Using Cyclic sort variants**:
- ![Screenshot from 2024-01-01 22-57-36](https://github.com/PranabNandy/Leetcode-Patterns/assets/34576104/46bd886b-b24c-4dcb-9f44-069ae220f576)
```
- Take the example of 1 element array
- Then 2 elements ( Check all possibilities like 3 cases)
- Then 3 elements (Check all possibilities like 6 case)
- Then 4 elements
class Solution {
public:
    int missingNumber(vector<int>& nums) {
        int n=nums.size();
        if(n==1){
            if(nums[0]==0) return 1;
            return 0;
        }
        for(int i=0;i<n;i++){
            int index=abs(nums[i]);
            if(index==INT_MAX)   // As we set the value of 0 to -INT_MAX
                index=0;
            /* Actions starts from here
             * [0,2]   even though for index=1, value=2 but "1" is not present in the array
             * So we did not do anything
             * If some index nums[i]=1 then nums[1]= -2 (new updated value)
             * It means value 1 present in the array
             */  
            if(index==n){
                continue;
            }
            else if(nums[index]==0)
                nums[index]=-INT_MAX;
            else
                nums[index]=-nums[index];   
        }
        for(int i=0;i<n;i++){
           if(nums[i]>=0)  return i;
           // Why not nums[i]>0  .... [2,0] here no one changing the value of "0" so return value should be "1" 
        }
        return n;
    }
};
```

