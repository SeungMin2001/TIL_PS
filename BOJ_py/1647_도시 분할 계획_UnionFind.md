```py
n,m=map(int,input().split())
matrix=[]
check=[0]*(n+1)
for i in range(1,n+1):
    check[i]=i
for i in range(m):
    a,b,c=map(int,input().split())
    matrix.append((a,b,c))
matrix=sorted(matrix,key=lambda x:x[2])
def find(key):
    if key!=check[key]:
        return find(check[key])
    return check[key]
def union(a,b):
    if check[a]>check[b]:
        check[a]=check[b]
    else:
        check[b]=check[a]
cnt=count=0
test=[]
for i in range(m):
    a,b,c=matrix[i]
    a=find(a)
    b=find(b)
    if a!=b:
        union(a,b)
        cnt+=c
        count+=1
        test.append((a,b,c))
        if count==n-1:
            break
print(cnt-test[-1][2])

```
<h1>느낀점</h1>
1번만에 성공 
처음 시도한 아이디어가 정답이였다.
그래프가 주어지면 두개의 그룹으로 분할한뒤 각각 스패닝트리를 구하고 그 가중치들의 합을 구하는 문제로 제시됬는데
처음부터 스패팅트리를 구해놓고 거기서 제일 큰 간선을 지워주면 자연스럽게 두 그룹으로 분할됨과 동시에 각각의 그룹에서 스패닝트리를 구한 효과를 볼수 있다.
이 생각으로 접근해서 한 5분만에 푼것같다.
