Algo2020 HW8

邮箱：sswu@pku.edu.cn

- 1. 编辑距离
  - 链接：https://leetcode-cn.com/problems/edit-distance/
  
  - 代码：
    ````c++
        class Solution {
          public:
            int minDistance(string word1, string word2) {
                int s1 = word1.length(), s2 = word2.length();
                if (s1 == 0 || s2 == 0) return s1 + s2;
                vector<vector<int> > dp(s1 + 1);
                for (int i = 0; i <= s1; ++i) dp[i].resize(s2 + 1);
                for (int i = 0; i <= s2; ++i) dp[0][i] = i;
                for (int i = 0; i < s1; ++i) {
                    dp[i + 1][0] = i + 1;
                    for (int j = 0; j < s2; ++j) {
                        dp[i + 1][j + 1] = min(min(dp[i + 1][j] + 1, dp[i][j + 1] + 1),
                                              dp[i][j] + (word1[i] != word2[j]));
                    }
                }
                return dp[s1][s2];
            }
        };
    ````
    
  - 截图：
  
    ![s1](./imgs/h8-1.png)
  
  - 思路：设$dp(i,j)$为字符串$s1$前$i$位与字符串$s2$前$j$位相匹配的最小编辑距离，则状态转移方程为$dp(i + 1,j + 1)=min(dp(i + 1,j) + 1, dp(i,j + 1) + 1,dp(i,j)+(s1[i]!=s2[j]))$，三项分别对应增加、删除、替换。

- 2.  戳气球
  
  - 链接： https://leetcode-cn.com/problems/burst-balloons/
  
  - 代码：
    ````c++
        #define max_n 5001
        int dp[max_n][max_n];
        bool used[max_n][max_n];
        int max(int a, int b) { return a > b ? a : b; }
        int dfs(int l, int r, int* a, int n) {
            if (used[l][r])
                return dp[l][r];
            else if (l == r)
                return 1;
            used[l][r] = true;
            int ans = 0, k = (l == 0 ? 1 : a[l - 1]) * (r == n ? 1 : a[r - 1]);
            for (int i = l + 1; i < r; ++i)
                ans = max(ans, dfs(l, i, a, n) + dfs(i, r, a, n) + a[i - 1] * k);
            return dp[l][r] = ans;
        }
        int maxCoins(int* nums, int numsSize) {
            memset(used, 0, sizeof(used));
            return dfs(0, numsSize + 1, nums, numsSize + 1);
        }
    ````

  - 截图：
  
    ![s1](./imgs/h8-2.png) 
  
- 思路：$dp(l,r)$代表区间$(l,r)$(即$[l+1,r-1]$)之间戳气球的最优值，则$dp(l,r)=max{dp(l,i)+dp(i,r)+a[l]*a[i]*a[r]}, l < i < r $。
  
- 3.  我的日程安排表 I
  
  - 链接：https://leetcode-cn.com/problems/my-calendar-i/
  
  - 代码：
    ````c++
      class MyCalendar {
        public:
          map<int, int> f;
          MyCalendar() {
              f[-1] = -1;
              f[1000000001] = 1000000001;
          }
          bool book(int start, int end) {
              auto r = f.upper_bound(start);
              auto l = r;
              --l;
              if (l->second > start || r->first < end) return false;
              f[start] = end;
              return true;
          }
      };
    ````
    
  - 截图：
  
    ![s1](./imgs/h8-3.png)

  - 思路：如果允许离线处理，那么用离散化+差分树状数组可以达到代码量和时间复杂度较好的平衡；然而这题强制在线，只能用平衡树一类才能达到$O(logN)$的单次操作复杂度，使用map自带的红黑树实现。
