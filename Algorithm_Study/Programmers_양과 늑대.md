```py
def solution(info, edges):
    answer=[]
    check = [0] * (len(edges) + 1)
    check[0] = 1
    def dfs(sheep, wolf):
        if sheep <= wolf:
            return
        else:
            answer.append(sheep)

        for x, y in edges:
            if check[x] == 1 and check[y] == 0:
                check[y] = 1
                if info[y] == 1:
                    dfs(sheep, wolf + 1)
                else:
                    dfs(sheep + 1, wolf)
                check[y]=0
    dfs(1, 0)
    answer.sort(reverse=True)
    return answer[0]
```
<h1>느낀점</h1>
어려웠던 문제....
일단 문제풀이를 어떻게 접근해야할지 고민하는데 시간이 많이 걸렸고 bfs로 접근할려다가 잘 안되서 시간을 좀 썻다.
dfs로 먼저 풀었으면 시간이 많이 걸리진 않았을것같다.
일단 dfs로 접근하면서 edges에 들어있는 좌표를 다 돌아줘야한다. 다시말해서 dfs 깊이가 하나씩 증가할때마다 edges모든 좌표를 다 돌아주도록 설정을 해줘야한다.
이진트리로 되어있기 때문에 왼쪽자식 탐색했다가 오른쪽 자식 탐색을 한 뒤 다시 왼쪽으로 돌아오는 경우의수도 있기때문에 모든좌표를 깊이 하나당 전부 돌아주도록 해야한다.
여기서 핵심은 모든 좌표를 돌때 check 방문리스트를 만들어줘서 부모는 방문처리 되있고 자식만 방문처리가 안된 좌표만 dfs를 돌려줘야한다.
그래야 양,늑대 카운트가 정확하게 이루어진다. 둘다 방문처리가 안되어있으면 아직 연결이 안된 좌표라는 뜻이고 둘다 방문처리가 되있으면 이미 카운트 한것이기 때문이다.
그리고 각 dfs마다 리턴조건을 걸어줘야하는데 이 조건은 양보다 늑대가 같거나 많을때 리턴해준다
양이 많은경우 answer리스트에 append해주고 마지막에 가장 높은 answer원소를 출력해준다.<br><br>
<b>이 문제는 카카오 2022 코딩테스트 출제된 문제이다. 왠지 쉽게 안풀리더라...</b>


