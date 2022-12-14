---
title:  "프로그래머스 Lv.1 Day 35"
excerpt: "자바(java) - 문자열 내 마음대로 정렬하기"

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-14
last_modified_at: 2022-12-14
---

#### 35. 문자열 내 마음대로 정렬하기


- **문제 설명** 

문자열로 구성된 리스트 strings와, 정수 n이 주어졌을 때, 각 문자열의 인덱스 n번째 글자를 기준으로 오름차순 정렬하려 합니다. 예를 들어 strings가 ["sun", "bed", "car"]이고 n이 1이면 각 단어의 인덱스 1의 문자 "u", "e", "a"로 strings를 정렬합니다.


- **제한 조건**

strings는 길이 1 이상, 50이하인 배열입니다.
strings의 원소는 소문자 알파벳으로 이루어져 있습니다.
strings의 원소는 길이 1 이상, 100이하인 문자열입니다.
모든 strings의 원소의 길이는 n보다 큽니다.
인덱스 1의 문자가 같은 문자열이 여럿 일 경우, 사전순으로 앞선 문자열이 앞쪽에 위치합니다.

- **입출력 예**

|**strings**|**n**|**return**|
|:---:|:---:|:---:|
|["sun", "bed", "car"]|1|["car", "bed", "sun"]|
|["abce", "abcd", "cdx"]|2|["abcd", "abce", "cdx"]|

입출력 예 설명

입출력 예 1
"sun", "bed", "car"의 1번째 인덱스 값은 각각 "u", "e", "a" 입니다. 이를 기준으로 strings를 정렬하면 ["car", "bed", "sun"] 입니다.

입출력 예 2
"abce"와 "abcd", "cdx"의 2번째 인덱스 값은 "c", "c", "x"입니다. 따라서 정렬 후에는 "cdx"가 가장 뒤에 위치합니다. "abce"와 "abcd"는 사전순으로 정렬하면 "abcd"가 우선하므로, 답은 ["abcd", "abce", "cdx"] 입니다.


- **My Solution**

```java
import java.util.Arrays;

class Solution {
    public String[] solution(String[] strings, int n) {
        String[] answer = new String[strings.length];
        
        for(int i=0; i<strings.length; i++) {
            strings[i] = strings[i].charAt(n) + strings[i];
        }
        
        Arrays.sort(strings);
        
        for(int i=0; i<strings.length; i++) {
            answer[i] = strings[i].substring(1);
        }
        
        return answer;
    }
}
```

⭐처음에 생각한건 strings배열에서 인덱스별로 값을 뽑아준 다음 n번째 값을 뽑아서 오름차순 정렬을 해주려고 했지만 그 정렬한 값으로 다시 원래의 단어대로 돌아가는것을 생각해내지 못했다. 계속 생각해본 결과 좋은 방법이 떠올랐다.

⭐먼저 strings.length 만큼 반복문을 실행하고 strings 배열안에 있는 단어들의 n번째 값을 뽑아서 그 단어의 앞에다 붙여주는 것이다. 그리고 sort() 오름차순 메소드를 이용하여 오름차순 정렬해주었다. 그 다음으로 substring() 메소드로 1번째 값부터 즉, 더해준 값 다음 값부터 뽑아서 answer배열에 담아줬다. 그리고 answer배열을 반환해주면 문제는 해결된다.

- **Other Solution**

```java

```

⭐


**프로그래머스 Lv.1 Day 35 문자열 내 마음대로 정렬하기 - 자바(java)**