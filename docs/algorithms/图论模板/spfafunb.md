# spfa判负环优化

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=700,M=100010;
int n;
int h[N],e[M],w[M],ne[M],idx;
double dist[N];
int q[N],cnt[N];
bool st[N];
void add(int a,int b,int c){
    e[idx]=b,w[idx]=c,ne[idx]=h[a],h[a]=idx++;
}
bool check(double mid){
    memset(st,0,sizeof(st));
    memset(cnt,0,sizeof(cnt));
    memset(dist,0,sizeof(dist));
    int hh=0,tt=0;
    for(int i=0;i<676;i++){
        q[tt++]=i;
        st[i]=true;
    }
    int count=0;
    while(hh!=tt){
        int t=q[--tt];
        st[t]=false;
        for(int i=h[t];~i;i=ne[i]){
            int j=e[i];
            if(dist[j]<dist[t]+w[i]-mid){
                dist[j]=dist[t]+w[i]-mid;
                cnt[j]=cnt[t]+1;
                if(cnt[j]>=N) return true;
                if(!st[j]){
                    q[tt++]=j;
                    st[j]=true;
                }
            }
        }
    }
    return false;
}
int main(){
    char str[1010];
    while(cin>>n,n){
        memset(h,-1,sizeof(h));
        idx=0;
        for(int i=0;i<n;i++){
            cin>>str;
            int len=strlen(str);
            if(len>=2){
                int left=(str[0]-'a')*26+str[1]-'a';
                int right=(str[len-2]-'a')*26+str[len-1]-'a';
                add(left,right,len);
            }
        }
        if(!check(0)) cout<<"No solution"<<endl;
        else{
            double l=0,r=1000;
            while(r-l>1e-4){
                double mid=(l+r)/2;
                if(check(mid)) l=mid;
                else r=mid;
            }
            printf("%.2lf\n",l);
        }
    }
    return 0;
}
```