https://school.programmers.co.kr/learn/courses/30/lessons/152996
## 풀이
문제 읽으면 O(n^2)으로 짜고 싶지만 시간복잡도를 고려해 적절한 자료구조를 선택하여 더 효율적인 코드를 짜야하는 문제
HashMap을 활용<br>
무게 배열을 정렬한 후 map에 넣어준다 map에 넣기 전에 지금 값에 1/2,2/3,3/4 한 값이 key 값으로 있는지 확인하고 각 값에 대해 있으면 answer+=1
지금 값에 1/2,2/3,3/4인 값이 있는지 확인하는 이유는 배열이 정렬되어있기 때문에 지금의 무게가 map에 있는 key값보다 작을 수가 없기 때문이다
- Java
```
import java.util.*;
class Solution {
    public long solution(int[] weights) {
    	long answer = 0;
        Arrays.sort(weights);
        Map<Double, Integer> map = new HashMap<>();
        for(int i : weights) {
    		double a = i*1.0;
    		double b = (i*2.0)/3.0;
    		double c = (i*1.0)/2.0;
    		double d = (i*3.0)/4.0;
    		if(map.containsKey(a)) answer += map.get(a);
    		if(map.containsKey(b)) answer += map.get(b);
    		if(map.containsKey(c)) answer += map.get(c);
    		if(map.containsKey(d)) answer += map.get(d);
    		map.put((i*1.0), map.getOrDefault((i*1.0), 0)+1);
        }
        
        return answer;
    }
}
```
