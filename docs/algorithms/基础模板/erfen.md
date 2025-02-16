# 二分搜索模板

```cpp
//找最后一个满足条件的元素
while(ll<rr){
	int mid=(ll+rr+1)/2;
	if(chk(mid)){
		ll=mid;
	}
	else{
		rr=mid-1;
    }
}
//找第一个满足条件的元素
while(ll<rr){
	int mid=(ll+rr)/2;
	if(chk(mid)){
		rr=mid;
	}
	else{s
		ll=mid+1;
    }
}
```