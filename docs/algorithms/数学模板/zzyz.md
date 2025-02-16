# 找所有数最小质因子

质数为0
```cpp
int primes[N],cnt=0;
int st[N];
void init(){
    st[1]=1;
    for(int i=2;i<=N-5;i++){
        if(!st[i]){
            primes[cnt++]=i;
        }
        for(int j=0;primes[j]*i<=N-5;j++){
            st[primes[j]*i]=primes[j];
            if(i%primes[j]==0){
                break;
            }
        }
    }
}
```