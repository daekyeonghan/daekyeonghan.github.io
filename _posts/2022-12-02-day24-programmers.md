---
title:  "프로그래머스 Lv.1 Day 24"
excerpt: "자바(java) - 약수의 개수와 덧셈 "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-02
last_modified_at: 2022-12-02
---

#### 24. 약수의 개수와 덧셈


- **문제 설명** 

두 정수 left와 right가 매개변수로 주어집니다. left부터 right까지의 모든 수들 중에서, 약수의 개수가 짝수인 수는 더하고, 약수의 개수가 홀수인 수는 뺀 수를 return 하도록 solution 함수를 완성해주세요.

- **제한 사항**

1 ≤ left ≤ right ≤ 1,000

- **입출력 예**

|**left**|**right**|**result**|
|:---:|:---:|:---:|
|13|17|43|
|24|27|52|



- **My Solution**

```java
class Solution {
    public int solution(int left, int right) {
        int answer = 0;
        for(int i=left; i<=right; i++) {
            int cnt = 0;
            for(int j=1; j<=i; j++) {
                if(i%j == 0) {
                    ++cnt;
                }
            }
            if(cnt%2==0) {
                answer += i;
            }else {
                answer -= i;
            }
        }
        return answer;
    }
}
```

⭐ 이중 for문으로 간단하게 구현했습니다. 첫번째 for문에서는 시작값으로 left값, 마지막 값으로 right값을 조건으로 했습니다. 두번째 for문에서는 약수를 구해줬고 그 약수의 갯수대로 카운트값을 증가시켜줬습니다. 카운트 값이 짝수 일때는 더해주고 홀수 일때는 빼줘 최종 값을 반환해줬습니다.

**프로그래머스 Lv.1 Day 24 약수의 개수와 덧셈 - 자바(java)**