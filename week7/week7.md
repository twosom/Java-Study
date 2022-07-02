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

각각의 바이트코드에서 하나는 그냥 클래스 이름만 명시되어있고 또다른 하나는 패키지 이름 + 클래스 이름으로 명시되어 있는것을 볼 수 있다.<br/>
이러한 클래스 이름을 FQCN<sup>Full Qualified Class Name</sup>

이렇게 패키지로 구분지음으로 인해 클래스가 저장되는 공간이 분리돼어 클래스명이 충돌되는 현상을 방지할 수 있음을 알 수 있다.<br/>
즉, **서로 다른 패키지 상에 존재하는 같은 이름을 가진 클래스는 서로 전혀 다른 존재로 인식된다.**

# import 키워드

import
---
> 다른 패키지 내의 클래스를 사용하기 위한 문법 요소

자신의 패키지에 위치한 클래스가 아닌 다른 패키지의 클래스 사용 방법은 크게 2가지이다.

### 1. 클래스의 풀네임 사용

클래스의 풀네임은 `패키지명.클래스명`이다.<br/>
패키지 내의 클래스들을 사용할 때는 클래스 이름만으로 사용할 수 있지만, 다른 패키지의 클래스를 사용할 때는 풀네임을 사용해야 한다.

### 2. 임포트 사용

클래스의 풀네임을 사용하는 것이 아닌 클래스의 이름만으로 사용하게 하려면 해당 패키지의 클래스를 임포트 해야 한다.<br/>
이때 사용하는 방법이 임포트이다.

# 클래스패스

클래스패스
---
> 빌드시 컴파일된 class 파일들의 위치 경로

프로젝트 내에서의 클래스패스
--
`/Users/hope/Library/Java/JavaVirtualMachines/openjdk-17.0.2/Contents/Home/bin/java -javaagent:/Users/hope/Library/Application Support/JetBrains/Toolbox/apps/IDEA-U/ch-0/221.5921.22/IntelliJ IDEA.app/Contents/lib/idea_rt.jar=53857:/Users/hope/Library/Application Support/JetBrains/Toolbox/apps/IDEA-U/ch-0/221.5921.22/IntelliJ IDEA.app/Contents/bin -Dfile.encoding=UTF-8 -classpath /Users/hope/Desktop/study/design-pattern/target/classes main.Main`

위의 명령어는 `Intellij`에서 특정 클래스의 `main` 메소드를 실행시켰을 때 나오는 커맨드라인 명령어이다.
위에서 볼 수 있듯이 마지막에 `-classpath` 옵션이 추가된 것을 볼 수 있을 것이다.

즉, 프로젝트 내에서의 클래스패스는 `프로젝트이름/target/classes`이다.
`target` 디렉토리는 클래스들이 컴파일 된 후 바이트코드가 저장되는 공간이다.

# CLASSPATH 환경변수

`classpath`가 지정된 환경변수이다. 위의 내용에서 나온 것과 같이 `IntelliJ`와 같은 IDE를 사용할 경우,
IDE에서 `classpath`를 자동으로 지정해주기 때문에 개인적으로는 그렇게 중요하지는 않다고 생각한다.

# -classpath 옵션

> 컴파일러가 컴파일하려는 코드에서 참조하고있는 클래스 파일들을 찾기 위해서 컴파일시 파일 경로를 지정해주는 옵션

예를 들어 이러한 디렉토리 구조를 가진 프로젝트가 있다고 가정해보겠다.

```shell
|____main
| |____java
| | |____pack1
| | | |____B.java
| | | |____pack2
| | | | |____C.java
| | | | |____D.java
| | | |____A.java
| | |____main
| | | |____Main.java
```

`main` 패키지 밑에는 `pack1`과 `main` 패키지가 각각 존재하고 `pack1` 패키지 밑에는 `pack2` 패키지가 있는 구조다.

`main` 패키지의 `Main` 클래스의 내용은 다음과 같다.

```java
package main;

import pack1.A;
import pack1.B;
import pack1.pack2.C;
import pack1.pack2.D;

public class Main {
    public static void main(String[] args) {
        A a = new A();
        B b = new B();

        C c = new C();
        D d = new D();
    }
}
```

이 `Main` 클래스를 컴파일하기 위해서는 `A`클래스, `B`클래스, `C`클래스 `D`클래스가 필요하다.

그렇기 때문에 단순히 `javac ./src/main/java/main/Main.java` 명령어를 입력하면 다음과 같은 오류가 발생한다.

```shell
./src/main/java/main/Main.java:3: error: package pack1 does not exist
import pack1.A;
            ^
./src/main/java/main/Main.java:4: error: package pack1 does not exist
import pack1.B;
            ^
./src/main/java/main/Main.java:5: error: package pack1.pack2 does not exist
import pack1.pack2.C;
                  ^
./src/main/java/main/Main.java:6: error: package pack1.pack2 does not exist
import pack1.pack2.D;
                  ^
./src/main/java/main/Main.java:10: error: cannot find symbol
        A a = new A();
        ^
  symbol:   class A
  location: class Main
./src/main/java/main/Main.java:10: error: cannot find symbol
        A a = new A();
                  ^
  symbol:   class A
  location: class Main
./src/main/java/main/Main.java:11: error: cannot find symbol
        B b = new B();
        ^
  symbol:   class B
  location: class Main
./src/main/java/main/Main.java:11: error: cannot find symbol
        B b = new B();
                  ^
  symbol:   class B
  location: class Main
./src/main/java/main/Main.java:13: error: cannot find symbol
        C c = new C();
        ^
  symbol:   class C
  location: class Main
./src/main/java/main/Main.java:13: error: cannot find symbol
        C c = new C();
                  ^
  symbol:   class C
  location: class Main
./src/main/java/main/Main.java:14: error: cannot find symbol
        D d = new D();
        ^
  symbol:   class D
  location: class Main
./src/main/java/main/Main.java:14: error: cannot find symbol
        D d = new D();
                  ^
  symbol:   class D
  location: class Main
12 errors
```

이 경우에는 참조할 클래스 파일들이 `pack1` 패키지 및 `pack1.pack2`에 존재하므로
`pack1` 및 `pack2`의 상위 패키지인 `java` 패키지를 클래스패스로 잡아준다.

```shell
javac -classpath ./src/main/java ./src/main/java/main/Main.java
```

만약 참조할 클래스의 디렉토리가 제각각이라 여러개의 클래스패스를 정의해야 하는 경우에는 `;`로 구분하여 실행하면 된다.

```shell
javac -classpath /some/package;/another/package ./src/main/java/Main.class 
```

# 접근지시자

> 클래스 필드, 메소드, 생성자 등에게 어떠한 특징을 부여하는 문법 요소

종류
---

멤버 및 생성자에는 다음과 같은 4가지 종류의 접근지시자를 사용할 수 있다.

* public
* protected
* default(또는 package)
* private

private
---
자신의 클래스 내부에서만 사용할 수 있는 접근지시자.


default
---
같은 패키지 안의 모든 클래스에서 사용할 수 있는 접근 접근지시자.

protected
---
`default` 범위에 다른 패키지의 자식 클래스 까지 사용할 수 있는 접근지시자.

public
---
동일 패키지의 모든 클래스 및 다른 패키지의 모든 클래스에도 접근할 수 있는 접근지시자.