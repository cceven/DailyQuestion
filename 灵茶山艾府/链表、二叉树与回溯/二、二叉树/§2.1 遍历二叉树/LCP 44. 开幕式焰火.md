# [LCP 44. 开幕式焰火](https://leetcode.cn/problems/sZ59z6/)

「力扣挑战赛」开幕式开始了，空中绽放了一颗二叉树形的巨型焰火。 给定一棵二叉树 `root` 代表焰火，节点值表示巨型焰火这一位置的颜色种类。请帮小扣计算巨型焰火有多少种不同的颜色。

## **示例 1：**

> 输入：`root = [1,3,2,1,null,2]`
>
> 输出：`3`
>
> 解释：焰火中有 3 个不同的颜色，值分别为 1、2、3

## **示例 2：**

> 输入：`root = [3,3,3]`
>
> 输出：`1`
>
> 解释：焰火中仅出现 1 个颜色，值为 3

## **提示：**

- `1 <= 节点个数 <= 1000`
- `1 <= Node.val <= 1000`

## 代码

```cpp
/**
 * definition for a binary tree node.
 * struct treenode {
 *     int val;
 *     treenode *left;
 *     treenode *right;
 *     treenode(int x) : val(x), left(null), right(null) {}
 * };
 */
class solution {
private:
    unordered_set<int> ans;

    void dfs(treenode* root) {
        if (root == nullptr)
            return;

        if (ans.find(root->val) == ans.end())
            ans.insert(root->val);

        if (root->left)
            dfs(root->left);
        if (root->right)
            dfs(root->right);
    }

public:
    int numcolor(treenode* root) {
        dfs(root);
        return ans.size();
    }
}
```

