# 14주차 : 제네릭

## 목표

자바의 제네릭에 대해 학습하세요.

## 학습할 것 (필수)

- 제네릭 사용법
- 제네릭 주요 개념(바운디드 타입, 와일드 카드)
- 제네릭 메소드 만들기
- Erasure

## 마감일시

2021년 2월 27일 토요일 오후 1시까지.

---

### Generics를 사용하는 이유

제네릭은 클래스, 인터페이스 및 메서드를 정의 할 때 자료형이 매개 변수가 되도록한다. 메서드 선언에 사용하는 다른 파라미터들과 마찬가지로 타입 파라미터는 서로 다른 입력으로 동일한  코드를 재사용 할 수 있는 방법을 제공한다. 차이점은 매개 변수에 대한 입력은 값이고 타입 매개 변수에 대한 입력은 자료형이라는 것이다.

### 제네릭 사용법

제네릭 클래스 선언하기

다음과 같은 형식으로 정의한다.

```java
class name <T1, T2, ..., Tn> {/ * ... * /}
```

꺽쇠 괄호 <>로 구분 된 타입 매개 변수는 클래스 이름 뒤에 온다. 객체가 생성될 때 타입 파라미터를 받는 부분이다.

타입 파라미터와 일반 클래스 타입 파라미터는 단일 대문자를 사용한다.

가장 일반적으로 사용하는 타입 매개변수

```
E-엘리먼트
K-키
N-숫자
T-타입
V-값
S,U,V 등 -2,3,4 종
```

```
public class WitchPot<T> { 
    private T meterial;
}
```

#### **제네릭 타입 호출하기**

코드 내에서 제네릭 클래스를 참조하려면 `T` 를 `Integer` 와 같은 구체적인 값으로 대체하는 제네릭 타입 호출을 수행해야한다 .

```
GenericClass<Type args> var;
```

객체 만들기는 일반적인 객체 생성과 유사하지만 인스턴스 생성 부분에서도 선언처럼 `<Type args>`를 기입해야 한다.

```
GenericClass<Type args> var = new GenericClass<Type args>();
```

### 제네릭 주요 개념 (바운디드 타입, 와일드 카드)

바운디드 타입

제네릭 타입에서 타입 인자로 사용할 수 있는 타입을 제한하려는 경우가 있을 수 있다. 

바운디드 타입 파라미터를 선언하려면 타입 파라미터의 이름, `extends`키워드, 상위 바운드를 나열한다.

```
<T extends UpperBound>
```

뭐가 뭔지 모르겠다...

#### 제네릭과 상속 및 하위 타입

일반적인 상속 관계에서 아래처럼 상위 클래스 타입으로 대입이 가능한 것 처럼,

```java
public void someMethod(Number n) { /* ... */ }
someMethod(new Integer(10));   // OK
someMethod(new Double(10.1));   // OK
```

제네릭 타입도 이와 같이 타입 파라미터로 주어진 타입에 하위 타입으로 대입할 수 있다.

### 와일드 카드

제네릭 타입 코드에서 와일드 카드라고 하는 물음표 ? 는 알 수 없는 유형을 말한다. 와일트 카드는 파라미터 변수, 필드 또는 지역변수의 타입 등 다양한 상황에서 사용할 수 있다. 

와일드 카드는 제네릭 메서드 호출, 제네릭 클래스 인스턴스 생성 또는 수퍼 타입의 타입 인자로는 사용할 수 없다.

### Upper Bounded Wildcards

상한 와일드 카드를 사용하여 바운디드 상위 제한을 완화할 수 있다.

```
<? extends UpperBound>
```

이런 제네릭 타입은 UpperBound 클래스 또는 인터페이스의 하위 타입과 매칭할 수 있다.

**와일드 카드 주의사항**

와일드 카드를 사용한 제네릭 List 타입은 비공식적으로 read-only로 간주한다.  하지만 아래 작업이 가능하기 때문에 이 말이 완전히 보장하지 않는다. 

- null 을 추가할 수 있다.
- clear 를 호출할 수 있다.
- iterator 를 가져오고 remove를 호출 할 수 있다.
- 와일드 카드를 캡쳐하고 List에서 읽은 요소를 쓸 수 있다.

