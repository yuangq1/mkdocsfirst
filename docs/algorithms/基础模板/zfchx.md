# 字符串哈希

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef unsigned long long ULL;
const int N=100010,P=131;
int n,m;
string str;
ULL h[N],p[N];
ULL get(int l,int r){
    return h[r]-h[l-1]*p[r-l+1];
}
int main(){
    cin>>n>>m>>str;
    str=' '+str;
    p[0]=1;
    for(int i=1;i<=n;i++){
        p[i]=p[i-1]*P;
        h[i]=h[i-1]*P+str[i];
    }
    while(m--){
        int l1,r1,l2,r2;
        cin>>l1>>r1>>l2>>r2;
        
        if(get(l1,r1)==get(l2,r2)) cout<<"Yes"<<endl;
        else cout<<"No"<<endl;
    }
    return 0;
}
```