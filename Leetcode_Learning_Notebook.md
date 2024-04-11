# Leetbook图解算法数据结构/Leetcode 101笔记

>本笔记是作者在学习Leetbook《图解算法数据结构》及高畅 Chang Gao老师的《LeetCode 101：和你一起你轻松刷题（C++）》时所做的笔记。感谢这些开源资源让我的学习更方便！

## 死活想不明白的题

1. Leetcode101-Page64：正则表达式匹配https://leetcode.cn/problems/regular-expression-matching/description/

## 关于基础数据结构的操作

### 向量vector

```cpp
#include<vector>
using namespace std;

// 构造函数
vector<int> myVec1 = {1, 2, 3};
vector<int> myVec2(3, 0); // 3个元素，每个元素都是0

// 删除某个元素和添加某个元素
std::vector<int> myVector = {1, 2, 3, 4, 5};
int i = 2; // 要删除的元素的索引
myVector.erase(myVector.begin() + i);// 删除第i个元素
myVector.insert(myVector.begin() + i, 3); // 在索引为2的位置插入值为3的元素

// 在尾部添加和删除
myVector.push_back(1);
myVector.pop_back();

// 获取尾部元素的值
int a = myVector.back();
```

### 字符串string

```cpp
// 构造函数
string()  // 构造一个空字符串。
string(const char* s)  // 使用 C 风格的字符串初始化 std::string。
string(size_t n, char c)  // 构造一个由 n 个字符 c 组成的字符串。
string(const string& str)  // 拷贝构造函数，用于创建一个字符串的副本。

// 赋值和连接
=  // 将一个字符串赋值给另一个字符串。
+=  // 将一个字符串连接到另一个字符串的末尾。
append  // 在字符串末尾添加字符、字符串或字符串的一部分。
+= 运算符也可以用于连接字符串。

// 访问字符
operator[]  // 访问字符串中的单个字符。
s.at(size_t pos)  // 返回指定位置处的字符，带有边界检查。
s.front() 和 s.back()  // 分别返回字符串的第一个和最后一个字符。

// 子字符串
string tmp = s.substr(2, 3)  // 2表示起始位置（从0开始），3表示长度

// 删掉字符
str.erase(p, n); // p表示索引，n表示个数
```



### 双向队列std::deque

```cpp
push_back(const T& value): 将元素添加到双端队列的尾部。
push_front(const T& value): 将元素添加到双端队列的头部。
pop_back(): 移除尾部的元素。
pop_front(): 从双端队列的头部移除元素。
back(): 返回双端队列的尾部的元素的引用。
front(): 返回双端队列的头部的元素的引用。
size(): 返回双端队列中的元素数量。
empty(): 检查双端队列是否为空。
clear(): 清空双端队列，移除所有元素。
at(size_type pos) / operator[](size_type pos): 返回指定位置的元素的引用。
insert(iterator pos, const T& value): 在指定位置插入。
erase(iterator pos): 在指定位置删除元素。
begin() / end(), rbegin() / rend(): 返回双端队列的迭代器或逆向迭代器，用于遍历双端队列的元素。
```
### 双向链表std::list

```cpp
push_back(const T& value): 将元素添加到链表的尾部。
push_front(const T& value): 将元素添加到链表的头部。
pop_back(): 从链表的尾部移除元素。
pop_front(): 从链表的头部移除元素。
back(): 返回链表的尾部的元素的引用。
front(): 返回链表的头部的元素的引用。
size(): 返回链表中的元素数量。
empty(): 检查链表是否为空。
clear(): 清空链表，移除所有元素。
insert(iterator pos, const T& value): 插入。
erase(iterator pos): 删除。
erase(iterator first, iterator last): 在指定位置插入或删除元素。
begin() / end(), rbegin() / rend(): 返回链表的迭代器或逆向迭代器，用于遍历链表的元素。
merge(list& other): 将另一个链表合并到当前链表。
sort(): 对链表进行排序。
```

### 用哈希表实现O(1)查找

`std::unordered_set\<int>`和`std::unordered_map\<int>`的区别在于，一个是无序集合容器，存储唯一的key，一个是无序关联容器，存储唯一的键值对key-value。

哈希表有一个好处，那就是当你插入重复的元素时，实际上不会插入。这可以自动去除重复的元素。

以下是`std::unordered_map`的用法。

```cpp
#include <unordered_map>
using namespace std;

unordered_map<int, string> myMap;

// 插入键值对
myMap[1] = "Apple";
myMap[2] = "Banana";
myMap[3] = "Orange";

// 通过迭代器遍历map
for (auto it = myMap.begin(); it != myMap.end(); ++it) {
    cout << "Key: " << it->first << ", Value: " << it->second << endl;
}

// 查找键
if (myMap.find(3) != myMap.end()) {
    cout << "Key 3 found in map" << endl;
}

// 使用 count() 方法检查键是否存在
// count() 方法返回与特定键相对应的元素数量，因为 std::unordered_map 中的键是唯一的，所以该方法返回的值要么是 0（键不存在），要么是 1（键存在）。
if (myMap.count(keyToFind) > 0) {
    std::cout << "Key found in the map." << std::endl;
} else {
    std::cout << "Key not found in the map." << std::endl;
}

// 删除键值对，如果要删除的元素不存在也没关系，不会报错，也不会造成修改
myMap.erase(1);

// 获取map的大小
cout << "Size of map: " << myMap.size() << endl;

// 判断是否为空
bool a = myMap.empty();

// 清空map
myMap.clear();

// 用于获取值，需要谨慎使用[]，因为如果键不存在就会自己创建一个，value取默认值
std::string res = myMap[1];
// 也可以用find()，但返回值是一个迭代器iterator，如果没找到则it = myMap.end()
auto it = myMap.find(1);
// 对于 std::unordered_map，迭代器指向的元素是一个键值对（std::pair 类型），其中 first 表示键，second 表示值
int = it->first;
std::string = it->second;
```

以下是`std::unordered_set`的用法。

```cpp
#include <unordered_set>
using namespace std;

unordered_set<int> mySet;

// 插入元素
mySet.insert(3);
mySet.insert(1);
mySet.insert(5);

// 检查元素是否存在
if (mySet.find(5) != mySet.end()) {
    cout << "Element 5 found in set" << endl;
}

// 使用 count() 方法检查元素是否存在
// count() 方法返回与特定键相对应的元素数量，因为 std::unordered_set 中不允许重复元素，所以该方法返回的值要么是 0（元素不存在），要么是 1（元素存在）。
if (mySet.count(5) > 0) {
    std::cout << "Element found in the set." << std::endl;
} else {
    std::cout << "Element not found in the set." << std::endl;
}

// 删除元素，如果要删除的元素不存在也没关系，不会报错，也不会造成修改
mySet.erase(3);

// 通过迭代器遍历set
for (auto it = mySet.begin(); it < mySet.end(); ++it){
    cout << *it << endl;
}
// 获取set的大小
cout << "Size of set: " << mySet.size() << endl;

// 判断是否为空
bool a = mySet.empty();

// 清空set
mySet.clear();

```

### set与map

`std::set`与`std::map`是有序容器，通常使用红黑树来实现，插入、查找和删除等操作的平均时间复杂度为$O(log  n)$。

