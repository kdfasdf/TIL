https://swexpertacademy.com/main/code/problem/problemDetail.do

## 풀이
백트래킹을 활용한 문제 정답 코드를 작성한는데는 오래 걸리지 않았으나 시간초과가 발생하여 실행시간을 줄이는데 오래걸렸던 문제이다
<br>

처음에는 백트래킹을 돌릴 때
- 왼쪽에만 넣을 수 있는 경우
- 양쪽에 넣을 수 있는 경우(왼쪽, 오른쪽 둘다 넣어봄)
나누어서 백트래킹을 진행했는데 메서드 호출 횟수가 너무 많아서 시간초과가 발생하였다.<br>
사실 위 알고리즘에서는 왼쪽에만 넣을 수 있는 경우와 양쪽에서 넣을 수 있는 경우에서 왼쪽에 넣는 경우가 중복이다.(약간 헷갈려서 중복임에도 이렇게 작성하였다) 
코드에서 우선 왼쪽에 먼저 넣고(왼쪽에 넣는 것은 제한이 없으니까) 그 이후에 오른쪽에 넣을 수 있는 경우 오른쪽에 넣어보는 식으로 고쳐주었다
- 왼쪽에 먼저 넣어봄
- 오른 쪽에 넣을 수 있으면 오른쪽에 넣어봄
그래도 0개에서 18개가 통과되었는데 여전히 시간초과가 발생하는 케이스가 존재하였고 left와 right를 리스트가 아니라 숫자로 관리하였더니 통과하였다
- python
```
from itertools import permutations
def backtracking(data,depth):
    global cnt,left,right
    if left>=compare/2:
        cnt+=2**(len(data)-depth)
        return
    if depth==len(data):
        cnt+=1
        return
    else:
        left+=data[depth]
        backtracking(data,depth+1)
        left-=data[depth]
        if right+data[depth]<=left:
            right+=data[depth]
            backtracking(data,depth+1)
            right-=data[depth]


t=int(input())
for test in range(1,t+1):
    n=int(input())
    cnt=0
    left=0
    right=0
    data=list(map(int,input().split()))
    data2=permutations(data,n)
    for i in data2:
        compare=sum(i)
        left=i[0]
        right=0
        backtracking(i,1)
    print('#{}'.format(test),cnt)
```

