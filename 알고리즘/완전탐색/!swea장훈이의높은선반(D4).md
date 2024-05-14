https://swexpertacademy.com/main/code/problem/problemDetail.do

## 풀이
조합을 활용하면 쉽게 풀 수 있는 문제
조합으로 구할 수 있는 쌍들 중 그 쌍의 원소의 합을 구하여 탑과의 높이차가 최소인 것을 출력하는 문제(선반은 탑의 높이 이상임)

- python
```
from itertools import combinations
t=int(input())
for test in range(1,t+1):
    n,m=map(int,input().split())
    data=list(map(int,input().split()))
    result=1e9
    for i in range(len(data)+1):
        temp=combinations(data,i)  #고른 선반 조합
        for j in temp:        
            temp2=list(j)  
            if sum(temp2)>=m:    #고른 조합의 합 즉 선반의 높이
                result=min(result,sum(temp2)-m)
    print('#{}'.format(test),result)
```
