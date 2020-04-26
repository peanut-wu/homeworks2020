Algo2020 HW8

邮箱：sswu@pku.edu.cn

- 1. 平衡二叉树
  - 链接：https://leetcode-cn.com/problems/balanced-binary-tree/
  
  - 代码：
    ````c++
        /**
        * Definition for a binary tree node.
        * struct TreeNode {
        *     int val;
        *     TreeNode *left;
        *     TreeNode *right;
        *     TreeNode(int x) : val(x), left(NULL), right(NULL) {}
        * };
        */
        class Solution {
        public:
            int h(TreeNode *root, bool &result) {
                if (root == NULL) return 0;
                int l = h(root->left, result), r = h(root->right, result);
                result = result & (abs(l - r) <= 1);
                return max(l, r) + 1;
            }
            bool isBalanced(TreeNode *root) {
                bool ans = true;
                h(root, ans);
                return ans;
            }
        };
    ````
    
  - 截图：
  
    ![s1](./imgs/h9-1.png)
  
  - 思路：递归求树高，同时维护一下答案。

- 2.  二叉搜索树的最近公共祖先
  
  - 链接：https://leetcode-cn.com/problems/sort-list/
  
  - 代码：
    ````c++
        class Solution {
        public:
            TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
                int l = p->val, r = q->val;
                if (l > r) swap(l, r);
                for (;;) {
                    if (root->val < l)
                        root = root->right;
                    else if (root->val > r)
                        root = root->left;
                    else
                        return root;
                }
            }
        };
    ````
    
  - 截图：
  
    ![s1](./imgs/h9-2.png) 
 
  - 思路：利用二叉搜索树的性质判断下一步要走的子树。

- 3. 二叉树的所有路径
  
  - 链接：https://leetcode-cn.com/problems/binary-tree-paths/
  
  - 代码：
    ````c++
        class Solution {
            vector<string> result;

        public:
            void dfs(TreeNode* root, string ans) {
                if (root->left == NULL && root->right == NULL) {
                    result.push_back(std::move(ans));
                    return;
                }
                if (root->left != NULL) {
                    stringstream tmp;
                    tmp << "->" << root->left->val;
                    dfs(root->left, ans + tmp.str());
                }
                if (root->right != NULL) {
                    stringstream tmp;
                    tmp << "->" << root->right->val;
                    dfs(root->right, ans + tmp.str());
                }
            }
            vector<string> binaryTreePaths(TreeNode* root) {
                result.clear();
                if (root != NULL) {
                    stringstream tmp;
                    tmp << root->val;
                    dfs(root, tmp.str());
                }
                return result;
            }
        };
    ````
    
  - 截图：
  
    ![s1](./imgs/h9-3.png)

  - 思路：递归搜索即可。
