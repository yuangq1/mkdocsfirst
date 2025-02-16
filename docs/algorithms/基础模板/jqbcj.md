# 加权并查集

```cpp
int p[N],sizes[N];
void init(){
    for(int i=1;i<=n;i++){
        p[i]=i;
        sizes[i]=1;
    }
    return;
}
int find(int x){//加上路径压缩
    if(p[x]!=x) p[x]=find(p[x]);
    return p[x];
}
//---------------------------
cin>>op;
if(op[0]=='C'){
    cin>>a>>b;
    if(find(a)==find(b)) continue;
    sizes[find(b)]+=sizes[find(a)];
    p[find(a)]=find(b);
}
else if(op[1]=='1'){
    cin>>a>>b;
    if(find(a)==find(b)) cout<<"Yes"<<endl;
    else cout<<"No"<<endl;
}
else{
    cin>>a;
    cout<<sizes[find(a)]<<endl;
}
```