---
title:  "프로그래머스 Lv.1 Day 54"
excerpt: "자바(java) - 명예의 전당 (1)"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2023-11-22
last_modified_at: 2023-11-22
---

#### 54. 명예의 전당 (1)

- **문제 설명** 

"명예의 전당"이라는 TV 프로그램에서는 매일 1명의 가수가 노래를 부르고, 시청자들의 문자 투표수로 가수에게 점수를 부여합니다. 매일 출연한 가수의 점수가 지금까지 출연 가수들의 점수 중 상위 k번째 이내이면 해당 가수의 점수를 명예의 전당이라는 목록에 올려 기념합니다. 즉 프로그램 시작 이후 초기에 k일까지는 모든 출연 가수의 점수가 명예의 전당에 오르게 됩니다. k일 다음부터는 출연 가수의 점수가 기존의 명예의 전당 목록의 k번째 순위의 가수 점수보다 더 높으면, 출연 가수의 점수가 명예의 전당에 오르게 되고 기존의 k번째 순위의 점수는 명예의 전당에서 내려오게 됩니다.

이 프로그램에서는 매일 "명예의 전당"의 최하위 점수를 발표합니다. 예를 들어, k = 3이고, 7일 동안 진행된 가수의 점수가 [10, 100, 20, 150, 1, 100, 200]이라면, 명예의 전당에서 발표된 점수는 아래의 그림과 같이 [10, 10, 10, 20, 20, 100, 100]입니다.

![image](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/57bc9bea-73f6-4948-a36c-d344a0501ab2)

명예의 전당 목록의 점수의 개수 k, 1일부터 마지막 날까지 출연한 가수들의 점수인 score가 주어졌을 때, 매일 발표된 명예의 전당의 최하위 점수를 return하는 solution 함수를 완성해주세요.


- **제한사항**

3 ≤ k ≤ 100  
7 ≤ score의 길이 ≤ 1,000  
0 ≤ score[i] ≤ 2,000

- **입출력 예**

<table class="table">
        <thead><tr>
<th>k</th>
<th>score</th>
<th>result</th>
</tr>
</thead>
        <tbody><tr>
<td>3</td>
<td>[10, 100, 20, 150, 1, 100, 200]</td>
<td>[10, 10, 10, 20, 20, 100, 100]</td>
</tr>
<tr>
<td>4</td>
<td>[0, 300, 40, 300, 20, 70, 150, 50, 500, 1000]</td>
<td>[0, 0, 0, 0, 20, 40, 70, 70, 150, 300]</td>
</tr>
</tbody>
      </table>

- **입출력 예 설명**

입출력 예 #2

아래와 같이, [0, 0, 0, 0, 20, 40, 70, 70, 150, 300]을 return합니다.

![image](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/d73682cd-0d34-4ec0-be93-0068e73e7d29)


---

매일 1명의 가수가 노래를 부르고
시청자들의 문자 투표수로 점수가 부여됨

매일 출연한 가수의 점수가 지금까지 출연 가수들의 점수 중 상위 k번째 이내이면
해당가수의 점수를 명예의 전당이라는 목록에 올려 기념

즉, 프로그램 시작 이후 초기에 k일까지는 모든 출연 가수의 점수가 명예의 전당에 오르게 됨

k일 다음부터는 출연 가수의 점수가 기존의 명예의 전당 목록의 k번째 순위의 가수 점수보다 더 높으면,
출연 가수의 점수가 명예의 전당에 오르게 되고 기존의 k번째 순위의 점수는 명예의 전당에서 내려오게 됨

매일 최하위 점수를 발표함

EX) k = 3 이고 7일동안 진행된 가수의 점수가 [10, 100, 20, 150, 1, 200]이라면
명예의 전당에서 발표된 점수는 아래의 그림과 같이 [10, 10, 10, 20, 20, 100, 100] 입니다.

Q. 명예의 전당 목록의 점수의 개수k, 1일부터 마지막 날까지 출연한 가수들의 점수인 score가 주어졌을 때,
매일 발표된 명예의 전당의 최하위 점수를 return



- **My Solution**

```java
import java.util.*;

class Solution {
    public int[] solution(int k, int[] score) {
        int[] answer = new int [score.length];
        List<Integer> list = new ArrayList<>();
        
        for(int i=0; i < score.length; i++) {
            if(list.size() < k) {
                list.add(score[i]);
            }
            else {
                if(list.get(0) < score[i]) list.set(0, score[i]);
            }
            
            Collections.sort(list);
            answer[i] = list.get(0);
        }
        
        return answer;
    }
}
```
⭐
list를 만들어 주고 score의 길이만큼 반복문을 돌려준다.
list의 크기가 k보다 커질때까지 score의 값을 하나씩 add 해준다.
그 이후부터는 list의 0번째 값과 score 배열의 i번째 값과 비교해주면서 score 배열의 값이 더 크다면 0번째의 값을 그 값으로 바꿔준다.
`Collection.sort(list)`로 list 안에 값들을 정렬해주고 작은 값을 answer 배열에 넣어주면 된다.

- **Other Solution**

```java
class Solution {
    public int solution(int number, int limit, int power) {
        int answer = 0;
        for(int i=1; i<=number; i++) {
            int cnt = 0;
            for(int j=1; j*j<=i; j++) {
                if(j * j == i) cnt++;
                else if(i%j == 0) cnt += 2;
            }
            
            if(cnt > limit) cnt = power;
            answer += cnt;
        }
        return answer;
    }
}
```

![image](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/38cfd614-cfbc-4635-b92c-689623294027)

⭐ 최종

값이 나오는 대로 바로 더해주면 되기 때문에 배열을 사용할 필요가 없었다. 배열을 지우고 최종 제출해도 똑같이 시간초과로 실패가 나왔다. 약수 구하는 알고리즘에 변화를 주어야했다. 처음으로 생각했던 방법은 1부터 number까지 전부 검증을 해봐야하기 때문에 실행시간이 O(n)으로 number 값이 작을 땐 효율적이지만 number 값이 커지면 아주 비효율적이다.

number의 약수가 1일 때 다른 약수는 number/1이 되므로 다른 하나의 약수는 number가 된다. 제곱근을 기준으로 나눗셈을 절반만 실행하면 훨씬 빠른 계산 결과를 얻을 수 있다. 그 후 * 2를 해주면 된다. 이렇게 되면 실행시간이 O(√n)으로 단축된다.



**프로그래머스 Lv.1 Day 54 명예의 전당 (1) - 자바(java)**