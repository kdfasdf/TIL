https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AV5PpFQaAQMDFAUq

### 풀이

처음에 구현으로 풀었는데 51개 중 47개 맞은걸로 틀린문제 dp, dfs로 접근할 수 있는데 개인적으로 dp로 푸는 것은(모 아니면 도라) 시험장에서 떠올리기 힘드므로 DFS로 접근하는 것이 나을 것 같다

- dp
 
n월까지의 최소비용을 dp[n]에 저장한다고 했을 때 dp[n]의 값이 될 수 있는 경우는 4가지이다
  - 이번 달 사용 금액(일일) + n-1(지난 달 까지의) 최소금액
  - 이번 달 사용금액(1달) + n-1(지난 달 까지)의 최소금액
  - 이번 달 사용금액(3달) + n-3(3개월 전까지)의 최소금액
  - 이번 달 사용금액(1년) + n-12(12개월 전까지)의 최소금액

  - python
  ```
  T=int(input())
    for test in range(1,T+1):
        price = list(map(int,input().split()))
        month =[0]+list(map(int,input().split()))
        for i in range(1,13):
            day= month[i]*price[0]+month[i-1]
            mon=price[1]+month[i-1]
            tmon,year=1e9,1e9
            if i >=3:
                tmon=price[2]+month[i-3]
            if i>=12:
                year = price[3]+month[i-12]
            month[i]=min(day,mon,tmon,year)
        print("#{}".format(test),month[12])

  ```

- dfs
 
   - 1일권, 1달권, 3달권,1년권에 대한 dfs를 한 메서드 안에서 진행
   ```
   def dfs(n,temp):
    global answer
    if n>12:
        if answer>temp:
            answer=temp
        return
    dfs(n+1,temp+month[n]*price[0])
    dfs(n+1,temp+price[1])
    dfs(n+3,temp+price[2])
    dfs(n+12,temp+price[3])
    T=int(input())
    for test in range(1,T+1):
        price = list(map(int,input().split()))
        month =[0]+list(map(int,input().split()))
        answer=1e9
        dfs(1,0)
        print("#{}".format(test),answer)
   ```
