# 866 Problems
```c++
If N = 10^4   --> O(N^2)
   N=  10^5   --> O(N logN)
   N=  10^6   --> O(N)
```

 ```c++
   static bool compare(vector<int> &a, vector<int> &b){
        if(a[0]<b[0]) return 1;
        else if(a[0]>b[0]) return 0;
        else return a[1]<b[1];
    }
    int maxEvents(vector<vector<int>>& events) {
        int n = events.size();
        sort(events.begin(),events.end(),compare);
        .......
   }
```
1. G - **Mar, 2024** - Fail
2. G - **May, 2024** - Pass
3. G - **Mar, 2025** - Fail  [ 1 year ]
4. `F - Jun, 2025 - Fail`
5. G - **Mar, 2026** - Fail
6. G - **Mar, 2027** - Fail
7. G - **Mar, 2028** - Pass
- One Tree Problem ( parent has to send its data to child)
- One HwTimer Problem
```c++
8 Months = 16 courses
5 Months = 450 Q
```
2. Sorting :
3. Array :
4. Binary_search :
5. String : https://github.com/PranabNandy/Leetcode-Patterns/blob/main/2025/5.string.md
6. Linked_list:
7. Recursion:
8. Bit_manupulation:
9. stack_queue:
10. sliding_window_2_pointer:
11. Heaps:
12. Greedy:
13. Binary_tree:
14. BST :
15. Graphs: https://github.com/PranabNandy/Leetcode-Patterns/blob/main/2025/15.Graphs.md
16. DP : https://github.com/PranabNandy/Leetcode-Patterns/blob/main/2025/16.DP.md
17. Trie:
18. Random Question : https://github.com/PranabNandy/Leetcode-Patterns/blob/main/2025/18.Ramdom.md 
```c++
int main() {
    // 18 = (10010)
    bitset<5> bs1(18);
    // 5 = (00101)
    bitset<5> bs2(5);
    // AND Operator 
    cout << (bs1 & bs2) << endl;
    // OR Operator
    cout << (bs1 | bs2) << endl;
    // XOR operator
    cout << (bs1 ^ bs2);

    if(bs1==bs2) cout<<"Pranab";
    else cout<<"Nandy "<<bs1.count()<<" "<<bs2.count();
    return 0;
}
```
