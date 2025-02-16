# 链表法哈希

```cpp
int h[N],e[N],ne[N],idx;
void insert(int x){
    int k=(x%N+N)%N;
    e[idx]=x;
    ne[idx]=h[k];
    h[k]=idx++;
}
bool find(int x){
    int k=(x%N+N)%N;
    for(int i=h[k];i!=-1;i=ne[i]){
        if(e[i]==x){
            return true;
        }
    }
    return false;
}
```