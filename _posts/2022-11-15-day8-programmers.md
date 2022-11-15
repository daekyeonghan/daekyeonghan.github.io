---
title:  "프로그래머스 Lv.1 Day 8"
excerpt: "자바(java) - 하샤드 수 "

categories:
  - Blog
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-15
last_modified_at: 2022-11-15
---

#### 8. 하샤드 수


- **문제 설명** 

양의 정수 x가 하샤드 수이려면 x의 자릿수의 합으로 x가 나누어져야 합니다. 예를 들어 18의 자릿수 합은 1+8=9이고, 18은 9로 나누어 떨어지므로 18은 하샤드 수입니다. 자연수 x를 입력받아 x가 하샤드 수인지 아닌지 검사하는 함수, solution을 완성해주세요.

- **제한 사항**

`x`는 1 이상, 10000 이하인 정수입니다.

- **입출력 예**

입출력 예 #1
10의 모든 자릿수의 합은 1입니다. 10은 1로 나누어 떨어지므로 10은 하샤드 수입니다.

입출력 예 #2
12의 모든 자릿수의 합은 3입니다. 12는 3으로 나누어 떨어지므로 12는 하샤드 수입니다.

입출력 예 #3
11의 모든 자릿수의 합은 2입니다. 11은 2로 나누어 떨어지지 않으므로 11는 하샤드 수가 아닙니다.

입출력 예 #4
13의 모든 자릿수의 합은 4입니다. 13은 4로 나누어 떨어지지 않으므로 13은 하샤드 수가 아닙니다.



- **My Solution**

```java
class Solution {
    public boolean solution(int x) {
        boolean answer = true;
        String str = String.valueOf(x);
        String [] arr = str.split("");
        int sum =0;
        
        for(String i : arr ) {
            sum += Integer.parseInt(i);
        }
        return (x % sum == 0 ? true : false);
        
    }
}
```
정수형 x값을 문자열로 변환해준 뒤 하나씩 배열에 넣어줬다. 합을 저장할 변수 sum을 선언해주고 배열의 끝까지 값이 나올 때까지 반복문을 실행하며 그 값들을 더해줬다. 배열에 저장된 값은 문자열 값이기 때문에 Integer클래스의 parseInt() 메서드를 이용해 문자열을 정수로 변환해준 뒤 합을 구했다. 삼항연산자를 이용해 하샤드 수인지 아닌지 판별해줬다.

⭐

- **Other Solution**

```java
class Solution {
    public boolean solution(int x) {
            int num = x;
            int sum=0;
            
            while(num != 0) {
                sum += num%10;
                num/=10;
            }
            return (x % sum == 0 ? true : false);
    }	
}
```
자릿수를 구해서 활용하는 문제가 계속해서 나오고있다. 10으로 나눴을 때 나머지값이 그 수의 자릿수를 구하는 공식이다. 

⭐

**프로그래머스 Lv.1 Day 8 하샤드 수 - 자바(java)**