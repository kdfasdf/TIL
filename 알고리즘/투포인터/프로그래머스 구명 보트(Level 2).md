https://school.programmers.co.kr/learn/courses/30/lessons/42885

## 풀이 
정렬 후 양쪽에서 투포인터로 접근(두 사람의 무게 합이 한계 무게보다 적으면 태우고 아니라면 무거운 사람만 태우고)

- Java
```
import java.util.*;
class Solution {
    public int solution(int[] people, int limit) {
        int lpointer=0;
        int rpointer=people.length-1;
        int answer=0;
        Arrays.sort(people);
        while(lpointer<=rpointer){
            if(people[lpointer]+people[rpointer]<=limit && lpointer!=rpointer)
            {
                lpointer+=1;
                rpointer-=1;
                answer+=1;
            }
            else{
                rpointer-=1;
                answer+=1;
            }
        }
        return answer;
    }
}
```