```cpp
std::map<int, std::string> myMap;

// 插入键值对
myMap.insert({1, "one"});
myMap.insert({2, "two"});
myMap.insert({3, "three"});

// 遍历 map 并打印键值对
for (const auto& pair : myMap) {
    std::cout << pair.first << ": " << pair.second << std::endl;
}

// 查找键对应的值
auto it = myMap.find(2);
if (it != myMap.end()) {
    std::cout << "Value for key 2: " << it->second << std::endl;
} else {
    std::cout << "Key 2 not found!" << std::endl;
}

// 用operator[]来实现查找，但如果键不存在就会自己创建一个，value取默认值
string s = myMap[1];

// 删除键值对
myMap.erase(3);
```



## 关于栈与队列

### 最值栈

例题155.最小栈https://leetcode.cn/problems/min-stack/description/

设计一个最小栈 。它提供 `push` ，`pop` ，`top` 操作，并能在常数时间内检索到最小元素的栈。

设置完整的栈A，并设计一个辅助栈B。A每压入一个值，B的栈顶都应该是当前A中的最小值。

```cpp
/* 
A正常入栈，对于B，如果当前值大于B顶值，
意味着不论这个值在不在A栈中，都不影响最小值的取值，
因为天塌下来还有B顶值顶着，从小到大排顺序还没有排到当前值，
当前值就要从A出栈了。所以当前值不记录也罢。

从另一个角度想，如果当前值入A栈了，并不影响最小值的取值，
那么相比于它没有入栈的时候，最小值都是不变的。既然不变，
就没有必要让B顶值（即当前最小值）再入B栈一次。

但特殊情况是，如果当前值等于B顶值，就要再次入B栈。
因为pop规则是如果A出栈值等于当前最小值，那么B顶也要出栈。
如果当前值等于B顶值，就意味着这个值出A栈后A中还有同样小的值，
因此要在B中重复入栈。
*/
void push(int x) {
    A.push(x);
    if (B.empty()) B.push(x);
    else if (x <= B.top()) B.push(x);
}

/*
如果A出栈值等于当前最小值，那么B顶也要出栈，
这样才能做到A中最小值的排序更替
*/
void pop() {
    if (B.top() == A.top()){
        A.pop();
        B.pop();
    }
    else A.pop();
}

int top() {
    return A.top();
}

int getMin() {
    return B.top();
}
```



### 最值队列

一个队列，获取队列中的最大值，要求均摊时间复杂度均为 $O(1)$。

设置完整的队列q，并设置一个用于辅助的双向队列或双向链表l。以下是代码：

```cpp
class Checkout {
public:
    std::list<int> l;
    std::queue<int> q;
    Checkout() {}
    
    // 用于辅助的双向链表l始终维持从最大在前的非严格排序
    int get_max() {
        if (q.empty()) return -1;
        if (l.empty()) return -1;
        return l.front();
    }
    
    void add(int value) {
        // 压入完整队列q
        q.push(value);
        if (l.empty()) {
            l.push_back(value);
            return;
        }
        /* 对于辅助l的构建，要严格遵循大在前小在后的原则
           如果当前push_back的值比它前面的值更大，说明它前面的值失去了价值，
           这些值直到被pop出去也不会影响最大值的排序，因为他们后面有更大的
           所以要把这些比当前值小的靠前的值都扔掉，都pop_back()掉，然后再
           把当前值push_back进去*/
        while (!l.empty() && value > l.back()) {
            l.pop_back();
        }
        l.push_back(value);
        return;
    }
    
    // 和最值栈类似，当主队列q移除元素的时候，
    // 要看是否是l中记录的最大值，若是则同步移除
    int remove() {
        if (q.empty()) return -1;
        int temp = q.front();
        if (temp == l.front()) {
            l.pop_front();
            q.pop();
            return temp;
        }
        q.pop();
        return temp;
    }
};
```

### 单调栈

单调栈是指维护一个栈单调递增或递减。

例题：每日温度。给定一个整数数组 `temperatures` ，表示每天的温度，返回一个数组 `answer` ，其中 `answer[i]` 是指对于第 `i` 天，下一个更高温度出现在几天后。如果气温在这之后都不会升高，请在该位置用 `0` 来代替。https://leetcode.cn/problems/daily-temperatures/description/

```cpp
class Solution {
public:
    vector<int> dailyTemperatures(vector<int>& temperatures) {
        int n = temperatures.size();
        vector<int> res(n, 0);
        stack<int> st;
        for (int i = 0; i < temperatures.size(); ++i) {
            while (!st.empty() && temperatures[i] > temperatures[st.top()]) {
                auto t = st.top(); st.pop();
                res[t] = i - t;
            }
            st.push(i);
        }
        return res;
    }
};

作者：程序员吴师兄
链接：https://leetcode.cn/problems/daily-temperatures/solutions/71433/leetcode-tu-jie-739mei-ri-wen-du-by-misterbooo/
来源：力扣（LeetCode）
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。
```



## 关于二叉树

```cpp
struct TreeNode {
     int val;
     TreeNode *left;
     TreeNode *right;
     TreeNode() : val(0), left(nullptr), right(nullptr) {}
     TreeNode(int x) : val(x), left(nullptr), right(nullptr) {}
     TreeNode(int x, TreeNode *left, TreeNode *right) : val(x), left(left), right(right) {}
};
```

### 广度优先遍历二叉树（迭代）

```cpp
vector<int> doSomething(TreeNode* root) {
    vector<int> res;
    // 若传入树为空则返回空数据
    if (root == nullptr) return res; 
    // 节点队列q：用于存储将要遍历的节点，用队列是因为先进先出
    queue<TreeNode*> q;
    // 首先放入根节点，这就是第一个要遍历到的节点
    q.push(root); 
    // 开始遍历节点，用q是否为空判断有没有把树遍历完
    while (!q.empty()) { 
        // 从q中获取最前面的节点，就是当前要遍历的节点
        TreeNode* N = q.front(); 
        // 先将当前节点的子节点压入队列，准备后面遍历
        if (N->left != nullptr) q.push(N->left); 
        if (N->right != nullptr) q.push(N->right);
        // do something to TreeNode* N
        res.push_back(N->val);
        // 从q中弹出当前节点，表示已经遍历过了这个节点
        q.pop();
    }
    // 遍历结束
    return res;
}
```



### 深度优先遍历二叉树（递归，中序遍历）

```cpp
// 打印中序遍历
void dfs(Node* root) {
    if(root == nullptr) return;
    dfs(root->left); // 左子节点
    cout << root->val << endl; // 其实是对当前节点do sth.
    dfs(root->right); // 右子节点
}
```



## 关于排序

### 快速排序

* 快速排序算法是先将数组划分为两堆，一堆小于哨兵，一堆大于哨兵，此时哨兵的位置已经确定。
* 快速排序算法的思想可以适用于“快速选择问题”，即快速找到第n大/第n小的值。
* 时间复杂度$O(nlogn)$。
* 不稳定。

哨兵划分+递归。哨兵一般取第一个。

