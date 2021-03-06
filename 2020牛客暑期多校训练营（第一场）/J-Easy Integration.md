## J-Easy Integration
[原题链接][题目]

### 题目大意
这是一道数学题，求积分  
![积分](https://github.com/Harleylulu/Study/blob/master/picture/CodeCogsEqn.gif)
对于给定的N，给出这道积分的答案。

### 解题思路
在长时间都没有解出这道积分的情况下，我选择了在OEIS上查询这个序列，直接得出它的解析式，首先先求出当N=1、2、3时，该定积分的结果为

```cpp
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
const ll MOD = 998244353;
int N;
ll arr[2000005];
ll fastpow(ll a,ll b);

int main()
{
    arr[0]=1;
    for(int i=1;i<=2000005;i++){
        arr[i]=i*arr[i-1]%MOD;
    }
    while(~scanf("%d",&N)){
        ll p=arr[N]*arr[N]%MOD;
        ll q=arr[2*N+1]%MOD;
        printf("%lld\n",p*fastpow(q,MOD-2)%MOD);
    }
    return 0;
}

ll fastpow(ll a,ll b)
{
    ll res=1;
    ll base=a;
    while(b){
        if(b&1)res=res*base%MOD;
        base=base*base%MOD;
        b>>=1;
    }
    return res;
}
```

[题目]:https://ac.nowcoder.com/acm/contest/5666/J
