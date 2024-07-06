https://school.programmers.co.kr/learn/courses/30/lessons/154539
## 풀이
처음에 dp, 선형 탐색 등의 방법을 생각했으나 예외 처리가 되지 않아 다른사람의 풀이를 본 문제
스택을 활용한 문제 스택으로 푼 사람들이 어디서 힌트를 얻을 수 있어냐 하면은 뒤에 있는 수 중 가장 가까운 수가 그 위치에서의 답이라는 점에서 스택을 떠올렸다고 한다<br>
유형 : 스택<br>
힌트 : 뒤에 있는 수 중 지금 위치의 수 보다 큰데 그 중에서 지금위치에서 가장 가까운 수<br>
```
import java.util.*;
class Solution {
    public int[] solution(int[] numbers) {
        int [] answer=new int[numbers.length];
        Arrays.fill(answer,-1);
        Stack <Integer> stack = new Stack<>();
        int compare=-1;
        int maxValue=-1;
        answer[numbers.length-1]=-1;
        stack.add(numbers[numbers.length-1]);
        for(int i=numbers.length-2;i>=0;i--)
            {
                while(!stack.isEmpty()&&stack.peek()<=numbers[i]){
                    stack.pop();       
                }
                if (!stack.isEmpty())
                    answer[i]=stack.peek();
                else
                    answer[i]=-1;
                stack.add(numbers[i]);
            }
        return answer;
    }
}
```
