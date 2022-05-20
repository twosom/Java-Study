# 2주차 과제: 자바 데이터 타입, 변수 그리고 배열

# 목표

자바의 프리미티브 타입, 변수 그리고 배열을 사용하는 방법을 익힙니다.

# 학습할 것

* 프리미티브 타입 종류와 값의 범위 그리고 기본 값
* 프리미티브 타입과 레퍼런스 타입
* 리터럴
* 변수 선언 및 초기화하는 방법
* 변수의 스코프와 라이프타임
* 타입 변환, 캐스팅 그리고 타입 프로모션
* 1차 및 2차 배열 선언하기
* 타입 추론, var

# 프리미티브 타입 종류와 값의 범위 그리고 기본 값

자바는 총 8가지의 프리미티브 타입<sup>기본형 타입</sup>을 제공한다. 기본 값이 있기 대문에 null이 존재하지 않는다.<br/>
만약 null을 할당하고 싶은 경우 래퍼 클래스를 활용한다.

**실제 값을 저장하는 공간으로 스택 메모리에 저장된다.**

프리미티브 타입에 담을 수 있는 크기를 초과한 경우 컴파일 에러가 발생한다.

|     | 타입             | 할당되는 메모리 크기 | 기본값     | 데이터의 표현 범위                                             |
|-----|----------------|-------------|---------|--------------------------------------------------------|
| 논리형 | boolean        | 1 byte      | false   | true, false                                            |
| 정수형 | byte           | 1 byte      | 0       | -127 ~ 128                                             |
| 정수형 | short          | 2 byte      | 0       | -32,768 ~ 32,767                                       |
| 정수형 | **int(기본)**    | **4 byte**  | **0**   | **-2,147,483,648 ~ 2,147,483,647**                     |
| 정수형 | long           | 8 byte      | 0L      | -9,223,372,036,854,775,808 ~ 9,223,372,036,854,775,807 |
| 실수형 | float          | 4 byte      | 0.0F    | (3.4 X 10-38) ~ (3.4 X 1038) 의 근사값                     |
| 실수형 | **double(기본)** | **8 byte**  | **0.0** | **(1.7 X 10-308) ~ (1.7 X 10308) 의 근사값**               |

