https://school.programmers.co.kr/learn/courses/30/lessons/49993

## 풀이
Hashset을 사용하여 풀이 
1. 스킬순서를 해시셋에 저장
2. 스킬트리를 한 문자 단위로 탐색
3. 스킬트리의 특정 인덱스의 문자가 해시셋에 존재하면 스킬의 순서에 맞게 나왔는지 확인


- Java
```
import java.util.*;
class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer=0;
        for(int i=0;i<skill_trees.length;i++)
        {
            int index=0;
            boolean flag = true;
            HashSet set = new HashSet();
            for(int j=0;j<skill.length();j++)
                set.add(skill.charAt(j));
            for(int j=0;j<skill_trees[i].length();j++)   
            {
                if(set.contains(skill_trees[i].charAt(j))) //해시셋에 스킬트리 특정 순서의 스킬이 있으면
                   {
                        System.out.println(skill_trees[i].charAt(j));
                       if (skill.charAt(index)!=skill_trees[i].charAt(j))// 순서 확인
                       {
                           flag=false;
                           break;
                       }
                        else{
                            if(index<skill.length())
                                index+=1;
                            else break;
                        }
                           
                   }
            }
            System.out.println();
            if(flag) answer+=1;
        }
        return answer;
    }
}
```
해시셋을 사용하지 않고 비슷한 알고리즘으로 풀이할 수 있었다
```
class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer = 0;
        for (String skillTree : skill_trees) {
            int learningIdx = 0;
            boolean isAble = true;
            for (char curSkill : skillTree.toCharArray()) {
                int skillIdx = skill.indexOf(curSkill);
                if (skillIdx == -1)
                    continue;
                else if (skillIdx == learningIdx)
                    learningIdx++;
                else {
                    isAble = false;
                    break;
                }
            }
            if (isAble)
                answer++;
        }
        return answer;
    }
}
```

<br>
정규식을 활용하면 간략하게 풀 수 있었다
- 정규표현식

```
import java.util.*;

class Solution {
    public int solution(String skill, String[] skill_trees) {
        int answer = 0;
        ArrayList<String> skillTrees = new ArrayList<String>(Arrays.asList(skill_trees));
        //ArrayList<String> skillTrees = new ArrayList<String>();
        Iterator<String> it = skillTrees.iterator();

        while (it.hasNext()) {
            if (skill.indexOf(it.next().replaceAll("[^" + skill + "]", "")) != 0) {
                it.remove();
            }
        }
        answer = skillTrees.size();
        return answer;
    }
}
```
