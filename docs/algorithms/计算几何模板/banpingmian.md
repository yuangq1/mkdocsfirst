# 半平面交

```cpp
#include <bits/stdc++.h>
using namespace std;
#define x first 
#define y second
typedef pair<double,double> PDD;
const int N=510;
const double eps=1e-8;
int cnt;
struct Line{
    PDD st,ed;
}line[N];
int q[N];
PDD pg[N],ans[N];
PDD operator- (PDD a,PDD b){
    return {a.x-b.x,a.y-b.y};
}
int sign(double x){
    if(fabs(x)<eps) return 0;
    if(x<0) return -1;
    return 1;
}
int dcmp(double x,double y){
    if(fabs(x-y)<eps) return 0;
    if(x<y) return -1;
    return 1;
}
double get_angle(const Line &a){
    return atan2(a.ed.y-a.st.y,a.ed.x-a.st.x);
}
double cross(PDD a,PDD b){
    return a.x*b.y-a.y*b.x;
}
double area(PDD a,PDD b,PDD c){
    return cross(b-a,c-a);
}
bool cmp(const Line& a,const Line& b){
    double A=get_angle(a),B=get_angle(b);
    if(!dcmp(A,B)) return area(a.st,a.ed,b.ed)<0;
    return A<B;
}
PDD get_line_intersection(PDD p,PDD v,PDD q,PDD w){
    auto u=p-q;
    double t=cross(w,u)/cross(v,w);
    return {p.x+v.x*t,p.y+v.y*t};
}
PDD get_line_intersection(Line a,Line b){
    return get_line_intersection(a.st,a.ed-a.st,b.st,b.ed-b.st);
}
bool on_right(Line &a,Line &b,Line &c){
    auto o=get_line_intersection(b,c);
    return sign(area(a.st,a.ed,o))<=0;
}
double half_plane_intersection(){
    sort(line,line+cnt,cmp);
    int hh=0,tt=-1;
    for(int i=0;i<cnt;i++){
        if(i && !dcmp(get_angle(line[i]),get_angle(line[i-1]))) continue;
        while(hh+1<=tt && on_right(line[i],line[q[tt-1]],line[q[tt]])) tt--;
        while(hh+1<=tt && on_right(line[i],line[q[hh]],line[q[hh+1]])) hh++;
        q[++tt]=i;
    }
    while(hh+1<=tt && on_right(line[q[hh]],line[q[tt-1]],line[q[tt]])) tt--;
    while(hh+1<=tt && on_right(line[q[tt]],line[q[hh]],line[q[hh+1]])) hh++;
    q[++tt]=q[hh];
    
    int k=0;
    for(int i=hh;i<tt;i++){
        ans[k++]=get_line_intersection(line[q[i]],line[q[i+1]]);
    }
    double res=0;
    for(int i=1;i+1<k;i++){
        res+=area(ans[0],ans[i],ans[i+1]);
    }
    return res/2;
}
int main(){
    int n,m;
    cin>>n;
    while(n--){
        cin>>m;
        for(int i=0;i<m;i++) cin>>pg[i].x>>pg[i].y;
        for(int i=0;i<m;i++){
            line[cnt++]={pg[i],pg[(i+1)%m]};
        }
    }
    double res=half_plane_intersection();
    printf("%.3lf\n",res);
    return 0;
}
```