#### 와일드 카드 캡쳐

헬퍼 메소드를 이용하여 컴파일러에게 와일드 카드 타입을 유추할 수 있도록 도와주는 방식을 와일드 카드 캡쳐라고 한다.

컴파일러는 기본적으로 List<?> 에 대해 List<Object> 로 처리하려고 하며 set() 메소드에 엘리먼트 타입을 컴파일 타임에 확인할 수 없기 때문에 오류가 발생한다.

```
public class WildCardTest {

    static void foo (List<?> i) {
        //컴파일 오류
        i.set(0, i.get(2));
    }

    public static void main(String[] args) {
        List<Integer> li = Arrays.asList(1,2,3);
        System.out.println(li);
        foo(li);
        System.out.println(li);
    }
}
```

헬퍼 메소드를 추가해서 컴파일러가 와일드 카드 타입을 추론할 수 있도록 해준다.

```
public class WildCardTest {

    static void foo (List<?> i) {
        originalMethodNameHelper(i);
    }

    private static <T> void originalMethodNameHelper(List<T> i) {
        i.set(0, i.get(2));
    }

    public static void main(String[] args) {
        List<Integer> li = Arrays.asList(1,2,3);
        System.out.println(li);
        foo(li);
        System.out.println(li);
    }
}
```

### Type Erasure

컴파일러는 컴파일 타임에 타입 파라미터를 사용하는 대상의 타입을 컴파일러가 정하는 타입으로 대체하는 Type Erasure를 실행하게 된다. 컴파일한 바이트코드에서 T 대신 특정 타입으로 대체한다.

Type Erasure의 규칙

- 제네릭 타입의 타입 파라미터가 상하한이 있는 경우에는 타입 파라미터를 한계 타입으로, 없는 경우 모든 타입 파라미터를 object로 바꾼다.  따라서 생성 한 바이트 코드는 보통의 클래스, 인터페이스 및 메섯드 만 포함한다.
- type-safety를 유지하기 위해 필요한 경우 타입 캐스팅을 사용할 수 있다.
- 제네릭 타입을 상속받은 클래스에서 다형성을 유지하기 위해 브리지 메서드를 생성한다.

### 제네릭 타입 Erasure

Java 컴파일러는 타입 Erasure 프로세스로서 모든 파라미터를 지우고 타입 파라미터가 바인드 된 경우 첫 번째 바인드로 대체하고 타입 파라미터가 바인드 되지 않은 경우 Object 대체한다.

```java
package javageneric;

public class WitchPot<T> {
    private T meterial;

    public WitchPot(T meterial) {
        this.meterial = meterial;
    }
    public T get() {
        return this.meterial;
    }
    public void set(T meterial) {
        this.meterial = meterial;
    }
}
```

### 브릿지 메소드

제네릭 클래스를 상속받거나 제네릭 인터페이스를 구현하는 클래스 또는 인터페이스를 컴파일 할 때 컴파일러는 타입 Erasure 프로세스의 일부로 브리지 메서드 라는 합성 메서드를 만들어야 할 수 있다.

일반적으로 브리지 메서드에 대해서는 걱정할 필요가 없지만 stack trace에 나타나는 경우 당황 할 수 있기 때문에 알아두는 것이 좋다.

### 제네릭 타입 주의사항

- 프리미티프 타입을 타입 인자로 사용할 수 없다. 
- 타입 매개변수로 인스턴스를 생성할 수 없다. 
- 타입 매개변수는 정적 필드로 사용할 수 없다.
- 제네릭 타입에 캐스팅 또는 instanceof 사용 불가
- 제네릭 타입 배열 생성 불가
- 제네릭 클래스는 Throwable 클래스를 직접 또는 간접적으로 상속받을 수 없다.
- 제네릭 메소드의 타입 매개변수의 객체를 catch 할 수 없다.
- 타입 Erasure 단계 후에 동일한 서명을 가지게 되는 메소드 오버로딩 불가능.

------

해당 블로그 가기 :

https://rockintuna.tistory.com/102


