# 高斯消元

```cpp
const double eps=1e-6;
int gauss(){
    int c,r;
    for(c=0,r=0;c<n;c++){
        int t=r;
        for(int i=r;i<n;i++){
            if(fabs(a[i][c])>fabs(a[t][c]))
                t=i;
        }
        if(fabs(a[t][c])<eps)
            continue;
        for(int i=c;i<=n;i++){
            swap(a[t][i],a[r][i]);
        }
        for(int i=n;i>=c;i--){
            a[r][i]/=a[r][c];
        }
        for(int i=r+1;i<n;i++){
            if(fabs(a[i][c])>eps){
                for(int j=n;j>=c;j--){
                    a[i][j]-=a[r][j]*a[i][c];
                }
            }
        }
        r++;
    }
    if(r<n){
        for(int i=r;i<n;i++){
            if(fabs(a[i][n])>eps)
                return 2;
        }
        return 1;
    }
    for(int i=n-1;i>=0;i--){
        for(int j=i+1;j<n;j++){
            a[i][n]-=a[i][j]*a[j][n];
        }
    }
    return 0;
}
```