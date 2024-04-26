![image](https://github.com/kdfasdf/TIL/assets/96770726/ccbbb54c-cc50-4612-af97-1de7075b6446)[[https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV4suNtaXFEDFAUf](https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5PoOKKAPIDFAUq)

[Uploading image.png…]()

## 풀이
우선 내가 짠 알고리즘을 설명해보자면
처음에 등산로에서 가장 높은 봉우리를 리스트에 넣어두고 하나씩 꺼내어 dfs를 수행한다
수행하는 dfs 에서는 평범하게 다음 깊이로 dfs를 진행하는 경우와 봉우리를 한번 깎고 진행하는 dfs로 나눠서 수행한다
봉우리를 깎을 수 있는 경우의 조건은 data[현단계x][현단계y]-k<data[전단계x][전단계y]<=data[현단계x][현단계y]를 만족하면 깎을 수 있는데
봉우리를 한번 깎는 dfs는 더 깊은 단계의 dfs에서 봉우리를 깎는 일이 없도록 flag 값과 깎는 봉우리의 값은 이전 단계 봉우리 높이-1로 수정해주고(이전 단계 봉우리-1인 경우가 경로가 가장 기므로)
한단계 더 깊은 DFS를 수행하고나서 봉우리와 flag 값을 원래 값으로 다시 수정해준다

<br>
- python
```
def dfs(x,y):
    global flag
    for i in range(4):
        n_x=x+dx[i]
        n_y=y+dy[i]
        if 0<=n_x<n and 0<=n_y<n:
            if data[n_x][n_y]-k<data[x][y]<=data[n_x][n_y] and flag and visited[n_x][n_y]==0:
                flag=False
                visited[n_x][n_y]=visited[x][y]+1
                tdata=data[n_x][n_y]
                data[n_x][n_y]=data[x][y]-1
                dfs(n_x,n_y)
                visited[n_x][n_y]=0
                data[n_x][n_y]=tdata
                flag=True
            if data[n_x][n_y] < data[x][y] and visited[n_x][n_y]==0:
                visited[n_x][n_y]=visited[x][y]+1
                dfs(n_x, n_y)
                visited[n_x][n_y]=0

    result.append(visited[x][y])
    return


t=int(input())
dx=[-1,1,0,0]
dy=[0,0,-1,1]
for test in range(t):
    n,k=map(int,input().split())
    data=[]
    q=[]
    result=[]
    for i in range(n):
        data.append(list(map(int,input().split())))
    s=0
    flag=True
    for i in range(n):
        for j in range(n):  #가장 큰 값 찾기
            s=max(s,data[i][j])
    for i in range(n):      #가장 큰 값 인덱스 추가
        for j in range(n):
            q.append([i,j])
    while q:
        n_x,n_y=q.pop(0)
        visited=[[0]*n for _ in range(n)]
        visited[n_x][n_y]=1
        dfs(n_x,n_y)

    print('#{}'.format(test+1),max(result))
```
