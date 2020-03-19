Algo2020 HW1

邮箱：sswu@pku.edu.cn

- 1.两数之和
  - 链接：https://leetcode-cn.com/problems/two-sum/
  
  - 代码：
    ````c++
    class Solution {
    public:
        vector<int> twoSum(vector<int>& nums, int target) {
            map<int, int> p;
            vector<int> ans;
            for (int i = 0; i < nums.size(); ++i)
                if (p.find(target - nums[i]) != p.end()) {
                    ans.push_back(p[target - nums[i]]);
                    ans.push_back(i);
                    break;
                } else {
                    p[nums[i]] = i;
                }
            return ans;
        }
    };
    ````
    
  - 截图：
  
    ![s1](https://peanut-1256769371.cos.ap-chengdu.myqcloud.com/s1.png)
  
  - 思路：遍历每个元素，对于$a_i$，判断$target-a_i$是否在$a_j,0 \leq j \leq i-1$中出现过；第二步的判断可以使用数据结构如哈希表、二叉平衡树加速；使用哈希表时总时间复杂度为$O(n)$，使用二叉平衡树时总时间复杂度为$O(nlogn)$。代码中使用c++内置的红黑树加速，时间复杂度为$O(nlogn)$。
  
- 2.x的平方根
  
  - 链接：https://leetcode-cn.com/problems/sqrtx/
  
  - 代码：
    ````c++
    class Solution {
    public:
        int mySqrt(int x) {
            long long l = 1, r = x, mid;
            int ans = 0;
            while (l <= r) {
                mid = (l + r) >> 1;
                if (mid * mid <= x)
                    ans = mid, l = mid + 1;
                else
                    r = mid - 1;
            }
            return ans;
        }
    };
    ````
    
  - 截图：
  
    ![s2](https://peanut-1256769371.cos.ap-chengdu.myqcloud.com/s2.png)
  
  - 思路：设$f(i)=(i*i\leq x?0:1)$，则题目要求找到满足$f(i)=0$的最大整数$i$，显然函数$f$具有单调性，因此可以使用二分查找，时间复杂度为$O(logx)$。  
- 3.爬楼梯
  
  - 链接：https://leetcode-cn.com/problems/climbing-stairs
  
  - 代码：
    ````c++
    class Solution {
    public:
        int climbStairs(int n) {
            int f0 = 1, f1 = 1;
            for (int i = 1; i < n; ++i) {
                f0 += f1;
                swap(f0, f1);
            }
            return f1;
        }
    };
    ````
    
  - 截图：
  
    ![s3](https://peanut-1256769371.cos.ap-chengdu.myqcloud.com/s3.png)
  
  - 思路：由题意可以得出递推公式$f(i)=f(i-1)+f(i-2),f(0)=f(1)=1$，即斐波那契数列，常用算法矩阵快速幂/公式求解/线性递推。由题目返回值是int却没要求答案取模可知，数据范围不大，使用线性递推即可，时间复杂度为$O(n)$。