[原题链接][题目]

### 题目大意
给定一棵无根树，连接其中两个节点组成一条链，使树中的每一条边至少被一条链覆盖。  
输出最少的链数量和其中任何一个解决方案。

### 解题思路


### AC代码
```cpp
#include<bits/stdc++.h>
using namespace std;

int N,res,cnt;
vector<int>arr[200005];
int brr[200005];
void dfs(int x,int y);
int main()
{
    scanf("%d",&N);
    for(int i=1;i<N;i++){
        int a,b;
        scanf("%d%d",&a,&b);
        arr[a].push_back(b);
        arr[b].push_back(a);
    }
    
    if(N==2){
        printf("1\n1 2");
        return 0;
    }
    else if(N==1){
        printf("0");
        return 0;
    }
    
    for(int i=1;i<=N;i++){
        if(arr[i].size()>1){
            dfs(i,i); res=i;
            break;
        }
    }
    
    printf("%d\n",(cnt+1)/2);
    for(int i=1;i<=cnt/2;i++)
        printf("%d %d\n",brr[i],brr[i+(cnt+1)/2]);
    if(cnt%2==1) printf("%d %d",res,brr[(cnt+1)/2]);
    return 0;
}

void dfs(int x,int y)
{
    if(arr[x].size()==1){
        brr[++cnt]=x;
        return;
    }
    for(int i=0;i<arr[x].size();i++){
        if(arr[x][i]!=y){
            dfs(arr[x][i],x);
        }
    }
}
```

[题目]:https://ac.nowcoder.com/acm/contest/5667/C
