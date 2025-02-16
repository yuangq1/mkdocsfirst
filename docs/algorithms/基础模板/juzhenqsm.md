# 矩阵快速幂

```cpp
int g[N][N];
int res[N][N];
void mul(int c[][N],int a[][N],int b[][N]){
    static int temp[N][N];
    memset(temp,0x3f,sizeof(temp));
    for(int k=1;k<=n;k++){
        for(int i=1;i<=n;i++){
            for(int j=1;j<=n;j++){
                temp[i][j]=min(temp[i][j],a[i][k]+b[k][j]);
            }
        }
    }
    memcpy(c,temp,sizeof(temp));
}
void qmi(){
    memset(res,0x3f,sizeof(res));
    for(int i=1;i<=n;i++){
        res[i][i]=0;
    }
    while(k){
        if(k&1) mul(res,res,g);
        mul(g,g,g);
        k>>=1;
    }
}
```