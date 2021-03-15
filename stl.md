# 哈希表

## 相关概念

避免碰撞 — 构造哈希函数、再散列函数法、**哈希表加链表**

![img](https://i.loli.net/2021/03/14/qYL6KAlCgMzwZ3n.jpg)



1. 虽然很好的处理了碰撞的问题，但是当单链表很长时，遍历链表的速度会很慢。
2.  当链表太长时（经验法则：当元素个数比 bucket <vector> 数还要多时），想办法将其打散 — 将 bucket 扩充大约两倍。选择53的倍数附近的素数 53 -> 97 -> 193........。（G2.9适用，其他的不一定。）
3.  哈希表的成长过程：bucket 会增加、 所有的元素所在的 bucket 会重新计算一遍，会花费一定的时间

![img](https://i.loli.net/2021/03/14/Yy9PQjusFngXBvA.jpg)

1. **HashFcn** 由元素**对象抽象出哈希码**的函数
2. ExtraKey 如何从元素（可能是 pair 等）取出 key 值的函数
3. EqualKey 如何**判断 key 相等的函数**



哈希表本身的大小为20个字节：3个函数对象、1个 Vector、1个 unsigned int。

hashtable_node 为节点构成的单向链表（VC中为双向链表）。

迭代器必须实现智能的 ++ 等操作，在链表末端后重新定位回 bucket ，其中有两个指针，一个指向节点，一个指向哈希表本身。



```c++
//Application
hashtable<const char*,
          const char*,
          hash<const char*>,
          identity<const char*>,
          eqstr,
          alloc>
ht(50,hash<const char*>(),eqstr());

ht.insert_unique("kiwi");
ht.insert_unique("plum");
ht.insert_unique("apple");

struct eqstr{
    bool operator()(const char* s1,
                    const char* s2,) const
    {return strcmp(s1,s2) == 0;}
};
```

关于 hashfcn：当模板参数为简单类型时，传入的简单类型的值可以直接作为抽象的哈希编码，其他：

![img](https://i.loli.net/2021/03/14/1dEkmn8VevlOh5F.jpg)

其中的 hash_string(处理 c 风格字符串) 方案也是经验设计。

由 **hash code%number_of_bucket** 的除数取余算法方案是**业内公认的做法**。



![img](https://i.loli.net/2021/03/14/OiJ8XdfcIFagwym.jpg)



find 和 operator 是哈希表中的一些成员函数，其中要计算元素会落在哪个篮子里。按其调用的路径，**最后都会归结到 hash(key)%n** 。



首先生成哈希值，然后使用hash code%number_of_bucket计算元素位置



## hash_set与hash_multiset

### 相关概念

1. hash_set是以hashtable为底层机制实现的。故对hash_set的各种操作可以转调用hashtable来实现。
2. hash_set与set的不同：hash_set的底层机制是hashtable，而set的底层机制是RB-tree；set的元素能够自动排序，而hash_set的元素没有排序功能
3. hash_set中键值就是实值，实值就是键值。
4. hash_multiset的与hash_set有很大的相同性，其唯一差别就是hash_multiset中的元素可以重复。hash_set中的插入函数使用的是hashtable中的insert_unique()，而hash_multiset中的插入函数使用的是hashtable中的insert_equal()。
   

### 实现

```
// hash_set类定义
template <class Value, class HashFcn = hash<Value>,
          class EqualKey = equal_to<Value>,
          class Alloc = alloc>
class hash_set
{
private:
  typedef hashtable<Value, Value, HashFcn, identity<Value>, 
                    EqualKey, Alloc> ht;
  ht rep;        //底层机制 hashtable

public:
....
  hash_set() : rep(100, hasher(), key_equal()) {}    //缺省使用100个篮子，
                                                     //最后将被调整成对应的质数193

  hash_set(size_type n, const hasher& hf) : rep(n, hf, key_equal()) {}    //构造函数
  hash_set(size_type n, const hasher& hf, const key_equal& eql)           //构造函数
    : rep(n, hf, eql) {}

//方法，通过hash table实现
  size_type size() const { return rep.size(); }
  size_type max_size() const { return rep.max_size(); }
  bool empty() const { return rep.empty(); }
  void swap(hash_set& hs) { rep.swap(hs.rep); }
  friend bool operator== __STL_NULL_TMPL_ARGS (const hash_set&,
                                               const hash_set&);

  iterator begin() const { return rep.begin(); }
  iterator end() const { return rep.end(); }
```

## hash_map 与 hash_multimap

### 相关概念

SGI在STL标准外提供了hash_map，以hashtable作为底层机制。运用map为的是能够根据键值快速搜索元素，这一点RB-tree或是hashtable都能够实现。但RB-tree有自动排序能力而hashtable没有，其结果就是set元素会自动排序而hash_set不会。map和hash_map一样，拥有键和值，它们的使用方法也一样。 
需要很简单： 
1、hash函数（库有则使用库，没有则自己提供仿函数）。 
2、key大小比较函数（库有，则使用库提供的模板实例化类，否则自己编写仿函数） 
3、使用很简单，插入的时候，注意 insert 和 [ ] 方法的不同。

### 实现

```c++
int main(void){
    hash_map<const char * , int , __gnu_cxx::hash<const char*> , eqstr> Mymap;
    Mymap["January"] = 31;//设置map特有的操作符重载，下面重点讲解，将hashmap键和值可以用来计算键的次数
    Mymap["February"] = 28;
    Mymap["March"] = 31;
    Mymap["April"] = 30;
    Mymap["May"] = 31;
    Mymap["June"] = 30;
    Mymap["July"] = 31;
    Mymap["August"] = 31;
    Mymap["September"] = 30;
    Mymap["October"] = 31;
    Mymap["November"] = 30;
    Mymap.insert( pair<const char * , int>("December" , 31) );//产生临时对象，并pair起来

    //测试输出对应的键和值
    cout << "December " << Mymap["December"] << endl;
    cout << "June " << Mymap["June"] << endl;
    cout << "April " << Mymap["April"] << endl;
    cout << "March " << Mymap["March"] << endl;
     
    cout << endl << "测试遍历操作" << endl;
    for(hash_map<const char * , int , __gnu_cxx::hash<const char*> , eqstr>::const_iterator ite = Mymap.begin() ; ite!= Mymap.end() ; ite++)
        cout << (*ite).first << "  " << ite->second << endl;//记住这两种操作符重载类型
    cout << endl;

}
```

这是最重要的地方，通过key获取对应的value。如果key存在，则返回value的引用，如果key不存在，则插入并且将value初始化为默认值并返回其引用，对应int，就相当于int()那么就是0。

```cpp
T& operator[](const key_type& key) {
    return rep.find_or_insert(value_type(key, T())).second;
  }//这个是最重要的方法，区别与set的，很重要，直接调用了find_or_insert
```

find_or_insert的功能在前一讲hashtable已经详细说明，反正返回的是hashtable第一个模板参数类型。若key存在则返回存在的，否则插入hashtable并返回对应的引用。 
所以这里可以将IP地址作为key，IP出现的频率作为value，用来统计每个IP出现的频率，在大数据的时候特别有用，所以这个就是map牛逼的地方，存储和查找都非常块。

![img](https://i.loli.net/2021/03/14/qR24NyhUKndHClV.jpg)



# 红黑树

## 相关概念

![img](https://i.loli.net/2021/03/14/5hzu2Knbw3jOP7N.jpg)

1 rb_tree 是一种高度平衡的搜索二叉树，其元素排列的规则有利于 search 和 insert，并同时保持适度的平衡。
2 rb_tree 提供遍历操作以及 iterator。元素放入后有一定的排列规则，按正常规则(++ iter)迭代器遍历时为输出为排序状态(sorted)。
3 不应使用 rb_tree 的 iterator 改变元素值(影响原有排序)。语法层面是不禁止这种操作的。如此设计的原因是，由 rb_tree 实现的 map 其 key 值(排序以 key 值为依据) 是不能改动的，而通过 iterator 改变 map 的 data 值是允许的。
4 rb_tree 提供两种 insertion 操作：insert_unique() 和 insert_equal()。 前者表示节点的 key 一定在整个 tree 中独一无二，否则安插失败（但不返回error，不做任何操作）；后者表示节点的 key 可重复。



## 实现

![img](https://i.loli.net/2021/03/14/pKBCGvck7QIfyPS.jpg)

Key 为 key 值的类型，Value 为放入的整个元素节点的数据类型、

KeyOfValue 为从 Value 中 取得 key 值的方法，此处应为一个函数对象、（例：identity<int>、select1st<value_type>）

Compare 为比较两个元素大小的函数对象。



![img](https://i.loli.net/2021/03/14/T59udWnzhUOYwcv.jpg)



## 测试代码

```c++
#include <iostream>
//添加set头文件或者map头文件，否则_Rb_tree找不到定义
#include <set>

using namespace std;

void Test1()
{
	/*

	在Linux环境下可以正常调用
	
	_Rb_tree<int, int, _Identity<int>, less<int>> itree;
	cout << itree.empty() << endl;  //1
	cout << itree.size() << endl;   //0
	
	itree._M_insert_unique(3);
	itree._M_insert_unique(8);
	itree._M_insert_unique(5);
	itree._M_insert_unique(9);
	itree._M_insert_unique(13);
	itree._M_insert_unique(5);  //no effect, since using insert_unique().
	cout << itree.empty() << endl;  //0
	cout << itree.size() << endl;   //5
	cout << itree.count(5) << endl; //1
	
	itree._M_insert_equal(5);
	itree._M_insert_equal(5);
	cout << itree.size() << endl;   //7, since using insert_equal().
	cout << itree.count(5) << endl; //3 
	
		*/

}



int main(int argc, char *argv[])
{
	Test1();
    return 0;
}
```

## map/multimap-rbtree

### 相关概念

1. map/multimap 以 rb_tree 为底层结构，因此有**元素自动排序**特性。排序的依据是 key。
2. key 不能修改，data 可以修改。map/multimap 内部自动**将 user 指定的 key type 设为 const**，如此便能禁止 user 对 key 的赋值。

### 实现

![img](https://i.loli.net/2021/03/14/GpFLvalsge3Efth.jpg)

1. select1st<pair<const int, string>> 从 Value 中 取得 key 值的方法，即取 pair 中的第一个类型 int 作为 key。

2. map 的 iterator 就是 rb_tree 的迭代器。其中 pair 的第一个模板参数为 const int。
   

![img](https://i.loli.net/2021/03/14/xXdRhuiSv5HVOoL.jpg)

### map 独有的 operator [ ]

Allows for easy lookup with the subscript (@c[ ]) operator. Returns data asscoiated with the key specified subscript. If the key does not exist, a pair with that key is created using default values, which is then returned.
**如果 key 值不存在，则生成一个带有默认 data 值的 value安插进去**。

![img](https://i.loli.net/2021/03/14/YJ597h6yZKLIrEc.jpg)



lower_bound() 是二分查找的一种，试图在排序过的元素中寻找 value 。若查找范围内拥有与 value 相等的元素(s)，便返回一个 iterator 指向其中第一个元素。如果没有这样的元素存在，便返回“假设该元素存在是应该出现的位置”。也就是说它会返回 iterator 指向第一个不小于 value 的元素。如果 value 大于查找范围内的任何元素，将返回 last 。换句话说，lower_bound 返回的是“不破坏排序得以安插 value 的第一个适当位置”。

而 operator [ ] 最终返回的是这个位置的 .second引用，可以利用这个引用直接赋值，相当于 insert() 操作 。


## set/multiset-rbtree

### 相关概念

1 set/multiset 以 rb_tree 为底层结构，因此有元素自动排序特性。排序的依據是 key，set/multiset 的 value 就是 key。
2 set/multiset 提供遍历操作以及 iterator。元素放入后有一定的排列规则，按正常规则(++ iter)迭代器遍历时为输出为排序状态(sorted)。
3 无法使用 set/multiset 的 iterator 改变元素值（因为 key 就是 value）。其 iterator 底层实现是 RBtree 的 const iterator，禁止对元素赋值。
4 set 的元素不允许重复，所以 insert() 调用 insert_unique()。multiset 的元素可以重复，所以 insert() 调用 insert_equal()。

### 实现

![img](https://i.loli.net/2021/03/14/Y4yTlihVwgHLarN.jpg)



1 rep_type (定义了一个成员变量)说明了其底层实现为一个红黑树。其红黑树的5个模板参数都可由 set 的三个模板参数得来。
2 无法使用 set/multiset 的 iterator 改变元素值（key 就是 value），因为 set 的 iterator 是 const 不允许通过它改变元素。
3 set 的所有操作都转调用底层 t 的类方法。



![img](https://i.loli.net/2021/03/14/YjOf3lcPMKE2F6Z.jpg)



## 注意事项

map和set的迭代器类型以及相关操作的时间复杂度

双向迭代器
随机访问每个元素 O(logn)
末尾插入删除元素 O(logn)
中间或开头删插元素 O(logn)

为何map和set的插入删除效率比用其他序列容器高？

map和set中所有元素都是以节点的形式来存储，插入删除操作只涉及到指针的转换，无需像vetor和deque一样考虑内存重新申请与拷贝




# map与unpordered_map

结论：如果需要内部元素自动排序，使用map，不需要排序使用unordered_map

查找插入删除unordered_map效率高，unordered_map的内部实现是使用hash_table

map占用内存较少，查找删除效率稳定，内部元素根据key值排序，map的内部实现是使用红黑树

非频繁的查询用map比较稳定；频繁的查询用hash_map效率会高一些



使用时map的key需要定义operator<。而unordered_map需要定义hash_value函数并且重载operator==。但是很多系统内置的数据类型都自带这些，

如果是自定义类型，那么就需要自己重载operator<或者hash_value()了



hash_map其插入过程是：

1. 得到key
2. 通过hash函数得到hash值
3. 得到桶号(一般都为hash值对桶数求模)
4. 存放key和value在桶内。

 

其取值过程是:

1. 得到key
2. 通过hash函数得到hash值
3. 得到桶号(一般都为hash值对桶数求模)
4. 比较桶的内部元素是否与key相等，若都不相等，则没有找到。
5. 取出相等的记录的value。

# multimap（多重映射）

# 注意事项

不支持下标运算符

## 一般知识

允许键重复的映射，表示一对多的逻辑关系。不支持下标运算符。
根据键查找匹配的元素集合：
pair<IT, IT> equal_range (KEY const& key);
^ ^
| |
begin end
begin指向第一个和参数key匹配的元素；
end指向最后一个和参数key匹配的元素的下一个元素。
IT lower_bound (KEY const& key); // 匹配下限迭代器
IT upper_bound (KEY const& key); // 匹配上限迭代器



## 测试代码

```c++
#include <iostream>
#include <map>
using namespace std;
int main (void) {
	multimap<string, int> msi;
	msi.insert (make_pair ("张飞", 80));
	msi.insert (make_pair ("赵云", 70));
	msi.insert (make_pair ("关羽", 60));
	msi.insert (make_pair ("张飞", 50));
	msi.insert (make_pair ("赵云", 40));
	msi.insert (make_pair ("关羽", 30));
	typedef multimap<string, int>::
		iterator IT;
	for (IT it = msi.begin (); it !=
		msi.end (); ++it)
		cout << it->first << "："
			<< it->second << endl;
	cout << "--------" << endl;
	pair<IT, IT> res = msi.equal_range (
		"张飞");
	int sum = 0;
	for (IT it = res.first; it !=
		res.second; ++it)
		sum += it->second;
	cout << "张飞：" << sum << endl;
	return 0;
}
```



# map（映射）

## 注意事项

（1） 支持"下标"运算，用键做下标，得到对应的值的引用。

​            如果所给键不存在，会增加一个节点，如果value为内置类型，其值将被初始化为0；

​           																	如果value为自定义数据结构且用户定义了默认值则初始化为默认值，否则初始化为0。

​             如果键存在，直接返回对应的值

```c++
map<int,int> emptyMap{};
int i = emptyMap[100]; // i = 0
emptyMap[101]++;	//可以直接这样使用
```

（2） 只有map支持下标运算，multimap不支持下标运算

## 一般知识        

1)逻辑模型：一一对应，键(信息索引)值(信息内容)对，用于信息检索，检索性能可以对数级(O(logN))。
2)物理模型：平衡有序二叉树，又名红黑树。
5 4 3 2 1
      3 
   2     4
1          5
3)键必须是唯一的。
4)迭代过程实际上是关于键的中序遍历(L-D-R)，键升序。
5)存储单位是由键和值组成的pair。
template<typename FIRST, typename SECOND>
class pair {
public:
pair (FIRST const& f, SECOND const& s) : first (f), second (s) {}
FIRST first; // 键
SECOND second; // 值
};
映射的迭代器相当于是指向pair对象的指针。
6)映射中键都是只读的。
7)构建和修改性能较差。适用于结构稳定但是频繁检索的场合。
8)支持"下标"运算，用键做下标，得到对应的值的引用。如果所给出键不存在，会增加一个节点，返回其值，如果键存在，直接返回对应的值。

注意：只有map支持下标运算，multimap不支持下标运算

## 测试代码

```c++
#include <iostream>
#include <map>
#include <string>

using namespace std;
class Candidate {
public:
	Candidate(string const& name = "") :
		m_name(name), m_votes(0) {}
	string const& name(void) const {
		return m_name;
	}
	int votes(void) const {
		return m_votes;
	}
	void vote(void) {
		++m_votes;
	}
private:
	string m_name;
	int m_votes;
};
int main(void) {
	map<char, Candidate> mcc;
	mcc.insert(pair<char, Candidate>(
		'A', Candidate("张飞")));
	mcc.insert(make_pair(
		'B', Candidate("赵云")));
	mcc['C'] = Candidate("关羽");
	mcc['D'] = Candidate("马超");
	mcc['E'] = Candidate("黄忠");
	typedef map<char, Candidate>::
		iterator IT;
	/*
	pair<IT, bool> res = mcc.insert (
		make_pair ('B',
			Candidate ("杨健")));
	if (! res.second)
		cout << "插入失败！" << endl;
	*/
	mcc['B'] = Candidate("杨健");
	IT it = mcc.begin();
	//	it->first = 'X';
	it->second = Candidate("杨健");
	for (int i = 0; i < 10; ++i) {
		for (IT it = mcc.begin(); it !=
			mcc.end(); ++it)
			cout << '(' << it->first
			<< ')'
			<< it->second.name()
			<< ' ';
		cout << endl
			<< "请投下宝贵的一票："
			<< flush;
		char key;
		cin >> key;
		IT it = mcc.find(key);
		if (it == mcc.end()) {
			cout << "废票！" << endl;
			continue;
		}
		it->second.vote();
	}
	IT win = mcc.begin();
	for (IT it = mcc.begin(); it !=
		mcc.end(); ++it) {
		cout << it->second.name()
			<< "获得"
			<< it->second.votes()
			<< "票。" << endl;
		if (it->second.votes() >
			win->second.votes())
			win = it;
	}
	cout << "热烈祝贺"
		<< win->second.name()
		<< "成功当选首席保洁员！" << endl;
	return 0;
}
```