```cpp
void quickSort (vector<int>& nums, int leftBound, int rightBound) { 
    // 当要排序的序列等于1时终止并返回
    if (leftBound >= rightBound) return;
    // 按照哨兵划分成左右两个序列，取leftBound为哨兵
    int i = leftBound, j = rightBound;
    while (i < j) {
        while (i < j && nums[j] >= nums[leftBound]) j--; 
        // 注意这里一定是右侧指针先动，左侧指针后动，
        // 这样可以保证右侧指针先触发nums[j] >= nums[leftBound]
        // 因此当i == j时，可以保证num[i] = nums[j] <= nums[leftBound]
        // 只会把小的换到前面去，不会把大的换到前面去
        while (i < j && nums[i] <= nums[leftBound]) i++;
        swap(nums[i], nums[j]);
    }
    // 此时i == j，并且num[i] = nums[j] <= nums[leftBound]
    // 把哨兵换到它该在的位置上，确保它左边的都小于它，它右边的都大于它
    // 这样就完成了一次哨兵划分
    swap(nums[leftBound], nums[i]);
    
    // 分别对划分出的左序列和右侧序列执行递归
    quickSort(nums, leftBound, i - 1);
    quickSort(nums, i + 1, rightBound);
}
```

现在就要详细地说一说为什么递归返回条件是`leftBound >= rightBound`，而不是“==”。

这里有一个特殊情况，假设我们对一个序列{2,1}执行递归，很显然`l = 0, r = 1, i = 0, j = 1`。那么，进入循环后，j的位置不动，仍旧为1。i变为了1。不再满足循环条件，所以跳出循环。然后交换`nums[leftBound]`，`nums[i]`，序列变为{1,2}，完成了排序。但程序还没完，还有两次递归呢。

首先是左递归。此时`l = 0, i - 1 = 0`，二者相等，`leftBound == rightBound`而触发返回。

但是在右递归处，此时`l = i + 1 = 2, r = 1`，我们发现`leftBound > rightBound`了，如果维持原先的判断条件“==”，就会导致无限递归。所以应该是“>=”。



### 堆排序

* 先将数组建立成最大堆/最小堆，然后取出根节点为二叉树中最大/最小值，将这个值与数组最末一个交换位置，完成这个最大/最小值的归位。
* 然后剩下的这个堆，除了根节点之外，其他节点并没有发生变化。从根节点开始，将每个子树的根节点与左右孩子进行比较，如果位置不合适就交换根节点、左/右孩子的值，直到根节点的那个值出现在正确的位置，整个堆重整为最大/最小堆。
* 最大堆，排序后为从小到大；最小堆，排序后为从大到小。
* 时间复杂度$O(nlogn)$。
* 不稳定。

```cpp
// 重整堆（最大堆）将根节点root下沉到正确位置
void maxHeapify(vector<int>& nums, int size, int root_idx) {
    int max_idx = root_idx;
    int left_idx = 2 * root_idx + 1;
    int right_idx = 2 * root_idx + 2;

    // 找到root、leftChild、rightChild三者里值最大的一个，
    // 不要忘记检验计算出的左右子节点是否存在
    if (left_idx  < size && nums[left_idx]  > nums[max_idx]) max_idx = left_idx;
    if (right_idx < size && nums[right_idx] > nums[max_idx]) max_idx = right_idx;

    // 如果值最大的不是root，则把最大的值换到root位置
    if (max_idx != root_idx) {
        swap(nums[root_idx], nums[max_idx]);
        // 因为发生了交换，所以被交换的那个子树也受到了影响,
        // 子树的根节点（即max_idx节点）可能不再符合最大堆的定义，因此要重整
        heapify(nums, size, max_idx);
    }
}

// 堆排序（最大堆）
void maxHeapSort(vector<int>& nums) {
    int size = nums.size();

    // 首先进行建堆，从第一个非叶子节点开始进行下沉操作
    for (int i = size / 2 - 1; i >= 0; --i) {
        maxHeapify(nums, size, i);
    }

    // 然后将堆顶元素（当前的最大值）移动到尾部，完成该元素的排序，待排序数组长度减一
    for (int i = 1; i <= size; ++i) {
        swap(nums[size - i], nums[0]);
        maxHeapify(nums, size - i, 0);
    }
}

int main(){
    vector<int> nums = {3,2,3,1,2,4,5,5,6};
    maxHeapSort(nums);
    
    for (int num : nums) 
        cout << num << ", ";
    
    return 0;
}
```



### top-k问题

非常重要的一类问题，求一堆东西中第k大/第k小的东西。通常限制平均时间复杂度为$O(n)$，一般使用基于快速排序和堆排序的选择算法，在排序的基础上进行剪枝。一般时间复杂度不稳定，排序结果也不稳定。

* 堆排序一般比快排更快一些。
* 堆排序可以考虑一下最大堆还是最小堆。

#### 快排实现

```cpp
int quickSelect (vector<int>& nums, int leftBound, int rightBound, int target) { 
    // 当要排序的序列等于1时终止并返回
    if (leftBound >= rightBound) return nums[rightBound];
    // 按照哨兵划分成左右两个序列，取leftBound为哨兵
    int i = leftBound, j = rightBound;
    while (i < j) {
        while (i < j && nums[j] >= nums[leftBound]) j--; 
        // 注意这里一定是右侧指针先动，左侧指针后动
        while (i < j && nums[i] <= nums[leftBound]) i++;
        swap(nums[i], nums[j]);
    }
    swap(nums[leftBound], nums[i]);
    
    // 对target所在的区间做递归
    if (i == target) return nums[i];
    else if (i < target) leftBound = i + 1;
    else rightBound = i - 1;
    return quickSelect(nums, leftBound, rightBound, target);
}

int main(){
    vector<int> nums = {3,2,3,1,2,4,5,5,6};
    int k = 3;
    std::cout << quickSelect(nums, 0, nums.size() - 1, nums.size() - k);
}
```



#### 堆排序实现

```cpp
// 重整堆（最大堆）将根节点root下沉到正确位置
void maxHeapify(vector<int>& nums, int size, int root_idx) {
    // 与普通堆排序一致，不再赘述
}

// 堆排序（最大堆），根据top-k问题剪枝
int maxHeapSort(vector<int>& nums, int k) {
    int size = nums.size();

    // 首先进行建堆
    for (int i = size / 2 - 1; i >= 0; --i) {
        maxHeapify(nums, size, i);
    }

    // 然后将堆顶元素（当前的最大值）移动到尾部，只做k-1次（剪枝）
    for (int i = 1; i < k; ++i) {
        swap(nums[size - i], nums[0]);
        maxHeapify(nums, size - i, 0);
    }

    // nums[0]即为第k大的值
    return nums[0];
}
```



### 桶排序

* 桶排序适用于待排序序列中有多个重复数字，或者基本已知其分布特征的情况。
* 例如频率top-k问题，即序列中第k频繁的数字。

根据先验信息，可以构建多个“桶”，每个桶代表了一个范围。遍历序列，将每个元素放入对应范围的桶中，先在桶内排序，然后给每个桶进行排序。

例题https://leetcode.cn/problems/top-k-frequent-elements/description/



### 归并排序

先通过 **<u>递归</u>** 在每个序列的中点`m=(l+r)/2`进行划分，划分为`l~m`和`m+1~r`，最终将一个序列划分为单个元素，然后比大小，进行合并。

例如序列{7，3，2，6}，先分为{7，3}、{2，6}，然后分别划分为<u>{7}、{3}</u>、<u>{2}、{6}</u>。然后进行合并。先合并为{3，7}、{2，6}，然后令i、j分别指向两个序列的头部，逐个比较，合并，得到{2，3，6，7}。

