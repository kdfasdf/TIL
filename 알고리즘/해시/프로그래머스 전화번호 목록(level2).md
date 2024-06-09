https://school.programmers.co.kr/learn/courses/30/lessons/42577
## 풀이
- phone_book에 있는 전화 번호를 해시맵에 저장
- phone_book에 있는 전화번호를 하나씩 0번째 인덱스에서 끝 인덱스까지의 서브스트링이 해시맵에 있는지 확인한다

- Java
```
import java.util.*;
class Solution {
    public boolean solution(String[] phone_book) {
        Map<String,Integer> map = new HashMap<>();
        for(int i=0;i<phone_book.length;i++){
            map.put(phone_book[i],i);
        }
        for(int i=0;i<phone_book.length;i++){
            for(int j=0;j<phone_book[i].length();j++){
                if(map.containsKey(phone_book[i].substring(0,j)))
                    return false;
            }
        }
        return true;
    }
}
```
