# 11주차 : 애노테이션

## 목표

자바의 애노테이션에 대해 학습하세요.

## 학습할 것 (필수)

- 애노테이션 정의하는 방법
- [@retention](https://github.com/retention)
- [@target](https://github.com/target)
- [@documented](https://github.com/documented)
- 애노테이션 프로세서

## 마감일시

2021년 2월 6일 토요일 오후 1시까지.

---

## 어노테이션

어노테이션은 주석이라는 뜻입니다. 

기본적으로 주석이라는 뜻 입니다.

우리가 아는 주서은 // 또는 /* */ 이렇게 생겼는데,

어노테이션은 어떤 점이 다를까요.

- 어노테이션의 역할도 주석과 크게 다르지 않습니다.
- 일반 주석과 다른 점은 코드를 작성할 수 있다는 점입니다.
- 코드를 작성할 수 있다는 것은 어떤 것을 구현할 수 있고 작동할 수 있다는 의미입니다.
- 어노테이션도 enum처럼 1.5에 등장했습니다. 

## 어노테이션 정의하는 방법

```java
public @interface Make {
}
```

이렇게 합니다.

enum은 java.lang.Enum에 상속되어 있습니다.

그러면 어노테이션의 조상은 무엇일까요? 바이트 코드로 확인해보면

```java
public abstract @interface study/whiteship/homework12/Make 
                             implements java/lang/annotation/Annotation {
    // compiled from: Make.java
}
```

### 어노테이션 요소의 규칙

- 요소의 타입은 기본형, String, enum, 어노테이션, Class만 허용한다.
- ()안에 매개변수는 선언할 수 없다.
- 예외를 선언할 수는 없다.
- 요소를 타입 매개변수로 정의 할 수 없다.

### 표준 어노테이션

자바에서 제공하는 어노테이션은 크게 2가지입니다. 하나는 자바코드를 작성할 대, 사용하는 어노테이션, 다른 하나는 어노테이션을 정의하기 위해 필요한 것입니다.



## [@retention](https://github.com/retention)

어노테이션이 유지되는 범위를 지정하는데 사용합니다.

funtionalInterface로 확인

```java
@Documented
@Retention(RetentionPolicy.RUNTIME)
@Target(ElementType.TYPE)
public @interface FunctionalInterface {}
```

런타임까지 유지합니다.

#### sourccee로 사용하면 일반 주석처럼 사용한다는 뜻.

소스단에서만 사용하고 컴파일 할 때에는 이 어노테이션이 필요 없다는 의미예요.

대표적으로 override가 있어요.

```java
public class Korea implements Great{

    @Override
    public String country() {
        return "한국";
    }
}
```

컴파일 이후 override가 사라져요.

#### class

컴파일할 때까지 어노테이션을 유지함을 의미해요.

자바에서 제공하는 어노테이션은 class가 존재하지 않아요.

retation의 기본전략입니다.

```
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.CLASS)
public @interface Make {}
```

Make라는 어노테이션을 만ㄷ르었

## [@target](https://github.com/target)

어노테이션이 적용 가능한 대상을 지정하는데 사용해요.

만약 다른 타입이 온다면 컴파일 에러를 보여준다.

위에서 Override를 다시 확인해볼까요.

```
@Target(ElementType.METHOD)
@Retention(RetentionPolicy.SOURCE)
public @interface Override {
}
```



## [@documented](https://github.com/documented)

어노테이션 정보가 javadoc 으로 작성된 문서에 포함된다.

정확히 말하면 자바 docs에 올라간다가 아니라,

내가 직접 자바doc을 만들 수 있다는 뜻이다.

## 애노테이션 프로세서

어노테이션을 프로세싱하는 기술이다.

어노테이션 프로세서의 대표적인 기술로는 롬복이 있다. 

런타임시에 리플랙션을 사용하는 어노테이션과 달리 컴파일 타임에 이뤄진다.

컴파일 타임에 어노테이션을 프로세싱하는 javac에 속한 빌드 툴로 어노테이션의 소스코드를 분석하고 처리하기 위해 사용하는 훅이다.

------

해당 블로그 가기 :

https://b-programmer.tistory.com/264


