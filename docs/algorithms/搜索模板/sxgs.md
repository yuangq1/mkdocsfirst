# 双向广搜

```cpp
#include <bits/stdc++.h>
#include <ext/pb_ds/assoc_container.hpp>
#include <ext/pb_ds/tree_policy.hpp>
#include <ext/pb_ds/hash_policy.hpp>
#include <ext/pb_ds/priority_queue.hpp>
using namespace std;
using namespace __gnu_pbds;
using ordered_multiset=tree<int,null_type,less_equal<int>,
rb_tree_tag,tree_order_statistics_node_update>;
typedef long long ll;
const int N=6;
string a[N],b[N];
int n;
int extend(queue<string>& q,unordered_map<string,int>& da,unordered_map<string,int>& db,string a[],string b[]){
    int d=da[q.front()];
    while(q.size() && da[q.front()]==d){
        auto t=q.front();
        q.pop();
        for(int i=0;i<t.size();i++){
            for(int j=0;j<n;j++){
                if(t.substr(i,a[j].size())==a[j]){
                    string state=t.substr(0,i)+b[j]+t.substr(i+a[j].size());
                    if(db.count(state)) return da[t]+1+db[state];
                    if(da.count(state)) continue;
                    da[state]=da[t]+1;
                    q.push(state);
                }
            }
        }
    }
    return 11;
}
int bfs(string A,string B){
    if(A==B) return 0;
    queue<string> qa,qb;
    unordered_map<string,int> da,db;
    qa.push(A),da[A]=0;
    qb.push(B),db[B]=0;
    int step=0;
    while(qa.size() && qb.size()){
        int t;
        if(qa.size()<=qb.size()){
            t=extend(qa,da,db,a,b);
        }
        else{
            t=extend(qb,db,da,b,a);
        }
        if(t<=10) return t;
        if(++step==10) return -1;
    }
    return -1;
}
void solve(){
    string A,B;
    cin>>A>>B;
    while(cin>>a[n]>>b[n]) n++;
    int step=bfs(A,B);
    if(step==-1) cout<<"NO ANSWER!"<<endl;
    else cout<<step<<endl;
}
int main(){
    int T=1;
    while(T--){
        solve();
    }
    

    return 0;
}
```