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
## Binary Search Variations
```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int n=nums.size();
        int low=1;
        int high=n-1;
        int mid;
        int cnt;
        while(low<high){
            mid=low+(high-low)/2;
            cnt=0;
            for(int i=0;i<n;i++){
                if(nums[i]<=mid) cnt++;
            }
            if(cnt<=mid) low=mid+1;
            else high=mid;
        }
        return low;
    }
};
```
## special bit manipulation with array element and array index
- The inner loop calculates the count of set bits at the bit position for both the `array elements (x)` and the `array positions (y)`.
- If `x (count of set bits in the array)` is greater than `y (count of set bits in the array positions)`, it means there is a duplicate number with a set bit at the current position.
```
class Solution {
public:
    int findDuplicate(vector<int>& nums) {
        int n = nums.size();
        int bits=31;
        while((n-1)>>bits==0)
        {
            bits--;
        } 
        int x=0,y=0,ans=0;
        for(int bit=0;bit<=bits;bit++){
            x=0,y=0;
            for(int i=0;i<n;i++){
                if((nums[i]&(1<<bit))!=0) x++;
                if(i!=0){ // as there m+1 elements counting from 1 to m
                    if((i & (1<<bit))!=0) y++;
                }
            }
            if(x>y)
                ans |=(1<<bit);
        }
        return ans;
    }
};
```
**7.https://leetcode.com/problems/find-all-duplicates-in-an-array/**

**Making the array elements -ve     || Pigeon Hole Principle**
```
class Solution {
public:
    vector<int> findDuplicates(vector<int>& nums) {
          ios_base::sync_with_stdio(false);
          cin.tie(NULL);
          cout.tie(NULL);
          int n=nums.size();
          vector<int> ans;
          for(int i=0;i<n;i++){
              int index=abs(nums[i]);
              if(nums[index-1]<0) ans.push_back(index);
              else nums[index-1]=-nums[index-1];
          }
          return ans;
    }
};
```

**8.https://leetcode.com/problems/set-matrix-zeroes/**

