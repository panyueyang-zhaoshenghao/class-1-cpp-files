# 第一题
代码：
```cpp
#include<bits/stdc++.h>
using namespace std;
int main()
{
  int v,n;
  cin >> v >> n;
  int a[n];
  int dp[v+1];
  memset(dp, 0, sizeof(dp));
/*状态转移方程为：dp[j] = max(dp[j], dp[j-a[i]]+a[i])。*/
  for(int i=0; i<n; i++)
  {
    cin>>a[i];
    for(int j=v; j>=a[i]; j--)
    {
      dp[j] = max(dp[j], dp[j-a[i]]+a[i]);
    }
    cout << v-dp[v];
}
```
构思：知状态转移方程
```cpp
dp[j] = max(dp[j], dp[j-a[i]]+a[i])
```
就可以用`dp`做了
# 第二题
没解决
# 第三题
上代码
```cpp
#include <bits/stdc++.h>
int dp[201][2001];
int num[201];
 
int max(int a, int b)
{
	return a>b?a:b;
}
 
int main()
{
	int sum[201] = {
		0
	};
	int n;
	cin>>n;
	for (int i=1; i<=n; ++i)
	{
		cout<<num[i];
		sum[i] = sum[i-1] + num[i];
 
	}
	memset(dp, 0x8f, sizeof(dp));
	dp[0][0] = 0;
	for (int i=1; i<=n; ++i)
	{
		for (int j=sum[i]; j>=0; --j)
		{
			dp[i][j] = max(dp[i-1][j], dp[i-1][j+num[i]]);// 不放, 放矮塔还是矮塔
			if (j>=num[i])
			{
				// 放高塔
				dp[i][j] = max(dp[i][j], dp[i-1][j-num[i]]+num[i]);
			}
			else
			{
				// 放矮塔变高塔
				dp[i][j] = max(dp[i][j], dp[i-1][num[i]-j]+j);
			}
		}/*
		for (int j = sum[i]; j >= 0; j--)
		{
			dp[i][j] = max(dp[i-1][j], dp[i-1][j+num[i]] + num[i]);
			if (j >= num[i])
			{
				dp[i][j] = max(dp[i][j], dp[i-1][j-num[i]]);
			}
			else
			{
				dp[i][j] = max(dp[i][j], dp[i-1][num[i]-j] + num[i]-j);
			}
		}*/
	}
 
	int ans = dp[n][0];
	if (ans > 0)
		cout<<ans;
	else
		cout<<"Impossible";
	return 0;
}

```
