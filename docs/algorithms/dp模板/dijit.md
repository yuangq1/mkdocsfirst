# 数位dp

```cpp
#include<bits/stdc++.h>
using namespace std;
typedef long long ll;
const int N=20,p=1e9+7;
struct F{
    ll s0,s1,s2;
}f[N][10][7][7];
int power7[N],power9[N];
int mod(ll x,int y){
    return (x%y+y)%y;
}
void init(){
    for(int i=0;i<=9;i++){
        if(i==7) continue;
        auto &v=f[1][i][i%7][i%7];
        v.s0++;
        v.s1+=i;
        v.s2+=i*i;
    }
    ll power=10;
    for(int i=2;i<N;i++,power*=10){
        for(int j=0;j<=9;j++){
            if(j==7) continue;
            for(int a=0;a<7;a++){
                for(int b=0;b<7;b++){
                    for(int k=0;k<=9;k++){
                        if(k==7) continue;
                        auto &v1=f[i][j][a][b],&v2=f[i-1][k][mod(a-j*power%7,7)][mod(b-j,7)];
                        v1.s0=(v1.s0+v2.s0)%p;
                        v1.s1=(v1.s1+j*(power%p)%p*v2.s0+v2.s1)%p;
                        v1.s2=(v1.s2+j*j*(power%p)%p*(power%p)%p*v2.s0%p + 2*j*(power%p)%p*v2.s1%p + v2.s2)%p;
                    }
                }
            }
        }
    }
    power7[0]=power9[0]=1;
    for(int i=1;i<N;i++){
        power7[i]=power7[i-1]*10%7;
        power9[i]=(ll)power9[i-1]*10%p;
    }
}
F get(int i,int j,int a,int b){
    int s0=0,s1=0,s2=0;
    for(int x=0;x<7;x++){
        for(int y=0;y<7;y++){
            if(x==a || y==b) continue;
            auto v=f[i][j][x][y];
            s0=(s0+v.s0)%p;
            s1=(s1+v.s1)%p;
            s2=(s2+v.s2)%p;
        }
    }
    return {s0,s1,s2};
}
int dp(ll n){
    if(!n) return 0;
    ll backup_n=n%p;
    vector<int> nums;
    while(n) nums.push_back(n%10),n/=10;
    int res=0;
    ll last_a=0,last_b=0;
    for(int i=nums.size()-1;i>=0;i--){
        int x=nums[i];
        for(int j=0;j<x;j++){
            if(j==7) continue;
            int a=mod(-last_a*power7[i+1],7);
            int b=mod(-last_b,7);
            auto v=get(i+1,j,a,b);
            res=(res + (last_a%p)*(last_a%p)%p*power9[i+1]%p*power9[i+1]%p*v.s0%p + 2*(last_a%p)%p*power9[i+1]%p*v.s1 + v.s2)%p;
        }
        if(x==7) break;
        last_a=last_a*10+x;
        last_b+=x;
        if(!i && last_a%7 && last_b%7) res=(res+backup_n*backup_n)%p;
    }
    return res;
}
int main(){
    init();
    int T;
    cin>>T;
    while(T--){
        ll l,r;
        cin>>l>>r;
        cout<<mod(dp(r)-dp(l-1),p)<<endl;
    }
    return 0;
}
```