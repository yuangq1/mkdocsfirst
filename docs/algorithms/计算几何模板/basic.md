# 计算几何基本操作

```cpp
#define x first
#define y second
typedef pair<double,double> PDD;
const double eps=1e-8;
const double pi=acos(-1);
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
double get_angle(PDD a,PDD b){//求角度
    return acos((a&b)/get_len(a)/get_len(b));
}
double area(PDD a,PDD b,PDD c){//求面积
    return (b-a)*(c-a);
}
double get_len(PDD a){//求长度
    return sqrt(a&a);
}
double get_dist(PDD a,PDD b){//求距离
    return get_len(b-a);
}
double project(PDD a,PDD b,PDD c){//计算点c到ab的投影长度
    return ((c-a)&(b-a))/get_len(b-a);
}
PDD rotate(PDD a,double b){//旋转
    return {a.x*cos(b)+a.y*sin(b),-a.x*sin(b)+a.y*cos(b)};
}
PDD norm(PDD a){//单位线段
    return a/get_len(a);
}
PDD get_line_intersection(PDD p,PDD v,PDD q,PDD w){//两线焦点
    auto u=p-q;
    auto t=w*u/(v*w);
    return p+v*t;
}
double distance_to_line(PDD p,PDD a,PDD b){//点到直线距离
    PDD v1=b-a,v2=p-a;
    return fabs((v1*v2)/get_len(v1));
}
double distance_to_segment(PDD p,PDD a,PDD b){//点到线段距离
    if(a==b){
        return get_len(p-a);
    }
    PDD v1=b-a,v2=p-a,v3=p-b;
    if(sign(v1&v2)<0) return get_len(v2);
    if(sign(v1&v3)<0) return get_len(v3);
    return distance_to_line(p,a,b);
}
bool on_segment(PDD p,PDD a,PDD b){//判断点是不是在线上
    return !sign((p-a)*(p-b)) && sign((p-a)&(p-b))<=0;
}
double get_circle_line_intersection(PDD a,PDD b,PDD &pa,PDD &pb){//求直线和圆的交点
    auto e=get_line_intersection(a,b-a,r,rotate(b-a,pi/2));
    auto mind=get_dist(r,e);
    if(!on_segment(e,a,b)) mind=min(get_dist(r,a),get_dist(r,b));
    if(dcmp(R,mind)<=0) return mind;
    auto len=sqrt(R*R-get_dist(r,e)*get_dist(r,e));
    pa=e+norm(a-b)*len;
    pb=e+norm(b-a)*len;
    return mind;
}
double get_sector(PDD a,PDD b){//求扇形面积
    auto angle=acos((a&b)/get_len(a)/get_len(b));
    if(sign(a*b)<0) angle=-angle;
    return R*R*angle/2;
}
```