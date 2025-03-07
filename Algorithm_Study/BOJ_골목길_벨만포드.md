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
해결하고 다시 여기에 기록하기로 하자.<br>
<br><br>
한 3,4시간은 더 쓴거같다..... 매우 어려웠던 문제 solved티어도 골드1로 높은편
일단 첫번째 문제점은 나의 간단한 코드오류.. next랑 node랑 헷갈려서 다르게 쓴것
두번째는 벨만포드 알고리즘 사용하면서 마지막 for문에서 사이클 판별할때 사이클인게 목격되면 그 노드는 check리스트에 체크해뒀었는데
이렇게 하면 문제접이 체크만 하고 값은 바꿔주질 않으니까 얘가 다른 노드까지 값 변화에 영향을 줬음. 이게 결정적임
그래서 check만 하는게 아니라 Dp값 자체를 sys.maxsize를 먹여버림 그러면 if문에서 부등호에 안걸리기 때문에 영행 안줌
이거 발견하고 결국 풀어냄 ㅋㅋ
