---
title:  "[Java 기본 원리] 기본형과 참조형 타입의 모든 것(+wrapper)"
categories : Java
tag : [java, primitive, reference, memory]
toc: true
toc_sticky: true
author_profile: false
sidebar:
  nav: "docs"
typora-root-url: ../../..
published: true
---



**Java의 데이터 타입은 기본형(primitive type)과 참조형(reference type)으로 나뉜다.**

<br>

<br>

## 기본형과 참조형 타입의 특징 💡

### 기본형(Primitive Type)

- 스택 메모리 사용 -> 실제 값 저장
- 값 복사(깊은 복사) 발생
- 8가지 기본 타입: boolean , byte , char , short , int , long , float, double

```java
boolean flag = true;
byte b = 127;
char c = 'A';
short s = 32767;
int num = 2147483647;
long bigNum = 9223372036854775807l;
float f = 3.14f;
double d = 3.14159265359;
```

<br><br>

### 참조형(Reference Type)

- 스택, 힙 메모리 사용 -> 스택:주소 저장 / 힙:실제 값 저장
- 주소값 복사(얕은 복사) 발생
- 예시: Array, Object, String 등

- 주의: C++의 STL은 깊은 복사가 되는데, Java는 얕은 복사이다. 깊은 복사처럼 보이지만 아니란 걸 꼭 이해하자.

```java
// 주의 -> 깊은 복사처럼 보이는 자바의 String
String a = "hello"; // a : hello
String b = a; // b : &a (a주소값 가지는 중)
a = "world"; // a : world (새로운 메모리 주소에 새로 world 저장) -> 핵심

// 출력 결과 (마치 깊은 복사를 진행한것 같은 효과)
a : world
b : hello
```

<br>

#### Wrapper Class Type

해당 타입은 `Integer, Double, Character, Boolean` 등을 의미한다.  
**기본 데이터 유형을 객체로 감싼 클래스**로 객체 처럼 사용 가능, **참조형 타입**이다!

<br>

<br>

## 4가지 핵심 관점 💡

### 1. 성능 관점

**원시 타입은 스택 영역에 값으로 존재한다.** 

**반면 참조 타입은 스택 영역에는 참조 값만 있고, 실제 값은 힙 영역에 존재한다.**   
참조 타입은 최소 2번 메모리 접근을 해야 하고, 일부 타입(=wrapper)의 경우 값을 필요로 할 때 언박싱 과정(ex. Double → double, Integer → int)을 거쳐야 하므로 원시 타입과 비교해서 접근 속도가 느린 편이다.

```java
// 기본형: 1번의 메모리 접근
int primitive = 10;

// 참조형: 최소 2번의 메모리 접근(wrapper type은 언박싱 필요)
Integer wrapper = 10;
int number = wrapper;  // 언박싱 발생
```

<br><br>

## 2. 메모리 관점

**원시 타입보다 참조 타입이 사용하는 메모리 양이 압도적으로 높다.**  
최근 들어 64 비트의 JVM을 많이 사용하므로 일반적으로 64 bits를 차지한다고 한다.

```java
// 기본형: 정확한 크기
int num = 10;         // 4 bytes
double d = 3.14;      // 8 bytes

// 참조형: 추가 메모리 필요
Integer wrapperNum = 10;  // 16 bytes + 객체 오버헤드
```

<br><br>

## 3. NULL 관점

**원시 타입은 null을 담을 수 없지만, 참조 타입은 null을 담을 수 있다.**   
원시 타입의 경우, 값이 없으면 디폴트 값을 반환하기 때문이다. (ex. int은 0, boolean은 false)

```java
// 기본형: null 불가능, 기본값 존재
int primitive = 0;     // 기본값 0

// 참조형: null 가능
Integer wrapper = null;
String str = null;
```

<br><br>

## 4. 제네릭 관점

원시 타입은 제네릭 타입에서 사용할 수 없지만, 참조 타입은 가능하다.

```java
// 기본형: 제네릭 사용 불가
// List<int> list = new ArrayList<>();  // 컴파일 에러

// 참조형: 제네릭 사용 가능
List<Integer> list = new ArrayList<>();
list.add(10);
```
