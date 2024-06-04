https://school.programmers.co.kr/learn/courses/30/lessons/138476

## 풀이
1. tangerine을 해시에 저장하여 value 값을 기준으로 내림차순으로 바꿔줌
2. k에서 value 정렬된 순서로 뺴줌
3. k 값이 0이하일 경우 정답
- Java
```
import java.util.*;
class Solution {
    public int solution(int k, int[] tangerine) {
        int answer = 0;
        int tk=k;
        HashMap<Integer,Integer> map = new HashMap<>();
        for(int i=0;i<tangerine.length;i++)
        {    map.put(tangerine[i],map.getOrDefault(tangerine[i],0)+1);
        }
        List<Integer> keyList = new ArrayList<>(map.keySet());
        keyList.sort(((o1, o2) -> map.get(o2) - map.get(o1)));
        for (Integer i : keyList) {
            if (k <= 0) {
                break;
            }
            answer++;
            k -= map.get(i);
        }
        return answer;
    }
}
```
