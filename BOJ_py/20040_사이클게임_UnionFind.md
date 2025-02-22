```py
import sys
sys.setrecursionlimit(500000)
n,m=map(int,sys.stdin.readline().split())
check=[0]*(n+1)
for i in range(n):
    check[i]=i
def find(x):
    if check[x]==x:
        return x
    return find(check[x])
def union(a,b):
    a=find(a)
    b=find(b)
    if a>b:
        check[a]=check[b]
    elif a<b:
        check[b]=check[a]
    else:
        return -1
    return 1
for i in range(m):
    a, b = map(int, sys.stdin.readline().split())
    if union(a,b)==-1:
        print(i+1)
        exit(0)
print(0)
```
<h1>느낀점</h1>
기본적인 유니온-파인드 문제였는데 시간초과가 났다.
그래서 최상위부모노드가 더 작은애에 값으로 통일시켜줬는데
제일 큰 부모노드로 통일시키는걸로 바꿔줬더니 맞았다.
값이 더 큰걸로 하면 걸리는 시간이 줄어드는것을 알수 있었다.
