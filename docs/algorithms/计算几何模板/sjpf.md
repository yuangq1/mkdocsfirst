# 三角剖分

```cpp
#include<bits/stdc++.h>
#define x first
#define y second
using namespace std;
typedef pair<double,double> PDD;
const double eps=1e-8;
const double pi=acos(-1);
const int N=55;
double R;
int n;
PDD q[N],r;
int sign(double x){
    if(fabs(x)<eps){
        return 0;
    }
    if(x<0) return -1;
    else return 1;
}
int dcmp(double x,double y){
    if(fabs(x-y)<eps) return 0;
    if(x<y) return -1;
    else return 1;
}
PDD operator+ (PDD a,PDD b){
    return {a.x+b.x,a.y+b.y};
}
PDD operator- (PDD a,PDD b){
    return {a.x-b.x,a.y-b.y};
}
PDD operator* (PDD a,double t){
    return {a.x*t,a.y*t};
}
PDD operator/ (PDD a,double t){
    return {a.x/t,a.y/t};
}
double operator*(PDD a,PDD b){
    return a.x*b.y-a.y*b.x;
}
double operator& (PDD a,PDD b){
    return a.x*b.x+a.y*b.y;
}
double area(PDD a,PDD b,PDD c){
    return (b-a)*(c-a);
}
double get_len(PDD a){
    return sqrt(a&a);
}
double get_dist(PDD a,PDD b){
    return get_len(b-a);
}
double project(PDD a,PDD b,PDD c){
    return ((c-a)&(b-a))/get_len(b-a);
}
PDD rotate(PDD a,double b){
    return {a.x*cos(b)+a.y*sin(b),-a.x*sin(b)+a.y*cos(b)};
}
PDD norm(PDD a){
    return a/get_len(a);
}
PDD get_line_intersection(PDD p,PDD v,PDD q,PDD w){
    auto u=p-q;
    auto t=w*u/(v*w);
    return p+v*t;
}
bool on_segment(PDD p,PDD a,PDD b){
    return !sign((p-a)*(p-b)) && sign((p-a)&(p-b))<=0;
}
double get_circle_line_intersection(PDD a,PDD b,PDD &pa,PDD &pb){
    auto e=get_line_intersection(a,b-a,r,rotate(b-a,pi/2));
    auto mind=get_dist(r,e);
    if(!on_segment(e,a,b)) mind=min(get_dist(r,a),get_dist(r,b));
    if(dcmp(R,mind)<=0) return mind;
    auto len=sqrt(R*R-get_dist(r,e)*get_dist(r,e));
    pa=e+norm(a-b)*len;
    pb=e+norm(b-a)*len;
    return mind;
}
double get_sector(PDD a,PDD b){
    auto angle=acos((a&b)/get_len(a)/get_len(b));
    if(sign(a*b)<0) angle=-angle;
    return R*R*angle/2;
}
double get_circle_triangle_ares(PDD a,PDD b){
    auto da=get_dist(r,a),db=get_dist(r,b);
    if(dcmp(R,da)>=0 && dcmp(R,db)>=0) return a*b/2;
    if(!sign(a*b)) return 0;
    PDD pa,pb;
    auto mind=get_circle_line_intersection(a,b,pa,pb);
    if(dcmp(R,mind)<=0) return get_sector(a,b);
    if(dcmp(R,da)>=0) return get_sector(pb,b)+a*pb/2;
    if(dcmp(R,db)>=0) return get_sector(a,pa)+pa*b/2;
    return get_sector(a,pa)+pa*pb/2+get_sector(pb,b);
}
double work(){
    double res=0;
    for(int i=0;i<n;i++){
        res+=get_circle_triangle_ares(q[i],q[(i+1)%n]);
    }
    return fabs(res);
}
int main(){
    while(cin>>R>>n){
        for(int i=0;i<n;i++){
            cin>>q[i].x>>q[i].y;
        }
        printf("%.2lf\n",work());
    }
    return 0;
}
```