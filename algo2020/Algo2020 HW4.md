Algo2020 HW4

邮箱：sswu@pku.edu.cn

- 1. 最接近的三数之和
  - 链接：https://leetcode-cn.com/problems/3sum-closest/
  
  - 代码：
    ````c++
        class Solution {
        public:
            int threeSumClosest(vector<int>& nums, int target) {
                sort(nums.begin(), nums.end());
                int ans, mindelt = 1e9;
                for (int i = 0; i < nums.size(); ++i) {
                    int k = target - nums[i], l = i + 1, r = nums.size() - 1;
                    while (l < r) {
                        int delt = k - nums[l] - nums[r];
                        if (abs(delt) < mindelt)
                            mindelt = abs(delt), ans = nums[i] + nums[l] + nums[r];
                        if (delt <= 0)
                            --r;
                        else
                            ++l;
                    }
                    if (mindelt == 0) return ans;
                }
                return ans;
            }
        };
    ````
    
  - 截图：
  
    ![s1](./imgs/h4-1.png)
  
  - 思路：$O(nlogn)$排序后，枚举最小的一个数字，剩下两个数字采用中途相遇的方式求，复杂度$O(n^2)$。

- 2. 电话号码的字母组合
  
  - 链接：https://leetcode-cn.com/problems/letter-combinations-of-a-phone-number/submissions/
  
  - 代码：
    ````c++
        class Solution {
            const char f[8][5] = {"abc", "def",  "ghi", "jkl",
                                "mno", "pqrs", "tuv", "wxyz"};

        public:
            void dfs(const char *a, int p, int len, string &tmp, vector<string> &ans) {
                if (p == len) {
                    ans.push_back(tmp);
                    return;
                }
                int i = a[p] - '2';
                for (int j = 0; f[i][j] != '\0'; ++j) {
                    tmp[p] = f[i][j];
                    dfs(a, p + 1, len, tmp, ans);
                }
            }
            vector<string> letterCombinations(string digits) {
                string tmp = digits;
                vector<string> ans;
                if (digits.length() != 0) {
                    dfs(digits.c_str(), 0, digits.length(), tmp, ans);
                }
                return ans;
            }
        };
    ````
    
  - 截图：
  
    ![s1](./imgs/h4-2.png)  
  - 思路：dfs深度优先搜索

- 3. 删除链表的倒数第N个节点
  
  - 链接：https://leetcode-cn.com/problems/remove-nth-node-from-end-of-list/submissions/
  
  - 代码：
    ````c++
        /**
        * Definition for singly-linked list.
        * struct ListNode {
        *     int val;
        *     ListNode *next;
        *     ListNode(int x) : val(x), next(NULL) {}
        * };
        */
        class Solution {
        public:
            ListNode* removeNthFromEnd(ListNode* head, int n) {
                ListNode tmp;
                ListNode* t0 = &tmp;
                t0->next = head;
                ListNode *t1 = t0, *t2 = t0;
                for (int i = 0; i < n + 1; ++i) t2 = t2->next;
                while (t2 != NULL) t1 = t1->next, t2 = t2->next;
                // ListNode *tt=t1->next;t1->next=tt->next;free(tt);
                t1->next = t1->next->next;
                return t0->next;
            }
        };
    ````
    
  - 截图：
  
    ![s1](./imgs/h4-3.png)

  - 思路：两个相隔n+1位的指针同步挪动，后指针到达链表尾时，前指针删除其下一个节点。trick:为了防止删除头指针，事先加一个空节点。
