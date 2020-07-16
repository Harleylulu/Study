## F-Fake Maxpooling
[原题链接][题目]

### 题目大意
给出矩阵的行数n和列数m，矩阵 Aij = lcm( i , j ) ,求每个大小为k*k的子矩阵的最大值的和。

### 解题思路
这是一道二维矩阵上求子矩阵最大值的问题，  
如果它是一维的数列，则可以通过单调队列，求出每一个长度为k的区间的最大值，然后进行相加。  
把这题套到这种思路中，那便是，先利用单调队列求出每一行的每个长度为k的区间的最大值，  
再对已经求出的最大值，对它的列再利用单调队列求出每一列长度为k的最大值，此时即为每一个k*k矩阵的最大值  
将其求和即可得到答案。

### AC代码

``` cpp
#include<bits/stdc++.h>
using namespace std;

int N,M,K;
long long sum;
int arr[5005][5005],brr[5005][5005];
deque<int>Q;
int gcd(int a,int b);
int lcm(int a,int b);

int main()
{
    scanf("%d%d%d",&N,&M,&K);
    for(int i=1;i<=N;i++)
        for(int j=1;j<=M;j++){
            arr[i][j]=lcm(i,j);
            sum+=arr[i][j];
        }
    if(K==1){
        printf("%lld",sum);
        return 0;
    }
    
    for(int i=1;i<=N;i++){
        Q.clear();
        for(int j=1;j<K;j++){
            while(!Q.empty()&&arr[i][Q.back()]<arr[i][j]) Q.pop_back();
            Q.push_back(j);
        }
        for(int j=K;j<=M;j++){
            while(!Q.empty()&&Q.front()<=j-K) Q.pop_front();
            while(!Q.empty()&&arr[i][Q.back()]<arr[i][j]) Q.pop_back();
            Q.push_back(j);
            brr[i][j]=max(brr[i][j],arr[i][Q.front()]);
        }
    }
    
    long long ans=0;
    for(int j=K;j<=M;j++){
        Q.clear();
        for(int i=1;i<K;i++){
            while(!Q.empty()&&brr[Q.back()][j]<brr[i][j])Q.pop_back();
            Q.push_back(i);
        }
        for(int i=K;i<=N;i++){
            while(!Q.empty()&&Q.front()<=i-K) Q.pop_front();
            while(!Q.empty()&&brr[Q.back()][j]<brr[i][j])Q.pop_back();
            Q.push_back(i);
            ans+=max(brr[i][j],brr[Q.front()][j]);
        }
    }
    
    printf("%lld",ans);
    return 0;
}

int gcd(int a,int b)
{
    return b==0?a:gcd(b,a%b);
}

int lcm(int a,int b)
{
    return a*b/gcd(a,b);
}
```

[题目]:https://ac.nowcoder.com/acm/contest/5667/F
