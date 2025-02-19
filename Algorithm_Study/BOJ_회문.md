```py
t=int(input())
def go(data,ans):
    start = 0
    end = len(data) - 1
    key = 0
    while start < end:
        if data[start] == data[end]:
            start += 1
            end -= 1
        else:
            if data[start + 1] == data[end] and ans==1:
                if key == 0:
                    key = 1
                    start += 1
                else:
                    return 2
            elif data[start] == data[end - 1] and ans==2:
                if key == 0:
                    key = 1
                    end -= 1
                else:
                    return 2
            else:
                return 2
    if key==1:
        return 1
    else:
        return 0
for i in range(t):
    data=list(input())
    val=go(data,1)
    val=min(val,go(data,2))
    print(val)
```
<h1>느낀점</h1>
기본적인 투포인터 느낌인데 조건 한두개만 추가적으로 주면 풀리는 문제였다.
일단 중요한 조건이라 생각되는건 양쪽 포인터가 다를경우에 start+1 , end-1 둘중 하나를 해줌으로써 답을 구해 나가는데
두개의 케이스가 다 적용될수 있게? 해줘야 한다는 점
예를 들어 start+1 end 이 두개가 같다고 나올때 바로 넘어가는게 아니라 end-1,start 이것도 같이 체크해주면서 가야한다는 말임
그래서 go함수를 돌릴때 ans에 값을 줌으로써 결과적으로 go함수를 한 문자열당 두번 실행해주면서 start+1 , end-1 이 두가지를 전부 해줘야
오답없이 문제를 맞칠수 있음 그러나 이문제는 쉬운문제였음
