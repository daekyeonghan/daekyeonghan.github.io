---
title:  "프로그래머스 Lv.1 Day 4"
excerpt: "자바(java) - 자릿수 더하기 "

categories:
  - Blog
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-11-10
last_modified_at: 2022-11-10
---

#### 4. 자릿수 더하기


- **문제 설명** 

자연수 N이 주어지면, N의 각 자릿수의 합을 구해서 return 하는 solution 함수를 만들어 주세요.
예를들어 N = 123이면 1 + 2 + 3 = 6을 return 하면 됩니다.

- **제한 사항**

N의 범위 : 100,000,000 이하의 자연수

- **입출력 예**

|**N**|**answer**|
|:---:|:---:|
|123|6|
|987|24|

입출력 예 #1
문제의 예시와 같습니다.

입출력 예 #2
9 + 8 + 7 = 24이므로 24를 return 하면 됩니다.

- **My Solution**

```java
class Solution {
    public int solution(int n) {
        int n = 0;
        System.out.println("풀지 못함");
    }
}
```
n값이 들어왔을 때 문자열로 변환해주고
하나씩 자른 후 다시 정수형으로 변환해주면서
합을 구하는 방식으로 코드를 짜려 했으나
구현 능력이 부족해 하지 못했다.

- **Solution**

```java
import java.util.*;

public class Solution {
    public int solution(int n) {
        int answer = 0;
        String str = Integer.toString(n);
        
        for(int i=0; i<str.length(); i++) {
            answer += Integer.parseInt(str.substring(i,i+1));
        }

        return answer;
    }
}
```
생각을 토대로 구현해보면, 정수형 n 값을 String으로 변환해주고 그 문자열의 길이만큼 반복문을 수행하면서 다시 substring으로 자른 후 정수형으로 변환해 더하는 방식이다.


- **Other Solution 1**

```java
class Solution {
    public int solution(int n) {
        int answer = 0;
        
        while(n > 0) {
            answer += n%10;
            n/=10;
        }
        return answer;
    }
}

```

정수형 n 값을 10으로 나눈 나머지가 1의 자릿수가 된다.
이것을 반복하면 자릿수의 합을 구할 수 있다. 

- **Other Solution 2**

```java
class Solution {
	public int solution(int n) {
		int answer = 0;
		String [] arr = String.valueOf(n).split("");
		
		for(String a : arr) {
			answer += Integer.parseInt(a);
		}
		return answer;
	}
}
```

배열을 선언해 split함수로 하나씩 뽑아주고 합을 구할 수 있다.

**프로그래머스 Lv.1 Day 4 자릿수 더하기 - 자바(java)**