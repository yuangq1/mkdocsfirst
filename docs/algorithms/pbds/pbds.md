# pbds用法

```cpp
gp_hash_table<int,int> hash_table;
//与unordered_map类似

ordered_multiset st;
st.order_of_key(val) //小于val数的数量
st.lower_bound(val) //第一个大于等于val的数的指针
st.upper_bound(val) //第一个大于val的数的指针
st.insert(val)//插入元素
st.erase(st.lower_bound(val))//删除元素
st.find_by_order(k)//找到第k+1小的元素的指针
//less处改成less_equal可以插入相同元素，使用后upper_bound和lower_bound功能互换
```
