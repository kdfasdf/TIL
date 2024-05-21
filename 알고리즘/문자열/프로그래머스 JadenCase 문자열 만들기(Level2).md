https://school.programmers.co.kr/learn/courses/30/lessons/12951

## 풀이
단어의 첫 글자는 대문자로 나머지는 소문자로 바꿔주면 되는 문제 
처음 풀이가 나의 풀이고 다른사람들의 몇가지 좋은 풀이가 있어 기록한다.
- Java
```
class Solution {
    public String solution(String s) {
        String answer = "";
        if(s.charAt(0)>=97)
            answer+=(char)(s.charAt(0)-32);
        else
            answer+=s.charAt(0);
        for (int i=1; i<s.length();i++){
            if(s.charAt(i)!=' ' && s.charAt(i-1)==' ' )
                if (s.charAt(i)>=97)
                    answer+=(char)(s.charAt(i)-32);
                else
                    answer+=s.charAt(i);
            else if(s.charAt(i)<97 && s.charAt(i)>=65)
                answer+=(char)(s.charAt(i)+32);
            else
                answer+=s.charAt(i);
        }
        return answer;
    }
}
```

- 추천 제일 많은 풀이
```
class Solution {
    public String solution(String s) {
        String answer = "";
        String[] data=s.toLowerCase().split("");
        boolean flag = true;
        for(String i: data){
            answer+=flag? i.toUpperCase():i;
            flag=i.equals(" ")?true:false;
        }
        return answer;
    }
}
```

- 그 다음으로 추천 많은 풀이
```
import java.util.regex.*;

class Solution {
    public String solution(String s) {
        Matcher m = Pattern.compile("\\b([\\w])([\\w]*)").matcher(s);
        while (m.find()) {
            s = s.replaceAll("\\b" + m.group(), m.group(1).toUpperCase() + m.group(2).toLowerCase());
        }
        return s;
    }
}
```
