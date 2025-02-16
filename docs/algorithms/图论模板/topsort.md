# 拓扑排序模板

```cpp
int h[N],e[N],ne[N],idx;
int q[N],d[N];//队列里同时存着拓扑序
void add(int a,int b){
    e[idx]=b,ne[idx]=h[a],h[a]=idx++;
}
bool topsort(){
    int hh=0,tt=-1;
    for(int i=1;i<=n;i++){
        if(!d[i])
            q[++tt]=i;
    }
    while(hh<=tt){
        int t=q[hh++];
        for(int i=h[t];i!=-1;i=ne[i]){
            int j=e[i];
            d[j]--;
            if(d[j]==0) q[++tt]=j;
        }
    }
    return tt==n-1;
}
```