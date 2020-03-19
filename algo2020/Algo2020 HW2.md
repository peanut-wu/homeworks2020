Algo2020 HW2

邮箱：sswu@pku.edu.cn
 
- 1.整数反转
  - 链接：https://leetcode-cn.com/problems/reverse-integer
  
  - 代码：
    ````c++
      class Solution {
        public:
          int reverse(int x) {
              int op = 1;
              long long ans = 0, xx = x;
              if (xx < 0) xx = -xx, op = -1;
              while (xx) ans = ans * 10 + (xx % 10), xx /= 10;
              ans *= op;
              return (ans == (int)ans) ? ans : 0;
          }
      };
    ````
    
  - 截图：
  
    ![s1](https://peanut-1256769371.cos.ap-chengdu.myqcloud.com/h2_1.png)
  
  - 思路：使用取模运算从低到高取出数字，使用强制类型转换判断是否超出int表示范围。
  
- 2.加1
  
  - 链接：https://leetcode-cn.com/problems/plus-one/
  
  - 代码：
    ````c++
      class Solution {
        public:
          vector<int> plusOne(vector<int>& digits) {
              vector<int> ans;
              int siz = digits.size();
              ans.resize(siz + 1);
              ans[siz] = 1;
              for (int i = siz; i > 0; --i) {
                  ans[i] += digits[i - 1];
                  ans[i - 1] += (ans[i] / 10);
                  ans[i] %= 10;
              }
              if (ans[0] == 0) ans.erase(ans.begin());
              return ans;
          }
      };
    ````
    
  - 截图：
  
    ![s2](https://peanut-1256769371.cos.ap-chengdu.myqcloud.com/h2_2.png)
  
  - 思路：扩增一位后模拟加法进位，最后根据首位是否为0决定是否删去首位。  
- 3.罗马数字转整数
  
  - 链接：https://leetcode-cn.com/problems/roman-to-integer
  
  - 代码：
    ````c++
      class Solution {
          int a[256];
    
        public:
          Solution() {
              a['I'] = 1, a['V'] = 5, a['X'] = 10, a['L'] = 50, a['C'] = 100,
              a['D'] = 500, a['M'] = 1000;
          }
          int romanToInt(string s) {
              int len = s.length();
              int ans = a[s[len - 1]];
              for (int i = 0; i < len - 1; ++i)
                  if (a[s[i]] < a[s[i + 1]])
                      ans -= a[s[i]];
                  else
                      ans += a[s[i]];
              return ans;
          }
      };
    ````
    
  - 截图：
  
    ![s3](https://peanut-1256769371.cos.ap-chengdu.myqcloud.com/h2_3.png)
  
  - 思路：遍历字符串，当当前位置字符对应值小于下一位置字符对应值时用减法，否则用加法。