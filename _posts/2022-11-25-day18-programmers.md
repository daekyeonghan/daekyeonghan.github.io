---
title:  "프로그래머스 Lv.1 Day 18"
excerpt: "자바(java) - 음양 더하기"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-25
last_modified_at: 2022-11-25
---

#### 18. 음양 더하기



- **문제 설명** 

어떤 정수들이 있습니다. 이 정수들의 절댓값을 차례대로 담은 정수 배열 absolutes와 이 정수들의 부호를 차례대로 담은 불리언 배열 signs가 매개변수로 주어집니다. 실제 정수들의 합을 구하여 return 하도록 solution 함수를 완성해주세요.

- **제한 사항**

absolutes의 길이는 1 이상 1,000 이하입니다.
absolutes의 모든 수는 각각 1 이상 1,000 이하입니다.
signs의 길이는 absolutes의 길이와 같습니다.
signs[i] 가 참이면 absolutes[i] 의 실제 정수가 양수임을, 그렇지 않으면 음수임을 의미합니다.




- **입출력 예**

|absolutes|signs|result|
|:---:|:---:|:---:|
|[4,7,12]|[true,false,true]|9|
|[1,2,3]|[false,false,true]|0|


- **My Solution**

```java
class Solution {
    public int solution(int[] absolutes, boolean[] signs) {
        int answer = 0;
        int value = absolutes.length;
    
        for(int i=0; i<value; i++) {
            if(signs[i] == true) {
                absolutes[i] = absolutes[i] * 1;
            }else {
                absolutes[i] = absolutes[i] * -1;
            }
        }
        for(int i=0; i<value; i++) {
            answer += absolutes[i];
        }
        return answer;
    }
}
```

⭐첫번째 for문에서는 boolean 배열의 값 중 true이면 양수, false이면 음수가 되도록 했고, 두번째 for문에서는 absolutes배열의 모든 값들을 더해줬다.


**프로그래머스 Lv.1 Day 18 음양 더하기 - 자바(java)**