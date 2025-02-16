# stl库

```cpp
vector
    vector<int> a(10,3);//定义一个长度为10的vector，其每个元素都是3
    a.size(),a.empty();//时间复杂度 O(1)
    a.clear()
    a.front()//返回第一个数 
    a.back()//返回最后一个数
    a.push_back(),a.pop_back();
    a.begin(),a.back()//返回头尾指针
    vector支持比较操作，按字典序排序
pair<int,string>
    first //第一个元素
    second //第二个元素
    支持比较操作，first第一关键字，second第二关键字
    p={20,"abc"};
string
    string a="abc";
	a+="def";
	a+="c";
	a.substr(1,2);//i下标开始，共返回两个字符，省略第二个数，则是从i开始输出完
	a.c_str()//存储字符数组的起始地
queue
   	size(),empty(),push(),front(),pop(),back();
priority_queue
    push(),top(),pop();
stack
    push(),top(),pop();
deque//双端队列
    size(),empty(),clear(),front(),back(),push_back(),pop_back(),push_front(),
	pop_front()
set,map,multiset,multimap
  	size(),empty(),clear()
        
    set/multiset
    	insert()
        find()
        count()
        erase()//输入一个数x，删除所有x或者输入一个迭代器，删除这个迭代器
        lower_bound()/upper_bound()
        	lower_bound//返回大于等于x的最小的迭代器
        	upper_bound//返回大于x的最小的迭代器
    map/multimap
        insert()
        erase()
        find()
        lower_bound()/upper_bound()
unordered_set,unordered_map,unordered_multiset,unordered_multimap
    和上面操作类似，增删改查操作复杂度为O(1)
    不支持lower_bound()/upper_bound()
bitset,压位
	bitset<10000> s;
	~ & | ^
    >>, <<
    ==, !=
    []
    count() 返回有多少个1
    any()//返回是否至少有一个1
    none()//返回是否全为空
    set()//把所有位置成1
    set(k,v)//将第k位变成v
    reset()//把所有位变成0
    flip()//把所有位取反，等价于~
    flip(k)//第k位取反
```