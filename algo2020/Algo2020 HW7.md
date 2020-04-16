Algo2020 HW7

邮箱：sswu@pku.edu.cn

- 1. 背包问题
  - 题目：一个旅行者随身携带一个背包, 可以放入背包的物品有n种, 每种物品的重量和价值分别是wi, vi, i=1,…, n. 如果背包的最大容量限制是V, 怎样选择放入背包的物品以使得背包的价值最大? 
  
  - 代码：
    ````c++
      /*
      struct Node {
          int w, v;
      } a[max_n];
      */
      int sol(vector<Node> &a, int V) {
          vector<int> dp(V + 1);
          for (int i = 0; i < a.size(); ++i)
              for (int j = V; j >= a[i].w; --j)
                  dp[j] = max(dp[j], dp[j - a[i].w] + a[i].v);
          return dp[V];
      }
    ````
  
  - 思路：
    - 当每种物品只能拿一次时，为01背包，NPC问题，不存在多项式解法。常用的是动态规划解法，转移方程为$dp[i][j]=max(dp[i-1][j],dp[i-1][j-weight[i]]+value[i]
    $，具备伪多项式时间复杂度$O(n*V)$，优化递推顺序后需要$O(V)$额外空间，代码如上所示。此外，当V较大而n较小时，中途相遇法也常用于解背包问题，会更加划算。
- 2. 投资问题
  
  - 题目：设有m元钱，n项投资，函数fi(x) 表示将x元钱投入到第i项项目所产生的效益，i=1，……，n。问：如何分配这m元钱，使得投资的总效益最高？
  
  - 代码：
    ````c++
        int sol(vector<vector<int>> f, int m) {
            vector<int> dp(m + 1);
            int n = f.size();
            for (int i = 0; i < n; ++i)
                for (int j = m; j >= 0; --j)
                    for (int k = 0; k <= j; ++k)
                        dp[j] = max(dp[j], dp[j - k] + f[i][k]);
            return dp[m];
        }
    ````
  
- 思路：不对fi(x)的函数性质做任何假设时，可以看作分组背包问题，转移方程$f[k][j]=max(f[k−1][j],f[k−1][j−c[i]]+w[i] item i \in group k)$，时间复杂度$O(n*m*m)$，需要$O(m)$额外空间。当fi(x)有一些性质时，可以进行别的优化。
  
- 3.  最小花费爬楼梯
  
  - 链接：https://leetcode-cn.com/problems/min-cost-climbing-stairs/submissions/
  
  - 代码：
    ````c++
      class Solution {
        public:
          int minCostClimbingStairs(vector<int>& cost) {
              int n = cost.size();
              for (int i = 2; i < n; ++i) cost[i] += min(cost[i - 1], cost[i - 2]);
              return min(cost[n - 1], cost[n - 2]);
          }
      };
    ````
    
  - 截图：
  
    ![s1](./imgs/h7-3.png)

  - 思路：状态转移方程：$f[i]=min(f[i-1],f[i-2])+a[i]$,
