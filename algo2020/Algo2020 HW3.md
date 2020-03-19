Algo2020 HW3

邮箱：sswu@pku.edu.cn

- 1. 搜索插入位置
  - 链接：https://leetcode-cn.com/problems/search-insert-position/
  
  - 代码：
    ````c++
        class Solution {
        public:
            int searchInsert(vector<int>& nums, int target) {
                int l = 0, r = nums.size() - 1, ans = -1;
                while (l <= r) {
                    int mid = (l + r) >> 1;
                    if (nums[mid] < target)
                        l = mid + 1, ans = mid;
                    else
                        r = mid - 1;
                }
                return ans + 1;
            }
        };
    ````
    
  - 截图：
  
    ![s1](https://peanut-1256769371.cos.ap-chengdu.myqcloud.com/h3-1.png)
  
  - 思路：题目等价描述：在一个有序数组中，找到最后一个小于$target$的数字的下标$i$，并返回$i+1$，$i$不存在时以$-1$计，因此采用二分求解。

- 2. 最后一个单词的长度
  
  - 链接：https://leetcode-cn.com/problems/length-of-last-word
  
  - 代码：
    ````c++
        class Solution {
        public:
            int lengthOfLastWord(string s) {
                int len = s.length() - 1, ans = 0;
                while (len >= 0 && s[len] == ' ') --len;
                while (len >= 0 && s[len] != ' ') --len, ++ans;
                return ans;
            }
        };
    ````
    
  - 截图：
  
    ![s2](https://peanut-1256769371.cos.ap-chengdu.myqcloud.com/h3-2.png)
  
  - 思路：先枚举除去末尾的空格，再枚举最后一个单词的长度。 

- 3. 删除排序链表中的重复元素
  
  - 链接：https://leetcode-cn.com/problems/remove-duplicates-from-sorted-list
  
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
            ListNode* deleteDuplicates(ListNode* head) {
                for (ListNode* t = head; t != NULL; t = t->next) {
                    ListNode* nx = t->next;
                    while (nx != NULL && nx->val == t->val) {
                        t->next = nx->next;
                        // free(nx);
                        nx = t->next;
                    }
                }
                return head;
            }
        };
    ````
    
  - 截图：
  
    ![s2](https://peanut-1256769371.cos.ap-chengdu.myqcloud.com/h3-3.png)
  
  - 思路：循环遍历有序链表，对于点$i$，删除其接下来与$i$值相等的节点。坑点：代码里不需要自行释放删除节点的内存。
