---
title:  "프로그래머스 Lv.1 Day 19"
excerpt: "자바(java) - 없는 숫자 더하기 "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-26
last_modified_at: 2022-11-26
---

#### 19. 없는 숫자 더하기


- **문제 설명** 

0부터 9까지의 숫자 중 일부가 들어있는 정수 배열 numbers가 매개변수로 주어집니다. numbers에서 찾을 수 없는 0부터 9까지의 숫자를 모두 찾아 더한 수를 return 하도록 solution 함수를 완성해주세요.

- **제한 사항**

1 ≤ numbers의 길이 ≤ 9
0 ≤ numbers의 모든 원소 ≤ 9
numbers의 모든 원소는 서로 다릅니다..

- **입출력 예**

|**numbers**|**result**|
|:---:|:---:|
|[1,2,3,4,6,7,8,0]|14|
|[5,8,4,0,6,7,9]|6|

입출력 예 #1

5, 9가 numbers에 없으므로, 5 + 9 = 14를 return 해야 합니다.

입출력 예 #2

1, 2, 3이 numbers에 없으므로, 1 + 2 + 3 = 6을 return 해야 합니다.



- **My Solution**

```java
class Solution {
    public int solution(int[] numbers) {
        int answer = 0;
        for(int i=0; i<=9; i++) {
            for(int j=0; j<numbers.length; j++) {
                if(numbers[j] == i) {
                    break;
                }
                else if(numbers.length - 1 == j) {
                    answer += i;
                }
            }
        }
        return answer;
        }
    }
```

⭐ 이중 for문을 통해서 값을 찾아줬다. 값이 있으면 break로 나와서 다시 첫번쨰 for문으로 돌아가고, 값이 없으면 answer 변수에 그 값을 더해준다.

- **Other Solution**

```java
class Solution {
    public int solution(int[] numbers) {
        int sum = 45;
        for (int i : numbers) {
            sum -= i;
        }
        return sum;
    }
}
```

⭐ 너무 어렵게 생각했나보다.. numbers 배열의 원소의 값은 1부터 9까지라고 정해져있으니 총 합은 45이다. 모든 배열의 원소들의 값을 더해주고 총 합에서 그 더해준 값을 빼면 없는 값들의 합이 나온다...

⭐ for (int i : numbers) 기존의 for문과는 다른 모습으로
for(대입받을 변수정의 : 배열명)으로 구성되어 있다. numbers배열의 항목들을 처음부터 하나씩 실행해준다. 배열을 가지고 반복작업을 할 때 많이 활용되며 단점으로는 배열만 사용가능하며, 값을 직접 바꿀 수는 없다.

**프로그래머스 Lv.1 Day 19 없는 숫자 더하기 - 자바(java)**