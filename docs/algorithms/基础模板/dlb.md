# 手写单链表

```cpp
int head,e[N],ne[N],idx;
void init(){
    head=-1;
    idx=0;
}
//将x插入头
void add_to_head(int x){
    e[idx]=x,ne[idx]=head,head=idx,idx++;
}
//将x插入k后面
void add(int k,int x){
    e[idx]=x;
    ne[idx]=ne[k];
    ne[k]=idx;
    idx++;
}
//将下标是k后面的元素删掉
void remove(int k){
    ne[k]=ne[ne[k]];
}
```