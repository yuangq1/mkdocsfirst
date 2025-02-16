# 斜率优化dp

```cpp
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
#include <ext/pb_ds/hash_policy.hpp>
#include <ext/pb_ds/priority_queue.hpp>
using namespace std;
using namespace __gnu_pbds;
using ordered_multiset=tree<int,null_type,less_equal<int>,
rb_tree_tag,tree_order_statistics_node_update>;
typedef long long ll;
const int N=3e5+10;
int n,s;
ll t[N],c[N];
ll f[N];
ll q[N];
void solve(){
    cin>>n>>s;
    for(int i=1;i<=n;i++){
        cin>>t[i]>>c[i];
        t[i]=t[i]+t[i-1];
        c[i]=c[i]+c[i-1];
        f[i]=1e18;
    }
    int hh=0,tt=0;
    q[0]=0;
    for(int i=1;i<=n;i++){
        while(hh<tt && (f[q[hh+1]]-f[q[hh]])<=(t[i]+s)*(c[q[hh+1]]-c[q[hh]])) hh++;
        int j=q[hh];
        f[i]=f[j]-(t[i]+s)*c[j]+t[i]*c[i]+s*c[n];
        while(hh<tt && (f[q[tt]]-f[q[tt-1]])*(c[i]-c[q[tt]])>=(f[i]-f[q[tt]])*(c[q[tt]]-c[q[tt-1]]));
        q[++tt]=i;
    }
    cout<<f[n];
}
int main(){
    int T=1;

    while(T--){
        solve();
    }
    

    return 0;
}
```