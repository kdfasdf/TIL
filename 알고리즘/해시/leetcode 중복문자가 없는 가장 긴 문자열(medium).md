https://leetcode.com/problems/longest-substring-without-repeating-characters/submissions/1300341871/
## 풀이 
HashSet과 투포인터를 확인하여 풀이 <br>
rpointer부터 문자열을 하나씩 순서대로 탐색해나가는데 rpointer가 가르키는 문자가 HashSet에 없으면 추가하고 
있다면 lpointer를 하나 움직이고 hashset 안에 lpointer가 움직이기 전에 가르키던 문자를 삭제한다
길이는 rpointer를 움직이기 전 answer에 answer값과 rpointer-lpointer+1중 더 큰 값을 할당한다
```
import java.util.*;
class Solution {
    public int lengthOfLongestSubstring(String s) {
        int answer=0;
        HashSet<Character> set  = new HashSet<>();
        int rPointer=0;
        int lPointer=0;
        while(rPointer!=s.length())
        {
            if(!set.contains(s.charAt(rPointer))){
                set.add(s.charAt(rPointer));
                answer=Math.max(answer,rPointer-lPointer+1);
                rPointer+=1;
            }
            else{
                set.remove(s.charAt(lPointer));
                lPointer+=1;
            }
        }
        return answer;
    }
}
```

런타임(O(n))
![image](https://github.com/kdfasdf/TIL/assets/96770726/778baed3-c191-4356-8b7c-7bd8e4802863)

메모리(O(min(m,n))(HashSet에 저장될 수 있는 서로 다른 문자,문자열 길이)

![image](https://github.com/kdfasdf/TIL/assets/96770726/5f282bb8-b35b-4d96-8bea-2ca794144a0e)

메모리 사용량은 같은 코드를 넣어도 결과가 조금씩 다르게 나오므로 의미가 없는 것 같다

## 다른 풀이
HashMap을 사용하여 문자를 key 값으로 투포인터 인덱스를 value값으로 사용한 풀이 HashSet을 사용할 떄와 비교되는 점은 HashSet에서 중복 문자가 판별되면 left를 하나씩 옮겨가며 제거했지만 HashMap은 left의 인덱스가 저장되어있기 떄문에 바로 left가 중복문자 인덱스를 가르킬 수 있다.
```
import java.util.*;
class Solution {
    public int lengthOfLongestSubstring(String s) {
        HashMap<Character,Integer> used = new HashMap<>();
        int maxLength=0;
        int left=0;
        int right=0;
        for(char c: s.toCharArray())
        {
            if(used.containsKey(c)&&left<=used.get(c)){
                left=used.get(c)+1;
            }
            else{
                maxLength=Math.max(maxLength,right-left+1);
            }
            used.put(c,right);
            right++;
        }
        return maxLength;
    }
}
```

