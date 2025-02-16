# 线性筛

```cpp
int primes[N],cnt;
bool sg[N];
for(int i=2;i<=n;i++){
    if(!sg[i]) primes[cnt++]=i;
    for(int j=0;primes[j]*i<=n;j++){
        sg[primes[j]*i]=true;
    }
}
```