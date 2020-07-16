# F-Fake Maxpooling
[原题链接][题目]

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

[题目]:https://ac.nowcoder.com/acm/contest/5667/F
