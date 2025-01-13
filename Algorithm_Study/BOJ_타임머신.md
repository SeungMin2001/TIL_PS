```py
n,m=map(int,input().split())
matrix=[]
INF=int(1e9)
dp=[INF]*(n+1)
for k in range(m):
    a,b,c=map(int,input().split())
    matrix.append((a,b,c))

def bf(start):
    dp[start]=0
    for i in range(n):
        for j in range(m):
            cur=matrix[j][0]
            node=matrix[j][1]
            cost=matrix[j][2]
            if dp[cur]+cost<dp[node] and dp[cur]!=INF:
                dp[node]=dp[cur]+cost
                if i==(n-1):
                    return True
    return False

if bf(1):
    print(-1)
else:
    for i in range(2,n+1):
        if dp[i]==INF:
            print(-1)
        else:
            print(dp[i])



```
<h1>느낀점</h1>
벨만포드 알고리즘 기본문제였다.
만약 간선비용이 모두 양수였으면 벨만포드가 아니라 다익스트라를 썻으면 됬다. 음수가 있었기 때문에 벨만포드를 사용하였고 
벨만포드 알고리즘은 다익스트라에 비해 시간복잡도가 더 많이 나가기 때문에 문제조건을 잘 보고 시간내에 풀릴거같으면 사용한다.
벨만포드는 visited, 즉 방문체크를 안한다는게 특징이다. 
