https://school.programmers.co.kr/learn/courses/30/lessons/76502

## 풀이
1. 시작점 반복문(i: 0~문자열 길이)
2. 각 반복문 마다 문자열 길이만큼 탐색(j~ 문자열 길이)
   - 회정 표현은 (i+j)%문자열 길이로 오버플로 방지
3. [,{,(는 무조건 스택에 추가
4. },],)는 스택의 최상단이 대응되는 괄호면 스택에서 제거(스택이 비어있지 않는 상황이라면)
5. 이번 반복문에서 문자열을 끝까지 탐색 후 스택에 문자가 없고 flag가 true면 answer+=1
+ 예외 처리 : 스택이 비어있을 때  },),]가 나오는 것

- Java
```
import java.util.*;
class Solution {
    public int solution(String s) {
        int answer=0;
        for(int i=0;i<s.length();i++){
            Stack<Character> data= new Stack<>();
            boolean flag = true;
            for(int j=0;j<s.length();j++)
            {
                int index=(i+j)%s.length();
                if (s.charAt(index)=='['||s.charAt(index)=='('||s.charAt(index)=='{')
                    data.add(s.charAt(index));
                else if(!data.isEmpty()){
                    if(s.charAt(index)==']')
                        if(data.peek()=='[')
                            data.pop();
                        else flag=false;
                    else if(s.charAt(index)=='}')
                        if(data.peek()=='{')
                            data.pop();
                        else flag=false;
                    else if(s.charAt(index)==')')
                        if(data.peek()=='(')
                            data.pop();
                        else flag=false;
                }
                else{
                    flag=false;
                }
            }
            if (flag&&data.isEmpty())
                answer+=1;
        }
        return answer;
    }
}
```
