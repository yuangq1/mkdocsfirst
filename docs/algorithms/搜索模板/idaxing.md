# idea*

```cpp
#include<bits/stdc++.h>
using namespace std;
const int N=24;
int op[8][7]={
    {0,2,6,11,15,20,22},
    {1,3,8,12,17,21,23},
    {10,9,8,7,6,5,4},
    {19,18,17,16,15,14,13},
    {23,21,17,12,8,3,1},
    {22,20,15,11,6,2,0},
    {13,14,15,16,17,18,19},
    {4,5,6,7,8,9,10}
};
int opposite[8]={5,4,7,6,1,0,3,2};
int center[8]={6,7,8,11,12,15,16,17};
int q[N];
int path[100];
int f(){
    int sum[4]={0};
    for(int i=0;i<8;i++) sum[q[center[i]]]++;
    int s=0;
    for(int i=1;i<=3;i++){
        s=max(sum[i],s);
    }
    return 8-s;
}
void operate(int x){
    int t=q[op[x][0]];
    for(int i=0;i<6;i++) q[op[x][i]]=q[op[x][i+1]];
    q[op[x][6]]=t;
}
bool dfs(int depth,int max_depth,int last){
    if(depth+f()>max_depth) return false;
    if(f()==0) return true;
    for(int i=0;i<8;i++){
        if(opposite[i]!=last){
            operate(i);
            path[depth]=i;
            if(dfs(depth+1,max_depth,i)) return true;
            operate(opposite[i]);
        }
    }
    return false;
}
int main(){
    while(cin>>q[0],q[0]){
        for(int i=1;i<N;i++) cin>>q[i];
        int depth=0;
        while(!dfs(0,depth,-1)) depth++;
        if(!depth) cout<<"No moves needed";
        else{
            for(int i=0;i<depth;i++){
                cout<<char(path[i]+'A');
            }
        }
        cout<<endl<<q[6]<<endl;
    }
}
```