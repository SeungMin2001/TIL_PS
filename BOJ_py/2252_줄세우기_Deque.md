```py
m,n=map(int,input().split())
checked=[0]*(m+1)
queue=[]
for i in range(n):
    a,b=map(int,input().split())
    if checked[a]==0 and checked[b]==0:
        queue.append(b)
        queue.insert(0,a)
        checked[a]=1
        checked[b]=1
    elif checked[a]==0 and checked[b]!=0:
        queue.insert(0, a)
        checked[a]=1
    elif checked[a]!=0 and checked[b]==0:
        queue.append(b)
        checked[b]=1
    elif checked[a]!=0 and checked[b]!=0: #key 
        x=queue.index(a)
        y=queue.index(b)
        if x>y:
            queue[x],queue[y]=queue[y],queue[x]
for i in range(1,m+1):
    if checked[i]==0:
        queue.append(i)
for i in queue:
    print(i,end=' ')
```
<h1>느낀점</h1>
골드3 치고는 많이 쉬웠던 문제
보자마자 deque로 풀어야겠다고 판단. 하지만 케이스에서 제시한 두 원소가 전부 Deque에 있을경우 순서바꾸기가 시간이 너무많이걸림
그래서 리스트로 다시 접근
-> 바로 풀림 
리스트가 좋은이유가 deque처럼 사용할수 있고 두 원소를 바꿀때 인덱스로 바로 접근가능하니까 시간절약이 훨씬 많이 됨
insert(0,a) = appendleft 이렇게 사용하면 같은기능됨
