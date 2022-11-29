---
title:  "프로그래머스스쿨 코딩테스트 연습"
excerpt: "자주 등장하는 메소드들 "

categories:
  - Programmers
tags:
  - [Blog, Study]

toc: true
toc_sticky: true
 
date: 2022-11-29
last_modified_at: 2022-11-29
---

### 프로그래머스스쿨 코딩테스트 연습

#### 자주 등장하는 메소드들 정리



##### 1. StringBuffer클래스와 StringBuilder클래스

String클래스는 인스턴스를 생성할 때 지정된 문자열을 변경할 수 없지만 StringBuffer클래스는 변경이 가능하다. 내부적으로 문자열 편집을 위한 버퍼를 가지고 있으며 인스턴스를 생성할 때 그 크기를 지정할 수 있다.

`StringBuffer`클래스는 String클래스와 같이 문자열을 저장하기 위한 char형 배열의 참조변수를 인스턴스변수로 선언해 놓고 있다. StringBuffer인스턴스가 생성될 때, char형 배열이 생성되며 이 때 생성된 char형 배열을 인스턴스변수 value가 참조한다.


▶️ 1-1 StringBuffer의 생성자

- StringBuffer(String str)
```java
StringBuffer sb = new StringBuffer("abc");
```
지정된 문자열 값("abc")을 갖는 StringBuffer 인스턴스를 생성한다.

- StringBuffer(int length)
```java
StringBuffer sb = new StringBuffer(10);
```
지정된 개수의 문자를 담을 수 있는 버퍼를 가진 StringBuffer 인스턴스를 생성한다.


- char charAt(int index)
```java
StringBuffer sb = new StringBuffer("abc");
char c = sb.charAt(2);
```
지정된 위치(index)에 있는 문자를 반환

- StringBuffer reverse()
```java
StringBuffer sb = new StringBuffer("0123456");
sb.reverse();
```
출력값 : `"6543210"`
StringBuffer인스턴스에 저장되어 있는 문자열의 순서를 거꾸로 나열한다.


- String toString()
```java
StringBuffer sb = new StringBuffer("0123456");
String str = sb.toString();
```
출력값 : `str = "0123456"`
StringBuffer인스턴스의 문자열을 String으로 변환해준다.


- String substring(int start), String substring(int start, int end)
```java
StringBuffer sb = new StringBuffer("0123456");
String str = sb.subString(3);
String str2 = sb.subString(3,5);
```
지정된 범위 내의 문자열을 String으로 뽑아서 반환한다. 시작위치(start)만 지정하면 시작위치부터 문자열 끝까지 뽑아서 반환한다.

▶️ StringBuilder 클래스  
StringBuffer는 멀티쓰레드에 안전하도록 동기화되어있다. StringBuffer에서 쓰레드의 동기화만 뺀것, 두 클래스는 완전히 똑같은 기능으로 작성되어 있다.
쓰레드에 관련해서는 다음에 정리해보도록 하자!