```cpp
void merge_sort(vector<int>& nums, int l, int r) {
    if (l >= r) return; // 如果长度为1则返回
    int m = (l + r) / 2;
    // 进行递归，二分法进行划分
    merge_sort(nums, l, m);
    merge_sort(nums, m + 1, r);
    // 当划分到长度为1时，或者更低级的递归合并完成并返回时
    // 程序就会到这里，开始对本级递归进行合并
    vector<int> tmp; // 建一个临时数组把要合并的存起来
    for (int k = l; k <= r; ++k)
        tmp.push_back(nums[k]);
    int i = 0, j = m - l + 1;
    for (int k = l; k <= r; ++k) {
        if (i == m - l + 1) nums[k] = tmp[j++];
        else if (j == r - l + 1) nums[k] = tmp[i++];
            // 上面两处都要+1，因为越过最后一个才意味着真正结束
        else if (tmp[i] <= tmp[j]) nums[k] = tmp[i++];
        else nums[k] = tmp[j++];
    }
}
```



## 关于查找

通常的查找方法包括哈希表`unordered_map<char, bool> hmap;`、二分查找等。

### Z字形查找

最精妙的在于有序二维数组（同一行、同一列递增）的查找。将其看作根节点在右上角的二叉搜索树，从右上角进行类似二叉树的查找，右上角节点偏小则向下，偏大则向左，如果移动到左下角则说明找不到。形成Z字形的查找路径，最终在$O(N+M)$的时间复杂度中解决问题。例题：搜索二维矩阵https://leetcode.cn/problems/search-a-2d-matrix-ii/description/

### 二分法的迭代实现

```cpp
int find(vector<int>& records) {
    int i = 0, j = records.size() - 1;
    while(i <= j) {
        int m = (i + j) / 2;
        if(要找的在右边) i = m + 1;
        else j = m - 1;
    }
    return i;
}
```

## 关于搜索

### 广度优先搜索

广度优先搜索（BFS）是一层一层地进行查找，与深度优先搜索（DFS）的一口气直插到底不同。

BFS通过一个先进先出的队列queue来记录所有需要遍历的节点。有时还需要设置一个整数int num来记录这一层中有多少个节点，然后每遍历一个节点就num--，这样当我们遍历完这一层的时候num就归零，我们就可以进行相关操作。

BFS开始的条件是，队列queue中至少有一个节点待遍历。同理，BFS结束的标致是队列为空。当进行BFS时，首先将队列queue顶端的节点pop出，然后将其子节点（或与之相关的下一层节点）push进队列queue中。对于一些可能引起重复遍历的场景，需要将当前节点对应的flag标志进行置位。

* **广度优先搜索还是回溯法？**

  二者有一定相似之处，但不同情况适合用不同方法。回溯法适合搜索空间不大，且需要找到所有解的情况。广度优先搜索适合搜索空间较大，且只需找到最短路径的情况。



### 回溯法

回溯一般用递归而不是迭代。因为递归有天然的优势，可以自动记录每个步骤的参数，形成“历史记录”。需要回溯到上述某步骤时，可方便地回溯。

回溯较为通用的框架为：

```cpp
void backtrack(/* 可能需要其他参数 */) {
    // 终止条件：满足特定条件时结束递归
    if (/* 满足结束条件 */) {
        // 处理结果或保存结果
        return;
    }

    // 遍历所有可能的选择
    for (/* 遍历选择 */) {
        // 做出选择

        // 递归调用 backtrack()，处理下一个状态

        // 撤销选择
    }
}
```

经典问题：N皇后问题https://leetcode.cn/problems/n-queens/description/

如果按照经典的回溯思路，就要在每一次递归中逐个尝试每个可能的选项。这种情况虽然可行，但每次尝试的选项数量过多，时间复杂度甚至大于$O(N!)$，因此需要剪枝。

应当注意到，N皇后问题的隐藏条件是棋盘每一行都有且仅有一个皇后。因此在每次回溯时，只需逐个尝试下一行中的可能选项，无需尝试其他行的选项，大大减小了需要尝试的选项数量，使时间复杂度小于$O(N!)$，实现了剪枝。

```cpp
class Solution {
public:
    vector<vector<string>> solveNQueens(int n) {
        vector<vector<string>> res;
        vector<vector<bool>> flags(n, vector<bool>(n, true));
        vector<pair<int, int>> restmp;
        int targetLayer = 0;
        backtrace(n, targetLayer, flags, restmp, res);
        return res;
    }

    void restmp2res(int n, 
                    vector<vector<string>>& res, 
                    vector<pair<int, int>>& restmp) {
        vector<string> oneRes(n, string(n, '.'));
        for (auto pos : restmp) {
            int x = pos.first, y = pos.second;
            oneRes[x][y] = 'Q';
        }
        res.push_back(oneRes);
    }

    void backtrace(int n, 
                   int targetLayer, 
                   vector<vector<bool>>& flags, 
                   vector<pair<int, int>>& restmp, 
                   vector<vector<string>>& res) {
        if (restmp.size() == n || targetLayer == n) {
            restmp2res(n, res, restmp);
            return;
        }
        vector<int> avaliablePos;
        for (int i = 0; i < n; ++i) {
            if (flags[targetLayer][i]) {
                avaliablePos.push_back(i);
            }
        }
        if (avaliablePos.empty()) return;
        for (int avaY : avaliablePos) {
            vector<pair<int, int>> paintedThisTime = paintAttackArea(n, targetLayer, avaY, flags);
            restmp.push_back(make_pair(targetLayer, avaY));
            backtrace(n, targetLayer + 1, flags, restmp, res);
            restmp.pop_back();
            eraseAttackArea(paintedThisTime, flags);
        }
        
    }

    void eraseAttackArea(vector<pair<int, int>>& paintedThisTime, 
                         vector<vector<bool>>& flags) {
        for (auto pos : paintedThisTime) {
            int x = pos.first, y = pos.second;
            flags[x][y] = true;
        }
    }
    vector<pair<int, int>> paintAttackArea(int n, 
                                           int x, 
                                           int y, 
                                           vector<vector<bool>>& flags) {
        vector<pair<int, int>> paintedThisTime;
        for (int i = 0; i < n; ++i) {
            if (flags[x][i]) {
                flags[x][i] = false;
                paintedThisTime.push_back(make_pair(x, i));
            }
        }
        for (int i = 0; i < n; ++i) {
            if (flags[i][y]) {
                flags[i][y] = false;
                paintedThisTime.push_back(make_pair(i, y));
            }
        }
        int xt = x, yt = y;
        while (xt >= 0 && xt < n && yt >= 0 && yt < n) {
            if (flags[xt][yt]) {
                flags[xt][yt] = false;
                paintedThisTime.push_back(make_pair(xt, yt));
            }
            xt++;
            yt++;
        }
        xt = x, yt = y;
        while (xt >= 0 && xt < n && yt >= 0 && yt < n) {
            if (flags[xt][yt]) {
                flags[xt][yt] = false;
                paintedThisTime.push_back(make_pair(xt, yt));
            }
            xt--;
            yt--;
        }
        xt = x, yt = y;
        while (xt >= 0 && xt < n && yt >= 0 && yt < n) {
            if (flags[xt][yt]) {
                flags[xt][yt] = false;
                paintedThisTime.push_back(make_pair(xt, yt));
            }
            xt++;
            yt--;
        }
        xt = x, yt = y;
        while (xt >= 0 && xt < n && yt >= 0 && yt < n) {
            if (flags[xt][yt]) {
                flags[xt][yt] = false;
                paintedThisTime.push_back(make_pair(xt, yt));
            }
            xt--;
            yt++;
        }
        return paintedThisTime;
    }
};
```



例题79.单词搜索https://leetcode.cn/problems/word-search/description/

