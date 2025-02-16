# 基础bellman_ford

O(nm)
```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=510,M=10010;
int n,m,k;
int dist[N],bakcup[N];
struct Edge{
    int a,b,w;
}edges[M];
int bellman_ford(){
    memset(dist,0x3f,sizeof(dist));
    dist[1]=0;
    for(int i=0;i<k;i++){
        memcpy(bakcup,dist,sizeof(dist));
        for(int j=0;j<m;j++){
            int a=edges[j].a,b=edges[j].b,w=edges[j].w;
            dist[b]=min(dist[b],bakcup[a]+w);
        }
    }
    if(dist[n]>0x3f3f3f3f/2) return -2147483647;
    return dist[n];
}
int main(){
    cin>>n>>m>>k;
    for(int i=0;i<m;i++){
        int a,b,w;
        cin>>a>>b>>w;
        edges[i]={a,b,w};
    }
    int t=bellman_ford();
    if(t==-2147483647) cout<<"impossible";
    else cout<<t<<endl;
    return 0;
}
```