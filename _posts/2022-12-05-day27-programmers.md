---
title:  "프로그래머스 Lv.1 Day 27"
excerpt: "자바(java) - 직사각형 별찍기 "

categories:
  - Programmers
tags:
  - [Blog]

toc: true
toc_sticky: true
 
date: 2022-12-05
last_modified_at: 2022-12-05
---

#### 27. 직사각형 별찍기


- **문제 설명** 

이 문제에는 표준 입력으로 두 개의 정수 n과 m이 주어집니다.
별(*) 문자를 이용해 가로의 길이가 n, 세로의 길이가 m인 직사각형 형태를 출력해보세요.

- **제한 사항**

n과 m은 각각 1000 이하인 자연수입니다.

- **입출력 예**

입력

```
5 3
```

출력
```
*****
*****
*****
```


- **My Solution**

```java
import java.util.Scanner;

class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int a = sc.nextInt();
        int b = sc.nextInt();
        
        for(int i=0; i<b; i++) {
            for(int j=0; j<a; j++) {
                System.out.print("*");
            }
            System.out.println();
        }
    }
}
```

⭐이중 for문으로 구현해줬습니다.


**프로그래머스 Lv.1 Day 27 직사각형 별찍기 - 자바(java)**