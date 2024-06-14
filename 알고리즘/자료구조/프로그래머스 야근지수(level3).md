https://school.programmers.co.kr/learn/courses/30/lessons/12927
## 풀이
우선순위큐에 내림차순 기준으로 입력 배열의 요소를 하나씩 넣고
가장 큰 값을 뺴낸 후 1을 빼서 다시 우선순위 큐에 넣는 것을 n번 반복하면 되는 문제
- Java
```
import java.util.*;
class Solution {
    public long solution(int n, int[] works) {
        PriorityQueue<Integer>pq = new PriorityQueue<>(Collections.reverseOrder());
        for(int i: works)
            pq.add(i);
        for(int i=0;i<n;i++)
        {
            int num=pq.poll()-1;
            if(num<0)
                break;
            pq.add(num);
        }
        long answer=pq.stream().mapToLong(i->i*i).sum();
        return answer;
    }
}
```
