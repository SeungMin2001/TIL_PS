```cpp
#include<stdio.h>
#include<math.h>
using namespace std;
int A[15],cnt=0,N;
bool check(int level){
	for(int i=0;i<level;i++){
		if(A[i]==A[level]||abs(A[level]-A[i])==abs(level-i)) return false;
	}
	return true;
}
int queen_dfs(int level){
	if(level==N){
		cnt++;
		return 0;
	}
	else{
		for(int i=0;i<N;i++){
			A[level]=i;
			if(check(level)==true) queen_dfs(level+1);
		}
	}
	return 0;
}
int main(){
	scanf("%d",&N);
	queen_dfs(0);
	printf("%d",cnt);
	return 0;
}
```
### 이 문제는 혼자힘으로 못푼 문제다... 블로그에 도움을 받았다.
##### 앞으로 이 문제를 많이 복습할 예정이다.
##### 문제를 풀때 포인트를 잡자면 일단 더 쉽게 풀기위한 아이디어 발상이 가장 중요한것 같다.
##### 이 문제에서 쓰인 아이디어를 기록하겠다.
##### 1. 퀸 특성상 한 열당 하나밖에 퀸이 못놓인다. 따라서 N*N체스판인데도 불구하고 1차원 배열로 문제를 풀수 있다.
##### 2. 대각선에 위치하느냐를 판별하기가 까다로운데 (X,Y)의 대각선의 위치한 (a,b)는 (X-a)==(Y-b)특징을 갖고있다. 물론 둘의 위치를 바꿔줘도 무방하다.
##### 따라서 대각선 두 방향을 다 판별하기 위해서는 abs라는 절댓값을 구해주는 함수를 사용해야 풀수있다. abs는 include<cmath> 에 포함되어있다.
