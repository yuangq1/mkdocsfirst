# 约瑟夫问题

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
void solve(){
    ll n,m,k;
    cin>>n>>m>>k;
    if(m<=k){
        ll f;
        f=k%(n-m+1);
        if(f==0) f=n-m+1;
        for(ll i=2;i<=m;i++){
            f=(f+k)%(n-m+i);
        }
        cout<<f;
    }
    else{
        if(k==1) cout<<m,return;
        ll a=n-m+1,b=1;
        ll f=k%a,x=0;
        if(f==0) f=a;
        while(b+x<=m){
            a+=x,b+=x,f+=k*x;
            f%=a;
            if(f==0) f=a;
            x=(a-f)/(k-1)+1;
        }
        f+=(m-b)*k;
        f%=n;
        if(f==0) f=n;
        cout<<f;
    }
}
int main(){
    int T;
    cin>>T;
    for(int _=1;_<=T;_++){
        cout<<"Case #"<<_<<": ";
        solve();
        cout<<endl;
    }
    return 0;
}
```