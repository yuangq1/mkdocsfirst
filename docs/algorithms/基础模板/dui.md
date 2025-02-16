# 手写堆和带映射的堆

```cpp
//手写堆
int n,m;
int h[N],sizes;
void down(int u){
    int t=u;
    if(u*2<=sizes && h[u*2]<h[t]) t=u*2;
    if(u*2+1<=sizes && h[u*2+1]<h[t]) t=u*2+1;
    if(u!=t){
        swap(h[u],h[t]);
        down(t);
    }
    return;
}
void up(int u){
    while(u/2 && h[u/2]>h[u]){
        swap(h[u/2],h[u]);
        u=u/2;
    }
    return;
}
//---------------------------------------
sizes=n;
for(int i=n/2;i>0;i--){
    down(i);
}
while(m--){
    cout<<h[1]<<" ";
    h[1]=h[sizes];
    sizes--;
    down(1);
}

//手写带映射的堆
#include<bits/stdc++.h>
using namespace std;
const int N=1e5+10;
int n,m;
int ph[N],hp[N];
int h[N],sizes;
void heap_swap(int a,int b){
    swap(ph[hp[a]],ph[hp[b]]);
    swap(hp[a],hp[b]);
    swap(h[a],h[b]);
}
void down(int u){
    int t=u;
    if(u*2<=sizes && h[u*2]<h[t]) t=u*2;
    if(u*2+1<=sizes && h[u*2+1]<h[t]) t=u*2+1;
    if(u!=t){
        heap_swap(u,t);
        down(t);
    }
    return;
}
void up(int u){
    while(u/2 && h[u/2]>h[u]){
        heap_swap(u/2,u);
        u=u/2;
    }
    return;
}
int main(){
    cin>>n;
    while(n--){
        char op[10];
        int k,x;
        cin>>op;
        if(op[0]=='I'){
            cin>>x;
            sizes++;
            m++;
            ph[m]=sizes,hp[sizes]=m;
            h[sizes]=x;
            up(sizes);
        }
        else if(op[0]=='P'){
            cout<<h[1]<<endl;
        }
        else if(op[1]=='M'){
            heap_swap(1,sizes);
            sizes--;
            down(1);
        }
        else if(op[0]=='D'){
            cin>>k;
            k=hp[k];
            heap_swap(k,sizes);
            sizes--;
            down(k),up(k);
        }
        else{
            cin>>k>>x;
            k=ph[k];
            h[k]=x;
            down(k),up(k);
        }
    }
    return 0;
}
```