# 7주차 과제: 패키지

# 목표

자바의 패키지에 대해 학습하세요.

학습할 것 (필수)

* package 키워드
* import 키워드
* 클래스패스
* CLASSPATH 환경변수
* -classpath 옵션
* 접근지시자

# package 키워드

pakcage
---
> 패키지<sup>package</sup>는 비슷한 목적으로 생성된 클래스 파일들을 한곳에 모아 둔 **폴더**

즉, 동일한 목적으로 만들어진 클래스들을 1개의 공간<sup>폴더</sup>에 묶어 사용하는 것.

예로 동일한 클래스를 생성하는데 **하나는 패키지를 지정하지 않고 소스 파일을 생성**할 때와

또다른 하나는 **`com.icloud`라는 이름의 패키지를 지정하고 소스파일을 생성**할 때를 비교해보면 다음과 같다.

1. 패키지를 지정하지 않고 소스파일 생성
    ```java
    public class Hello {
    
    }
    ```
   위의 소스파일을 바이트코드로 변환하면 다음과 같다.
   ```java
   // class version 61.0 (61)
   // access flags 0x21
   public class Hello {
   
    // compiled from: Hello.java
    
    // access flags 0x1
      public <init>()V
        L0
            LINENUMBER 1 L0
            ALOAD 0
            INVOKESPECIAL java/lang/Object.<init> ()V
            RETURN
        L1
            LOCALVARIABLE this LHello; L0 L1 0
            MAXSTACK = 1
            MAXLOCALS = 1
   }

   ```
2. 패키지를 지정하고 소스파일을 생성
   ```java
   package com.icloud;
   
   public class Hello {
   
   }
   ```
   마찬가지로 위의 소스파일을 바이트코드로 변환하면 다음과 같다.
   ```java
    // class version 61.0 (61)
    // access flags 0x21
    public class com/icloud/Hello {
    
    // compiled from: Hello.java
    
    // access flags 0x1
    public <init>()V
        L0
            LINENUMBER 3 L0
            ALOAD 0
            INVOKESPECIAL java/lang/Object.<init> ()V
            RETURN
        L1
            LOCALVARIABLE this Lcom/icloud/Hello; L0 L1 0
            MAXSTACK = 1
            MAXLOCALS = 1
   }
   ```

각각의 바이트코드에서 하나는 그냥 클래스 이름만 명시되어있고 또다른 하나는 패키지 이름 + 클래스 이름으로 명시되어 있는것을 볼 수 있다.

이렇게 패키지로 구분지음으로 인해 클래스가 저장되는 공간이 분리돼어 클래스명이 충돌되는 현상을 방지할 수 있음을 알 수 있다.<br/>
즉, **서로 다른 패키지 상에 존재하는 같은 이름을 가진 클래스는 서로 전혀 다른 존재로 인식된다.**