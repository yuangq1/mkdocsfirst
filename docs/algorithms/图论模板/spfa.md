# 基础spfa

O(m)->O(nm)
```cpp
#include<bits/stdc++.h>
using namespace std;
typedef pair<int,int> PII;
const int N=110010;
int n,m;
int h[N],w[N],e[N],ne[N],idx=0;
int dist[N];
bool st[N];
void add(int a,int b,int c){
    e[idx]=b,w[idx]=c,ne[idx]=h[a],h[a]=idx++;
}
int spfa(){
    memset(dist,0x3f,sizeof(dist));
    dist[1]=0;
    queue<int> q;
    q.push(1);
    st[1]=true;
    while(q.size()){
        int t=q.front();
        q.pop();
        st[t]=false;
        for(int i=h[t];i!=-1;i=ne[i]){
            int j=e[i];
            if(dist[j]>dist[t]+w[i]){
                dist[j]=dist[t]+w[i];
                if(!st[j]){
                    q.push(j);
                    st[j]=true;
                }
            }
        }
    }
    if(dist[n]==0x3f3f3f3f) return -2147483647;
    return dist[n];
}
int main(){
    cin>>n>>m;
    memset(h,-1,sizeof(h));
    while(m--){
        int a,b,c;
        cin>>a>>b>>c;
        add(a,b,c);
    }
    int t=spfa();
    if(t==-2147483647) cout<<"impossible"<<endl;
    else cout<<t<<endl;
    return 0;
}
```