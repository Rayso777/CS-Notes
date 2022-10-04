[c语言中文网](http://c.biancheng.net/)

# C++
## STL 标准库
### 介绍
![](vx_images/382135620234028.png =600x)

### 容器种类选择
[C++ STL容器这么多，怎样选出最适合的？](http://www.cdsy.xyz/computer/programme/stl/20210307/cd161510784412019.html)


### 序列容器
#### 容器分类
![](vx_images/12825620235315.png =600x)

#### 迭代器分类

![](vx_images/250885920235882.png =600x)
**注意，容器适配器 stack 和 queue 没有迭代器，它们包含有一些成员函数，可以用来对元素进行访问。**
![](vx_images/576465920237050.png =500x)

#### array
1. array的底层实现
对普通的数组进行了封装
[C++ array容器：普通数组的“升级版”](http://www.cdsy.xyz/computer/programme/stl/20210307/cd161510778111964.html)

使用 array 容器代替普通数组，最直接的好处就是 array 模板类中已经为我们写好了很多实用的方法，可以大大提高我们编码效率。例如，array 容器提供的 at() 成员函数，可以有效防止越界操纵数组的情况；fill() 函数可以实现数组的快速初始化；swap() 函数可以轻松实现两个相同数组（类型相同，大小相同）中元素的互换。等等...

2. array的使用
初始化：
![](vx_images/4110621244809.png =600x)

std::array<double, 10> values; 
各个元素的值是不确定的（array 容器不会做默认初始化操作）。

std::array<double, 10> values {}; 
使用该语句，容器中所有的元素都会被初始化为 0.0。

std::array<double, 10> values {0.5,1.0,1.5,,2.0};
初始化了前 4 个元素，剩余的元素都会被初始化为 0.0。

![](vx_images/147790221231212.png =600x)

#### vector
1. vector底层实现
[vector底层实现的机制](http://www.cdsy.xyz/computer/programme/stl/20210307/cd161510778611969.html)
![](vx_images/532131921251559.png =600x)
![](vx_images/172192121224796.png =600x)

2. vector的使用
初始化：
[vector初始化的5中方式](http://c.biancheng.net/view/6749.html)

![](vx_images/229031121247715.png =600x)

![](vx_images/46340821230912.png =600x)

![](vx_images/360991321252053.png =600x)

![](vx_images/307771421249244.png =600x)

#### deque
1.底层实现
[深度剖析deque容器底层实现原理](http://xn--deque-pv6h20f70ibsnxhay7c88ncg969i18t36u2jb)
![](vx_images/109012621222781.png =600x)

2. 使用方法

![](vx_images/121901621244384.png =800x)

![](vx_images/327401621230459.png =700x)

![](vx_images/541062721246348.png =600x)

![](vx_images/38522821237816.png =600x)

#### list
1. 底层实现
[C++ list容器底层存储结构](http://www.cdsy.xyz/computer/programme/stl/20210307/cd161510780311983.html)

![](vx_images/15943021240603.png =600x)

2. 使用方法
![](vx_images/34163221251956.png =600x)

![](vx_images/345373221222995.png =600x)

#### forward_list
#include <forward_list>
using namespace std;
1. 底层实现
![](vx_images/1433621249319.png =600x)
2. 使用方法
![](vx_images/178273621242052.png =600x)

![](vx_images/332633621231182.png =600x)

forward_list 容器中是不提供 size() 函数的，但如果想要获取 forward_list 容器中存储元素的个数，可以使用头文件 <iterator> 中的 distance() 函数。


### 关联容器
#### 定义及种类
![](vx_images/515484121237176.png =600x)
![](vx_images/322354021224061.png =600x)
#### pair用法
[pair详解](http://c.biancheng.net/view/7169.html)
<utility> 头文件里面 make_pair也在里面

1. 用法
![](vx_images/385984521228068.png =600x)
![](vx_images/572464721230139.png =600x)



#### map
![](vx_images/486494322226413.png =700x)

#### set
![](vx_images/134804422232890.png =700x)


### 无序关联容器
#### 定义及种类
![](vx_images/9195221238687.png =600x)


![](vx_images/541185021250772.png =700x)

#### unordered_map
##### 1. 底层实现
[unordered_map底层实现](http://www.cdsy.xyz/computer/programme/stl/20210307/cd161510783312009.html)
![](vx_images/290220222236906.png =600x)
![](vx_images/479590222246623.png =600x)
![](vx_images/47330322237314.png =600x)

![](vx_images/261050322233156.png =600x)

![](vx_images/361235321242345.png =600x)
- 

##### 2. 使用
![](vx_images/215615421224380.png =600x)

![](vx_images/75325521236766.png =600x)

#### unordered_multimap

可以存相同的键值对，其他同上。

注意，当 unordered_multimap 容器中存储键值对的键为自定义类型时，默认的哈希函数 hash<key> 以及比较函数 equal_to<key> 将不再适用，这种情况下，需要我们自定义适用的哈希函数和比较函数，并分别显式传递给 Hash 参数和 Pred 参数。

![](vx_images/232390122233050.png =600x)



#### unordered_set
1. 定义
![](vx_images/592360622238064.png =600x)

2. 使用
注意，和 unordered_set 容器一样，unordered_multiset 模板类也没有重载 [ ] 运算符，没有提供 at() 成员方法。不仅如此，无论是由哪个成员方法返回的迭代器，都不能用于修改容器中元素的值。
![](vx_images/210910522243176.png =600x)


#### unordered_multiset
注意，此容器模板类中没有重载 [ ] 运算符，也没有提供 at() 成员方法。不仅如此，由于 unordered_set 容器内部存储的元素值不能被修改，因此无论使用那个迭代器方法获得的迭代器，都不能用于修改容器中元素的值。

可以存相同元素 ，其他同上


#### 自定义 哈希函数  和 比较规则

[如何自定义C++ STL无序容器的哈希函数和比较规则？](http://www.cdsy.xyz/computer/programme/stl/20210307/cd161510784312018.html)


### 容器适配器
#### 定义分类
1. 定义
![](vx_images/14581422240493.png =600x)
2. 分类
![](vx_images/357321422233576.png =600x)


#### stack
##### 1. 定义实现
![](vx_images/299791622220820.png =600x)
##### 2. 创建
![](vx_images/448991622243822.png =700x)

##### 3. 函数API
![](vx_images/525791722223924.png =700x)

#### queue
##### 1. 定义
![](vx_images/270332022241043.png =600x)

##### 2. queue创建
![](vx_images/69222122248913.png =600x)

##### 3. API
![](vx_images/271522122236732.png =600x)


#### priority_queue
##### 1. 定义

![](vx_images/452883422246361.png =800x)

##### 2. 使用

![](vx_images/501343322233082.png =800x)

![](vx_images/132363222236909.png =700x)

##### 3. 自定义排序

前面讲解 priority_queue 容器适配器时，还遗留一个问题，即当 <function> 头文件提供的排序方式（std::less<T> 和 std::greater<T>）不再适用时，如何自定义一个满足需求的排序规则。

函数对象

[priority_queue容器适配器实现自定义排序](http://cdsy.xyz/computer/programme/stl/20210307/cd161510785212026.html)


##### 4. 底层实现（堆）
[底层实现](http://www.cdsy.xyz/computer/programme/stl/20210307/cd161510785412027.html)


### 迭代器适配器
![](vx_images/59924022232328.png =700x)

![](vx_images/249534022251943.png =700x)


![](vx_images/343663922238741.png =700x)

### C++ STL常用算法（排序、合并、搜索和分区）
![](vx_images/364174122241298.png =700x)


## 模板元编程
[C++ 模板 全特化与偏特化](https://zhuanlan.zhihu.com/p/346400616)


## C++ primer笔记

1. 有道云：
[《C++Primer》全书学习笔记（详细）](https://zhuanlan.zhihu.com/p/454873031)

2. github1
[《C++Primer》github](https://zhuanlan.zhihu.com/p/109298643)























