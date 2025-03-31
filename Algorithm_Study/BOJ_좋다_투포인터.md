```py
import sys
n=int(sys.stdin.readline())
data=list(map(int,sys.stdin.readline().split()))
data.sort()
cnt=0
for key in range(n):
    start=0
    end=n-1
    while start<end:
        if key==start:
            start+=1
            if start>=end:
                break
        if key==end:
            end-=1
            if start>=end:
                break

        val=data[start]+data[end]
        if val==data[key]:
            #print(val,start,end) debug
            cnt+=1
            break
        elif val<data[key]:
            start+=1
        else:
            end-=1
print(cnt)

```

<h1>느낀점</h1>
방향만 잘 잡으면 매우 쉬운문제였는데 처음에 방향을 잘못잡아서 시간이 좀 걸린 문제
일단 무지성으로 반복문 돌리면 무조건 시간초과가 나올걸 예상하고
이분탐색으로 하나의 값을 잡아놓고 나머지 값을 이분탐색으로 찾을 생각을 했었다. 이러면 
for문으로 모든 key 값을 돌면서 또 for문을 돌리면서 key를 제외한 n-1개의 값을 돈다. 지금 돌고있는 for문에 값과 합했을때 key값이 되는
애를 찾을때 이분탐색으로 찾아버리면 O(n*n*logn)이 나오고 문제 조건이 2초에 케이스 2000개다. 즉 2000*2000*log2000인데
아슬아슬하게 2초 언저리 나올거 같아서 시도했지만 이분탐색+키값과 다른 값 비교+값 찾을때 중복값이 있으면 안됨 이 3가지 조건을 다 맟출려다보니까
코드가 꼬여버려서 뭔가 모를 에러가 계속 났었다. 
그래서 투포인터 로 방향을 바꿧고 다행히 바로 풀렸다.... for문 하나로 key값 돌리면서 두개의 값을 투포인터로 간격 좁히면서 탐색 하니까 풀림
