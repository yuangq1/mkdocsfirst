# 初始化模板

```cpp
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
#include <ext/pb_ds/hash_policy.hpp>
#include <ext/pb_ds/priority_queue.hpp>
using namespace std;
using namespace __gnu_pbds;
template <typename T>
using ordered_multiset=tree<T,null_type,less_equal<T>,
//less<int>表升序，greater<int>表降序
rb_tree_tag,tree_order_statistics_node_update>;//平衡树
typedef long long ll;
void solve(){
    
}
int main(){
    int T;
    cin>>T;
    while(T--){
        solve();
    }

    return 0;
}
```
