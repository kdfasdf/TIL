https://school.programmers.co.kr/learn/courses/30/lessons/12909

## 풀이
문자열을 순서대로 탐색 
문자가 '('이라면 스택에 더하고 아니라면 스택에서 빼낸다(이 때 스택이 비어 있으면 안된다 스택이 비어있다면 false)
끝까지 탐색 후 스택이 비어있지 않다면 false 비어있다면 true
- Java
```
import java.util.*;
class Solution {
    boolean solution(String s) {
        Stack<String> stack = new Stack<>();
        for (int i = 0; i < s.length(); i++) {
            if (s.charAt(i) == '(') stack.add("(");
            else {
                if (stack.isEmpty()) {
                    return false;
                } else
                    stack.pop();
            }
        }
        if(!stack.isEmpty())
            return false;
        else{
            return true;
    }}
}
```
