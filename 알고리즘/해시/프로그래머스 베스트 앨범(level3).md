https://school.programmers.co.kr/learn/courses/30/lessons/42579
의
## 풀이
HashMap<String,Integer>와 HashMap<String,PriorityQueue\<Object\>> 두개를 사용하여 해결<br>
첫 해시맵에는 장르와 플레이 수를 저장하고 두번 째 해시맵 value로 PriorityQueue를 사용했다 비교 기준 플레이 횟수(내림차순)->인덱스 번호(오름차순)<br>
처음에는 각 장르의 곡이 1개인 경우를 고려하지 못해 틀렸으나 해결하고 통과했다
- Java
```
import java.util.*;
class pni implements Comparable<pni>{//플레이수 인덱스
    int plays;
    int index;
    pni(int plays,int index)
    {
        this.plays=plays;
        this.index=index;
    }
    @Override 
    public int compareTo(pni other) {
        if (this.plays != other.plays) {
            return Integer.compare(other.plays, this.plays);
        }
        return Integer.compare(this.index, other.index);
    }
}
class Solution {
    public int[] solution(String[] genres, int[] plays) {
        HashMap<String,Integer> gnp = new HashMap<>();//장르,플레이 횟수
        for(int i=0;i<genres.length;i++)
        {
            gnp.put(genres[i],gnp.getOrDefault(genres[i],0)+plays[i]);
        }
        List<String> key = new ArrayList(gnp.keySet());
        key.sort((o1,o2)->gnp.get(o2).compareTo(gnp.get(o1)));
        HashMap<String,PriorityQueue<pni>> gni = new HashMap<>();//장르,인덱스
        for(int i=0;i<genres.length;i++)
        {
            PriorityQueue<pni> pq = gni.getOrDefault(genres[i],new PriorityQueue<pni>());
            pq.add(new pni(plays[i],i));
            gni.put(genres[i],pq);
        }
        int index=0;
        int limit=key.size()*2;
        int loop=0;
        int answerSize=0;
        for(String genre : key)
        {
            PriorityQueue<pni> pq = gni.get(genre);
            answerSize+=pq.size()>1?2:1;
        }
        int [] answer = new int[answerSize];
        for(String genre : key)
        {
            PriorityQueue<pni> pq = gni.get(genre);
            int k=0;
            int pqSize=pq.size();
            while(!pq.isEmpty()&&k<Math.min(pqSize,2)&&loop<limit)
            {
                answer[index]=pq.poll().index;
                index+=1;
                k+=1;
                loop+=1;
            }   
        }
        return answer;
    }
}
```
한번 생각해볼 다른 사람의 풀이
- 스트림
```
import java.util.List;
import java.util.stream.Collectors;
import java.util.stream.IntStream;

public class Solution {
  public class Music implements Comparable<Music>{

    private int played;
    private int id;
    private String genre;

    public Music(String genre, int played, int id) {
      this.genre = genre; 
      this.played = played;
      this.id = id;
    }

    @Override
    public int compareTo(Music other) {
      if(this.played == other.played) return this.id - other.id;
      return other.played - this.played;
    }

    public String getGenre() {return genre;}
  }

  public int[] solution(String[] genres, int[] plays) {
    return IntStream.range(0, genres.length)
    .mapToObj(i -> new Music(genres[i], plays[i], i))
    .collect(Collectors.groupingBy(Music::getGenre))
    .entrySet().stream()
    .sorted((a, b) -> sum(b.getValue()) - sum(a.getValue()))
    .flatMap(x->x.getValue().stream().sorted().limit(2))
    .mapToInt(x->x.id).toArray();
  }

  private int sum(List<Music> value) {
    int answer = 0;
    for (Music music : value) {
      answer+=music.played;
    }
    return answer;
  }
}
```
이 풀이 외에도 다른사람 풀이 보기에서 더 읽어볼 것
