```py
import sys, heapq
n,e=map(int,input().split())
queue=[]
matrix=[[] for i in range(n+1)]
for _ in range(e):
    a,b,c=map(int,sys.stdin.readline().split())
    matrix[a].append((b,c))
    matrix[b].append((a,c))
v1,v2=map(int,input().split())
def bfs(start):
    dp = [int(1e9)] * (n + 1)
    heapq.heappush(queue,(0,start))
    dp[start]=0
    while queue:
        cost,node=queue.pop()
        for val in matrix[node]:
            next=val[0]
            cnt=val[1]
            if dp[next]>cnt+cost:
                dp[next]=cnt+cost
                heapq.heappush(queue,(dp[next],next))
    return dp

key=bfs(1)
sum1=sum2=0
sum1+=key[v1]
sum2+=key[v2]
case1=bfs(v1)
case2=bfs(v2)
sum1+=case1[v2]
sum2+=case2[v1]
case1=bfs(v2)
case2=bfs(v1)
sum1+=case1[n]
sum2+=case2[n]
if sum1>sum2:
    end=sum2
else:
    end=sum1

if end>=int(1e9):
    print(-1)
else:
    print(end)

```
<h1>느낀점</h1>
다익스트라 알고리즘으로 풀리는 문제였다.
기본적인 최단경로문제에 꼭 지나야하는 노드 2개가 존재한다는 조건이 추가된 문제였다.
나는 그냥 다익스트라 함수를 몇번 돌리면 될거라는 생각을 하였는데 시간복잡도가 충분히 될거라고 생각했기 때문이다.
그래서 v1,v2입력 받고 v1->v2 v2->v1 이렇게 두가지 경우를 다 계산하였다. 
1부터 시작해서 v1,v2까지 dp테이블 더하고 그다음 나머지 v1,v2까지 가는 dp테이블 또 더하고 마지막으로 v1,v2에서 n으로 가는 dp테이블도 더해주었다.
각각dp테이블은 다익스트라 함수를 계속 실행해서 새로운 테이블을 그냥 구해버렸다.
이 문제는 C++로 한번 풀어본적이 있어서 쉽게 접근할수 있었던것 같다.
