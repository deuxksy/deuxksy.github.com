---
layout: post
title: Java 8 functional interface
date:  2019-02-10 18:29:00 
categories: [java, 8, functional, interface]
---
# Java Funcional Interface

Java Lamda 가 지원 이후로 많이 생겨난 Functioanl Interface 확실히 몰라서 이번에 정리  
외우는것이 육체 건강에 좋음  

## 1. 목차

1. 테스트 예제
2. 참조

## 2. Example

### 2.1 Runnable 리턴 없음 인자 없음

```java
  public void 리턴_X_인자_X() {
    Runnable runnable = () -> System.out.println("Runnable");
    runnable.run();
  }
```

### 2.2 Supplier 리턴 1개 인자 없음

```java
  @Test
  public void 리턴_1_인자_X() {
    Supplier<String> supplier = () -> "Supplier";
    assertThat(supplier.get())
            .isEqualTo("Supplier");
  }
```

### 2.3 Consumer 리턴 없음 인자 1개

```java
  @Test
  public void 리턴_X_인자_1() {
    Consumer<String> consumer = str -> System.out.println(str);
    consumer.accept("consumer");
  }
```

### 2.4 Function 리턴 1개 인자 1개

```java
  @Test
  public void 리턴_1_인자_1() {
    //Function<String(parameter), Integer(return)>
    Function<String, Integer> function = str -> Integer.parseInt(str);
    assertThat(function.apply("1"))
            .isEqualTo(1);
  }
```

### 2.5 Predicate 리턴 Boolean 인자 1개

```java
  @Test
  public void 리턴_Boolean_인자_1() {
    Predicate<String> predicate = str -> str.isEmpty();
    assertThat(predicate.test("HELLO"))
            .isEqualTo(false);
  }
```

### 2.6 UnaryOperator 리턴 1개 인자 1개 리턴 과 인자 같은 타입

Generic 때 많이 사용함

```java
  @Test
  public void 리턴_1_인자_1_리턴_과_인자_같은_타입() {
    UnaryOperator<String> unaryOperator = str -> str += " WORLD";
    assertThat(unaryOperator.apply("HELLO"))
            .isEqualTo("HELLO WORLD");
  }
```

### 2.7 BinaryOperator 리턴 1개 인자 2개 리턴 과 인자 같은 타입

```java
  @Test
  public void 리턴_1_인자_2_리턴_과_인자_같은_타입() {
    BinaryOperator<String> binaryOperator = (str1, str2) -> str1 + str2;
    assertThat(binaryOperator.apply("HELLO", "WORLD")).isEqualTo("HELLOWORLD");
  }
```

### 2.8 BiPredicate 리턴 Boolean 인자 2개

```java
  @Test
  public void 리턴_Boolean_인자_2() {
//  BiFunction<String(parmeter1), Integer(parmeter2)>
    BiPredicate<String, Integer> biPredicate = (str, num) -> Integer.parseInt(str) > num;
    assertThat(biPredicate.test("5", 2)).isTrue();
  }
```

### 2.9 BiConsumer 리턴 없음 인자 2개

```java
  @Test
  public void 리턴_X_인자_2() {
    BiConsumer<String, Integer> biConsumer = (str, num) -> System.out.println(Integer.parseInt(str) + num);
    biConsumer.accept("5", 2);
  }
```

### 2.10 BiFunction 리턴 1개 인자 2개

```java
  @Test
  public void 리턴_1_인자_2() {
//  BiFunction<String(parmeter1), String(parmeter2), Integer(return)>
    BiFunction<String, String, Integer> biFunction = (str1, str2) -> Integer.parseInt(str1) + Integer.parseInt(str2);
    assertThat(biFunction.apply("2", "3")).isEqualTo(5);
  }
```

### 2.11 Comparator 리턴 1개 인자 2개

기존 정렬 할때 Comparable 많이 사용 하였지만 Lamda 이후에는 Comparator 더 많이 쓰임

```java
  @Test
  public void 리턴_int_인자_2_Comparator() {
    Comparator<Integer> comparator = (num1, num2) -> num1.compareTo(num2);
    assertThat(comparator.compare(2, 1)).isEqualTo(1);
  }
```

## 3. 참조

[Java8#02. 함수형 인터페이스(Functional Interface)](https://multifrontgarden.tistory.com/125)