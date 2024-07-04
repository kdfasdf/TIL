https://school.programmers.co.kr/learn/courses/30/lessons/12973
## 풀이
입력 문자열의 길이를 보고 선형탐색으로 할 경우 시간초과가 날 것이라고 예측할 수 있다 스택으로 주어진 규칙에 따라 문자열을 삭제할 수 있는지 확인하는 문제
- Java
```
import java.util.*;
class Solution
{
    public int solution(String s)
    {
        int answer = 0;
        Stack<Character> stack = new Stack<>();
        for(char a : s.toCharArray())
        {
            if(!stack.isEmpty()&&stack.peek()==a)
            {    stack.pop();
                continue;
            }
            stack.add(a);
        }
        if(stack.isEmpty())
            answer=1;
        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다.
        System.out.println("Hello Java");

        return answer;
    }
}
```
