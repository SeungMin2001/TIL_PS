```py
n=int(input())
data=list(map(str,input().split()))
for i in range(len(data)):
    if data[i]=='>':
        data[i]=0
    else:
        data[i]=1
res=[]
answer=[0]*11
check=[0]*11
def dfs(depth):
    if depth==n+1:
        res.append(answer[:])
        return
    for i in range(10):
        if check[i]==0:
            if depth==0:
                answer[depth]=i
                check[i]=1
                dfs(depth+1)
                check[i]=0
                answer[depth]=0
            else:
                if (data[depth-1]==0 and answer[depth-1]>i) or (data[depth-1]==1 and answer[depth-1]<i):
                    check[i]=1
                    answer[depth]=i
                    dfs(depth+1)
                    check[i]=0
                    answer[depth]=0
dfs(0)
for i in range(len(res[-1])):
    if i>=n+1:
        continue
    print(res[-1][i],end='')
print()
for i in range(len(res[0])):
    if i>=n+1:
        continue
    print(res[0][i],end='')
```
<h1>느낀점</h1>
무난했던 문제
기본적인 dfs+백트래킹 문제