在一个字母组成的二维数组中找指定的单次，且不能重复使用格子。

```cpp
class Solution {
public:
    struct P2D{
        int i;
        int j;
    };
    bool exist(vector<vector<char>>& board, string word) {
        vector<vector<char>> b = board;
        queue<P2D> q; // 用于记录所有的起点
        int ii,ji;
        for (int i = 0; i < b.size(); ++i) { // 遍历寻找所有可能的起点
            for (int j = 0; j < b[0].size(); ++j) {
                if (b[i][j] == word[0]) {
                    q.push({i, j});
                }
            }
        }
        if (q.empty()) return false;
        while (!q.empty()) {// 对每个可能的起点，从其开始进行探索
            b = board;
            P2D cur = q.front();
            q.pop();
            ii = cur.i;
            ji = cur.j;
            if (helper(b, ii, ji, word, 0)) return true;
        }
        return false;
    }
    // 用于递归的函数
    bool helper(vector<vector<char>>& b, int i, int j, string word, int cur) {
        if (i < 0 || i >=b.size() || j < 0 || j >= b[0].size()) return false;
        if (b[i][j] != word[cur]) return false;
        if (cur == word.size() - 1) return true;
        // 本步若符合条件，则对走过的格子进行标记
        b[i][j] = ' ';
        // 通过“or”依次进行探索
        bool res = helper(b, i, j+1, word, cur + 1) || helper(b, i+1, j, word, cur + 1) || helper(b, i, j-1, word, cur + 1) || helper(b, i-1, j, word, cur + 1);
        // 如果下一步探索失败，就要在本步进行回溯，恢复被改变的数值
        if (!res) {
            b[i][j] = word[cur];
        }
        return res;
    }
};
```





## 关于分治

这里有一道题很好：给算式加括号https://leetcode.cn/problems/different-ways-to-add-parentheses/description/

* 分治的模板包括三个步骤：1. 分解；2. 解决；3. 合并。

```cpp
class Solution {
public:
    // 辅助函数，与分治无关
    bool isdigit(string s) {
        for (char c : s) {
            if (c < '0' || c > '9') return false;
        }
        return true;
    }
    
    // 动态规划，降低时间复杂度
    unordered_map<string, vector<int>> umap;
    
    // 正式的函数，也递归自身
    vector<int> diffWaysToCompute(string expression) {
        // 动态规划，如果过去做过这件事就不再重复做了
        if (umap.find(expression) != umap.end()) {
            return umap[expression];
        }
        
        // 递归终止条件：分解到不可再分
        vector<int> vres;
        if (isdigit(expression)) {
            vres.push_back(stoi(expression));
            return vres;
        }
        
        // 开始正式进入问题
        for (int i = 0; i < expression.size(); ++i) {
            char c = expression[i];
            if (c == '+' || c == '-' || c == '*') {
                // 1. 分解：把字符串根据此次选定的核心运算符划分为左串和右串
                string lstr = expression.substr(0, i);
                string rstr = expression.substr(i + 1);
                // 2. 解决：分别解决每一个子问题，得到子问题结果
                vector<int> vl = diffWaysToCompute(lstr);
                vector<int> vr = diffWaysToCompute(rstr);
                // 3. 合并：把子问题的结果合并为母问题的结果
                for (int l : vl) {
                    for (int r : vr) {
                        if (c == '+') vres.push_back(l + r);
                        else if (c == '-') vres.push_back(l - r);
                        else vres.push_back(l * r);
                    }
                } 
            }
        }
        // 动态规划，存储本级问题的结果
        umap[expression] = vres;
        // 返回本级问题的结果
        return vres;
    }
};
```

### 递归建立对象：堆与栈

首先要记住，如果想返回一个数据结构的指针，例如一棵树的根节点指针，那么在递归时一定要将节点建在堆上（new）而不是栈上（构造函数）。否则递归结束超出作用域，栈上的内存会被回收，造成这个指针失效。

### 关于迭代器

随机访问迭代器（如 `vector` 的迭代器）支持加减操作（+2、-3），支持比较（==、!=、>、<）操作，支持相减操作（求两个迭代器的距离关系），支持++和--。

迭代器的用法有点类似于指针，例如`std::vector<int>::iterator it = myVector.begin();`，通过`cout << *(it) << endl;`可以解析得到迭代器指向的变量。

要特别注意的是，`vector`的`begin()`方法指向第一个元素，但`end()`方法并不指向最后一个元素！在 C++ 的标准库中，`std::vector` 的 `end()` 方法返回的迭代器指向容器最后一个元素的下一个位置。换句话说，它指向的是容器的尾后位置，而不是最后一个元素本身。

这个特性使得 `end()` 迭代器可以用于边界标记和表示结束的位置。通常，遍历容器时，`end()` 迭代器用于判断遍历是否结束。

### 二叉树递归一定要从根到叶

不论如何，二叉树的递归一定要想个办法从根到叶，不要想着从叶到根。否则一定做不对。



## 动态规划

### 普通、一维、二维

动态规划通常比递归具有更好的时间复杂度。动态规划是从底到顶的，而递归是从顶到底的。

演化流程是这样的：

1. 暴力递归：通常产生很多重复的计算。例如斐波那契数列，$f(n) = f(n-1) + f(n-2)$。
2. 记忆化递归：还是递归的架构，但建立一个数组存储第一次计算出的结果，下次再递归到相同的计算就直接查表，减少很多的重复计算。例如斐波那契数列，$f(n) = f(n-1) + f(n-2)$。但同时建立一个数组`vector<int> dp(n + 1, 0)`（此处用到构造函数，建立n+1长度的数组，每个元素初始化为0），每计算出一个$f(i)$就让$dp[i]=f(i)$，这样每个$f(i)$只计算一次，后面再递归的时候就直接查表。
3. 动态规划：推翻递归的架构，不再从顶到底，而是老老实实从底到顶。同样建立一个数组存储从底到顶的每一步计算结果方便调用（如有必要）。例如斐波那契数列，已知$f(0) = 1，f(1) = 1$，那就计算$f(2)$，然后计算$f(3)$，直到$f(n)$。当然，这里由于$f(n)$ 只与 $f(n-1)$ 和 $f(n-2)$有关，就不再存储之前的值，所以总共只需要三个变量来回倒就行。

动态规划的一个核心要点是：找到一个状态转移方程。也就是说，找到$f(n)$与$f(n-1)$之间的联系。例如问$n$个东西的xx问题最优解是什么，那就考虑假如$n-1$个东西的最优解**<u>已经得到了</u>**，是$f(n-1)$，那么现在新加了1个东西，$n-1→n$，该怎样在已知$n-1$个东西最优解$f(n-1)$的情况下求得$n$个东西的最优解。如果需要更靠前的结果，就设置数组进行存储，如果不需要，就设置几个变量来回倒。很显然状态转移方程的初始变量很简单，例如只有1个或2个元素时最优解是肉眼可见的。这样就有了迭代的基础，从$1→n$。

需要注意的是，“最优子结构”和“重叠子问题”不意味着只能用贪心算法来解决问题，也不意味着无法规避陷入局部最优解的问题。动态规划不是一条路径走到黑，而是切实考虑如何从$n-1$的最优解得到$n$的最优解的问题。确保迭代到第几代，就能得到第几代的最优解，因此时间复杂度往往是$O(N)$。

