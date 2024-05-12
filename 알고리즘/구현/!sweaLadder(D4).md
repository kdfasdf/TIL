https://swexpertacademy.com/main/code/problem/problemDetail.do?problemLevel=4&contestProbId=AV14ABYKADACFAYh&categoryId=AV14ABYKADACFAYh&categoryType=CODE&problemTitle=&orderBy=RECOMMEND_COUNT&selectCodeLang=ALL&select-1=4&pageSize=10&pageIndex=1

## 풀이
처음에는 dfs로 풀려고 했지만 재귀를 리턴값으로 받는데 문제가 있어서 bfs로 푼 문제 
방문 배열의 기본 값을 0으로 하면 올바른 값을 반환 못하니 다른 값으로 초기화할 것(좌표를 0~99를 쓰기 떄문)
- python
```
def bfs(i,j,start):
    q=[]
    q.append([i,j,start])
    while q:
        x,y,start=q.pop(0)
        if data[x][y]==2:
            return start
        for i in range(3):
            nx=x+dx[i]
            ny=y+dy[i]
            if 0<=nx<100 and 0<=ny<100 and visited[x][y]==-1 and visited[nx][ny]==-1 and data[nx][ny]!=0:
                visited[x][y]=start
                q.append([nx,ny,start])
    return -1

dx=[0,0,1]
dy=[-1,1,0]
for test in range(1,10+1):
    data=[]
    n=int(input())
    result=0
    for _ in range(100):
        data.append(list(map(int,input().split())))
    for i in range(100):
        if data[0][i]==1:
            visited=[[-1]*100 for _ in range(100)]
            result = bfs(0,i,i)
            if result !=-1:
                break

    print('#{}'.format(test),result)
```
