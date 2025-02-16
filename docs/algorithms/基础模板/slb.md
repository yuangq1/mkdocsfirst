# 手写双链表

```cpp
int l[N],r[N],e[N];
//0->head,1->tail
void init(){
    r[0]=1;
    l[1]=0;
    idx=2;
}
void add(int k,int x){
    e[idx]=x;
    r[idx]=r[k];
    l[idx]=k;
    l[r[k]]=idx;
    r[k]=idx;
    idx++;
}
void remove(int k){
    r[l[k]]=r[k];
    l[r[k]]=l[k];
}
```