因此往往需要一个与给定的要操作的变量大小相仿的变量作为辅助变量。例如要操作的变量是一个二维数组，那么往往需要建立一个同样长宽的二维数组作为辅助变量。如果二者不冲突，还可以合二为一，使得不额外占用空间，空间复杂度为$O(1)$。

以上两段话可以参考的例题是“珠宝的最高价值”https://leetcode.cn/leetbook/read/illustration-of-algorithm/5vokvr/。

一定要坚持$n-1→n$的思路。注意这道题：https://leetcode.cn/leetbook/read/illustration-of-algorithm/ozzl1r/。

* 对于二维网格，一定要记住，辅助变量的状态转移方程一定只与相邻结构有关。即$dp[i][j]$一定与$dp[i-1][j]$、$dp[i][j-1]$、$dp[i-1][j-1]$有关。当初始化时，先简单地初始化第一行和第一列，然后后面的即可开始迭代。另外要多想一想，迭代公式一定包含了所有的操作方法，有时是每种操作方法都试一遍然后取max或min。注意这道题：“最大正方形”https://leetcode.cn/problems/maximal-square/description/
* 一般都是“以$dp[i][j]$为结尾的xxx的指标记录在$dp[i][j]$中”，而不是“i、j矩阵中最大的xxx的指标记录在$dp[i][j]$中”。**<font color="red">统计最大最小的事不是动态规划的范畴。</font>**动态规划要求出所有解。

### 分割

给定一个东西，如何分割可以满足相应条件，例如分割数最小。

* 一般来说，分割问题的状态转移方程与前一个状态的关系不大，而与之前某个状态的关系较大。因此过去的结果要全部保留。
* 因此，不要执迷于寻找$dp[i]$与$dp[i-1]$的关系了。考虑一下其他更早的结果。

例题：给你一个整数 `n` ，返回 *和为 `n` 的完全平方数的最少数量* 。https://leetcode.cn/problems/perfect-squares/description/

```cpp
int numSquares(int n) {
    vector<int> dp(n + 1, INT_MAX);
    dp[0] = 0;
    for (int i = 1; i <= n; ++i) {
        for (int j = 1; j * j <= i; ++j) {
            dp[i] = min(dp[i], dp[i-j*j] + 1);
        }
    }
    return dp[n];
}
```

有时，在解决“多种可能的分割”问题时，**<u>动态规划和回溯往往都能奏效</u>**。但此时，往往回溯都具有更大的时间复杂度，导致超时。因此非必要不选回溯，动态规划的时间复杂度更可靠。例题：单词拆分：给你一个字符串 `s` 和一个字符串列表 `wordDict` 作为字典。如果可以利用字典中出现的一个或多个单词拼接出 `s` 则返回 `true`。https://leetcode.cn/problems/word-break/description/

### 子序列问题

> 一般来讲，子序列是主序列中某些元素组成的序列，不要求连续，但顺序不能变。例如主序列为1，2，5，4，3，子序列可以是2，4，3。

* 一个序列的子序列问题

  可以考虑的做法是：定义`vector<int> dp(n+1)`，让`dp[i]`存储以`nums[i]`为结尾的满足要求的子序列。例题：给你一个整数数组 `nums` ，找到其中最长严格递增子序列的长度。

  https://leetcode.cn/problems/longest-increasing-subsequence/description/

* 两个序列的公共子序列问题

  这道题十分经典。给定两个字符串 `text1` 和 `text2`，返回这两个字符串的最长 **公共子序列** 的长度。如果不存在 **公共子序列** ，返回 `0` 。做法十分经典，就是设置二维辅助数组`dp[i][j]`，让`dp[i][j]`存储对于`text1` 到索引`i`，`text2` 到索引`j`时，此时的最长公共子序列的长度。注意，此时`dp[i][j]`并不要求以`i`、`j`结尾。

  https://leetcode.cn/problems/longest-common-subsequence/description/

```cpp
int longestCommonSubsequence(string text1, string text2) {
    int m = text1.length(), n = text2.length();
    vector<vector<int>> dp(m + 1, vector<int>(n + 1, 0));
    for (int i = 1; i <= m; ++i) {
        for (int j = 1; j <= n; ++j) {
            if (text1[i-1] == text2[j-1]) dp[i][j] = dp[i-1][j-1] + 1;
            else dp[i][j] = max(dp[i-1][j], dp[i][j-1]);
        }
    }
    return dp[m][n];
}
```

### 背包问题

>模板：有N个物品和容量为W的背包，每个物品有体积w和价值v，求问拿哪些物品可以使背包的容量最大？
>
>1. 0-1背包问题：每样物品只有一个，只能选择拿(1)与不拿(0)
>2. 完全背包问题：每样物品有无限多个
>3. 完全背包问题-改版：凑钱问题：N种面值的硬币，每种可以取无限多个，凑满M元，问最低取多少硬币（必须把背包装满，且价值最低）

对于**<u>0-1背包问题</u>**，典型思路是定义二维数组，$dp[i][j]$表示前$i$件物品在总价值不超过$j$时所能取得的最大价值。为了方便起见，定义为`vector<vector<int>> dp(N + 1, vector<int>(W + 1, 0))`，这样其实索引$i$时，对应的物品索引是$i-1$，就无需单独考虑边角的特殊情况。

* 空间压缩：我们注意到，状态转移方程$dp[i][j] = max(dp[i-1][j], dp[i-1][j-w] + v)$中，只用到了上一行的数据，没有用到更早的数据。因此可以进行空间压缩。在遍历时，要**<font color="red"><u>从右往左遍历</u></font>**。

```cpp
// 常规解法
int knapsack(vector<int> weights, vector<int> values, int N, int W) {
    vector<vector<int>> dp(N + 1, vector<int>(W + 1, 0));
    for (int i = 1; i <= N; ++i) {
        int wei = weights[i-1], val = values[i-1];
        for (int j = 1; j <= W; ++j) {
            if (j >= wei) 
                // dp[i-1][j]:           这一件不拿，不拿就满足了j
                // dp[i-1][j-wei] + val: 这一件拿，拿了才满足j
                dp[i][j] = max(dp[i-1][j], dp[i-1][j-wei] + val);
            else dp[i][j] = dp[i-1][j];
        }
    }
    return dp[N][W];
}

// 空间压缩
int knapsack(vector<int> weights, vector<int> values, int N, int W) {
    vector<int> dp(W + 1, 0);
    for (int i = 1; i <= N; ++i) {
        int wei = weights[i-1], val = values[i-1];
        /* 
        下面要进行从右往左的遍历，因为如果从左往右的话，
        在更新到dp[i][j]时用到的dp[i-1][j-wei]是被更新过的，不是原来的，就错了
        从右向左只遍历到wei而不是0，因为wei左边的相当于常规解法中的else{}
        无需选择，只需要照抄上一行的数即可，由于在原处更新，此处即不动
        */
        for (int j = W; j >= wei; --j) {
            // dp[j]:         这一件不拿，不拿就满足了j，其实相当于dp[i-1][j]
            // dp[j-wei] + v: 这一件拿，拿了才满足j，其实相当于dp[i-1][j-wei]
            dp[j] = max(dp[j], dp[j-wei] + val);
        }
    }
    return dp[W];
}
```

对于**<u>完全背包问题</u>**，典型思路和上面的一样。唯一的差异是状态转移方程有些许不同。虽然可以拿很多个，但那些情况之前都考虑过了，所以只考虑拿一个的问题。

