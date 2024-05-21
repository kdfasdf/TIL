https://school.programmers.co.kr/learn/courses/30/lessons/12924
## 풀이
투포인터로 접근 1부터 시작해서 숫자보다 작으면 rpointer를 옮겨서 다음 자연수를 더하고
숫자보다 크면 lpointer를 우측으로 옮겨서 연속된 자연수의 합의 크기를 줄인다 <br><br>
최근 코테를 봐서 그런지 문제를 어렵게 생각하는 경향이 생긴 것 같다 쉽게 생각하자 하단의 다른 풀이 참고

- Java
```
class Solution {
    public int solution(int n) {
        int[] data =new int[n+1];
        for (int i=1;i<n+1;i++)
            data[i]=i;
        int lpointer=1;
        int rpointer=1;
        int compare=data[rpointer];
        int result=0;
        while(rpointer<n+1)
        {
            if(compare==data[n]){
                result+=1;
                if (rpointer==n)
                    break;
                rpointer+=1;
                compare+=data[rpointer];
            }
            else if (compare<data[n]){
                rpointer+=1;
                compare+=data[rpointer];
            }
            else if(compare>data[n])
            {
                compare-=data[lpointer];
                lpointer+=1;
            }
                
        }
        return result;
    }
}
```
다른 풀이
1. 2중 for문으로 완전탐색으로 구하기
2. 정수론에 있는 정리 : 주어진 자연수를 연속된 자연수의 합으로 표현하는 방법의 수는 주어진 수의 홀수 약수의 개수와 같다

1.풀이
```
class Solution {
    public int solution(int n) {
        int answer = 0;

        for(int i = 1; i <= n; i++){
            int sum = 0;
            for(int j = i; j <= n; j++){
                sum += j;
                if(sum >= n){
                    if(sum == n) answer++;
                    break;
                }
            }
        }   
        return answer;
    }
}
```
2. 풀이
```
public class Expressions {

    public int expressions(int num) {
        int answer = 0;
   for (int i = 1; i <= num; i += 2) 
       if (num % i == 0) 
           answer++;

   return answer;
    }

    public static void main(String args[]) {
        Expressions expressions = new Expressions();
        // 아래는 테스트로 출력해 보기 위한 코드입니다.
        System.out.println(expressions.expressions(15));
    }
}
```
