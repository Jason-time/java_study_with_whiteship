# 11주차 : Enum

## 목표

자바의 열거형에 대해 학습하세요.

## 학습할 것 (필수)

### enum 정의하는 방법

### enum이 제공하는 메소드 (values()와 valueOf())

### java.lang.Enum

### EnumSet

## 마감일시

2021년 1월 23일 토요일 오후 1시까지.

---

## enum

> 열거형이라고 부른다. 서로 연관된 상수들의 집합이다.
>
> jdk1.0에 추가되었다. c언어에서 enum은 상수들의 집합으로 상요하지만, java에서는 자료형까지 비교 가능하다.

## enum 만드는 방법

```java
public enum Language
{
	c, JAVA, KOTLIN, JAVASCRIPT
}
```

위코드는 이렇게 출력할 수 있다.

```java
System.out.println(Language.C.ordinal());
System.out.println(Language.JAVA.ordinal());
System.out.println(Language.KOTLIN.ordinal());
System.out.println(Language.JAVASCRIPT.ordinal());
```

> 0
>
> 1
>
> 2
>
> 3

ordinal() : enum의 순서를 의미한다.

만약,

```java
public enum Language 
{
    JAVA, KOTLIN, JAVASCRIPT,C
}
```

라면 순서가 바뀐다.

## enum 에서 값을 꺼내오는 방법

값을 읽는 방법은 3가지이다.

```java
1.System.out.println(Language.C);
2.System.out.println(Language.valueOf("JAVA"));
3.System.out.println(Enum.valueOf(Language.class,"JAVASCRIPT"));
```

```
C
JAVA
JAVASCRIPT
```

아래와 같이 작성하는 방법도 있다. name을 적어주었다.

```java
 System.out.println(Language.KOTLIN.name());
```

enum 클래스를 아래처럼 작성할 수 있다.

```java
public static final LanguageClass C = new LanguageClass("C");
public static final LanguageClass JAVA = new LanguageClass("JAVA");
public static final LanguageClass KOTLIN = new LanguageClass("KOTLIN");
public static final LanguageClass JAVASCRIPT = new LanguageClass("JAVASCRIPT");

private String name;
public LanguageClass(String name) {
  this.name = name;
}
```

## enum이 제공하는 메소드

ordinal() : enum의 순서

name() : 각 요소들의 이름 (toString에 기본으로 작성되어있다)

valueOf() : 문자열로 enum요소의 이름을 찾아서 요소의 이름을 리턴한다.

values() : 모든 enum의 요소들을 배열로 만들어준다.

```java
Language[] values = Language.values();
```

```java
for (Language value : values) {
    System.out.println(value);
}
```

> 출력값
>
> C
>
> JAVA
>
> KOTLIN
>
> JAVASCRIPT

## java.lang.Enum

모든 enum 클래스는 위 클래스의 자손이다. 모든 열거형은 Enum 클래스를 상속받기 때문에 enum type은 별도의 상속을 받을 수 없다.

```java
public abstract class Enum<E extends Enum<E>>
        implements Constable, Comparable<E>, Serializable {
        
    private final String name;
    
    private final String name() {
        return name;
    }
    ......
}
```

 toString을 제외한 대부분의 메서드는 final로 선언되어 있기 때문에 별도의 오버라이딩을 할 수 없다.

## EnumSet

EnumSet을 사용하여 Enum을 Set 자료구조로 만들 수 있다.

allOf : enum 에 정의된 정보를 모두 추가할 수 있다.

```java
EnumSet.allOf(Language.class);
```

noneOf : 아무것도 추가하지 않는다.

of : 요소를 직접넣을 수 있다.

```java
EnumSet<Language> languages = EnumSet.of(Language.C, Language.JAVA);
```

------

해당 블로그 가기 :

https://b-programmer.tistory.com/262