* 空间压缩：在遍历时，要**<font color="red"><u>从左往右遍历</u></font>**。因为状态转移方程$dp[i][j] = max(dp[i-1][j], dp[i][j-w] + v)$中用到的$dp[i][j-w]$是本行的数据，也就是更新过的数据。注意和0-1背包问题不同！！！

```cpp
// 常规解法中的状态转移方程
if (j >= w) 
    // dp[i-1][j]：       这一件不拿，不拿就满足了j
    // dp[i][j-w] + v：   这一件拿1个，拿了1个才满足j
    dp[i][j] = max(dp[i-1][j], dp[i][j-w] + v);
else dp[i][j] = dp[i-1][j];

// 空间压缩
int knapsack(vector<int> weights, vector<int> values, int N, int W) {
    vector<int> dp(W + 1, 0);
    for (int i = 1; i <= N; ++i) {
        int wei = weights[i-1], val = values[i-1];
        /* 
        下面要进行从左往右的遍历，因为
        在更新到dp[i][j]时用到的dp[i][j-w]就是被更新过的，不是原来的
        要先更新dp[i][j-w]才能更新dp[i][j]
        */
        for (int j = wei; j <= W; ++j) {
            // dp[i-1][j]：       这一件不拿，不拿就满足了j
            // dp[i][j-w] + v：   这一件拿1个，拿了1个才满足j
            dp[j] = max(dp[j], dp[j-wei] + val);
        }
    }
    return dp[W];
}
```

完全背包问题-改版：凑钱问题：N种面值的硬币，每种可以取无限多个，凑满M元，计算并返回可以凑成总金额所需的 最少的硬币个数。如果没有任何一种硬币组合能组成总金额，返回-1。（必须把背包装满，且价值最低）

```cpp
int coinChange(vector<int>& coins, int amount) {
    if (coins.empty()) return -1;
    vector<int> dp(amount + 1, amount + 2); // 注意这里初始化的值
    dp[0] = 0;
    for (int i = 1; i <= amount; ++i) {
        for (const int & coin : coins) {
            if (i >= coin) dp[i] = min(dp[i], dp[i-coin] + 1);
        }
    }
    // 最后对比一下，得出能不能凑齐金额
    return dp[amount] == amount + 2? -1: dp[amount];
}
```

### 股票问题

股票问题主要是给你一个数组，存储了很多天的股票价格，然后在交易次数等方面有所限制，问如何最大化利润。

例如：买卖股票的最佳时机：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/description/

主要思路是：假如买卖次数是k，那么设立数组`vector<int> buy(k+1, INT_MIN)`和`vector<int> sell(k+1, 0)`。其中，`buy[i]`代表第i次买获得的最大收益；`sell[i]`代表第i次卖获得的最大收益。需要注意的是，先是第1次买，然后第1次卖，然后第2次买，第2次卖……依此类推。每次买卖，都只和前一次有关系。例如，假如只允许买两次，就有：

```python
# python
class Solution:
    def maxProfit(self, prices: List[int]) -> int:

        b1, b2, s1, s2 = -float("inf"), -float("inf"), 0, 0

        for p in prices:
            b1 = max(b1, 0 - p)
            s1 = max(s1, b1 + p)
            b2 = max(b2, s1 - p)
            s2 = max(s2, b2 + p)
            
        return s2

作者：洛必达泉
链接：https://leetcode.cn/problems/best-time-to-buy-and-sell-stock-iv/solutions/740596/5xing-dai-ma-gao-ding-suo-you-gu-piao-ma-j6zo/
```



## 贪心

这道题没做出来，https://leetcode.cn/leetbook/read/illustration-of-algorithm/lhrww7/。

可以看一下lambda表达式的东西。

内置排序函数`std::sort`中可以自定义排序函数，但是要注意，这个函数不能是成员函数。如果一定要是成员函数，就要用lambda表达式进行调用，例如

```cpp
class Solution {
public:
    bool compare(const int& a, const int& b) {
        std::string astr = std::to_string(a);
        std::string bstr = std::to_string(b);
        std::string ab = astr;
        ab.append(bstr);
        std::string ba = bstr;
        ba.append(astr);
        return ab < ba;
    }

    string crackPassword(vector<int>& password) {
        std::string res;
        // lambda表达式调用Solution::compare()
        std::sort(password.begin(), password.end(), [this](const int& a, const int& b)
        {return compare(a, b);});
        for (int num : password) {
            std::string tmp = std::to_string(num);
            res.append(tmp);
        }
        return res;
    }
};
```



## 位运算

### 异或

异或(XOR)：同真或同假则为0，不同则为1

| A    | B    | A XOR B |
| ---- | ---- | ------- |
| 0    | 0    | 0       |
| 0    | 1    | 1       |
| 1    | 0    | 1       |
| 1    | 1    | 0       |

位运算异或可以用于消除偶数个相同的数。且异或运算具有交换律和结合律。这意味着$A~XOR~B~XOR~C~XOR~B~XOR~A=C$。

且$A~XOR~A=0$，$A~XOR~0=A$。

例题：一个数组中只有一个数出现了一次，其他都出现了两次，找这个出现一次的数：https://leetcode.cn/problems/single-number/description/

### 有限状态机

这道题很经典，在一个数组中只有一个数出现了1次，其余数字均出现3次。https://leetcode.cn/leetbook/read/illustration-of-algorithm/9hyq1r/

通过有限状态自动机进行状态转移计算，然后化简逻辑关系，总结出状态转移方程。

### 2与4的整数次方

如果一个数$n$是2的整数次方，则它的二进制表示一定是$0b~0...010...0$这样的形式，即只有一个1，其余全是0。判断方法就是，令$n$和$n-1$做按位与，如果结果是0，则$n$是2的整数次方。

如果一个数$n$是4的整数次方，那它首先是2的整数次方，要满足上述条件。其次，它的二进制表示一定是0b0...010...0这样的形式，仅有一个1，且1后面的0是偶数个。判断方法就是，首先判断$n$是2的整数次方，如果是，则令$n$和$0b~0101~0101~0101~0101~0101~0101~0101~0101$（即$0x~5555~5555$）按位与，如果结果不为0则$n$是4的整数次方。

* 注意！按位运算符号（&等）的优先级低于比较符号（==、>、<等）！

  ```cpp
  if (n & (n-1) == 0) return true;    // 错误写法，会先执行“(n-1) == 0”
  if ((n & (n-1)) == 0) return true;  // 正确写法
  ```


### 用于统计重复项

尤其是对于字符串问题。例如，有大量长度很长的小写字母字符串，比较两两之间是否有相同字符。此时，如果使用`unordered_set`，可能依旧无法满足时间复杂度要求。可以考虑用26位的整数统计每个字母是否出现，并通过位运算（按位与）来计算两个字符串是否有相同字母。

例题：最大单词长度乘积https://leetcode.cn/problems/maximum-product-of-word-lengths/description/

## 数学

### 约瑟夫环问题（动态规划）

* n, m问题：n个数字的环，0~n-1，首尾相接。从0开始往后数，删掉第m个，然后从删掉的下一个位置开始往后数，删掉第m个，循环往复直到最后一个，求这个数是多少。
* (n-1), m问题：n-1个数字的环，0~n-2，首尾相接。从0开始往后数，删掉第m个，然后从删掉的下一个位置开始往后数，删掉第m个，循环往复直到最后一个，求这个数是多少。

https://leetcode.cn/leetbook/read/illustration-of-algorithm/oxrkot/

