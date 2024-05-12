https://swexpertacademy.com/main/code/problem/problemDetail.do?problemLevel=4&contestProbId=AV5LtJYKDzsDFAXc&categoryId=AV5LtJYKDzsDFAXc&categoryType=CODE&problemTitle=&orderBy=RECOMMEND_COUNT&selectCodeLang=ALL&select-1=4&pageSize=10&pageIndex=1

## 풀이
완전탐색에 bfs를 활용한 문제
- python
```
def bfs(x,y):
    q=[]
    q.append([x,y])
    visited[x][y]=1
    tx=0
    ty=0
    while q:
        tx,ty=q.pop(0)
        for i in range(4):
            nx=tx+dx[i]
            ny=ty+dy[i]
            if 0<=nx<n and 0<=ny<n and data[tx][ty]+1==data[nx][ny] :
                visited[nx][ny]=visited[tx][ty]+1
                q.append([nx,ny])
    return visited[tx][ty]

dx=[-1,1,0,0]
dy=[0,0,-1,1]
t=int(input())
for test in range(1,t+1):
    data=[]
    n=int(input())
    maxDis=-1e9
    minRoom=1e9
    visited=[[0]*n for i in range(n)]
    distance=[[0]*n for i in range(n)]
    for i in range(n):
        data.append(list(map(int,input().split())))
    for i in range(n):
        for j in range(n):
            if visited[i][j]==0:
            	distance[i][j]=bfs(i,j)
            if maxDis<distance[i][j]:
                maxDis=distance[i][j]
                minRoom=data[i][j]
            if maxDis == distance[i][j] and  minRoom>data[i][j]:
                minRoom=data[i][j]
    print('#{}'.format(test),minRoom,maxDis)
```
