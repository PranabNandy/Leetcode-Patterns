- Bhai Tume dekkar me motivate ho jata tha
- Bhai tum caho toh kuch kar sakte ho
- Bhai tere pas toh System Engineering domain ka pura data hai
- Kon kaha swicth kiya hai ...kaise wo top position pe hai
- bhai hum logo ka batch me tumse tez kohi nehi tha be
  
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
**2. https://leetcode.com/problems/find-all-numbers-disappeared-in-an-array/description/**

**Alternative of bitset is boolean array**
```
vector<bool> seen(size(nums)+1);
```
**Cyclic Sort Variations**

![Screenshot from 2024-01-12 21-09-46](https://github.com/PranabNandy/Leetcode-Patterns/assets/34576104/846e6285-3b5a-4c53-ae69-005e60b0080c)
```
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        vector<int> ans;
        int n=nums.size();
        for(int i=0;i<n;++i){
            while(nums[i]!=nums[nums[i]-1]){
                   swap(nums[i],nums[nums[i]-1]);
            }
        }
        for(int i=0;i<n;i++){
            if(nums[i]!=i+1) ans.push_back(i+1);
        }
      return ans;
        
    }
};
```
**Make Negative of Array Elements**
```
class Solution {
public:
    vector<int> findDisappearedNumbers(vector<int>& nums) {
        vector<int> ans;
        int n=nums.size();
        for(int i=0;i<n;i++){
            int ele=abs(nums[i]);
            nums[ele-1]=-abs(nums[ele-1]);
        }
        for(int i=0;i<n;i++){
            if(nums[i]>0) ans.push_back(i+1);
        }
      return ans;
        
    }
};
```

**3. https://leetcode.com/problems/single-number/**

**Substract from set elements**
```
    int singleNumber(vector<int>& nums) {
        int sum_1=0,sum_2=0;
        unordered_set<int> um;
        for(int &i: nums){
            um.insert(i);
            sum_1+=i;
        } 
        for(auto it: um){
            sum_2+=2*(it);
        }
        return sum_2-sum_1;
    }
```
**4.https://leetcode.com/problems/move-zeroes/**

**`Alternative`** `of two pointer `: Basically it is an old step of two pointer


``` 
   void moveZeroes(vector<int>& nums) {
        ios_base::sync_with_stdio(false);
        cin.tie(0);
        cout.tie(0);
        int cnt=0;
        int j=0;
        int n=nums.size();
        for(int i=0;i<n;i++){
            if(nums[i]) nums[j++]=nums[i];
        }
        for(int i=j;i<n;i++) nums[i]=0;
    }
```
**5.https://leetcode.com/problems/product-of-array-except-self/**
- Space = O(1)
- Time = O(n)
```
class Solution {
public:
    vector<int> productExceptSelf(vector<int>& nums) {
          int n=nums.size();
          vector<int> L(n);
          L[0]=1;
          for(int i=1;i<n;i++) L[i]=L[i-1]*nums[i-1];
          int R=1;
          for(int i=n-1;i>=0;i--){
              L[i]=L[i]*R;
              R=R*nums[i];
          }
          return L;
    }
};
```
**6.https://leetcode.com/problems/find-the-duplicate-number/**

## Index Sort

```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int n=nums.size();
        for(int i=0;i<n;i++){
            int index=nums[i];
            if(index==i+1) continue;
            else if(nums[i]==nums[nums[i]-1]) return nums[i];
            else{
                swap(nums[i],nums[nums[i]-1]);
                i--;
            }
        }
        return 0;
    }
};
```
### Marking array elements to -ve
```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int n=nums.size();
        for(int i=0;i<n;i++){
            int index=abs(nums[i]);
            if(nums[index]<0) return index;
            nums[index]=-nums[index];
        }
        return 0;
    }
};
```
**Slow Pointer and fast pointer concept**
![Screenshot from 2024-01-19 18-02-26](https://github.com/PranabNandy/Leetcode-Patterns/assets/34576104/4fa9c675-8202-4324-a4fa-ffa371c4f9ab)

```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int n=nums.size();
        int fast=nums[0],slow=nums[0];
        do{
           slow=nums[slow];
           fast=nums[nums[fast]];
        }while(fast!=slow); 
        fast=nums[0];
        while(slow!=fast){
            slow=nums[slow];
            fast=nums[fast];
        } 
        return slow;
    }
};
```
