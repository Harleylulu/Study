[原题链接][题目]
### 题目大意
妥妥的签到题，给出两个时间，求出它们之间的秒数差

### 解题思路
分别求出两个时间的秒数，然后相减，即可得到秒数差


### AC代码
```cpp
#include <bits/stdc++.h>
using namespace std;
 
int main(){
    int h1,m1,s1,h2,m2,s2;
    scanf("%d:%d:%d",&h1,&m1,&s1);
    scanf("%d:%d:%d",&h2,&m2,&s2);
    int sum1=h1*60*60+m1*60+s1;
    int sum2=h2*60*60+m2*60+s2;
    printf("%d",max(sum1,sum2)-min(sum1,sum2));
    return 0;
}
```

[题目]:https://ac.nowcoder.com/acm/contest/5667/D