思路是：当n个数字的环删掉一个之后，就只剩下n-1个了。此时，可以化简为类似于(n-1), m问题，但区别在于真正的(n-1), m问题是从0~n-2，但这个问题的数字排布情况更为复杂，假设被删掉的数字的下一个数字是t，就是1, 2, ... , t-3, t-2, t, t+1, ... , n-2, n-1。变换一下顺序，可以写作t, t+1, ... , n-1, 0, 1, 2, ... , t-3, t-2。（需要注意的是，此处为了更加直观，举的例子中被删掉的数字不是在首尾的数字，而是一个在中间的数字。）

但是我们可以找到真正的(n-1), m问题与本题的关系。也就是A=(0, 1, 2, ... , n-3, n-2)与B=(t, t+1, ... , n-1, 0, 1, 2, ... , t-3, t-2)之间的换算关系。对于A中任意一个值A[i]，可以通过这样的关系换算到B[i]：$ B[i] = (A[i] + t) \:mod\:n $。

这也就是为什么要将1, 2, ... , t-3, t-2, t, t+1, ... , n-2, n-1变换顺序成为t, t+1, ... , n-1, 0, 1, 2, ... , t-3, t-2。这样就依然是从头开始，而不是从中间的某个地方开始了。这样有什么好处呢？你要知道，所有的数第m个然后删掉的过程其实都不关心删除的元素究竟是什么内容，只关心这个元素的位置。也就是说，变换顺序之后，从头开始的t, t+1, ... , n-1, 0, 1, 2, ... , t-3, t-2其实所有的被删除的元素的位置都等价于(n-1), m问题。(n-1), m问题第一次被删掉的是第几个元素，t, t+1, ... , n-1, 0, 1, 2, ... , t-3, t-2第一次被删掉的就是第几个元素，唯一的区别就是元素内容不同。

所以说，操作到最后，(n-1), m问题最终剩下的是第几个元素，t, t+1, ... , n-1, 0, 1, 2, ... , t-3, t-2这个序列最终剩下的就是在相同位置的元素。所以说假如(n-1), m问题的解是第k个元素，也就是k-1，那么t, t+1, ... , n-1, 0, 1, 2, ... , t-3, t-2的解也就是第k个元素。那么是多少呢？我们已经有了换算关系，计算一下就知道了，是$B[k] = (A[k] + t) \:mod\:n =(k-1+t)\:mod\:n$。

也就是说，这两个序列的解是在顺序上同质的。也就是说，如果你直到了(n-1), m问题的解，也就直到了n, m问题的解。使用动态规划即可。你知道了n = 0时不论m是多少，显然解是0。写在代码里，只需要把“mod”换成"%"就行了。

### 随机与采样

一般使用`rand()`函数进行随机数的生成。该函数会随机生成一个0~RAND_MAX范围内的整数，可看作均匀分布。通常情况下，RAND_MAX = 32767。该函数生成的是伪随机数。

当需要一个特定范围内的整数时，例如当我们需要一个0~100内的随机整数，可以使用`rand() % 101`来实现。

如果有更进一步的需求，可以用下面的方法。请注意，下面的方法生成的依然是伪随机数。

`std::uniform_real_distribution` 用于生成指定范围内的均匀分布的双精度或单精度浮点数。

`explicit uniform_real_distribution(RealType a = 0.0, RealType b = 1.0);`其中$a$和$b$：指定生成随机数的范围 $[a, b)$。

```cpp
std::random_device rd;
std::mt19937 gen(rd());
std::uniform_real_distribution<double> dis(0.0, 1.0);
double random_number = dis(gen);  // 生成 [0, 1) 之间的随机数
```

`std::uniform_int_distribution` 用于生成指定范围内的均匀分布的整数。

`explicit uniform_int_distribution(IntType a = 0, IntType b = 1);`其中$a$和$b$：指定生成随机数的范围 $[a, b]$。

```cpp
std::random_device rd;
std::mt19937 gen(rd());
std::uniform_int_distribution<int> dis(1, 6);
int random_number = dis(gen);  // 生成 [1, 6] 之间的随机整数
```



* 重要例题：按权重抽样：https://leetcode.cn/problems/random-pick-with-weight/description/

```cpp
class Solution {
public:
    std::mt19937 gen;
    std::uniform_int_distribution<int> dis;
    vector<int> pre;
    
    // 需要注意的是，这里通过初始化列表对随机数生成相关组件进行初始化
    Solution(vector<int>& w) : gen(random_device{}()), dis(1, accumulate(w.begin(), w.end(), 0)) {
        partial_sum(w.begin(), w.end(), back_inserter(pre));
    }
    
    int pickIndex() {
        int x = dis(gen);
        return lower_bound(pre.begin(), pre.end(), x) - pre.begin();
    }
};
```

再来放一个在构造函数内部进行初始化的例子。例题：链表抽取随机节点：https://leetcode.cn/problems/linked-list-random-node/description/。这种常规思路下，时间复杂度为$O(1)$，空间复杂度为$O(n)$。

```cpp
class Solution {
public:
    vector<int> v;
    std::mt19937 gen;
    std::uniform_int_distribution<int> dis;

    Solution(ListNode* head) {
        ListNode* pt = head;
        while (pt != nullptr) {
            v.push_back(pt->val);
            pt = pt->next;
        }
        std::random_device rd;
        gen = std::mt19937(rd());
        dis = std::uniform_int_distribution<int>(0, v.size() - 1);
    }
    
    int getRandom() {
        int pos = dis(gen);
        return v[pos];
    }
};
```

#### 水塘抽样

同样是这道题：链表抽取随机节点：https://leetcode.cn/problems/linked-list-random-node/description/，另一种抽样方法可以保证时间复杂度为$O(n)$，空间复杂度为$O(1)$，这就是水塘抽样。

水塘抽样：进行一次抽样时，需要从头到尾遍历链表一次。（默认节点序号从0开始）遍历到第$i$个节点时，有$1/m$的概率用第$i$个节点的值覆盖掉之前的选择。具体的来说，遍历到第$i$个节点时，在$[0,i]$中随机抽取一个整数，假如恰好为0，则用第$i$个节点的值覆盖掉之前的选择。由于每次抽样都需要遍历整个链表，所以时间复杂度为$O(n)$。

数学解释：第$i$个节点被最终抽取的概率 = 遍历到第$i$个节点时抽中 × 遍历到第$i+1$个节点时没抽中 × 遍历到第$i+2$个节点时没抽中 × ... × 遍历到最后一个节点时没抽中
$$
p(i)=\frac{1}{i}\times(1-\frac{1}{i+1})\times...\times(1-\frac{1}{n})=\frac{1}{i}\times\frac{i}{i+1}\times...\times\frac{n-1}{n}=\frac{1}{n}
$$


## 双指针问题

### 快慢指针

https://leetcode.cn/problems/linked-list-cycle-ii/description/

用快慢指针来探查链表中是否存在环路，并定位环路起点。其中快指针一次走两步，慢指针一次走一步。如果存在环路，则两个指针一定会相遇，如果不存在环路，快指针会先到达末尾。如果存在环路，在两个指针相遇时，将快指针重置到开头位置，两个指针下一次相遇的时候就是环路起点。

虽然这听起来很神奇，也很难立刻想明白，但只要列个方程就会发现这是一个简单的数学问题。

FUCK MATH!



## 关于溢出

常常遇到int类型溢出的问题。此时要变换思路，将乘法改成除法。
