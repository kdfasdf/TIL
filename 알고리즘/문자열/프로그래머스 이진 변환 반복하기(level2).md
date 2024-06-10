https://school.programmers.co.kr/learn/courses/30/lessons/70129
## 풀이
삭제하는 0의 개수는 문자열에 replace("0","")을 적용하기 전의 문자열의 길이에 적용 후 문자열의 길이를 빼고 반복문마다 변환 횟수를 1증가시킨다
- Java
```
class Solution {
    public int[] solution(String s) {
        int change=0;
        int delete=0;
        while(!s.equals("1"))
        {
            change+=1;
            delete+=s.length();//0 삭제 전 문자열의 길이
            s=s.replace("0","");
            delete-=s.length();//0 삭제 후 문자열의 길이
            s=Integer.toBinaryString(s.length());//길이를 이진숫자 문자열로 바꿈
        }
        int[] answer={change,delete};
        return answer;
    }
}
```