[참조](https://gbsb.tistory.com/6)

### 다른 언어에서는 어떻게 사용할까

* Kotlin
    * 프리미티브 타입이 존재하지 않는다. 다만 바이트 코드로 변환 시 가능한 한 프리미티브 타입으로 바꿔준다.
      또한, Collection에서는 오토 언박싱 처리를 하고있다.([출처](https://meteorkor.tistory.com/36))

* Swift
    * Int -> 32비트 환경에서는 Int32, 64비트 환경에서는 Int64

---

# 프리미티브 타입과 레퍼런스 타입

## 프리미티브 타입

기본형 타입에 대한 설명은 상기 기술한 **프리미티브 타입 종류와 값의 범위...** 로 댜체

## 레퍼런스 타입

프리미티브 타입이 아닌 모든 타입(클래스, 인터페이스, 배열, 열거형)<br/>
값을 변수에 대입하지만 변수는 참조값을 가지고 있지 값을 직접 들고 있지 않은 것이 특징.
(값은 Heap 메모리 영역에 저장됨)

레퍼런스 타입이 아무런 값을 참조하지 않도록 하는 것이 null이다.
[참조](https://jinbroing.tistory.com/3)
---

# 리터럴

### 사전적 의미

> lit·eral<br/>
> 1.문자 그대로의 2.직역의 3.상상력이 부족한

### Java 상에서의 의미

> 프로그램에서 직접 표현한 값<br/>
> 소스 코드의 고정된 값을 대표하는 용어 [출처](https://mine-it-record.tistory.com/100)

### 종류

* 정수
* 실수
* 문자
* 논리
* 문자열

### 정수리터럴

정수리터럴에는 10진수, 8진수(0으로 시작), 16진수(0x로 시작), 2진수(0b로 시작)가 존재.

정수리터럴은 `int`형으로 컴파일, long 타입 리터럴은 숫자 뒤에 `L` 또는 `l`을 붙여 표시한다.

### 실수리터럴

소수점 형태나 지수 형태로 표현한 값들. 실수 타입은 `double` 타입으로 컴파일 됨.

숫자 뒤에 `f`<sup>float</sup>나 `d`<sup>double</sup>을 명시적으로 붙이기도 함. -> `float`은 `f`를 붙여줘야 하지만 `double`은 생략 가능

### 문자리터럴

싱글 쿼테이션`''`으로 문자를 표현

다음과 같이 표현 가능

```java
    char a='H';
        char b="한";
        char c= \uae00; // 유니코드 값
```

### 문자열 리터럴

문자열은 기본 타입이 아님.

("")로 문자열을 표현

### 논리 타입 리터럴

boolean 타입 변수에 치환하거나 조건문에 이용

[출처](https://mine-it-record.tistory.com/100#recentComments)

# 변수 선언 및 초기화하는 방법

## 변수 선언 방법

변수 타입과 변수명을 함께 작성하는 것

```java
    String twosom;
```

이런 형태로 선언하면 변수가 해당하는 크기만큼 메모리에 할당 됨.

## 변수 초기화 방법

선언한 변수에 데이터를 집어넣는 것. 대입하는 과정이라고도 함.

```java
    String twosom;
        twosom="Hello twosom";
```

`twosom`이라는 변수에 "Hello twosom"이라는 데이터가 저장됨.

[출처](https://geundung.dev/7)

---

# 변수의 스코프와 라이프타임

## Class, Method, Static 변수의 스코프

> 변수를 사용할 수 있는 범위.
>
> `{}` 안에서 변수를 선언했을 경우 영역이 끝나기 전까지는 어디서든 사용이 가능함.

```java
public class ScopeTest { // Class 영역
    /**
     *  Class 영역에 선언한 변수(Global Variable)
     */
    String sClassVal = "Class Value";

    /**
     * 스태틱은 클래스 내에서 공유되어 아무데서나 사용 가능
     */
    static String sStaticVal = "Static Value";

    public void method1() { // 메소드 영역

        String sMethod1Val = "method1 value"; // Method 영역에 선언한 변수(Local Variable)
        System.out.println(sClassVal);  // Class 영역 안에 있는 메소드에서는 클래스 변수 사용 가능
    } // 메소드 영역

    public static void main(String[] args) {
        // 메인 메소드는 static 변수가 아닐 경우 객체화해야 클래스 변수 사용 가능 
        System.out.println(sStaticVal);
        ScopeTest s = new ScopeTest();
        System.out.println(s.sClassVal);
    }

} // Class 영역 끝
```

### 전역 변수

> 클래스 내의 모든 장소에서 사용할 수 있는 변수

### 지역 변수

> 메소드 내에서 선언하는 변수, 해당 메소드 안에서만 사용이 가능하다.

### static 변수

> 클래스 내에서 한 변수를 공유해서 어느 곳에라든지 사용할 수 있는 변수



[출처](https://wakestand.tistory.com/179)

## Loop 변수의 스코프

for와 같은 Loop 내에서 선언한 변수는 Loop 내에서만 접근 가능. Loop 밖에서 접근하려고 하면 컴파일 에러 발생

```java
public class LoopTest {
    public static void main(String[] args) {
        for (int i = 0; i < 10; i++) {
            int aa = i;
        }
        int bb = aa; // compile error!
    }
}

```

## 괄호 안 변수의 스코프

괄호 안에서 선언한 변수는 그 괄호 안에서만 접근할 수 있음. 괄호 밖에서 접근하려고 하면 compile error 발생.

```java
public class BracketTest1 {
    public static void main(String[] args) {
        {
            int bb = 100;
        }

        int aa = bb; // compile error

        {
            int cc = bb; // compile error
        }
    }
}
```

이와같은 이유로 다음처럼 괄호를 사용하여 동일한 이름의 변수를 여러번 선언해도 컴파일 에러가 발생하지 않음.

```java
public class BracketTest2 {
    public static void main(String[] args) {
        {
            int a = 10;
        }
        {
            int a = 10;
        }
    }
}
```

[출처](https://codechacha.com/ko/java-variable-scope/)

---

# 타입 변환, 캐스팅 그리고 타입 프로모션

자바에는 두 종류의 타입 변환이 있음.

* 자동 타입 변환(묵시적[프로모션])
* 강제 타입 변환(명시적[캐스팅])

## 자동 타입 변환[프로모션]

프로그램 실행 도중 자동으로 타입 변환이 일어남.

작은 크기를 가지는 타입이 큰 크기를 가지는 타입에 저장될 때 발생.

```java
큰_크기_타입=작은_크기_타입;
```

타입별 크기 순서
> byte(1) < short(2) < int(4) < long(8) < float(4) < double(8)

**float은 표현범위가 더 크기 때문에 더 큰 타입으로 들어감.**

#### 주의할 점

char 타입이 int 타입으로 들어가게 되면 **유니코드 값**이 저장된다.<br/>
단, 음수가 저장될 수 있는 byte, int 등의 타입은 char 타입으로 자동 변환할 수 없다.

```java
public class ByteTest {
    public static void main(String[] args) {
        byte byteVal = 65;
        char charVal = byteVal; // 컴파일 에러
        char charData = (char) byteVal;
    }
}
```

```java
public class PromotionExam {
    public static void main(String[] args) {
        byte byteVal = 10;
        int intVal = byteVal; // byte -> int
        System.out.println(intVal); // 10

        char charVal = '가';
        intVal = charVal; // char -> int
        System.out.println("가의 유니코드 : " + intVal); // 44032

        intVal = 500;
        long longVal = intVal; // int -> long
        System.out.println(longVal); // 500

        intVal = 200;
        double doubleVal = intVal; // int -> double
        System.out.println(doubleVal); // 200.0
    }
}
```

## 강제 타입 변환[캐스팅]

자동 타입 변환과는 반대로 큰 크기 타입을 작은 크기 타입으로 자동 타입 변환을 할 수 없다.

하지만 강제로 int 타입의 1byte를 잘라서 byte 타입 변수에 저장할 수 있음. -> 나머지 3바이트는 버려지게 됨...

```java
작은_크기_타입=(작은_크기_타입)큰_크기_타입;
```

int 타입 역시 char 타입으로 자동 타입 변환되지 않기 때문에 강제 타입 변환을 사용함.

실수 타입은 정수 타입으로 자동 타입 변환되지 않기 때문에 강제 타입 변환을 사용해야 함. -> 소숫점 이하 부분은 버려짐

```java
public class CastingExam {
    public static void main(String[] args) {
        int intVal = 44_032;
        char charVal = (char) intVal;
        System.out.println(charVal); // 44032에 해당하는 유니코드 '가' 출력

        long longVal = 500;
        intVal = (int) longVal;
        System.out.println(intVal);

        double doubleVal = 3.14;
        intVal = (int) doubleVal;
        System.out.println(intVal); // 정수 부분인 3 출력
    }
}
```

[출처](https://kephilab.tistory.com/27#recentComments)

---

# 1차 및 2차 배열 선언하기

## 배열

> 동일한 자료형의 데이터를 연속된 공간에 저장하기 위한 자료구조

## 1차원 배열 선언 및 사용

> 자료형[] 변수 = {데이터1, 데이터2, 데이터3...}

위 방법은 배열에 넣어야 하는 데이터들의 값을 미리 알고 있을 경우 편리.

> 자료형[] 변수 = new 자료형[배열크기];<br/>
> 변수[0] = 데이터 값;<br/>
> 변수[1] = 데이터 값;<br/>

위 방법은 배열의 값은 모르지만 향후 값을 저장하기 위한 배열을 생성하고 싶은 경우 사용.

## 2차원 배열 선언 및 사용

> 자료형[][] 변수 = new 자료형[10][10]<br/>
> 변수[0][0] = 데이터 값;<br/>
> 변수[0][1] = 데이터 값;<br/>
> 변수[0][2] = 데이터 값;<br/>

[참조](https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=heartflow89&logNo=220950491600)

---

# 타입 추론, var

Java 10 버전부터 도입된 `var` 키워드를 사용하여 변수 선언 시 타입 생략 가능. -> 컴파일러가 타입을 추론하게 됨.

```java
public class VarTypeTest {
    public static void main(String[] args) {
        var stringVal = "Hello, World";
    }
}
```

컴파일 타임에 추론하는 것이기 때문에, Runtime에 추가 연산을 하지 않아서 성능에 영향 주지 않음(중요!!)

## 제약사항

* `var` 키워드는 지역변수에만 사용할 수 있음.
* 초기화가 필요함. -> 초기화를 하지 않으면 어떤 타입인지 알 수 없음.
* null로 초기화 불가.
* 배열에 사용 불가 -> 타입 추론 불가
* Lambda에 사용 불가
* 컴파일러가 타입을 추론할 수 없는 애매한 상황일 때는 컴파일 에러가 발생함.

## 사용방법

### ~ JDK9

```java
public class BeforeJdk9Test {
    public static void main(String[] args) {
        List<String> myStringList = new ArrayList<>();
        myStringList.add("Hello");
        myStringList.add("World");
    }
}
```

### JDK10 ~

```java
public class AfterJdk10Test {
    public static void main(String[] args) {
        var myStringList = new ArrayList<String>();
        myStringList.add("Hello");
        myStringList.add("World");
    }
}
```

## var는 반복문에서도 사용 가능

```java
public class VarLoopTest {
    public static void main(String[] args) {
        int[] arr = {1, 2, 3};

        for (var n : arr) {
            System.out.println("n : " + n);
        }
    }
}
```

[참조](https://codechacha.com/ko/java-local-variable-type-inference/)