**Used Sets** : T=O(N*M) S=(N+M)
```
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        unordered_set<int> R,C;
        int n=matrix.size();
        int m=matrix[0].size();
        for(int i=0;i<n;i++){
            for(int j=0;j<m;j++){
                if(matrix[i][j]==0){
                    R.insert(i);
                    C.insert(j);
                }
            }
        }
        for(auto it=R.begin();it!=R.end();it++){
            int r=*it;
            for(int j=0;j<m;j++)
                matrix[r][j]=0;
        }
        for(auto it=C.begin();it!=C.end();it++){
            int c=*it;
            for(int i=0;i<n;i++)
                matrix[i][c]=0;
        }
        
    }
};
```
**Constant Space**
![Screenshot from 2024-01-23 03-49-00](https://github.com/PranabNandy/Leetcode-Patterns/assets/34576104/992d13fd-0f3f-4e55-8653-c8aa40235f1e)
```
class Solution {
public:
    void setZeroes(vector<vector<int>>& matrix) {
        
        int n=matrix.size();
        int m=matrix[0].size();
        bool R=false,C=false;
        for(int i=0;i<n;i++){
            if(matrix[i][0]==0)
                C=true;
        }
        for(int j=0;j<m;j++){
            if(matrix[0][j]==0)
                R=true;
        }
        for(int i=1;i<n;i++){
            for(int j=1;j<m;j++){
                if(matrix[i][j]==0){
                    matrix[0][j]=0;
                    matrix[i][0]=0;
                }
            }
        }
        for(int i=1;i<n;i++){
            if(matrix[i][0]==0){
                for(int j=0;j<m;j++) matrix[i][j]=0;
            }
        }
        for(int j=1;j<m;j++){
            if(matrix[0][j]==0){
                for(int i=0;i<n;i++) matrix[i][j]=0;
            }
        }
        if(R){
            for(int j=0;j<m;j++) matrix[0][j]=0;
        }
        if(C){
            for(int i=0;i<n;i++) matrix[i][0]=0;
        }
        
    }
};
```
**9.https://leetcode.com/problems/rotate-image/**
```
class Solution {
public:
    
    void rotate(vector<vector<int>>& matrix) {
        int n=matrix.size();
        int m=matrix[0].size();
        for(int i=0;i<n;i++){
            for(int j=0;j<i;j++)
                swap(matrix[i][j],matrix[j][i]);
        }

        for(int i=0;i<n;i++){
            reverse(matrix[i].begin(),matrix[i].end());
        }
    }
};
```
**10.https://leetcode.com/problems/longest-consecutive-sequence/**

Brute Force approach, T=O(N^3) S=O(1)
```
class Solution {
private:
    bool check(vector<int> &nums, int target){
        int n=nums.size();
        for(int i=0;i<n;i++){
            if(nums[i]==target) return true;
        }
        return false;
    }
public:
    int longestConsecutive(vector<int>& nums) {
        int longestSeq=1;
        int n=nums.size();
        for(int i=0;i<n;i++){
            int val=nums[i];
            int longest=1;
            while(check(nums,val+1)){
                longest++;
                val++;
            }
            longestSeq=max(longestSeq,longest);
        }
        return longestSeq;
        
    }
};
```
## There is a huge differenence between Hash.count(x) and Hash[x]
- If we don't erase the element of Hash Table ( `Hash.erase(x)` ) the `Hash.count(x)` will be 1
- `Hash[x]=count` then we can make it  `Hash[x]=0` but it does not impact the `Hash.count(x)`
- Unorder_set (Hash Table) Approach T=O(N) S=O(N)
- 
Hash Table count concept | Also Hash[nums[i]_+j] != 0 | 
--- | --- |
I used this concept in New Problem | 23/1/2024 | 
```
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int longestSeq=0;
        int n=nums.size();
        unordered_map<int,bool> Hash;
        for(int i=0;i<n;i++) 
            Hash[nums[i]]=true;
        for(int i=0;i<n;i++){
            // it means nums[i] is not the starting point of a consecutive subsequence
            if(Hash.count(nums[i]-1)>0) 
                Hash[nums[i]]=false;
        }
        for(int i=0;i<n;i++){
            int j=1;
            if(Hash[nums[i]]){
                while(Hash.count(nums[i]+j)>0)
                    j++;
            }
            longestSeq=max(longestSeq,j);
        }
        return longestSeq;
        
    }
};
```
## set does not have count function
- We can avoid the use of count in Hash Table if we follow this set technique
- T=O(N)   S=O(N)

```
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        int longestSeq=0;
        int n=nums.size();
        unordered_set<int> set;
        for(int i=0;i<n;i++) 
            set.insert(nums[i]);
        
        for(int i=0;i<n;i++){   
            int j=1;
            if(set.find(nums[i]-1)==set.end()){
                while(set.find(nums[i]+j)!=set.end())
                    j++;
            }
            longestSeq=max(longestSeq,j);
        }
        return longestSeq;
        
    }
};

```
## using Disjoint set Union
![Screenshot from 2024-01-24 11-37-11](https://github.com/PranabNandy/Leetcode-Patterns/assets/34576104/459284fb-da2c-4c27-84ca-612642c45414)

```
class Solution {
private:
    vector<int> parent, Rank;
    int find(int a){
        if(parent[a]==a) return parent[a];
        else return find(parent[a]);
    }
    void Union(int a,int b){
        int par_a=find(a);
        int par_b=find(b);
        if(par_a==par_b) return;
        if(Rank[par_a]>Rank[par_b]){
            parent[par_b]=par_a;
            Rank[par_a]+=Rank[par_b];
        }
        else{
            parent[par_a]=par_b;
            Rank[par_b]+=Rank[par_a];
        }
    }
public:
    int longestConsecutive(vector<int>& nums) {
        int n=nums.size();
        parent.clear(); parent.resize(n+1);
        Rank.clear(); Rank.resize(n+1);
        unordered_map<int,int> Hash;
        Hash.clear();
        int ans=0;

        for(int i=0;i<n;i++){
            parent[i]=i; Rank[i]=1;
        }
        for(int i=0;i<n;i++){
            if(Hash.count(nums[i])) continue;

            if(Hash.count(nums[i]+1)) Union(i,Hash[nums[i]+1]);        
            if(Hash.count(nums[i]-1)) Union(i,Hash[nums[i]-1]);
    
            Hash[nums[i]]=i;
        }
        for(int i=0;i<n;i++) ans=max(ans,Rank[i]);
        return ans;
    }
};
```
** We can use DP + Interval concept using Hash[val]={left,right}**
```
class Solution {
public:
    int longestConsecutive(vector<int>& nums) {
        unordered_map<int,bool> vis;
        unordered_map<int,pair<int,int>> Hash;
        int ans=0;
        int n=nums.size();
        for(int i=0;i<n;i++){
            int val=nums[i];
            if(vis[val]) continue;
            vis[val]=true;
            int l=val,r=val;
            if(Hash.count(val+1)){
                r=Hash[val+1].second;
            }
            if(Hash.count(val-1)){
                l=Hash[val-1].first;
            }
            // It will not work, we need to use while loop
            // Hash[val]={l,r};  
            Hash[l]={l,r};
            Hash[r]={l,r};
            ans=max(ans,r-l+1);
        }
        return ans;
    }
};
```
