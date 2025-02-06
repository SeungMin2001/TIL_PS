```py
n,m=map(int,input().split())
matrix=[]
dp=[int(-1e12)]*(n+1)
check=[0]*(n+1)
dp[1]=0
answer=[]
test=[0]*(n+1)
memory=[[] for _ in range(n+1)]
for _ in range(m):
    a,b,c=map(int,input().split()) #그래프 저장,양방향
    matrix.append((a,b,c))
for node in range(n): #모든 노드
    for i in range(m):
        now,next,cost=matrix[i]
        if dp[next]<cost+dp[now] and dp[now]!=int(-1e12):
            dp[next]=cost+dp[now]
            memory[next].append((now,dp[now]))
            if node==n-1:
                check[next]=1


key=-999
index=0
for i in range(2,n+1):
    memory[i]=sorted(memory[i],key=lambda x:x[1],reverse=True)
    if memory[i]:
        memory[i]=memory[i][0]
for i in range(len(dp)):
    if key<=dp[i] and check[i]==0:
        key=dp[i]
        index=i

answer.append(index)
while True:
    if not memory[index]: #empty
        break
    node=memory[index][0]
    if check[node]==1:
        break
    answer.append(node)
    index=node

if len(answer)<=1:
    print(-1)
else:
    answer.reverse()
    for i in range(len(answer)):
        print(answer[i],end=' ')

```
<h1>느낀점</h1>
일단 이문제는 아직 해결하지 못한상태이다. 너무 어렵다.... 반례 하나만 처리해주면 해결될거같은데,, 
반례=
4 3
1 2 1
1 4 100
2 1 1
-1

1->4가 존재함에도 불구하고 1<->2 무한사이클을 못잡아내고있다. 1<->2무한사이클이 4까지 영향을 줘서 check배열에 들어가버려서 실패가 뜨는것같다.
해결하고 다시 여기에 기록하기로 하자.
