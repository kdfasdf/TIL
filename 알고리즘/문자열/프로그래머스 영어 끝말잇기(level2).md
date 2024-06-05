https://school.programmers.co.kr/learn/courses/30/lessons/12981

## 풀이
첫 단어는 미리 check에 넣어두고 끝말잇기 규칙에 맞게 구현 이미 있는 단어를 말했는지 확인하기 위해 ArrayList contains를 사용해 확인했지만
set을 이용한 풀이도 가능하다
- Java
```
import java.util.*;
class Solution {
    static ArrayList<String> check= new ArrayList<>();
    public int[] solution(int n, String[] words) {
        int[] answer = {0,0};
        int temp=1; //사람
        int num=1;  //몇번째
        int i=1;
        check.add(words[0]);
        for(i=1;i<words.length;i++)
        {
            temp+=1;
            if(temp%(n+1)==0){
                temp=1;
                num+=1;
            }
            if(words[i].charAt(0)==words[i-1].charAt(words[i-1].length()-1) && !check.contains(words[i]))
            {
                check.add(words[i]);
            }
            else {
                break;
        }
        }
        if(i==words.length)
        {}
        else
        {answer[0]=temp;
        answer[1]=num;}
        // [실행] 버튼을 누르면 출력 값을 볼 수 있습니다. 
        System.out.println("Hello Java");

        return answer;
    }
}
```
-
