[原题链接][题目]

### 题目大意
给定字符串S，定义S<sup>∞</sup>为自身的无限次复制，如abc<sup>∞</sup>=abcabcabcabc...  
现给两个字符串，比较他们的无穷次方的字典序大小

### 解题思路
一开始，我的思路是，将这两个字符串扩充到长度一样，即为他们的最小公倍数，所以收获了俩发超时...  
正确的思路是，模拟俩个字符串的比较，将每个字符逐一比较，依次比较到他们长度的最大值的两倍即可，  
在出题人的讲题过程中，只要比较到S1+S2-gcd(S1,S2)即可

### AC代码
```cpp
#include<bits/stdc++.h>
using namespace std;

typedef long long ll;
string s1,s2;
ll gcd(ll a,ll b){
    return b==0?a:gcd(b,a%b);
}

int main()
{
    while(cin>>s1>>s2){

        ll cnt=0;
        ll len1=s1.length(),len2=s2.length();
        while(s1[cnt%len1]==s2[cnt%len2]){
            cnt++;
            if(cnt%len1==0&&cnt%len2==0)break;
        }
        
        if(s1[cnt%len1]<s2[cnt%len2])printf("<\n");
        else if(s1[cnt%len1]==s2[cnt%len2])printf("=\n");
        else printf(">\n");
    }
    return 0;
}
```

[题目]:https://ac.nowcoder.com/acm/contest/5666/F
