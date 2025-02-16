# tarjan求强连通分量

强连通分量代表这一堆点任意a可以走到任意b，求完强连通分量后可以将这些点缩为一个点

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=10010,M=50010;
int n,m;
int h[N],e[M],ne[M],idx;
int dfn[N],low[N],timestamp;
int stk[N],top;
bool in_stk[N];
int id[N],scc_cnt,siz[N];
int dout[N];

void tarjan(int u){
    dfn[u] = low[u] = ++timestamp;
    stk[++top] = u,in_stk[u] = true;
    for(int i = h[u];~i;i = ne[i]){
        int j=e[i];
        if(!dfn[j]){
            tarjan(j);
            low[u] = min(low[u],low[j]);
        }
        else if(in_stk[j]){
            low[u] = min(low[u],low[j]);
        }
    }
    if(dfn[u] == low[u]){
        int y;
        ++ scc_cnt;
        do{
            y=stk[top--];
            in_stk[y] = false;
            id[y] = scc_cnt;
            siz[scc_cnt]++;
        }while(y != u);
    }
}

void add(int a,int b){
    e[idx]=b,ne[idx]=h[a],h[a]=idx++;
}
int main(){
    cin>>n>>m;
    memset(h,-1,sizeof(h));
    while(m--){
        int a,b;
        cin>>a>>b;
        add(a,b);
    }
    for(int i=1;i<=n;i++){
        if(!dfn[i]){
            tarjan(i);
        }
    }
    for(int i=1;i<=n;i++){
        for(int j=h[i];~j;j=ne[j]){
            int k= e[j];
            int a=id[i],b=id[k];
            if(a!=b) dout[a]++;
        }
    }
    int zeros=0,sum=0;
    for(int i=1;i<=scc_cnt;i++){
        if(!dout[i]){
            zeros++;
            sum+=siz[i];
            if(zeros>1){
                sum=0;
                break;
            }
        }
    }
    cout<<sum<<endl;
    return 0;
}
```