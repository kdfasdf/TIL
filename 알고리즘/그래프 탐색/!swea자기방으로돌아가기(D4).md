https://swexpertacademy.com/main/code/problem/problemDetail.do?problemLevel=4&contestProbId=AWNcJ2sapZMDFAV8&categoryId=AWNcJ2sapZMDFAV8&categoryType=CODE&problemTitle=&orderBy=RECOMMEND_COUNT&selectCodeLang=ALL&select-1=4&pageSize=10&pageIndex=1

## 풀이
출발지, 도착지에 따른 복도 번호는 다음과 같다

|홀수방 번호|1|3|5|7|9|....|399|
|--|--|--|--|--|--|--|
|짝수방 번호|2|4|6|8|10|....|400|
|복도 번호|0|1|2|3|4|5....|200|

(출발지 번호-1)/2 에서 (도착지 번호-1)/2가 이용 복도 번호이므로 해당 범위 복도 이용횟수를 1증가시켜주면 된다

- python
```
t = int(input())
for test in range(1,t+1):
    n=int(input())
    data=[0 for i in range(200)]
    for i in range(n):
        a,b=map(int,input().split())
        if a==b:
            continue
        if b<a:  #a가 출발지, b가 도착지
            a,b=b,a
        a-=1
        b-=1
        a=a//2
        b=b//2
        for j in range(a,b+1): #복도 이용 횟수
            data[j]+=1
    print('#{}'.format(test),max(data))
```
