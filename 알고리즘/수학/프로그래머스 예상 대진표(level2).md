https://school.programmers.co.kr/learn/courses/30/lessons/12985

## 풀이
처음에는 단순히 a,b 모두 라운드를 진행하면서 2를 나눠간다(홀수라면 1을 더하고 나눈다)<br>
결과적으로 작은 수는 1로 향하고 큰 수는 2 향한다고 생각했는데 예외처리에서 막혔다.
조금 더 보편적인 상황을 생각하면 3,4로 주어지면 1라운드에서 만나므로 1, 2 가 아니어도 매칭이 된다 즉 a와 b가 특정 라운드에서 절대값이 1이면 멈춘다<br>
다만 아직 추가적으로 해줘야할 예외처리가 있는데 4,5 같은 경우이다 4, 5는 절대값 차이가 1이지만 매칭되지 않는다(3은 4랑 5는 6이랑 매칭되기 떄문)<br>
절대값 차이가 1임에도 매칭관계가 아닌 숫자들은 다음과 같은 특징이 있다 <br>
두 수를 더하고 1을 추가로 더한 뒤 4로 나누면 안나누어 떨어진다
<예시>
- 4,5 : (4+5+1)%4==2
- 3,4: (3+4+1)%4==0


- Java
```
class Solution
{
    public int solution(int n, int a, int b)
    {

        int answer = 1;
        int sa=a<b?a:b;
        int sb=a>b?a:b;
        while(Math.abs(sa-sb)!=1||(sa+sb+1)%4!=0)
        {
            if(sa%2==1)
            {
                sa+=1;
            }
            sa/=2;
            if(sb%2==1)
            {
                sb+=1;
            }
            sb/=2;
            answer+=1;
        }

        return answer;
    }
}
```

다른 사람 풀이에 수학적으로 놀라운 풀이가 있어서 적는다
```
class Solution
{
    public int solution(int n, int a, int b)
    {
        return Integer.toBinaryString((a-1)^(b-1)).length();
    }
}
```
```
class Solution
{
    public int solution(int n, int a, int b)
    {
        int round = 0;
        while(a != b)
        {
            a = a/2 + a%2;
            b = b/2 + b%2;
            round++;
        }
        return round;
    }
}
```
