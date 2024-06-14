https://school.programmers.co.kr/learn/courses/30/lessons/42576

## 풀이
마라톤 참여선수가 1명 이상 100000명 이하라 반복을 통해 확인해도 시간초과가 나지 않을 것이라고 생각했으나 시간초과에 걸렸다 완주자와 참가자를 해시맵에 저장하여 값이 짝수가 아닌 참가자를 찾으면 되는 문제
- Java(시간 초과)(O(N^2))
```
import java.util.*;
class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        ArrayList<String> complete = new ArrayList<>(Arrays.asList(completion));
        ArrayList<String>partici=new ArrayList<>(Arrays.asList(participant));
        Iterator<String> it = partici.iterator();
        while(it.hasNext())
        {
            String temp = it.next();
            if(complete.contains(temp))
            {
                complete.remove(temp);
            }
            else{
                answer=temp;
                break;
            }
        }
        return answer;
    }
}
```
- Java
```
import java.util.*;
class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer="";
        HashMap<String,Integer> map = new HashMap<>();
        for(String s: completion)
        {
            map.put(s,map.getOrDefault(s,0)+1);
        }
        for(String s: participant)
        {
            map.put(s,map.getOrDefault(s,0)+1);
        }
        for(Entry<String,Integer> s: map.entrySet())
        {
            if(s.getValue()%2!=0)
                answer=s.getKey();
        }
        return answer;
    }
}
```
