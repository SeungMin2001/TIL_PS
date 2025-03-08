```py
import sys
dp=[0]*1000000
key,a,b=map(int,sys.stdin.readline().split())
dp[0]=1
def dfs(k):
    if k>=100000:
        val=dfs(k//a)+dfs(k//b)
        return val
    else:
        if not dp[k]:
            dp[k]=dfs(k//a)+dfs(k//b)
            return dp[k]
        else:
            return dp[k]
print(dfs(key))
```
<h1>느낀점</h1>
처음에는 매우 어려운 문제라고 생각했다. 뭔가 수열에 반복되는 규칙을 찾아서 새로운 점화식을 만들어줘야겠다는 생각을 했기 때문이다.
근데 랭크도 골드5이고 뭔가 아니겠다는 느낌이 들어서 문제에서 제시된 점화식을 그대로 사용했다. 이제 10^12승까지 들어오니까 Dp를 사용하되
백만까지만 Dp를 사용하고 그 이상이 되면 그냥 계산을 때리는 dfs함수를 만들어줬다. 그리고 setrecursionlimit는 안써줘도 무난히 통과됬다.
