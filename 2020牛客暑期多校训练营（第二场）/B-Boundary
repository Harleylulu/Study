[原题链接][题目]

```cpp
#include<bits/stdc++.h>
using namespace std;

struct Point{
    int x,y;
}arr[2005];
int N,res=1,ans=1;
double X,Y;
void solve(Point a, Point b, Point c);
vector<pair<double,double>>mp;

int main()
{
    scanf("%d",&N);
    for(int i=1;i<=N;i++)
        scanf("%d%d",&arr[i].x,&arr[i].y);
    for(int i=1;i<N;i++){
        for(int j=i+1;j<=N;j++){
            solve({0,0},arr[i],arr[j]);
            if (X == Y && fabs(X - 1e18) < 1e-8) continue;
            else mp.push_back({X,Y});
        }
    }
    if(mp.size()==0){
        printf("1");
        return 0;
    }
    
    sort(mp.begin(),mp.end());
    pair<double,double>now=mp[0];
    for(int i=1;i<mp.size();i++){
        if(now==mp[i]) res++;
        else{
            ans=max(res,ans);
            res=1;
            now=mp[i];
        }
        ans=max(res,ans);
    }
    
    
    for(int i=1;i<=N;i++){
        if(i*(i-1)/2==ans){
            printf("%d",i);
            return 0;
        }
    }
}

void solve(Point a, Point b, Point c)
{
    double fm1=2 * (a.y - c.y) * (a.x - b.x) - 2 * (a.y - b.y) * (a.x - c.x);
    double fm2=2 * (a.y - b.y) * (a.x - c.x) - 2 * (a.y - c.y) * (a.x - b.x);
 
    if (fm1 == 0 || fm2 == 0)
    {
        X = Y = 1e18;
        return;
    }
    double fz1=a.x * a.x - b.x * b.x + a.y * a.y - b.y * b.y;
    double fz2=a.x * a.x - c.x * c.x + a.y * a.y - c.y * c.y;
    X = (fz1 * (a.y - c.y) - fz2 * (a.y - b.y)) / fm1;
    Y = (fz1 * (a.x - c.x) - fz2 * (a.x - b.x)) / fm2;
}
```

[题目]:https://ac.nowcoder.com/acm/contest/5667/B

