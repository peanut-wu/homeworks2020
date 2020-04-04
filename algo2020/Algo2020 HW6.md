Algo2020 HW6

邮箱：sswu@pku.edu.cn

- 1. 最长回文子串
  - 链接：https://leetcode-cn.com/problems/longest-palindromic-substring/
  
  - 代码：
    ````c++
        #define get(s, i) ((i & 0x1) ? '#' : s[i >> 1])
        class Solution {
        public:
            string longestPalindrome(string s) {
                int len = 1 + (s.length() << 1), c = -1, r = 0, ans = 0;
                vector<int> p;
                p.resize(len);
                for (int i = 0; i < len; ++i) {
                    p[i] = r > i ? min(r - i, p[2 * c - i]) : 0;
                    while (i - p[i] - 1 >= 0 && i + p[i] + 1 < len &&
                        get(s, i - p[i] - 1) == get(s, i + p[i] + 1))
                        ++p[i];
                    if (i + p[i] > r) r = i + p[i], c = i;
                    if (p[ans] < p[i]) ans = i;
                }
                int st = (ans - p[ans] + 1) >> 1, nd = (ans + p[ans]) >> 1;
                return s.substr(st, nd - st + 1);
            }
        };
    ````
    
  - 截图：
  
    ![s1](./imgs/h6-1.png)
  
  - 思路：Manacher算法裸题。

- 2. 最小路径和
  
  - 链接：https://leetcode-cn.com/problems/minimum-path-sum/
  
  - 代码：
    ````c++
        class Solution {
        public:
            int minPathSum(vector<vector<int>>& grid) {
                int n = grid.size(), m = grid[0].size();
                for (int j = 1; j < m; ++j) grid[0][j] += grid[0][j - 1];
                for (int i = 1; i < n; ++i) {
                    grid[i][0] += grid[i - 1][0];
                    for (int j = 1; j < m; ++j)
                        grid[i][j] += min(grid[i][j - 1], grid[i - 1][j]);
                }
                return grid[n - 1][m - 1];
            }
        };
    ````

  - 截图：
  
    ![s1](./imgs/h6-2.png) 
  
- 思路：状态转移方程：$dp[i][j]=min(dp[i-1][j],dp[i][j-1])+a[i][j]$。
  
- 3.  三角形最小路径和
  
  - 链接：https://leetcode-cn.com/problems/triangle/submissions/
  
  - 代码：
    ````c++
        class Solution {
        public:
            int minimumTotal(vector<vector<int>>& triangle) {
                for (int i = triangle.size() - 2; i >= 0; --i) {
                    for (int j = 0; j < triangle[i].size(); ++j)
                        triangle[i][j] +=
                            min(triangle[i + 1][j], triangle[i + 1][j + 1]);
                }
                return triangle[0][0];
            }
        };
    ````
    
  - 截图：
  
    ![s1](./imgs/h6-3.png)

  - 思路：状态转移方程：$dp[i][j]=min(dp[i-1][j],dp[i-1][j-1])+a[i][j]$,
