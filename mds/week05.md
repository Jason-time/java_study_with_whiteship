
5주차 과제
==========
* 과제링크 <https://github.com/whiteship/live-study/issues/5>
## 클래스 정의하는 방법
```java
class A {
   상수(static final) 또는 클래스 변수
   
   인스턴스 변수
   
   생성자
   
   메소드
}
```
class에서 지정할 수 있는 접근지시자는 public과 default입니다. 아무런 접근 지시자가 없으면 default로 지정됩니다.
## 객체 만드는 방법 (new 키워드 이해하기)

객체를 만들기 위해서는 객체를 만들 class가 있어야 합니다. class에서 객체를 만들기 위해서 new 키워드를 사용합니다.
```java
Car car = new Car();
```
car 변수에 주소값을 저장합니다.
## 메소드 정의하는 방법
메소드는 접근지시자, 반환값, 메소드명, 매개변수 등을 사용할 수 있습니다.
#### 접근지시자
    접근지시자에는 public, default, protected, private등이 있습니다.
    접근지시자를 지정해주지 않으면 default로 설정됩니다.
#### 반환값
    반환값이 있는 경우도 있지만 없는 경우도 있습니다. 
    반환값이 없으면 void로 표현합니다.
#### 메소드 명
    메소드 명은 주로 명령어로 표기합니다. 예) add()
#### 매개변수
    메소드를 실행하기 위해 필요한 값입니다. 
    메소드에 사용하는 용어는 '매개변수'이고, 함수를 사용할 때 넘겨주는 값은 '인자', '인수'라고 합니다.
## 생성자 정의하는 방법
생성자는 class 명과 같은 이름을 사용합니다. 접근지시자와 매개변수를 가집니다.
```java
class Car {
    String name;
    int year;
    
    public Car(String name, int year) {... } //생성자
}
```
#### 접근지시자
    접근지시자에는 public, default, protected, private가 있어요.
    접근지시자를 지정하지 않으면 default로 설정됩니다.
#### 매개변수
    메소드를 실행하기 위해서 필요한 값을 인자로 받습니다.
    매개변수 숫자와 형식을 맞춰야 합니다.
## this 키워드 이해하기 
this 키워드는 현재 객체를 말합니다.
메소드 매개변수와 객체의 변수명이 같을 때 사용할 수 있어요.
```java
class Car {
    String name;
    int year;
    
    public Car(String name, int year) {
        this.name = name;
        this.year = year;
    }
}
```

과제 (Optional)
===============
- int 값을 가지고 있는 이진 트리를 나타내는 Node 라는 클래스를 정의하세요.
- int value, Node left, right를 가지고 있어야 합니다.
- BinrayTree라는 클래스를 정의하고 주어진 노드를 기준으로 출력하는 - bfs(Node node)와 dfs(Node node) 메소드를 구현하세요.
- DFS는 왼쪽, 루트, 오른쪽 순으로 순회하세요.
