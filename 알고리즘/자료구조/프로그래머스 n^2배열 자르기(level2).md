https://school.programmers.co.kr/learn/courses/30/lessons/87390

## 풀이
문제 설명 영상에 2차원 배열에 어떻게 숫자가 들어가는지 나와있다<br>
행과 열 중 더 큰 숫자가 2차원 배열의 같에 들어가는데 행과 열이 각각 i/n, i%n으로 나타낼 수 있으므로(i는 1...n^2)
<br>
그 중 큰 값을 left<=i<=right일 때 1차원 배열에 순서대로 넣어주면 된다<br>
주의할 점은 return 타입이 int고 left, right 매개변수 타입이 long이므로 형변환에 조심해야한다
- Java
```
class Solution {
    public int[] solution(int n, long left, long right) {
        int index=0;
        int[] answer=new int[(int)right-(int)left+1];
        for(long i=left;i<=right;i++){
            answer[index]=Math.max((int)(i/n)+1,((int)(i%n)+1));   //형변환 오류났던 부분(long 끼리 먼저하고 int로 형변환)
            index+=1;}
        return answer;
    }
}
```
