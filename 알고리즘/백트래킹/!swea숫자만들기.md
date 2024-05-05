https://swexpertacademy.com/main/code/problem/problemDetail.do?contestProbId=AWIeRZV6kBUDFAVH
## 풀이
백준 연산자 끼워넣기랑 같은 문제 백준에서 짰던 코드랑 거의 비슷하게 풀어서 제출했는데 시간 초과가 났다
근데 반대로 이 문제에서 낸 코드를 연산자 끼워넣기 문제에 제출했을 때 원래 백준에서 풀었던 문제보다 근소하게 느렸다
<br>
예상컨데 백준에서 짠 코드가 작은 데이터에 더 효율적인게 아닌가 싶다 백트래킹의 시간 복잡도는 O(2^n)으로 알고 있는데 
swea의 입력 크기가(숫자의 개수)가 3에서 12이고 백준은 11까지이다 아마 입력케이스에서 숫자 개수 차이가 있어서 인 것 같다

1. 깊이와 첫번 쨰 숫자를 인자로 백트래킹 시작
2. 한번의 백트래킹에서 연산자의 길이만큼 반복문을 돌림
3. 반복문 안에서 연산자가 얼마나 남아있는지 확인하고 0보다 크면 -1(연산을 한다는 의미) 지금 해당하는 연산자로 숫자와 다음번째 숫자에 대한 연산을 하고 한단계 더 깊숙이 탐색(now 연산 next, depth+1)
4. 연산자 수 +1로 다시 복구(다음 반복문에서는 다른 연산자를 사용할 것이므로) 
- python
```
def backtracking(now,depth):
    global maxValue,minValue
    if depth == n:
        maxValue = max(maxValue,now)
        minValue = min(minValue,now)
        return
    for i in range(4): # 4.
        if operator[i]>0:# 3.
            operator[i]-=1
            if i==0:
                backtracking(now+data[depth],depth+1)# 2.
            if i==1:
                backtracking(now-data[depth],depth+1)
            if i==2:
                backtracking(now*data[depth],depth+1)
            if i==3:
                backtracking(int(now/data[depth]),depth+1)
            operator[i]+=1

T= int(input())
for i in range(1,T+1):
    temp=0
    result=[]
    maxValue=-1e9
    minValue=1e9
    n=int(input())
    operator = list(map(int,input().split()))
    data=list(map(int,input().split()))
    backtracking(data[0],1) # 1.
    print('#{}'.format(i),maxValue-minValue)
```
