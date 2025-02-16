# 并查集

```cpp
int p[N];
void init(){
    for(int i=1;i<=n;i++){
        p[i]=i;
    }
    return;
}
int find(int x){//加上路径压缩
    if(p[x]!=x) p[x]=find(p[x]);
    return p[x];
}
//-------------------------------------
if(op[0]=='M') p[find(a)]=find(b);
else{
    if(find(a)==find(b)) cout<<"Yes"<<endl;
    else cout<<"No"<<endl;
}
```