# 快速幂模板

```cpp

ll qsm(ll a,ll b){
    ll res=1;
    while(b){
        if(b&1) res=(res*a)%mod;
        a=(a*a)%mod;
        b>>=1;
    }
    return res;
}
```