https://school.programmers.co.kr/learn/courses/30/lessons/250137

## 풀이 
단순 구현 문제
- Java
```
class Solution {
    public int solution(int[] bandage, int health, int[][] attacks) {
        int answer = health;
        int looptime=attacks[attacks.length-1][0];
        int index=0;
        int time=0;
        for(int i=0;i<=looptime&&index<attacks.length;i++)
        {
            if(time==bandage[0]){
                answer= answer+bandage[2]<=health? answer+bandage[2]:health;
                time=0;
            }
            //공격경우 넣야함
            if(i==attacks[index][0])
            {
                answer-=attacks[index][1];
                if(answer<=0){
                    answer=-1;
                    break;
                }
                index+=1;
                time=0;
            }
            else{
                time+=1;
                answer= answer+bandage[1]<=health? answer+bandage[1]:health;
            }
        }
        return answer;
    }
}
```
