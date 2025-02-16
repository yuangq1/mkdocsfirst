# a*算法

```cpp
#include<bits/stdc++.h>
#define x first
#define y second
using namespace std;
typedef pair<int,string> PIS;
int f(string state){
    int res=0;
    for(int i=0;i<state.size();i++){
        if(state[i]!='x'){
            int t=state[i]-'1';
            res+=abs(i/3-t/3)+abs(i%3-t%3);
        }
    }
    return res;
}
string bfs(string start){
    string end="12345678x";
    unordered_map<string,int> dist;
    unordered_map<string,pair<char,string>> prev;
    priority_queue<PIS,vector<PIS>,greater<PIS>> heap;
    dist[start]=0;
    heap.push({f(start),start});
    int dx[4]={-1,0,1,0},dy[4]={0,1,0,-1};
    char op[]="urdl";
    while(heap.size()){
        auto t=heap.top();
        heap.pop();
        string state=t.y;
        if(state==end) break;
        int x,y;
        for(int i=0;i<9;i++){
            if(state[i]=='x'){
                x=i/3,y=i%3;
                break;
            }
        }
        string source=state;
        for(int i=0;i<4;i++){
            int a=x+dx[i],b=y+dy[i];
            if(a<0 || a>=3 || b<0 || b>=3) continue;
            state=source;
            swap(state[x*3+y],state[a*3+b]);
            if(dist.count(state) || dist[state]>dist[source]+1){
                dist[state]=dist[source]+1;
                prev[state]={op[i],source};
                heap.push({dist[state]+f(state),state}); 
            }
        }
    }
    string res;
    while(end!=start){
        res+=prev[end].x;
        end=prev[end].y;
    }
    reverse(res.begin(),res.end());
    return res;
}
int main(){
    string start,seq;
    char c;
    while(cin>>c){
        start+=c;
        if(c!='x') seq+=c;
    }
    int cnt=0;
    for(int i=0;i<8;i++){
        for(int j=i;j<8;j++){
            if(seq[i]>seq[j]){
                cnt++;
            }
        }
    }
    if(cnt & 1) cout<<"unsolvable";
    else cout<<bfs(start)<<endl;
    return 0;
}
```