[原题链接][题目]
### 题目大意
给了n个点，让你自己随便定义圆心(圆心不要求是n个点的其中一个)和半径，要求这n个点有尽可能多的点在圆上，并且该圆经过坐标原点(0,0)。求满足的圆上的点最多有多少个。
  
### 解题思路
在本题中，N的范围在2000以内，所以时间复杂度应小于O(n<sup>3</sup>)内。  
我们知道，三个点可以确定一个圆，其中一个点(0,0)已经确定，则可以枚举其他的俩个点，求出他们的圆心，  
则可以根据最多的圆心的数量，来求出该圆心经过多少个点，即可确定答案。  
一开始我使用map<pair<double,double>,int>mp来存储圆心的数量，只能通过70%的数据  
则需要进行优化，采用数据结构vector<pair<double,double>>mp，再将其排序，选出其中最多的那个圆心  
当mp的size()==0的时候，即无法用三个点确定一个圆，或者所有的点都共线，则输出答案“1”  
记圆心最多的数量为sum，则经过的点的数量与sum的关系为p*(p-1)/2=sum,即可求出答案p。

### AC代码
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

