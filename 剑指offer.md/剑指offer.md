
[视频](https://www.bilibili.com/video/BV1zK4y1r7tn?p=74&vd_source=d4df260b1907b7a2424f450d404e1eba)

# cost time
二叉搜索树的后序遍历序列
数组中的逆序对
正则表达式匹配
表示数值的字符串


# 【链表】
## JZ6 从尾到头打印链表 
解法1：  
```c++
/**
*  struct ListNode {
*        int val;
*        struct ListNode *next;
*        ListNode(int x) :
*              val(x), next(NULL) {
*        }
*  };
*/
class Solution {
public:
    vector<int> printListFromTailToHead(ListNode* head) {
        vector<int> ans;
          // 从头节点开始进行遍历
        while(head){
            // 将每个节点的权值放入动态数组里面
            ans.push_back(head->val);
            // 指针后移动
            head=head->next;
        }
        // 反转整个数组
        reverse(ans.begin(),ans.end());
        return ans;
    }
};
```

两种解法： 使用栈  或者 使用递归的方式
![](vx_images/393333617235474.png =800x)





## JZ24 反转链表
迭代法和递归法
![](vx_images/199503917246370.png =500x)


## JZ25 合并两个排序的链表

两个链表都不为空的时候，
 ![](vx_images/334954017247002.png =500x)


## JZ52 两个链表的第一个公共节点
![](vx_images/550483619230444.png =300x)
 ![](vx_images/445954017237738.png =500x)
 
 
## JZ23 链表入口环的节点
![](vx_images/288343719248232.png =300x)
 ![](vx_images/458964217230597.png =500x)
 
 
## JZ22 链表中倒数第k个节点

```java
class Solution {
public:
    ListNode* FindKthToTail(ListNode* pHead, int k) {
        // write code here
        // 检测是否符合范围
        if(pHead==NULL)return 0;
        ListNode* cur = pHead;
        int count = 0;
        while(cur){
            cur = cur->next;
            count++;
        }
        if(count<k)return 0;
        // 开始找倒数第k个节点
        ListNode* fast = pHead;
        ListNode* slow = pHead;
        while(k--){
            fast = fast->next;
        }
        
        while(fast){
            fast = fast->next;
            slow = slow->next;
        }
        return slow;
    }
};
```
 

## JZ35 复杂链表的复制 
![](vx_images/513675119221481.png =600x)

主要通过map进行原来的节点和新创建的节点映射，然后遍历进行新链表的构建。
 ![](vx_images/166024317244514.png =500x)
 
 
## JZ76 删除链表的重复节点
在一个排序的链表中，存在重复的结点，请删除该链表中重复的结点，重复的结点不保留，返回链表头指针。
 例如，链表 1->2->3->3->4->4->5  处理后为 1->2->5

例如输入{1,2,3,3,4,4,5}时，对应的输出为{1,2,5}，对应的输入输出链表如下图所示：

**哈希法**
![](vx_images/79985716228099.png =600x)

```c++
class Solution {
public:
    ListNode* deleteDuplication(ListNode* pHead) {
        //空链表
        if(pHead == NULL) 
            return NULL;
        unordered_map<int, int> mp;
        ListNode* cur = pHead;
        //遍历链表统计每个节点值出现的次数
        while(cur != NULL){ 
            mp[cur->val]++;
            cur = cur->next;
        }
        ListNode* res = new ListNode(0);
        //在链表前加一个表头
        res->next = pHead; 
        cur = res;
        //再次遍历链表
        while(cur->next != NULL){ 
            //如果节点值计数不为1
            if(mp[cur->next->val] != 1) 
                //删去该节点
                cur->next = cur->next->next; 
            else
                cur = cur->next; 
        }
        //去掉表头
        return res->next; 
    }
};
```

**直接法**
![](vx_images/519635916234654.png =600x)
```java
class Solution {
public:
    ListNode* deleteDuplication(ListNode* pHead) {
        //空链表
        if(pHead == NULL) 
            return NULL;
        ListNode* res = new ListNode(0);
        //在链表前加一个表头
        res->next = pHead; 
        ListNode* cur = res;
        while(cur->next != NULL && cur->next->next != NULL){ 
            //遇到相邻两个节点值相同
            if(cur->next->val == cur->next->next->val){ 
                int temp = cur->next->val;
                //将所有相同的都跳过
                while (cur->next != NULL && cur->next->val == temp) 
                    cur->next = cur->next->next;
            }
            else 
                cur = cur->next;
        }
        //返回时去掉表头
        return res->next; 
    }
};
```


## JZ18 删除链表的节点
![](vx_images/546854317252025.png =500x)


# 【树】
## JZ55 二叉树的深度
![](vx_images/10960121248364.png =400x)

```c++
class Solution {
public:
    int TreeDepth(TreeNode* pRoot)
    {
        if (!pRoot) return 0;
        int lval = TreeDepth(pRoot->left);
        int rval = TreeDepth(pRoot->right);
        return max(lval, rval) + 1;
     
    }
};
```

## JZ77 按之字形顺序打印二叉树

![](vx_images/352150121253382.png =400x)


```c++
class Solution {
public:
    vector<vector<int> > Print(TreeNode* pRoot) {
        vector<vector<int>> res;
        if(!pRoot)return res;
        vector<int> vec;
        queue<TreeNode*> q;
        q.push(pRoot);
        TreeNode* temp = NULL;
        int i = 1;
        while(!q.empty()){
            int size = q.size();
            vec.clear();
            for(int i = 0; i< size;i++){
                temp = q.front();
                q.pop();
                vec.push_back(temp->val);
                if(temp->left) q.push(temp->left);
                if(temp->right) q.push(temp->right);
            }
            if(i%2==0)reverse(vec.begin(),vec.end());
            res.push_back(vec);
            i++;
        }
        return res;
    }
};

```

##  JZ54 二叉搜索树的第k个节点

![](vx_images/518290121253477.png =400x)

![](vx_images/27583719237754.png =500x)

```c++
class Solution {
public:
    //记录返回的节点
    TreeNode* res = NULL;
    //记录中序遍历了多少个
    int count = 0;
    //当遍历到节点为空或者超过k时，返回
    void midOrder(TreeNode* root, int k){
        if(root == NULL || count > k) 
            return;
        midOrder(root->left, k);
        count++;
        //只记录第k个
        if(count == k)  
            res = root;
        midOrder(root->right, k);
    }
    
    int KthNode(TreeNode* proot, int k) {
        midOrder(proot, k);
        if(res)
            return res->val;
        //二叉树为空，或是找不到
        else 
            return -1;
    }
};
```

##  JZ7 重建二叉树

![](vx_images/129440221240757.png =400x)

![](vx_images/192484520230732.png =600x)


## JZ26 树的子结构
![](vx_images/273720321233579.png =400x)

```c++
bool HasSubtreeCore(TreeNode* pRoot1, TreeNode* pRoot2){
    
    if(pRoot2 == nullptr) return true;//p2为空 ，那么P1什么都是相等的了
    if(pRoot1 == nullptr ) return false;//如果p2不为空，但是p1为空，那肯定是不对的
    if(pRoot1->val == pRoot2->val)//当前一样，再判断左右子树，这里必须是 与 的并列关系才行
        return HasSubtreeCore(pRoot1->left,pRoot2->left) && 
                HasSubtreeCore(pRoot1->right,pRoot2->right);
    else{
        return false;
    }
}


bool HasSubtree(TreeNode* pRoot1, TreeNode* pRoot2){
    if(pRoot1 == nullptr || pRoot2 == nullptr) return false;
    
    return HasSubtree(pRoot1->left, pRoot2) ||//有可能是我的左子树
            HasSubtree(pRoot1->right, pRoot2) || //或则是右子树
            HasSubtreeCore(pRoot1, pRoot2);//或者是当前节点就开始比较，注意这里是 或 的关系

}
```

## JZ27 二叉树的镜像（翻转）
![](vx_images/41200421229443.png =400x)



```java
void Mirror(TreeNode *pRoot) {//有点类似于二叉树的层次遍历
    if(pRoot == nullptr) return;             
    swap(pRoot->left,pRoot->right);
    Mirror(pRoot->left);
    Mirror(pRoot->right);
}
```



## JZ32 从上往下打印二叉树
![](vx_images/557310421230461.png =400x)


```java
vector<int> PrintFromTopToBottom(TreeNode* root) {
    if(root == nullptr) return vector<int>();
    queue<TreeNode*>q;
    q.push(root);
    TreeNode *node = nullptr;
    vector<int> result;
    while(!q.empty()){
        node = q.front();
        q.pop();
        result.push_back(node->val);
        if(node->left) q.push(node->left);
        if(node->right) q.push(node->right);
    }
    return result;
}
```

## x JZ33 二叉搜索树的后序遍历序列 true? 

![](vx_images/334880521248249.png =500x)

```java
class Solution {
public:
    bool VerifySquenceOfBST(vector<int> sequence) {
        // 处理序列为空情况
        if(sequence.size() == 0) return false;
        
        stack<int> s;
        int root = INT_MAX;
        // 以根，右子树，左子树顺序遍历
        for(int i = sequence.size() - 1; i >= 0; i--) {
            // 确定根后一定是在右子树节点都遍历完了，
            //因此当前sequence未遍历的节点中只含左子树，
            //左子树的节点如果>root则说明违背二叉搜索的性质
            if(sequence[i] > root) return false;
            // 进入左子树的契机就是sequence[i]的值小于前一项的时候，这时可以确定root
            while(!s.empty() && s.top() > sequence[i]) {
                root = s.top();
                s.pop();
            }
            // 每个数字都要进一次栈
            s.push(sequence[i]);
        }
        return true;
    }
};

```

## JZ82 二叉树中和为某一值的路径(一) true

![](vx_images/186920721221498.png =400x)

给你二叉树的根节点 root 和一个表示目标和的整数 targetSum 。判断该树中是否存在 根节点到叶子节点 的路径，这条路径上所有节点值相加等于目标和 targetSum 。如果存在，返回 true ；否则，返回 false 

1. 参数：需要二叉树的根节点，还需要一个计数器，这个计数器用来计算二叉树的一条边之和是否正好是目标和，计数器为int型。
遍历的路线，并不要遍历整棵树，所以递归函数需要返回值，可以用bool类型表示。

2. 
不要去累加然后判断是否等于目标和，那么代码比较麻烦，可以用递减，让计数器count初始为目标和，然后每次减去遍历路径节点上的数值。
如果最后count == 0，同时到了叶子节点的话，说明找到了目标和。
如果遍历到了叶子节点，count不为0，就是没找到。

3. 
因为终止条件是判断叶子节点，所以递归的过程中就不要让空节点进入递归了。


![](vx_images/542384111240853.png =700x)



## JZ34 二叉树中和为某一值的路径(二) res

![](vx_images/555010721233036.png =500x)

```c++
class Solution {
public:
    vector<vector<int>> ret;
    vector<int> path;
    void dfs(TreeNode* root, int number) {
        // 处理树为空
        if (root == NULL) return;
        // 路径更新
        path.emplace_back(root->val);
        // number更新
        number -= root->val;
        // 如果递归当前节点为叶子节点且该条路径的值已经达到了expectNumber，则更新ret
        if(root->left == NULL && root->right == NULL && number == 0) {
            ret.emplace_back(path);
        }
        // 左右子树递归
        dfs(root->left, number);
        dfs(root->right, number);
        path.pop_back();
    }
    
    vector<vector<int>> FindPath(TreeNode* root,int expectNumber) {
        dfs(root, expectNumber);
        return ret;
    }
};
```

## JZ84 二叉树中和为某一值的路径(三) 不用root-leave的路径
![](vx_images/420551421239984.png =400x)



## JZ36 二叉搜索树与双向链表
![](vx_images/427420821242910.png =500x)

中序遍历二叉树，然后用一个数组类保存遍历的结果，这样在数组中节点就按顺序保存了，然后再来修改指针，虽然没有一点技术含量

```java
TreeNode* Convert(TreeNode* pRootOfTree)
{
	if (pRootOfTree == NULL) return pRootOfTree;
	vector<TreeNode*> result;
	Convert(pRootOfTree, result);
	return Convert(result);
}

void Convert(TreeNode* node,vector<TreeNode*>&result) {
	if (node->left != nullptr)
		Convert(node->left, result);
	result.push_back(node);
	if (node->right != nullptr)
		Convert(node->right, result);
}

TreeNode* Convert(vector<TreeNode*>& result) {
	for (int i = 0; i < result.size()-1; ++i) {
		result[i]->right = result[i + 1];
		result[i+1]->left = result[i];
}
	return result[0];
}
 
```


## JZ79 判断是不是平衡二叉树
![](vx_images/144050921222562.png =500x)

1. 明确递归函数的参数和返回值
// -1 表示已经不是平衡二叉树了，否则返回值是以该节点为根节点树的高度
int getHeight(TreeNode* node)
2. if (node == NULL) {
    return 0;
    }
    
3. 明确单层递归的逻辑
分别求出其左右子树的高度，然后如果差值小于等于1，则返回当前二叉树的高度，否则则返回-1，表示已经不是二叉平衡树了。

![](vx_images/306671311241039.png =700x)



## JZ8 二叉树的下一个结点

![](vx_images/107571121221008.png =500x)



```java
class Solution {
public:
    vector<TreeLinkNode*> nodes;
    TreeLinkNode* GetNext(TreeLinkNode* pNode) {
        TreeLinkNode* root = pNode;
        // 获取根节点
        while(root->next) root = root->next;    
        
        // 中序遍历用nodes储存所有节点指针
        InOrder(root);                          
        int n = nodes.size();
        
        for(int i = 0; i < n - 1; i++) {
            TreeLinkNode* cur = nodes[i];
            // 将结点进行匹配       
            if(pNode == cur) {
                // 如果有匹配到给出的结点，则下一个结点即返回结果                  
                return nodes[i+1];              
            }
        }
        // 否则如果没有下一个结点则返回NULL
        return NULL;                            
    }
    // 中序遍历
    void InOrder(TreeLinkNode* root) {          
        if(root == NULL) return;
        InOrder(root->left);
        nodes.push_back(root);
        InOrder(root->right);
    }
};
```


## JZ28 对称二叉树
给定一棵二叉树，判断其是否是自身的镜像（即：是否对称）

```java
bool isEqual(TreeNode*node1,TreeNode*node2){
    if(node1==nullptr && node2 ==nullptr)  return true;
    if(node1 ==nullptr || node2==nullptr) return false;//减少逻辑判断
    if(node1->val == node2->val) {
        return isEqual(node1->left,node2->right) && 
                isEqual(node1->right,node2->left);//注意这里是右左，左右来进行判断

    }else
        return false;
}
bool isSymmetrical(TreeNode* pRoot) {
    if(pRoot==nullptr) return true;//这里是返回true的
    return isEqual(pRoot->left,pRoot->right);
}
```

## JZ78 把二叉树打印成多行
给定一个节点数为 n 二叉树，要求从上到下按层打印二叉树的 val 值，同一层结点从左至右输出，每一层输出一行，将输出的结果存放到一个二维数组中返回。
![](vx_images/12901321229760.png =300x)

```java
vector<vector<int> > Print(TreeNode* pRoot) {
    if(pRoot == nullptr) return vector<vector<int>>();

    queue<TreeNode*> q;
    q.push(pRoot);
    vector<vector<int>> result;
    while(!q.empty()){
        int size = q.size();
        vector<int> temp;
        while(size--){
            pRoot = q.front();
            q.pop();
            temp.push_back(pRoot->val);
            if(pRoot->left)  q.push(pRoot->left);
            if(pRoot->right)  q.push(pRoot->right);

        }
        if(temp.size() > 0) result.push_back(temp);
    }
    return std::move(result);
}

```

## JZ37 序列化二叉树
请实现两个函数，分别用来序列化和反序列化二叉树，不对序列化之后的字符串进行约束，但要求能够根据序列化之后的字符串重新构造出一棵与原二叉树相同的树。
![](vx_images/132391421229662.png =400x)


```java
/*
struct TreeNode {
    int val;
    struct TreeNode *left;
    struct TreeNode *right;
    TreeNode(int x) :
            val(x), left(NULL), right(NULL) {
    }
};
*/
class Solution {
private:
	string SerializeCore(TreeNode* root) {
		if(root == nullptr) {
            return "#!";
        }
        
        string str;
        str +=to_string(root->val) + '!';
        str +=SerializeCore(root->left);
        str +=SerializeCore(root->right);
		return str;
	}

	TreeNode* DeserializeCore(char*& str) {
		if(*str == '#'){
            str++;
            return nullptr;
        }
        int num = 0;
        while( *str != '!'){
            num = num*10 + (*str)-'0';
            str++;
        }
        TreeNode *node = new TreeNode(num);
        node->left = DeserializeCore(++str);
        node->right = DeserializeCore(++str);
        
        return node;
	}

public:
	char* Serialize(TreeNode* root) {
		string str = SerializeCore(root);
        char *chs = new char[str.size()];
        for(int i = 0;i<str.size();++i){
            chs[i] = str[i];
        }
        return chs;

	}

	TreeNode* Deserialize(char* str) {
		return DeserializeCore(str);
	}
};

```






## JZ86 在二叉树中找到两个节点的最近公共祖先

给定一棵二叉树(保证非空)以及这棵树上的两个节点对应的val值 o1 和 o2，请找到 o1 和 o2 的最近公共祖先节点。

![](vx_images/156761621243368.png =400x)

先给出递归函数的定义：给该函数输入三个参数 root，p，q，它会返回一个节点：

情况 1，如果 p 和 q 都在以 root 为根的树中，函数返回的即使 p 和 q 的最近公共祖先节点。

情况 2，那如果 p 和 q 都不在以 root 为根的树中怎么办呢？函数理所当然地返回 null 呗。

情况 3，那如果 p 和 q 只有一个存在于 root 为根的树中呢？函数就会返回那个节点。

- 根据这个定义，分情况讨论：

情况 1，如果 p 和 q 都在以 root 为根的树中，那么 left 和 right 一定分别是 p 和 q（从 base case 看出来的）。

情况 2，如果 p 和 q 都不在以 root 为根的树中，直接返回 null。

情况 3，如果 p 和 q 只有一个存在于 root 为根的树中，函数返回该节点。


```java
class Solution {
public:
    TreeNode* lowestCommonAncestor(TreeNode* root, TreeNode* p, TreeNode* q) {
        if (root == q || root == p || root == NULL) return root;
        TreeNode* left = lowestCommonAncestor(root->left, p, q);
        TreeNode* right = lowestCommonAncestor(root->right, p, q);
        if (left != NULL && right != NULL) return root;

        if (left == NULL && right != NULL) return right;
        else if (left != NULL && right == NULL) return left;
        else  { //  (left == NULL && right == NULL)
            return NULL;
        }

    }
};
```




# 【栈和队列】
## JZ9 用两个栈实现队列

利用辅助栈，删除的时候装进去找到顶层，然后再拿出来返回第一个栈
 ![](vx_images/301044417251036.png =500x)
 
## JZ30 包含min函数的栈
![](vx_images/182331921244525.png =500x)


辅助数组 使用一个vector<int> 记录最小的数字 
Stack +vector
 ![](vx_images/407654417238376.png =500x)
  
## JZ31 栈的压入、弹出序列

输入两个整数序列，第一个序列表示栈的压入顺序，请判断第二个序列是否可能为该栈的弹出顺序。假设压入栈的所有数字均不相等。例如序列1,2,3,4,5是某栈的压入顺序，序列4,5,3,2,1是该压栈序列对应的一个弹出序列，但4,3,5,1,2就不可能是该压栈序列的弹出序列。

for循环嵌套while循环的用法，，常用 在滑动窗口中也可以使用 模拟（注意栈中途弹出的情况，不能单纯全比较）

 ![](vx_images/512414417225367.png =600x)
 
 


## 二叉搜索树的后序遍历序列 判断真假




两种思路 递归分治 和 单调栈
 ![](vx_images/60324517235844.png =700x)

单调栈

## JZ73 翻转单词序列

![](vx_images/161052021236610.png =600x)

```c++
class Solution {
public:
    string split(string s){
        istringstream sin(s);
        string str;
        vector<string> res;
        while(getline(sin,str,' ')){
            res.push_back(str);
        }
        reverse(res.begin(),res.end());
        string ret = "";
        for(int i = 0; i < res.size()-1;i++){
            ret += res[i];
            ret += " ";
        }
        ret += res[res.size()-1];
        return ret;
    }
    string ReverseSentence(string str) { 
        if(str=="") return "";
        return split(str);
    }
};
```
栈结构 或者 使用 双指针 容易出错
 ![](vx_images/224964517228414.png =500x)
 

## JZ59 滑动窗口的最大值
![](vx_images/207462316232563.png =600x)

 ![](vx_images/4934617248956.png =700x)
 ![](vx_images/158994617227571.png =700x)
 
# 【搜索算法】
## JZ53 数字在升序数组中出现的次数
 ![](vx_images/246872421227449.png =500x)


二分搜索的上下界

http://zhangxiaoya.github.io/2015/06/26/upper-bound-and-lower-bound-of-binary-search/ 
 ![](vx_images/98154717246250.png =700x)
  
![](vx_images/14003220227432.png =500x)
![](vx_images/90483220245073.png =500x)




## JZ4 二维数组中的查找
![](vx_images/489672421245090.png =500x)


 ![](vx_images/497434817253460.png =500x)


## JZ11 旋转数组的最小数字
![](vx_images/75702521236070.png =500x)

![](vx_images/191031713240352.png =800x)

 ![](vx_images/134124917240740.png =650x)

## JZ38 字符串的排列

![](vx_images/460572521235726.png =600x)


```c++
class Solution {
public:
    void recursion(vector<string> &res, string &str, string &temp, vector<int> &vis){
        //临时字符串满了加入输出
        if(temp.length() == str.length()){ 
            res.push_back(temp);
            return;
        }
        //遍历所有元素选取一个加入
        for(int i = 0; i < str.length(); i++){ 
            //如果该元素已经被加入了则不需要再加入了
            if(vis[i]) 
                continue;
            if(i > 0 && str[i - 1] == str[i] && !vis[i - 1])
                //当前的元素str[i]与同一层的前一个元素str[i-1]相同且str[i-1]已经用过了
                continue;
            //标记为使用过  
            vis[i] = 1;  
            //加入临时字符串
            temp.push_back(str[i]); 
            recursion(res, str, temp, vis);
            //回溯
            vis[i] = 0; 
            temp.pop_back();
        }
    }
    
    vector<string> Permutation(string str) {
        //先按字典序排序，使重复字符串相邻
        sort(str.begin(), str.end()); 
        //标记每个位置的字符是否被使用过s
        vector<int> vis(str.size(), 0); 
        vector<string> res;
        string temp;
        //递归获取
        recursion(res, str, temp, vis); 
        return res;
    }
};

```


## JZ44 数字序列中某一位的数字
数字以 0123456789101112131415... 的格式作为一个字符序列，在这个序列中第 2 位（从下标 0 开始计算）是 2 ，第 10 位是 1 ，第 13 位是 1 ，以此类题，请你输出第 n 位对应的数字。


```c++
class Solution {
public:
//比较详细了
    /*
    1-9       9个*1
    10-99     90个*2
    100-999   900个*3
    1000-9999 9000个*4
    */
    int findNthDigit(int n) {
        // write code here
        if(n==0)return 0;
        long long start=1;//起始数
        long long digit=1;//记录位数
        long long count=9;//记录区间个数，比如9 90 900
        while(n>count){//先减去前面有规律的数
            digit++;
            n-=count;
            start*=10;
            count=digit*9*start;
        }
        //以下就是n剩余的数
        //这里我们先判断剩余的n是在哪个数
        long long number=start+(n-1)/digit;//start就是开始的第一个数字，所以后面要n-1
        //判断好是在哪个数字后，下面对数字分解
        long long temp=(n-1)%digit+1;//这个数的第几位
        for(int i=digit;i>temp;i--){//把这个数后面多余的尾巴去掉
            number/=10;
            cout<<number<<" ";
        }
        return number%10;
    }
};
```



# 【动态规划】
## JZ42 连续子数组的最大和 有负数
可以用动态规划 或者 前缀和的思路进行解决
 ![](vx_images/539823320236053.png =500x)
 

## JZ85 连续子数组的最大和(二)？？？


## JZ69 跳台阶
一只青蛙一次可以跳上1级台阶，也可以跳上2级。求该青蛙跳上一个 n 级的台阶总共有多少种跳法（先后次序不同算不同的结果）。

![](vx_images/68083420251804.png =500x)
 

## JZ71 跳台阶扩展问题

一只青蛙一次可以跳上1级台阶，也可以跳上2级……它也可以跳上n级。求该青蛙跳上一个n级的台阶(n为正整数)总共有多少种跳法。

```c++
class Solution {
public:
    int climbStairs(int n) {
        vector<int> dp(n + 1, 0);
        dp[0] = 1;
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) { // 把m换成2，就可以AC爬楼梯这道题
                if (i - j >= 0) dp[i] += dp[i - j];
            }
        }
        return dp[n];
    }
};
```



## JZ10 斐波那契数列

```c++
class Solution {
public:
    int fib(int N) {
        if (N <= 1) return N;
        vector<int> dp(N + 1);
        dp[0] = 0;
        dp[1] = 1;
        for (int i = 2; i <= N; i++) {
            dp[i] = dp[i - 1] + dp[i - 2];
        }
        return dp[N];
    }
};
```


## JZ19 正则表达式匹配


解法一:动态规划
s 和 p 相互匹配的过程大致是，两个指针 i, j 分别在 s 和 p 上移动，如果最后两个指针都能移动到字符串的末尾，那么就匹配成功，反之则匹配失败。

正则表达算法问题只需要把住一个基本点：看 s[i] 和 p[j] 两个字符是否匹配，一切逻辑围绕匹配/不匹配两种情况展开即可。

动态规划算法的核心就是「状态」和「选择」，「状态」无非就是 i 和 j 两个指针的位置，「选择」就是模式串的 p[j] 选择匹配几个字符。

dp 函数的定义如下：

若 dp(s, i, p, j) = true，则表示 s[i..] 可以匹配 p[j..]；若 dp(s, i, p, j) = false，则表示 s[i..] 无法匹配 p[j..]。

```java
class Solution {
    public:
    // 备忘录
    vector<vector<int>> memo;

    bool isMatch(string s, string p) {
        int m = s.size(), n = p.size();
        memo = vector<vector<int>>(m, vector<int>(n, -1));
        // 指针 i，j 从索引 0 开始移动
        return dp(s, 0, p, 0);
    }

    /* 计算 p[j..] 是否匹配 s[i..] */
    bool dp(string& s, int i, string& p, int j) {
        int m = s.size(), n = p.size();
        // base case
        if (j == n) {
            return i == m;
        }
        if (i == m) {
            // 如果能匹配空串，一定是字符和 * 成对儿出现
            if ((n - j) % 2 == 1) {
                return false;
            }
            // 检查是否为 x*y*z* 这种形式
            for (; j + 1 < n; j += 2) {
                if (p[j + 1] != '*') {
                    return false;
                }
            }
            return true;
        }

        // 查备忘录，防止重复计算
        if (memo[i][j] != -1) {
            return memo[i][j];
        }

        bool res = false;

        if (s[i] == p[j] || p[j] == '.') {
            // 匹配
            if (j < n - 1 && p[j + 1] == '*') {
                // 1.1 通配符匹配 0 次或多次
                res = dp(s, i, p, j + 2)
                        || dp(s, i + 1, p, j);
            } else {
                 // 1.2 常规匹配 1 次
                res = dp(s, i + 1, p, j + 1);
            }
        } else {
            // 不匹配
            if (j < n - 1 && p[j + 1] == '*') {
                // 2.1 通配符匹配 0 次
                res = dp(s, i, p, j + 2);
            } else {
                // 2.2 无法继续匹配
                res = false;
            }
        }
        // 将当前结果记入备忘录
        memo[i][j] = res;
        return res;
    }
};
```


## JZ70 矩形覆盖
我们可以用 2*1 的小矩形横着或者竖着去覆盖更大的矩形。请问用 n 个 2*1 的小矩形无重叠地覆盖一个 2*n 的大矩形，从同一个方向看总共有多少种不同的方法？

![](vx_images/415190014233346.png =500x)


```c++
dp[1] = 1;
dp[2] = 2;
for(int i = 3; i <= number; i++)
    dp[i] = dp[i - 1] + dp[i - 2]; //公式不断相加

```


## JZ48 最长不含重复字符的子字符串 **
![](vx_images/441731908242235.png =500x)
```java
class Solution {
public:
    int lengthOfLongestSubstring(string s) {
        unordered_map<char, int> window;

        int left = 0, right = 0;
        int res = 0; // 记录结果
        while (right < s.size()) {
            char c = s[right];
            right++;
            // 进行窗口内数据的一系列更新
            window[c]++;
            // 判断左侧窗口是否要收缩
            while (window[c] > 1) {
                char d = s[left];
                left++;
                // 进行窗口内数据的一系列更新
                window[d]--;
            }
            // 在这里更新答案
            res = max(res, right - left);
        }
        return res;
    }
};
```

## JZ46 把数字翻译成字符串

有一种将字母编码成数字的方式：'a'->1, 'b->2', ... , 'z->26'。
我们把一个字符串编码成一串数字，再考虑逆向编译成字符串。
由于没有分隔符，数字编码成字母可能有多种编译结果，例如 11 既可以看做是两个 'a' 也可以看做是一个 'k' 。但 10 只可能是 'j' ，因为 0 不能编译成任何结果。
现在给一串数字，返回有多少种可能的译码结果

```c++
class Solution {
public:
    int solve(string nums) {
        //排除0
        if(nums == "0")  
            return 0;
        //排除只有一种可能的10 和 20
        if(nums == "10" || nums == "20")  
            return 1;
        //当0的前面不是1或2时，无法译码，0种
        for(int i = 1; i < nums.length(); i++){  
            if(nums[i] == '0')
                if(nums[i - 1] != '1' && nums[i - 1] != '2')
                    return 0;
        }
        //辅助数组初始化为1
        vector<int> dp(nums.length() + 1, 1);  
        for(int i = 2; i <= nums.length(); i++){
            //在11-19，21-26之间的情况
            if((nums[i - 2] == '1' && nums[i - 1] != '0') || (nums[i - 2] == '2' && nums[i - 1] > '0' && nums[i - 1] < '7'))
               dp[i] = dp[i - 1] + dp[i - 2];
            else
                dp[i] = dp[i - 1];
        }
        return dp[nums.length()];
    }
};

```

# 【回溯】
## JZ12 矩形中的路径
![](vx_images/275750516239479.png =600x)

```java
bool dfs(vector<vector<char>> &board, char* str, int index, int x, int y,
	vector<vector<bool>>& visited) 
{
	if (index == strlen(str)) return true;
	//搜寻超过路径长度，符合条件，返回true，
	//此时已经超过最大程度了 strlen返回不带 ‘\0’的长度，
	//此时str[k]已经越界了，所以这个判断一定要放在函数开头，如果放在if之后，str[k]会越界
	if ((x < 0) || (y < 0) || (x >= board.size()) || (y >= board[0].size()))
		return false;//访问越界，终止，返回false
	if (visited[x][y]) return false;//之前访问过，剪枝
	if (board[x][y] != str[index]) return false;//不相等，剪枝
	visited[x][y] = true;
	if (dfs(board, str, index + 1, x, y - 1, visited) || //上
		dfs(board, str, index + 1, x, y + 1, visited) ||     //下
		dfs(board, str, index + 1, x - 1, y, visited) ||     //左
		dfs(board, str, index + 1, x + 1, y, visited))      //右
		return true; //有符合要求的

	visited[x][y] = false;//记得此处改回false，以方便下一次遍历搜索。
	return false;
}

bool hasPath(char* matrix, int rows, int cols, char* str)
{
	if (str == NULL || rows <= 0 || cols <= 0)
		return false;
	vector<vector<char>> board(rows, vector<char>(cols));
	for (int i = 0; i < rows; ++i) {//将matrix装入二维数组board中
		for (int j = 0; j < cols; ++j) {
			board[i][j] = matrix[i * cols + j];
		}
	}
	vector<vector<bool>> visited(rows, vector<bool>(cols, false));
	for (int i = 0; i < rows; ++i) {
		for (int j = 0; j < cols; ++j) {
			if (dfs(board, str, 0, i, j, visited) == true)
				return true;//以矩阵board中的每个字符为起点进行广度优先搜索
			//找到一个符合条件的即返回true.
		}
	}
	return false;//遍历完都没找到匹配的路径，返回false
}
```


## JZ13 机器人的运动范围

![](vx_images/173540316240677.png =600x)


```java
int getValue(int row, int col) {
	int sum = 0;
	while (row != 0)
	{
		sum += row % 10;
		row = row / 10;
	}
	while (col != 0)
	{
		sum += col % 10;
		col = col / 10;
	}
	return sum;
}


void movingCountCore(int threshold, int rows, int cols, vector<vector<bool>>& visit, int row, int col, int &count) {
	if (row < 0 || col < 0 || row >= rows || col >= cols || visit[row][col] == true) return;
	if (getValue(row, col) > threshold) {
		visit[row][col] = true;
		return;
	}
	visit[row][col] = true;
	count++;
	movingCountCore(threshold, rows, cols, visit, row + 1, col, count);
	movingCountCore(threshold, rows, cols, visit, row - 1, col, count);
	movingCountCore(threshold, rows, cols, visit, row, col + 1, count);
	movingCountCore(threshold, rows, cols, visit, row, col - 1, count);
}

int movingCount(int threshold, int rows, int cols)
{
	if (rows < 0 || cols < 0) return 0;
	vector<vector<bool>> visit(rows, vector<bool>(cols, false));
	int count = 0;
	movingCountCore(threshold, rows, cols, visit, 0, 0, count);
	return count;
}
```

# 【排序】
## JZ3 数组中的重复数字 
![](vx_images/165771910224269.png =500x)
```java
class Solution {
public:
    int duplicate(vector<int>& numbers) {
        // write code here
        sort(numbers.begin(),numbers.end());
        for(int i= 1; i < numbers.size();i++){
            if(numbers[i]==numbers[i-1]) return numbers[i];
        }
        return -1;
    }
};

```





## JZ40 最小的K个数

输入n个整数，找出其中最小的K个数。例如输入4,5,1,6,2,7,3,8这8个数字，则最小的4个数字是1,2,3,4,。
快排
```java
class Solution {
public:
    vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {
        sort(input.begin(),input.end());
        return vector<int>(input.begin(),input.begin()+k);
    }
};
```

小顶堆
```java
vector<int> GetLeastNumbers_Solution(vector<int> input, int k) {

    if(k > input.size()) return vector<int>();
    priority_queue<int, vector<int>, greater<int>> pq;
	for (auto a : input)
		pq.push(a);
	vector<int> result;
	while (k--) {
		result.push_back(pq.top());
		pq.pop();
	}
	return result;
}

```


## JZ41 数据流中的中位数
![](vx_images/362373016225689.png =600x)


普遍的方法
```c++
class Solution {
public:
	void Insert(int num)
	{
		result.push_back(num);
	}

	double GetMedian()
	{
		sort(result.begin(), result.end());
		int len = result.size();
		if (len % 2 == 0) 
            return (result[len / 2] + result[-1 + len / 2]) / 2.0;//注意这里是2.0 这样才能返回值为double
		else
			return result[len / 2];
	}

	vector<int> result;
};

```

两个堆实现

```java
class Solution {

public:
    void Insert(int num){
	count += 1; //数据是奇数的时候 insert的数据进入 [左边，最大堆]中
	if (count % 2 == 1)//奇数
	{
		if (big_heap.empty())  big_heap.push(num); //直接插入到[左边，最小堆]中
		else {
			int rightMin = small_heap.top();
			if (num <= rightMin)  big_heap.push(num);
			else {
				small_heap.push(num);  //先把cur插入[右边最小rightMin|最小堆]中
				big_heap.push(rightMin);  //然后把rightMin放入[最大堆|左边最大leftMax]中
				small_heap.pop();
			}
		}
	}
	else {

		if (small_heap.empty()) {
		 //当第一个元素 比 第二个元素大的时候，会造成左边比右边大的情形，因此要加上判断
        //当第一个数据比第二个大的时候，比如[5,2,3,4,1,6,7,0,8]的情况，
        //会造成最大堆的唯一数据，比最小堆的唯一数据大的情况，
        //这跟思想就不同了，因此需要加上一层判断。
			if (num > big_heap.top())
			{
				small_heap.push(num);
			}
			else
			{
				small_heap.push(big_heap.top());
				big_heap.pop();
				big_heap.push(num);
			}
		}
		else {
			int leftMax = big_heap.top();
			if (num >= leftMax)  small_heap.push(num);//直接插入到[右边，最小堆]中
			else {
				big_heap.push(num);//先把cur插入[右边最小rightMin|最小堆]中，
				small_heap.push(big_heap.top()); //然后把rightMin放入[最大堆|左边最大leftMax]中
				big_heap.pop();
			}
		}
	}		
}

    double GetMedian(){
	    if (count & 0x1) {
	    //看见这个0x你肯定知道这就是16进制表示了，而0x1就是最后一位肯定是1。
	    //偶数的二进制表示中最后一位肯定是0，
		//如果是奇数那肯定是1，所以一个整数与0x1做按位与运算得到的结果是0
		//或者1就可以判断出这个整数是偶数还是奇数。
		    return big_heap.top();
	    }
	    else {
		    return double((small_heap.top() + big_heap.top()) / 2.0);
	    }
    }
private:
	int count = 0;
	priority_queue<int, vector<int>, less<int>> big_heap;        // 左边一个大顶堆
	priority_queue<int, vector<int>, greater<int>> small_heap;   // 右边一个小顶堆
};

```


# 【数位运算】
## JZ65 不用加减乘除做加法

写一个函数，求两个整数之和，要求在函数体内不得使用+、-、*、/四则运算符号。

数据范围：两个数都满足 -10 \le n \le 1000−10≤n≤1000
进阶：空间复杂度 O(1)，时间复杂度 O(1)

![](vx_images/394304819235861.png =400x)


**异或**：如果两个相应bit位相同，则结果为0，否则为1
step 1：两数进行与运算可以产生进位的信息
step 2：运算后执行左移1位就是每轮需要进位的方案
step 3：两数进行异或运算可以产生非进位的加和结果
step 4：将移位后的进位结果与非进位结果继续重复 step 1 - step 3 的步骤，直到不再产生进位为止

```c++
class Solution {
public:
    int Add(int num1, int num2) {
        // add表示进位值
        int add = num2;         
        // sum表示总和       
        int sum = num1;                
        // 当不再有进位的时候终止循环
        while(add != 0) {              
            // 将每轮的无进位和与进位值做异或求和
            int temp = sum ^ add;      
            // 进位值是用与运算产生的
            add = (sum & add) << 1;    
            // 更新sum为新的和
            sum = temp;                
        }
        return sum;
    }
};
```


##  JZ15 二进制中1的个数
![](vx_images/346933120228431.png =400x)

两种方案
1>>I   ->  1*2^I     n&(n-1)
C++运算符中的左移和右移   左移相当于x2   n>>1 相当于除2 （偶数可以，奇数不可以，奇数会发生截断）
https://www.imangodoc.com/137166.html 
https://blog.csdn.net/qq_39790992/article/details/82313960 详细

举个例子：一个二进制数1100，从右边数起第三位是处于最右边的一个1。减去1后，第三位变成0，它后面的两位0变成了1，而前面的1保持不变，因此得到的结果是1011.我们发现减1的结果是把最右边的一个1开始的所有位都取反了。

这个时候如果我们再把原来的整数和减去1之后的结果做与运算，从原来整数最右边一个1那一位开始所有位都会变成0。如1100&1011=1000.也就是说，把一个整数减去1，再和原整数做与运算，会把该整数最右边一个1变成0.那么一个整数的二进制有多少个1，就可以进行多少次这样的操作。


```c++
class Solution {
public:
    int NumberOf1(int n) {
        int res = 0;
        //当n为0时停止比较
        while(n){  
            n &= n - 1;
            res++;
        }
        return res;
     }
};

```


```c++
class Solution {
public:
    int  NumberOf1(int n) {
        int res = 0;
        //遍历32位
        for(int i = 0; i < 32; i++){
            //按位比较
            if((n & (1 << i)) != 0)   
                res++;
        }
        return res;
     }
};
```

## JZ16 数值的整数次方Power(x,n) 快速幂1        

二分角度
![](vx_images/313401610245114.png =300x)

快速幂解法

![](vx_images/102361914244807.png =500x)
```c++
class Solution {
public:
    //快速幂
    double Pow(double x, int y){
        double res = 1;
        while(y){
            //可以再往上乘一个
            if(y & 1)
                res *= x;
            //叠加
            x *= x;
            //减少乘次数
            y = y >> 1;
        }
        return res;
    }
    double Power(double base, int exponent) {
        //处理负数次方
        if(exponent < 0){
            base = 1 / base;
            exponent = -exponent;
        }
        return Pow(base, exponent);
    }
};
```


## JZ56 数组中只出现一次的两个数字
![](vx_images/164233920246267.png =500x)


方法一：异或运算（扩展思路）
![](vx_images/398850710251822.png =500x)
step 1：遍历整个数组，将每个元素逐个异或运算，得到a⊕ba \oplus ba⊕b。
step 2：我们可以考虑位运算的性质，找到二进制中第一个不相同的位，将所有数组划分成两组。
step 3：遍历数组对分开的数组单独作异或连算。
step 4：最后整理次序输出。


```c++
class Solution {
public:
    vector<int> FindNumsAppearOnce(vector<int>& array) {
        vector<int> res(2, 0);
        int temp = 0;
        //遍历数组得到a^b
        for(int i = 0; i < array.size(); i++) 
            temp ^= array[i];
        int k = 1;
        //找到两个数不相同的第一位
        while((k & temp) == 0) 
            k <<= 1;
        for(int i = 0; i < array.size(); i++){
            //遍历数组，对每个数分类
            if((k & array[i]) == 0) 
                res[0] ^= array[i];
            else
                res[1] ^= array[i];
        }
        //整理次序
        if(res[0] < res[1]) 
            return res;
        else
            return {res[1], res[0]};
    }
};
```

方法二：哈希表(推荐使用)

思路：
既然有两个数字只出现了一次，我们就统计每个数字的出现次数，利用哈希表的快速根据key值访问其频率值。

具体做法：
step 1：遍历数组，用哈希表统计每个数字出现的频率。
step 2：然后再遍历一次数组，对比哈希表，找到出现频率为1的两个数字。
step 3：最后整理次序输出。


```c++
class Solution {
public:
    vector<int> FindNumsAppearOnce(vector<int>& array) {
        unordered_map<int, int> mp;
        vector<int> res;
        //遍历数组
        for(int i = 0; i < array.size(); i++) 
            //统计每个数出现的频率
            mp[array[i]]++; 
        //再次遍历数组
        for(int i = 0; i < array.size(); i++) 
            //找到频率为1的两个数
            if(mp[array[i]] == 1) 
                res.push_back(array[i]);
        //整理次序
        if(res[0] < res[1]) 
            return res;
        else
            return {res[1], res[0]};
    }
};
```

## 打印从1到最大的n位数



两种情况 ： 不需要考虑大数越界  需要考虑大数越界（全排列）  
数字转为字符串 可以用 string s;  s[i] = a+’0’;   stoi函数的使用  s.substr(起始位置，个数)
String 类型常用函数总结 
字符串转整型数字：std::stoi, std::stol, std::stoll 字符串转浮点数：stod,stof,stold   to_string()
https://blog.csdn.net/zhaitianbao/article/details/118993685 
https://blog.csdn.net/luolaihua2018/article/details/109238559  全面
![](vx_images/392512420242893.png =600x) 





## 数组中数字出现的次数

进行异或操作，可以去除两两重复的数字，剩下的就是两个只出现一次的数字，然后再按照异或结果的位为1位置对原先数组进行分组，对两个组各自进行异或操作，结果就是两个数字。

 ![](vx_images/53062520222545.png =500x)


## 数组中数字出现的次数 II

在一个数组 nums 中除一个数字只出现一次之外，其他数字都出现了三次。请找出那个只出现一次的数字。
出现3次，则所有相同的数字加起来 对应位置上的1 为3的倍数，可以统计所有位置上1的个数，然后%3，结果就是最终的答案
![](vx_images/151422520220991.png =500x)

 
## JZ64 求1+2+3+...+n

求1+2+3+...+n，要求不能使用乘除法、for、while、if、else、switch、case等关键字及条件判断语句（A?B:C）。

题解一：递归+逻辑运算符
前置知识：
位运算|、&与逻辑运算符&&、||的区别。
1、&、|是按位运算，符号两端为两个数；&&、||是两个逻辑表达式；
2、&&、||运算具有短路功能，示例：(A)&&(B)当A部分不成立，则B部分不会执行，(A)||(B)当A部分成立，则B部分不会执行。

```c++
class Solution {
public:
    int res = 0;
    int Sum_Solution(int n) {
        n && (n += Sum_Solution(n - 1)); //要判断n是否为整数
        return n;
    }
};
```

# 【模拟】
## JZ29 顺时针打印矩阵

![](vx_images/593781115222043.png =500x)

## JZ61 扑克牌顺子
现在有2副扑克牌，从扑克牌中随机五张扑克牌，我们需要来判断一下是不是顺子。
有如下规则：
1. A为1，J为11，Q为12，K为13，A不能视为14
2. 大、小王为 0，0可以看作任意牌
3. 如果给出的五张牌能组成顺子（即这五张牌是连续的）就输出true，否则就输出false。
4. 数据保证每组5个数字，每组最多含有4个零，数组的数取值为 [0, 13]


题解一:排序+遍历
顺子牌的特点：
1、顺子一定没有相等的牌；
2、顺子中两张相邻的扑克牌的数值差为1，即满足interrapt=numbers[i + 1] - numbers[i] - 1==0;
3、当interrapt不为0，代表需要在顺子中插入对应interrapt张牌；
4、只有两张王牌；
主要思路：
1、排序五张牌；
2、遍历5张牌，并求出大小王的数量zero_num，与interrapt的大小；
3、判断interrapt的大小。
(1)interrapt==0,除大小王之外的牌本来就是顺子，大小王随便补齐在头部或者尾部；
(2)interrapt<=zero_num,除大小王之外的牌不是顺子，可以通过大小王变成特定的牌补在其中，使其成为顺子；
(2)interrapt>zero_num,除大小王之外的牌不是顺子,即使有大小王也补不成顺子。

**核心**
记录max到min的距离

```c++
class Solution {
public:
    bool IsContinuous( vector<int> numbers ) {
        sort(numbers.begin(), numbers.end());
        int zero_num = 0;//统计大小王数量
        int i = 0;
        while (numbers[i] == 0)zero_num++,i++;
        int interrapt = 0;//记录五张牌中最大值max到最小值min的距离
        for (; i < numbers.size()-1; ++i) {
            if (numbers[i] == numbers[i + 1])return false;//出现相同的扑克牌
            interrapt += numbers[i + 1] - numbers[i] - 1;//计算距离
        }
        if (zero_num >= interrapt) return true;
        return false;
    }
};
```

## JZ67 把字符串转换成整数(atoi)

思路：
既然是将字符串转化为数字，那我们可以遍历字符串，一个字符串，一个字符地检查，然后取出掉无用的，取出数字，利用如下代码，一个数字一个数字地转换，前面的扩大十倍加上后面一位。
> res = res * 10 + sign * (c - '0');

具体做法：
step 1：遍历字符串，用index记录全程的下标。
step 2：首先要排除空串，然后越过前导空格，以及前导空格后什么都没有就返回0.
step 3：然后检查符号，没有符号默认为正数。
step 4：再在后续遍历的时候，将数字字符转换成字符，遇到非数字则结束转换。
step 5：与Int型最大最小值比较，检查越界情况。

```c++
class Solution {
public:
    int StrToInt(string s) {
        int res = 0;
        int index = 0;
        int n = s.length();
        //去掉前导空格，如果有
        while(index < n){ 
            if(s[index] == ' ')
                index++;
            else
                break;
        }
        //去掉空格就什么都没有了
        if(index == n) 
            return 0;
        int sign = 1;
        //处理第一个符号是正负号的情况
        if(s[index] == '+')
            index++;
        else if(s[index] == '-'){
            index++;
            sign = -1;
        }
        //去掉符号就什么都没有了
        if(index == n) 
            return 0;
        while(index < n){
            char c = s[index];
            //后续非法字符，截断
            if(c < '0' || c > '9')  
                break;
            //处理越界
            if(res > INT_MAX / 10 || (res == INT_MAX / 10 && (c - '0') > INT_MAX % 10))
            
                return INT_MAX;
            if(res < INT_MIN / 10 || (res == INT_MIN / 10 && (c - '0') > -(INT_MIN % 10)))
                return INT_MIN;
            res = res * 10 + sign * (c - '0');
            index++;
        }
        return res;
    }
};
```

## JZ20 表示数值的字符串

请实现一个函数用来判断字符串str是否表示数值（包括科学计数法的数字，小数和整数）。
描述
请实现一个函数用来判断字符串str是否表示数值（包括科学计数法的数字，小数和整数）。

科学计数法的数字(按顺序）可以分成以下几个部分:
1.若干空格
2.一个整数或者小数
3.（可选）一个 'e' 或 'E' ，后面跟着一个整数(可正可负)
4.若干空格

小数（按顺序）可以分成以下几个部分：
1.若干空格
2.（可选）一个符号字符（'+' 或 '-'）
3. 可能是以下描述格式之一:
3.1 至少一位数字，后面跟着一个点 '.'
3.2 至少一位数字，后面跟着一个点 '.' ，后面再跟着至少一位数字
3.3 一个点 '.' ，后面跟着至少一位数字
4.若干空格

整数（按顺序）可以分成以下几个部分：
1.若干空格
2.（可选）一个符号字符（'+' 或 '-')
3. 至少一位数字
4.若干空格

例如，字符串["+100","5e2","-123","3.1416","-1E-16"]都表示数值。
但是["12e","1a3.14","1.2.3","+-5","12e+4.3"]都不是数值。


# 【其他】
## JZ66 构建乘积数组
给定一个数组 A[0,1,...,n-1] ,请构建一个数组 B[0,1,...,n-1] ,其中 B 的元素 B[i]=A[0]*A[1]*...*A[i-1]*A[i+1]*...*A[n-1]（除 A[i] 以外的全部元素的的乘积）。程序中不能使用除法。
（注意：规定 B[0] = A[1] * A[2] * ... * A[n-1]，B[n-1] = A[0] * A[1] * ... * A[n-2]）
对于 A 长度为 1 的情况，B 无意义，故而无法构建，用例中不包括这种情况。

![](vx_images/156292921230613.png =600x)


如上图所示，矩阵中由对角线1将其分成了上三角和下三角。我们先看下三角，如果我们累乘的时候，B[1]是在B[0]的基础上乘了新增的一个A[0]，B[2]是在B[1]的基础上乘了新增的一个A[1]，那我们可以遍历数组的过程中不断将数组B的前一个数与数组A的前一个数相乘就得到了下三角中数组B的当前数。同理啊，我们在上三角中，用一个变量存储从右到左的累乘，每次只会多乘上一个数字。这样，两次遍历就可以解决。

```c++
class Solution {
public:
    vector<int> multiply(const vector<int>& A) {
        //初始化数组B
        vector<int> B(A.size(), 1);
        //先乘左边，从左到右
        for(int i = 1; i < A.size(); i++)
            //每多一位由数组B左边的元素多乘一个前面A的元素
            B[i] = B[i - 1] * A[i - 1];
        int temp = 1;
        //再乘右边，从右到左
        for(int i = A.size() - 1; i >= 0; i--){
            //temp为右边的累乘
            B[i] *= temp;
            temp *= A[i];
        }
        return B;
    }
};
```

## JZ50 第一个只出现一次的字符

在一个长为 字符串中找到第一个只出现一次的字符,并返回它的位置, 如果没有则返回 -1（需要区分大小写）.（从0开始计数）

```c++
class Solution {
public:
    int FirstNotRepeatingChar(string str) {
        unordered_map<char, int> mp;
        //统计每个字符出现的次数
        for(int i = 0; i < str.length(); i++) 
            mp[str[i]]++;
        //找到第一个只出现一次的字母
        for(int i = 0; i < str.length(); i++) 
            if(mp[str[i]] == 1)
                return i;
        //没有找到
        return -1; 
    } 
};

```

## JZ5  替换空格

```c++
class Solution {
public:
    string replaceSpace(string s) {
        string res = "";
        //遍历字符串
        for(int i = 0; i < s.length(); i++){ 
            //非空格直接复制
            if(s[i] != ' ') 
                res += s[i];
            //空格就替换
            else 
                res += "%20"; 
        }
        return res;
    }
};
```

## JZ21 调整数组顺序使奇数位于偶数前面(一)
输入一个长度为 n 整数数组，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前面部分，所有的偶数位于数组的后面部分，并保证奇数和奇数，偶数和偶数之间的相对位置不变。

step 1：遍历数组，统计奇数出现的次数，即找到了偶数开始的位置。
step 2：准备一个和原数组同样长的新数组承接输出，准备双指针，x指向奇数开始的位置，y指向偶数开始的位置。
step 3：遍历原数组，遇到奇数添加在指针x后面，遇到偶数添加在指针y后面，直到遍历结束。

1 2 3 4 5 6
>>
1 3 5  |  2 4 6

```c++
class Solution {
public:
    vector<int> reOrderArray(vector<int>& array) {
        int n = array.size();
        vector<int> res(n);
        //统计奇数个数
        int odd = 0; 
        //遍历统计
        for(int i = 0; i < n; i++){ 
            if(array[i] % 2)
                odd++;
        }
        //x与y分别表示答案中奇偶数的坐标
        int x = 0, y = odd; 
        for(int i = 0; i < n; i++){
            //奇数在前
            if(array[i] % 2){ 
                res[x] = array[i];
                x++;
            //偶数在后
            }else{ 
                res[y] = array[i];
                y++;
            }
        }
        return res;
    }
};

```

## JZ81 调整数组顺序使奇数位于偶数前面(二) 空间复杂度1

输入一个长度为 n 整数数组，数组里面可能含有相同的元素，实现一个函数来调整该数组中数字的顺序，使得所有的奇数位于数组的前面部分，所有的偶数位于数组的后面部分，对奇数和奇数，偶数和偶数之间的相对位置不做要求，但是时间复杂度和空间复杂度必须如下要求。

1 2 3 4 5 6
>>
1 3 5  |  2 4 6


同一题变化就下面的：
**要求：时间复杂度 O(n)，空间复杂度 O(1)**

```c++
class Solution {
public:
    vector<int> reOrderArrayTwo(vector<int>& array) {
        //双指针
        int i = 0;
        int j = array.size() - 1; 
        //向中间聚合
        while(i < j){ 
            //左右都是奇数，左移右不动
            if(array[i] % 2 == 1 && array[j] % 2 == 1) 
                i++;
            //左奇数右偶数，左右都向中间缩
            else if(array[i] % 2 == 1 && array[j] % 2 == 0)
                i++, j--;
            //左偶右奇数
            else if(array[i] % 2 == 0 && array[j] % 2 == 1) 
                //交换
                swap(array[i], array[j]); 
            //左右都是偶数，只移动右指针
            else 
                j--;
        }
        return array;
    }
};

```


## JZ39 数组中出现次数超过一半的数字
给一个长度为 n 的数组，数组中有一个数字出现的次数超过数组长度的一半，请找出这个数字。
例如输入一个长度为9的数组[1,2,3,2,2,2,5,4,2]。由于数字2在数组中出现了5次，超过数组长度的一半，因此输出2。

方法一：哈希法 n n
根据题目意思，显然可以先遍历一遍数组，在map中存每个元素出现的次数，然后再遍历一次数组，找出众数。
```c++
int MoreThanHalfNum_Solution(vector<int> numbers) {
    unordered_map<int, int>unmp;
    int len = numbers.size();
    for (int i = 0; i < len; ++i) {
        unmp[numbers[i]]++;
        if (unmp[numbers[i]] > len / 2) return numbers[i];
    }
    return 0;
}
```

方法二：排序法 nlogn 1
可以先将数组排序，然后可能的众数肯定在数组中间，然后判断一下。


```c++
class Solution {
public:
    int MoreThanHalfNum_Solution(vector<int> numbers) {
        sort(numbers.begin(), numbers.end());
        int cond = numbers[numbers.size() / 2];
        int cnt = 0;
        // for循环进行检查，也可以不检查直接输出cond;
        for (const int k :numbers) {
            if (cond == k) ++cnt;
        }
        if (cnt > numbers.size() / 2) return cond;
        return 0;
    }
};
```

## JZ43 整数中1出现的次数（从1到n整数中1出现的次数）

输入一个整数 n ，求 1～n 这 n 个整数的十进制表示中 1 出现的次数
例如， 1~13 中包含 1 的数字有 1 、 10 、 11 、 12 、 13 因此共出现 6 次

注意：11 这种情况算两次

进阶：空间复杂度 O(1)  ，时间复杂度 O(logn)


方法一：暴力统计

```c++
class Solution {
public:
    int NumberOf1Between1AndN_Solution(int n) {
        int res = 0;
        //遍历1-n
        for(int i = 1; i <= n; i++){ 
            //遍历每个数的每一位
            int j = i;
            while(j){
                if(j%10==1)
                    res++;
                j=j/10;
            }
        }
        return res;
    }
};
```




## JZ45 把数组排成最小的数

只考虑首字符的大小不可靠，但是如果字符串a拼接b的得到的数字大于b拼接a，那么肯定b应该排在a的前面，我们要就按照这样的次序将排序的比较重载就可以了。

![](vx_images/556874022249422.png =400x)


step 1：优先判断空数组的特殊情况。
step 2：将数组中的数字元素转换成字符串类型。
step 3：重载排序比较为字符串类型的x + y < y + x，然后进行排序。
step 4：将排序结果再按照字符串拼接成一个整体。

```c++
class Solution {
public:
    //重载排序比较方式
    static bool cmp(string& x, string& y){
        //叠加
        return x + y < y + x;
    }
    string PrintMinNumber(vector<int> numbers) {
        string res = "";
        //空数组的情况
        if(numbers.size() == 0)
            return res;
            
        //将数字转成字符
        vector<string> nums;
        for(int i = 0; i < numbers.size(); i++)
            nums.push_back(to_string(numbers[i]));
            
        //排序
        sort(nums.begin(), nums.end(), cmp);
        
        //字符串叠加
        for(int i = 0; i < nums.size(); i++)
            res += nums[i];
        return res;
    }
};
```

## JZ49 丑数

基础数学 二分

把只包含质因子2、3和5的数称作丑数（Ugly Number）。
 习惯上我们把1当做是第一个丑数。求按从小到大的顺序的第 n个丑数。
 
![](vx_images/343714121249501.png =500x)


方法一：最小堆（推荐使用）

![](vx_images/248335722244530.png =600x)

```java
class Solution {
public:
    int GetUglyNumber_Solution(int index) {
        //排除0
        if(index == 0)
            return 0; 
        //要乘的因数
        vector<int> factors = {2, 3, 5}; 
        //去重
        unordered_map<long, int> mp; 
        //小顶堆
        priority_queue<long, vector<long>, greater<long>> pq; 
        //1先进去
        mp[1LL] = 1; 
        pq.push(1LL);
        long res = 0;
        for(int i = 0; i < index; i++){ 
            //每次取最小的
            res = pq.top(); 
            pq.pop();
            for(int j = 0; j < 3; j++){
                //乘上因数
                long next = res * factors[j]; 
                //只取未出现过的
                if(mp.find(next) == mp.end()){  
                    mp[next] = 1;
                    pq.push(next);
                }
            }
        }
        return (int)res;
    }
};
```

方法一：
step 1：第一个丑数1加入数组。
step 2：使用i、j、k三个索引表示该数字有无被乘2、乘3、乘5.
step 3：后续继续找n−1个丑数，每次取当前丑数索引乘2、乘3、乘5的最小值加入数组，并计数。
step 4：若是该丑数为相应索引乘上某个数字，则对应的索引往后一位。

```java
class Solution {
public:
    //寻找三个数中的最小值
    int findMin(int x, int y, int z){  
        int res = x; 
        res = y < res ? y : res;
        res = z < res ? z : res;
        return res;
    }
    int GetUglyNumber_Solution(int index) {
        //排除0
        if(index == 0)
            return 0; 
        //按顺序记录丑数
        vector<int> num; 
        num.push_back(1);
        //记录这是第几个丑数
        int count = 1; 
        //分别代表要乘上2 3 5的下标
        int i = 0, j = 0, k = 0; 
        while(count < index){
            //找到三个数中最小的丑数
            num.push_back(findMin(num[i] * 2, num[j] * 3, num[k] * 5)); 
            count++;
            //由2与已知丑数相乘得到的丑数，那该下标及之前的在2这里都用不上了
            if(num[count - 1] == num[i] * 2)
                i++; 
            //由3与已知丑数相乘得到的丑数，那该下标及之前的在3这里都用不上了
            if(num[count - 1] == num[j] * 3)
                j++; 
            //由5与已知丑数相乘得到的丑数，那该下标及之前的在5这里都用不上了
            if(num[count - 1] == num[k] * 5)
                k++; 
        }
        return num[count - 1];
    }
};

```



方法三：三指针法
维护三个index，采用三index齐头并进的做法

```java
int GetUglyNumber_Solution(int index) {
	if(index < 7) return index;
	vector<int> result(index, 0);
	result[0] = 1;
	int indexTwo = 0, indexThree = 0,indexFive = 0;
	for (int i = 1; i < index; ++i) {
		int minNum = min(min(result[indexTwo] * 2, result[indexThree] * 3),
		                     result[indexFive] * 5);
		if (minNum == result[indexTwo] * 2) indexTwo++;
		if (minNum == result[indexThree] * 3) indexThree++;
		if (minNum == result[indexFive] * 5) indexFive++;
		result[i] = minNum;
	}
	return result[index - 1];

}
```


## JZ74 和为S的连续正数序列

知识点 穷举

![](vx_images/324960023252041.png =700x)

输入：9
返回值：[[2,3,4],[4,5]]

方法一：滑动窗口（推荐使用）

```java
class Solution {
public:
    vector<vector<int> > FindContinuousSequence(int sum) {
        vector<vector<int> > res;
        vector<int> temp;
        //从1到2的区间开始
        int l = 1, r = 2;
        while(l < r){ 
            //计算区间内的连续和
            int sum1 = (l + r) * (r - l + 1) / 2; 
            //如果区间内和等于目标数
            if(sum1 == sum){ 
                temp.clear();
                //记录区间序列
                for(int i = l; i <= r; i++) 
                    temp.push_back(i);
                res.push_back(temp);
                //左区间向右
                l++; 
            //如果区间内的序列和小于目标数，右区间扩展
            }else if(sum1 < sum) 
                r++;
            //如果区间内的序列和大于目标数，左区间收缩
            else 
                l++;
        }
        return res;
    }
};
```

## JZ57 升序数组中和为S的两个数字
![](vx_images/328051123251052.png =600x)

方法一：双指针

```java
class Solution {
public:
    vector<int> FindNumbersWithSum(vector<int> array,int sum) {
        vector<int> res;
        //左右双指针
        int left = 0, right = array.size() - 1;
        //对撞双指针
        while(left < right){
            //相加等于sum，找到目标
            if(array[left] + array[right] == sum){
                res.push_back(array[left]);
                res.push_back(array[right]);
                break;
            //和太大，缩小右边
            }else if(array[left] + array[right] > sum)
                right--;
            //和太小，扩大左边
            else
                left++;
        }
        return res;
    }
};

```

方法二：map
```c++
class Solution {
public:
    vector<int> FindNumbersWithSum(vector<int> array,int sum) {
        vector<int> res;
        //创建哈希表,两元组分别表示值、下标
        unordered_map<int, int> mp; 
        //在哈希表中查找sum-array[i]
        for(int i = 0; i < array.size(); i++){
            int temp = sum - array[i];
            //若是没找到，将此信息计入哈希表
            if(mp.find(temp) == mp.end()){ 
                mp[array[i]] = i;
            }
            else{
                //取出数字添加
                res.push_back(temp);   
                res.push_back(array[i]);
                break;
            }
        }
        return res;
    }
};
```

## JZ58 左旋转字符串

字符序列 S = ”abcXYZdef” , 要求输出循环左移 3 位后的结果，即 “XYZdefabc”
将给定字符串循环左移n位
即最左边的nnn位按照顺序整体接到右边末尾

方法一：拼接
```c++
class Solution {
public:
    string LeftRotateString(string str, int n) {
        int m = str.length();
        //特殊情况
        if(m == 0)
            return "";
        //取余，因为每次长度为m的旋转数组相当于没有变化
        n = n % m;
        string res = "";
        //先遍历后面的，放到前面 3 - m
        for(int i = n; i < m; i++)
            res += str[i];
        //再遍历前面的放到后面  0 - 2
        for(int i = 0; i < n; i++)
            res += str[i];
        return res;
    }
};
```

方法二：三次旋转
```c++
class Solution {
public:
    string LeftRotateString(string str, int n) {
        int m = str.length(); // 总数
        //特殊情况
        if(m == 0)
            return "";
        //取余，因为每次长度为m的旋转相当于没有变化
        n = n % m;
        //第一次逆转全部数组元素
        reverse(str.begin(), str.end());
        //第二次只逆转开头m个
        reverse(str.begin(), str.begin() + m - n);
        //第三次只逆转结尾m个
        reverse(str.begin() + m - n, str.end());
        return str;
    }
};
```

## JZ62 孩子们的游戏(圆圈中最后剩下的数)

首先，让 n 个小朋友们围成一个大圈，小朋友们的编号是0~n-1。然后，随机指定一个数 m ，让编号为0的小朋友开始报数。每次喊到 m-1 的那个小朋友要出列唱首歌，然后可以在礼品箱中任意的挑选礼物，并且不再回到圈中，从他的下一个小朋友开始，继续0... m-1报数....这样下去....直到剩下最后一个小朋友，可以不用表演，并且拿到牛客礼品，请你试着想下，哪个小朋友会得到这份礼品呢？

![](vx_images/8654017238393.png =600x)

方法一：模拟的思路

```c++
class Solution {
public:
    int LastRemaining_Solution(int n, int m)
    {
        if(n < 1 || m < 1)
            return -1;

        vector<int> circle;
        for(int i=0; i<n; i++)
            circle.push_back(i);

        int start = 0;
        while(n > 1){
            start = (start + m - 1) % n;
            circle.erase(circle.begin() + start);
            n--;
        }
        return circle[0];
    }
};
```

## JZ75 字符流中第一个不重复的字符
请实现一个函数用来找出字符流中第一个只出现一次的字符。
例如，当从字符流中只读出前两个字符 "go" 时，第一个只出现一次的字符是 "g" 。当从该字符流中读出前六个字符 “google" 时，第一个只出现一次的字符是"l"。

```c++
class Solution
{
public:
    unordered_map<char, int> mp;
    //记录输入的字符串
    string s;    
    //Insert one char from stringstream
    void Insert(char ch) {
        //插入字符
        s += ch;  
        //哈希表记录字符出现次数
        mp[ch]++; 
    }  
    //return the first appearence once char in current stringstream
    char FirstAppearingOnce() {
        //遍历字符串
        for(int i = 0; i < s.length(); i++) 
            //找到第一个出现次数为1的
            if(mp[s[i]] == 1) 
                return s[i];
        //没有找到
        return '#'; 
    }
    
};
```

## JZ14 剪绳子
最大成绩

给你一根长度为 n 的绳子，请把绳子剪成整数长的 m 段（ m 、 n 都是整数， n > 1 并且 m > 1 ， m <= n ），每段绳子的长度记为 k[1],...,k[m] 。请问 k[1]*k[2]*...*k[m] 可能的最大乘积是多少？
例如，当绳子的长度是 8 时，我们把它剪成长度分别为 2、3、3 的三段，此时得到的最大乘积是 18 。

![](vx_images/232054018225384.png =600x)

```c++
class Solution {
public:
    int cutRope(int number) {
        //不超过3直接计算
        if(number <= 3) 
            return number - 1;
        //dp[i]表示长度为i的绳子可以被剪出来的最大乘积
        vector<int> dp(number + 1, 0);
        dp[1] = 1;
        dp[2] = 2;
        dp[3] = 3;
        dp[4] = 4;
        
        //遍历后续每一个长度
        for(int i = 5; i <= number; i++)
            //可以被分成两份
            for(int j = 1; j < i; j++)
                //取最大值
                dp[i] = max(dp[i], j * dp[i - j]);
        return dp[number];
    }
};
```




## JZ83 剪绳子（进阶版）
给你一根长度为 n 的绳子，请把绳子剪成整数长的 m 段（ m 、 n 都是整数， n > 1 并且 m > 1 ， m <= n ），每段绳子的长度记为 k[1],...,k[m] 。请问 k[1]*k[2]*...*k[m] 可能的最大乘积是多少？例如，当绳子的长度是 8 时，我们把它剪成长度分别为 2、3、3 的三段，此时得到的最大乘积是 18 。

由于答案过大，请对 998244353 取模。
进阶：空间复杂度 O(1) ， 时间复杂度 O(logn)

进阶版本

```java
int cutRope(int number) {

	if (number == 2) {
		return 1;
	}
	
	if (number == 3) {
		return 2;
	}
	
    int x = number % 3, y = number / 3;
	
    if (x == 0) {
		return pow(3, y);
	}
	else if (x == 1) {
		return 2 * 2 * pow(3, y - 1);
	}
	else 
		return 2 * pow(3, y);
	
}
```



## JZ17 打印从1到最大的n位数

输入数字 n，按顺序打印出从 1 到最大的 n 位十进制数。比如输入 3，则打印出 1、2、3 一直到最大的 3 位数 999。

```c++
class Solution {
public:
    vector<int> printNumbers(int n) {
        string s="";
        for(int i = 0; i < n; i++)
            s += '9';
        int max = stoi(s);
        vector<int> res;
        for(int j = 1; j <= max; j++)
            res.push_back(j);
        return res;
    }
};
```

 
# Leetcode 部分

## 剑指 Offer 58 - I. 翻转单词顺序
双指针法，进行切片，定义一个指针指向末尾，遇到非空格就另存，然后将其前向移动，再次遇到空格停止
 ![](vx_images/452532820250809.png =500x)


## 剑指 Offer 57. 和为s的两个数字
输入一个递增排序的数组和一个数字s，在数组中查找两个数，使得它们的和正好是s。如果有多对数字的和等于s，则输出任意一对即可。
双指针解法即可
 ![](vx_images/527142820229743.png =500x)

## 剑指 Offer 57 - II. 和为s的连续正数序列
输入一个正整数 target ，输出所有和为 target 的连续正整数序列（至少含有两个数）。
序列内的数字由小到大排列，不同序列按照首个数字从小到大排列。 滑动窗口法
当窗口的值大于target 右指针+1  小于 target 左指针+1
 ![](vx_images/7842920229645.png =600x)

## 剑指 Offer 58 - II. 左旋转字符串
指定k  将前k个字符移动到后面，
先翻转整体，然后翻转 前n-k个   后K个字符
 ![](vx_images/82462920239967.png =500x)


## 剑指 Offer 59 - I. 滑动窗口的最大值

 ![](vx_images/170902920243351.png =750x)

## 剑指 Offer 65. **不用加减乘除做加法**

![](vx_images/281712920248149.png =500x)


 

## 剑指 Offer 68 - I. 二叉搜索树的最近公共祖先
 ![](vx_images/349692920244508.png =700x)



## 剑指 Offer 43. 1～n 整数中 1 出现的次数
 ![](vx_images/373483020236593.png =800x)
 
