# 线性求欧拉函数

```cpp
int primes[N],cnt;
bool st[N];
int phi[N];
phi[1]=1;
for(int i=2;i<=n;i++){
    if(!st[i]){
        primes[cnt++]=i;
        phi[i]=i-1;
    }
    for(int j=0;primes[j]*i<=n;j++){
        st[primes[j]*i]=1;
        if(i%primes[j]==0){
            phi[i*primes[j]]=phi[i]*primes[j];
            break;
        }
        phi[i*primes[j]]=phi[i]*(primes[j]-1);
    }
}
```