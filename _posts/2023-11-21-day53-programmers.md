---
title:  "프로그래머스 Lv.1 Day 53"
excerpt: "자바(java) - 기사단원의 무기"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2023-11-21
last_modified_at: 2023-11-21
---

#### 53. 기사단원의 무기

- **문제 설명** 

숫자나라 기사단의 각 기사에게는 1번부터 `number`까지 번호가 지정되어 있습니다. 기사들은 무기점에서 무기를 구매하려고 합니다.

각 기사는 자신의 기사 번호의 약수 개수에 해당하는 공격력을 가진 무기를 구매하려 합니다. 단, 이웃나라와의 협약에 의해 공격력의 제한수치를 정하고, 제한수치보다 큰 공격력을 가진 무기를 구매해야 하는 기사는 협약기관에서 정한 공격력을 가지는 무기를 구매해야 합니다.

예를 들어, 15번으로 지정된 기사단원은 15의 약수가 1, 3, 5, 15로 4개 이므로, 공격력이 4인 무기를 구매합니다. 만약, 이웃나라와의 협약으로 정해진 공격력의 제한수치가 3이고 제한수치를 초과한 기사가 사용할 무기의 공격력이 2라면, 15번으로 지정된 기사단원은 무기점에서 공격력이 2인 무기를 구매합니다. 무기를 만들 때, 무기의 공격력 1당 1kg의 철이 필요합니다. 그래서 무기점에서 무기를 모두 만들기 위해 필요한 철의 무게를 미리 계산하려 합니다.

기사단원의 수를 나타내는 정수 `number`와 이웃나라와 협약으로 정해진 공격력의 제한수치를 나타내는 정수 `limit`와 제한수치를 초과한 기사가 사용할 무기의 공격력을 나타내는 정수 `power`가 주어졌을 때, 무기점의 주인이 무기를 모두 만들기 위해 필요한 철의 무게를 return 하는 solution 함수를 완성하시오.


- **제한사항**

1 ≤ number ≤ 100,000  
2 ≤ limit ≤ 100  
1 ≤ power ≤ limit

- **입출력 예**

<table class="table">
        <thead><tr>
<th>number</th>
<th>limit</th>
<th>power</th>
<th>result</th>
</tr>
</thead>
        <tbody><tr>
<td>5</td>
<td>3</td>
<td>2</td>
<td>10</td>
</tr>
<tr>
<td>10</td>
<td>3</td>
<td>2</td>
<td>21</td>
</tr>
</tbody>
      </table>

- **입출력 예 설명**

입출력 예 #1

1부터 5까지의 약수의 개수는 순서대로 [1, 2, 2, 3, 2]개입니다. 모두 공격력 제한 수치인 3을 넘지 않기 때문에 필요한 철의 무게는 해당 수들의 합인 10이 됩니다. 따라서 10을 return 합니다.

입출력 예 #2

1부터 10까지의 약수의 개수는 순서대로 [1, 2, 2, 3, 2, 4, 2, 4, 3, 4]개입니다. 공격력의 제한수치가 3이기 때문에, 6, 8, 10번 기사는 공격력이 2인 무기를 구매합니다. 따라서 해당 수들의 합인 21을 return 합니다.

---

- **My Solution**

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

⭐들어온 순서부터 값이 밑에 쌓이고 위로 또 값이 쌓이는 형식으로 Stack 구조와 유사하다. 따라서 stack을 선언한 뒤 처음 값과 비교할 대상이 필요하므로 0을 넣어준다.

moves의 길이와 board의 길이만큼 이중 for문을 통해 `board[j][moves[i]-1]`을 검사한다. 만약 0이라면 인형이 없는 것이기 때문에 넘어가고, 0이 아니라면 Stack의 가장 윗 요소와 `board[j][move-1]`가 같은지 비교한다. 값이 같다면 인형이 사라지는 것이기 때문에 pop을 해주고 answer에 2를 더해준다.

값이 다르다면 Stack에 `board[j][move-1]` 을 push해준다.

⭐ Stack 자료구조에 대한 간단한 메서드

`push(E item)` Stack에 top부분에 삽입한다.

`pop()` top에 있는 item을 삭제하고 item을 반환한다.

`peek()` top에 있는 item을 삭제하지 않고 item을 반환한다.

`empty()` Stack이 비어있으면 true를 그렇지 않으면 false를 반환한다.

`search(Object o)` 해당 Object의 위치를 반환한다.


**프로그래머스 Lv.1 Day 53 기사단원의 무기 - 자바(java)**