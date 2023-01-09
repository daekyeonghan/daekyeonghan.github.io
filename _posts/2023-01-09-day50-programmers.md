---
title:  "프로그래머스 Lv.1 Day 50"
excerpt: "자바(java) - 완주하지 못한 선수"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2023-01-08
last_modified_at: 2023-01-08
---

#### 50. 콜라 문제


- **문제 설명** 

수많은 마라톤 선수들이 마라톤에 참여하였습니다. 단 한 명의 선수를 제외하고는 모든 선수가 마라톤을 완주하였습니다.

마라톤에 참여한 선수들의 이름이 담긴 배열 participant와 완주한 선수들의 이름이 담긴 배열 completion이 주어질 때, 완주하지 못한 선수의 이름을 return 하도록 solution 함수를 작성해주세요.


- **제한사항**

마라톤 경기에 참여한 선수의 수는 1명 이상 100,000명 이하입니다.
completion의 길이는 participant의 길이보다 1 작습니다.
참가자의 이름은 1개 이상 20개 이하의 알파벳 소문자로 이루어져 있습니다.
참가자 중에는 동명이인이 있을 수 있습니다.

- **입출력 예**

|**participant**|**completion**|**return**|
|:---:|:---:|:---:|
|["leo", "kiki", "eden"]|["eden", "kiki"]|"leo"|
|["marina", "josipa", "nikola", "vinko", "filipa"]|	["josipa", "filipa", "marina", "nikola"]|	"vinko"|
|["mislav", "stanko", "mislav", "ana"]|["stanko", "ana", "mislav"]|"mislav"|

예제 #1
"leo"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #2
"vinko"는 참여자 명단에는 있지만, 완주자 명단에는 없기 때문에 완주하지 못했습니다.

예제 #3
"mislav"는 참여자 명단에는 두 명이 있지만, 완주자 명단에는 한 명밖에 없기 때문에 한명은 완주하지 못했습니다.

- **My Solution**

```java
import java.util.*;

class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";
        HashMap<String, Integer> hm = new HashMap<>();
        
        for(String key : participant) {
            hm.put(key, hm.getOrDefault(key, 0) + 1);
        }
        
        for(String key : completion) {
            hm.put(key, hm.get(key) - 1);
        }
        
        for(String key : hm.keySet()) {
            if(hm.get(key) != 0) {
                answer = key;
                break;
            }
        }
        return answer;
    }
}
```

⭐ HashMap() 메소드를 이용하여 푸는 문제이다. 참가자 이름을 key 값으로 1을 value로 HashMap에 넣어준다. getOrDefault()메소드로 중복된 key값을 넣어줄 수 있다.

두번째 for문으로 완주자와 같은 참가자(key)의 value값을 -1 해줌으로써 0으로 만들어 줄 수 있다.

최종적으로 value값이 0이 아닐때의 key값 즉 미완주자의 이름을 반환해주면 된다.

⭐ `getOrDefault(Object key, V DefaultValue)`
getOrDefault() 메소드는 key값에 매핑되는 value가 없을때 Default값을 넣겠다는 메소드이다. 

찾는 key가 존재한다면 해당 key에 매핑되어 있는 값을 반환하고, 그렇지 않으면 디폴트 값이 반환된다.

HashMap의 경우 동일 키 값을 추가할 경우 Value의 값이 덮어쓰기가 된다. 따라서 기존 key 값의 value를 계속 사용하고 싶을 경우 getOrDefault 메소드를 사용할 수 있다.

- **Other Solution**

```java
import java.util.Arrays;
class Solution {
    public String solution(String[] participant, String[] completion) {
        String answer = "";

        Arrays.sort(participant);
        Arrays.sort(completion);

        for(int i=0; i<participant.length-1; i++) {
          if(!completion[i].equals(participant[i])) {
            answer = participant[i];
            break;
          }
        }

        return answer;
    }
}
```

⭐HashMap() 메소드를 사용하지 않고 for문만으로도 문제를 풀 수가있다.

Arrays.sort() 메소드를 사용하여 각 배열을 오름차순으로 정렬해준 다음 for문으로 인덱스값을 넣어주고 중복값을 검사한 뒤 중복되지 않는 값이 있다면 완주하지 않은 선수이므로 마라톤에 참여한 선수들의 명단 배열인 participant의 값을 answer에 넣어주고 for문을 종료한다.

**프로그래머스 Lv.1 Day 50 완주하지 못한 선수 - 자바(java)**