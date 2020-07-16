
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
