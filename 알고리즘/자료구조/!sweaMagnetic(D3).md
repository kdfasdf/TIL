https://swexpertacademy.com/main/talk/solvingClub/problemView.do?solveclubId=AV6kld8aisgDFASb&contestProbId=AV14hwZqABsCFAYD&probBoxId=AV-4MojKLNADFATz+&type=PROBLEM&problemBoxTitle=%5BD2%7ED3+%EB%AC%B8%EC%A0%9C%ED%92%80%EC%9D%B4%5D+%EA%B8%B0%EC%B4%88+%EB%8B%A4%EC%A7%80%EA%B8%B0+Part4&problemBoxCnt=++14+

## 풀이
스택을 활용한 문제 1을 만나면 스택에 값을 추가하고(스택이 비어 있어야 함) 2를 만나면 스택에서 값을 뺴내주고
열을 옮길 때 스택을 비워주면 되는 문제

- python
```
for test in range(1,10+1):
    n=int(input())
    data=[]
    stack=[]
    result=0
    for i in range(100):
        data.append(list(map(int,input().split())))
    for i in range(100):
        stack=[]
        for j in range(100):
            if data[j][i]==1 and not stack:
                stack.append(1)
            elif data[j][i]==2 and stack:
                stack.pop(-1)
                result+=1
    print('#{}'.format(test),result)
```
