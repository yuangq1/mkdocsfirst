# 矩阵乘法
```cpp
void mul(int c[][N],int a[][N],int b[][N]){
    int t[N][N];
    memset(t,0,sizeof(t));
    for(int i=0;i<m;i++){
        for(int j=0;j<m;j++){
            for(int k=0;k<m;k++){
                t[i][j]=(t[i][j]+a[i][k]*b[k][j])%mod;
            }
        }
    }
    memcpy(c,t,sizeof(t));
}
```