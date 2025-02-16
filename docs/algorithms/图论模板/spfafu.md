# spfa 判断负环

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef pair<int,int> PII;
const int N=110010;
int n,m;
int h[N],w[N],e[N],ne[N],idx=0;
int dist[N],cnt[N];
bool st[N];
void add(int a,int b,int c){
    e[idx]=b,w[idx]=c,ne[idx]=h[a],h[a]=idx++;
}
int spfa(){
    queue<int> q;
    for(int i=1;i<=n;i++){
        st[i]=true;
        q.push(i);
    }
    while(q.size()){
        int t=q.front();
        q.pop();
        st[t]=false;
        for(int i=h[t];i!=-1;i=ne[i]){
            int j=e[i];
            if(dist[j]>dist[t]+w[i]){
                dist[j]=dist[t]+w[i];
                cnt[j]=cnt[t]+1;
                if(cnt[t]>=n) return true;
                if(!st[j]){
                    q.push(j);
                    st[j]=true;
                }
            }
        }
    }
    return false;
}
int main(){
    cin>>n>>m;
    memset(h,-1,sizeof(h));
    while(m--){
        int a,b,c;
        cin>>a>>b>>c;
        add(a,b,c);
    }
    if(spfa()) cout<<"Yes"<<endl;
    else cout<<"No"<<endl;
    return 0;
}
```