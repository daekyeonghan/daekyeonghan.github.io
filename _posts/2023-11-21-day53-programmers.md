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

각 기사 1번부터 number 까지 번호가 지정

무기점에서 무기 구매

자신의 기사 번호의 약수 개수에 해당하는 공격력을 가진 무기를 구매함

(이웃나라와의 협약에 의해 공격력의 제한수치를 정하고, 제한수치보다 큰 공격력을 가진 무기를 구매해야 하는 기사는
협약기관에서 정한 공격력을 가지는 무기를 구매해야 함)

EX) 15번으로 지정된 기사단원은 15의 약수가 1,3,5,15로 4개 이므로 공격력이 4인 무기를 구매

이웃나라와의 협약으로 정해진 공격력의 제한수치가 3이고
제한수치를 초과한 기사가 사용할 무기의 공격력이 2라면
15번으로 지정된 기사단원은 무기점에서 공격력이 2인 무기를 구매함

무기를 만들 때 무기의 공격력 1당 1kg의 철이 필요함

Q. 무기점에서 무기를 모두 만들기 위해 필요한 철의 무게를 미리 계산

기사단원의 수를 나타내는 정수 - `number`  
이웃나라와 협약으로 정해진 공격력의 제한수치를 나타내는 정수 - `limit`  
제한수치를 초과한 기사가 사용할 무기의 공격력을 나타내는 정수 - `power`  

- **My Solution**

```java
import java.util.Arrays;

class Solution {
    public int solution(int number, int limit, int power) {
        int answer = 0;
        int [] array = new int[number];
        int cnt = 0;
        for(int i=1; i<=number; i++) {
            for(int j=1; j<=i; j++) {
                if(i%j == 0) {
                    cnt++;
                }
            }
            if(cnt > limit) {
                cnt = power;
            }
            array[i-1] = cnt;
            answer += array[i-1];
            cnt = 0;
        }
        return answer;
    }
}
```
⭐ 첫 번째 풀이

1부터 number로 주어진 값 까지 반복문을 돌면서
약수를 구하고 그 갯수를 새 배열에 넣어준다.

새 배열에 넣어줄 때 limit 보다 크다면 power의 값이 들어가게 한다

배열에 들어간 값들을 더해주면 끝

⭐ 결과

![image](https://github.com/daekyeonghan/daekyeonghan.github.io/assets/117332830/27bc84eb-58b9-497f-8f8b-0c6deaa5ee5c)

시간 초과로 실패 하였다.





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

⭐ 최종

값이 나오는 대로 바로 더해주면 되기 때문에 배열을 사용할 필요가 없었다. 배열을 지우고 최종 제출해도 똑같이 시간초과로 실패가 나왔다. 약수 구하는 알고리즘에 변화를 주어야했다. 처음으로 생각했던 방법은 1부터 number까지 전부 검증을 해봐야하기 때문에 실행시간이 O(n)으로 number 값이 작을 땐 효율적이지만 number 값이 커지면 아주 비효율적이다.

number의 약수가 1일 때 다른 약수는 number/1이 되므로 다른 하나의 약수는 number가 된다. 제곱근을 기준으로 나눗셈을 절반만 실행하면 훨씬 빠른 계산 결과를 얻을 수 있다. 그 후 * 2를 해주면 된다. 이렇게 되면 실행시간이 O(√n)으로 단축된다.



**프로그래머스 Lv.1 Day 53 기사단원의 무기 - 자바(java)**