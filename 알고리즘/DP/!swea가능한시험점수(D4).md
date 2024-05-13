https://swexpertacademy.com/main/code/problem/problemDetail.do?problemLevel=4&contestProbId=AWHPkqBqAEsDFAUn&categoryId=AWHPkqBqAEsDFAUn&categoryType=CODE&problemTitle=&orderBy=RECOMMEND_COUNT&selectCodeLang=ALL&select-1=4&pageSize=10&pageIndex=1

## 풀이
백준에 있는 문제와 비슷한 문제 
0원은 모든 경우에 만들 수 있으므로 0에 대해 표시를 해준다
가지고 있는 동전 중 하나를 기준으로 하고 큰 수 부터 조사하면서 내려오는데 지금 (조사하고 있는 점수 - 기준 동전 값)의 값이 1이면 조사하고 있는 점수 역시 만들 수 있는 점수이므로 1로 표시해준다
가능한 점수는 방문 배열의 합
- python
```
t=int(input())
for test in range(1,t+1):
    n=int(input())
    data=list(map(int,input().split()))
    visited=[0]*(sum(data)+1)
    visited[0]=1
    for i in range(len(data)):
        for j in range(len(visited)-1,data[i]-1,-1):
            if visited[j-data[i]]==1:
                visited[j]=1
    print('#{}'.format(test),sum(visited))
```
