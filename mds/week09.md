## 목표

자바의 예외처리에 대해 학습하세요.

## 학습할 것 (필수)

- 자바에서 예외 처리 방법 (try, catch,throw,throws,finally)
- 자바가 제공하는 예외 계층 구조
- Exception과 Error의 차이는?
- RuntimeException과 RE가 아닌 것의 차이는?
- 커스텀한 예외 만드는 방법

## 마감일시

2021년 1월 16일 토요일 오후 1시까지.

---

### Error

- 컴퓨터 하드웨어 오동작이나 고장으로 인해 응용프로그램에 이상이 생겼거나 JVM 실행에 문제가 생겼을 경우 발생
- 프로세스에 영향을 준다.
- 시스템 레벨에서 발생한다.

### 종류 

VirtualMachineError

OutOfMemoryError

StackOverflowError

## Exception(예외)

### 개념

- 사용자의 잘못된 조작, 개발자의 잘못된 코딩으로 발생
- 예외처리를 통해 종료하지 않고 정상적으로 작동되게 할 수 있다. (Exception Handling)
- Try Catch문을 통해 할 수 있다.
- 개발자가 구현한 로직에서 발생하고 쓰레드에 영향을 준다.

### 종류

Checked Exception

#### 특징

- 반드시 예외 처리 한다.

#### 확인

- 컴파일 단계

#### 대표 예외

- RuntimeException을 제외한 모든 예외
- IOException
- SQLException 

### Runtime Exception(런타임 예외)

- 예외가 발생할 것을 미리 감지하지 못했을 때 발생.
- 런타임 예외에 해당하는 모든 예외들은 RuntimeException을 확장한 예외들이다.

#### 모든 예외의 부모 클래스는 java.lang.Throwable 클래스이다.

- Exception과 Error 클래스는 Throwable 클래스를 상속받아 처리하도록 되어있다.

- Exception이나 Error를 처리할 때 Throwable로 처리해도 된다.

- Throwable 클래스에 선언되어있다.

- Exception 클래스에서 Overring한 메소드가 10개이상이고 가장 많이 사용하는 메소드는 getMassage, toString, printStackTrace가 있다.

  - getMessage()
    - 예외 메시지를 String 형태로 제공한다.
    - 예외가 출력되었을 때 어떤 예외가 발생되었는지 확인할 때 매우 유용하다.
    - 메세지를 활용하여 별도의 예외 메시지를 사용자에게 보여줄 때 유용하다.
  - toString()
    - 예외처리를 String 형태로 제공한다.
    - getMessage() 메소드보다는 약간 더 자세하게, 예외 클래스 이름도 같이 제공한다.
  - printStatckTrace()
    - 가장 첫 줄에는 예외 메시지를 출력하고, 두 번째 줄 부터는 예외가 발생하게 된 메소드들의 호출 관계 를 출력한다. (스택 트레이스)
    - printStackTrace()는 서비스 운용시 드러내면 안 됨. 취약점 공격 위험

  ### getMessage()

  ```java
  public class ThrowableSample {
      public static void main(String[] args) {
          ThrowableSample sample = new ThrowableSample();
          sample.throwable();
      }
  
      private void throwable() {
          int[] intArray = new int[5];
          try {
              intArray =null;
              System.out.println(intArray[5]);
          } catch (Throwable t) {
              System.out.println(t.getMessage());
          }
  
      }
  }	//출력 null 간단하게 출력됨.
  ```

---

```java
public class ThrowableSample {
    public static void main(String[] args) {
        ThrowableSample sample = new ThrowableSample();
        sample.throwable();
    }

    private void throwable() {
        int[] intArray = new int[5];
        try {
            intArray = null;
            System.out.println(intArray[5]);
        } catch (Throwable t) {
            System.out.println(t.getMessage());
            System.out.println(t.toString());
        }

    }
} 
//출력 null
// java.lang.NullPointerException
// 좀 더 자세하게 
```

---



```java
public class ThrowableSample {
    public static void main(String[] args) {
        ThrowableSample sample = new ThrowableSample();
        sample.throwable();
    }

    private void throwable() {
        int[] intArray = new int[5];
        try {
            intArray =null;
            System.out.println(intArray[5]);
        } catch (Throwable t) {
            System.out.println(t.getMessage());
            System.out.println(t.toString());
            t.printStackTrace();
        }

    }
}

```

> //출력
> null
> java.lang.NullPointerException
> java.lang.NullPointerException
>     at me.thewing.liveStudy._9week.ThrowableSample.throwable(ThrowableSample.java:13)
>     at me.thewing.liveStudy._9week.ThrowableSample.main(ThrowableSample.java:6)

- 매우 자세한 메시지를 볼 수 있다.
- 이 메소드는 개발시만 사용해야함.
- 운영 시스템에 적용하면 많은 양의 로그가 쌓인다. 

### 반복문 내에서는 Checked Exception 에 대한 처리는 지양해야 함

```java
for (String item : items) {
    try {
        insert(item);
    }catch (SQLException e) {
        e.printStackTrace();
    }
}
```

- 반복문에 Checked Exception 예외처리 구문이 들어가면 성능이 현저히 떨어진다.
- insert 예외 발생 시, RuntimeExceptoin으로 Wrapping하여 Exception이 발생하도록 한다.
- 반복문 내에서는 예외처리 코드를 제거하는 것이 성능에 유리.

## 자바에서  예외 처리 방법

> java에서 예외 처리하기 위해 try, catch, finally 사용

### 문법

```java
try
{
	예외를 처리하길 원하는 실행 코드;
} catch (e1) {
	e1 예외가 발생할 경우에 실행될 코듣;
} catch (e2) {
	e2 예외가 발생할 경우에 실행될 코드;
}
...
finally {
	예외 발생 여부와 상관없이 무조건 실행될 코드;
}
```

#### try블록

- 기본적으로 맨 먼저 실행되는 코드
- 여기에서 발생한 예외는 catch블록에서 처리한다.

#### catch 블록

- try 블록에서 발생한 예외 코드나 예외 객체를 인수로 받아 처리

#### finally 블록

- try블록에서 예외가 발생하지 않아도 무조건 실행한다.

> catch 블록과 finally 블록은 선택적인 옵션으로 반드시 사용할 필요는 없다. 따라서 사용할 수 있는 모든 try 구문은 아래와 같다.
>
> 1. try	/	catch
> 2. try / finally
> 3. try / catch / ... /finally

#### 예외 throws

```java
public class ThrowSample {
    public static void main(String[] args) {
        ThrowSample sample = new ThrowSample();
        sample.throwException(13);

    }

    private void throwException(int number) {
        try {
            if(number > 12){
                throw new Exception("Number is over than 12");
            }
            System.out.println("Number is "+number);
        } catch (Exception e){
            e.printStackTrace();
        }
    }
}

```

```java
//결과
java.lang.Exception: Number is over than 12 << 이 부분 출력
    me.thewing.liveStudy._9week.ThrowSample.throwException(ThrowSample.java:13)
    me.thewing.liveStudy._9week.ThrowSample.main(ThrowSample.java:6)
```

강제 예외 발생

- throw new Exception("Number is over than 12");

```c
public void throwExceptions(int number) throws Exception {
    if(number > 12){
        throw new Exception("Number is over than 12");
    }
    System.out.println("Number is "+number);
}
```

- 예외가 발생 했을 때 try-catch 로 묶어주지 않아도 메소드를 호출한 메소드로 예외 처리를 위임하여 처리

- throwsException() 이라는 메소드는 Exception 을 던진다고 메소드 선언부에 throws 선언을 해놓았기 때문에, throwsException() 메소드를 호출한 메소드에서는 반드시 try-catch 블록으로 throwsException() 메소드를 감싸주어야 한다. 

- try-catch 블록으로 감싸주지 않으면 컴파일 에러가 발생한다.

  ```c
  public static void main(String[] args) {
      ThrowSample sample = new ThrowSample();
      sample.throwException(13);
      sample.throwExceptions(13); <<여기 오류
  }
  ```

  해결방안 1.

  ```c
  public static void main(String[] args) {
        ThrowSample sample = new ThrowSample();
        sample.throwException(13);
        try {
            sample.throwExceptions(13);
        } catch (Exception e){
  
        }
    }
  try-catch로 묶는 것이다.
  ```

해결방안 2

```c
 public static void main(String[] args) throws Exception {
        ThrowSample sample = new ThrowSample();
        sample.throwException(13);
        sample.throwExceptions(13);
  }
```

호출한 메소드에서도 다시 throws 하면 된다.

### trrows와 throw

- 메소드 선언할 때 매개 변수 소괄호 뒤에 throws 라는 예약어를 적어 준 뒤 예외를 선언하면, 해당 메소드에서 선언한 예외가 발생했을 때 호출한 메소드로 예외가 전달된다. 
- try 블록 내에서 예외를 발생시킬 경우에는 throw 라는 예약어 적어준 뒤 예외 객체를 생성하거나, 생성되어 있는 객체를 명시한다.
- throw 예외 클래스가 catch 블록에 선언되어 있지 않거나, throws 선언에 포함되어 있지 않으면 컴파일 에러 발생
- catch 블록에서 예외를 throw 할 경우에도 메소드 선언의 throws 구문에 해당 예외가 정의해야 한다.

### try - with - resources

- exception 시 resources 를 자동으로 close() 해준다.
- 사용 로직을 작성할 때 객체는 AutoCloseable 인터페이스를 구현한 객체여야 한다.
- 자바 7추가

### AutoCloseable 인터페이스

```java
public interface AutoCloseable { 
    void close() throws Exception; 
}
```

- 자동으로 리소스를 close()해주는 인터페이스

### try - catch - finally 예제

```java
FileOutputStream out = null;
try {
    out = new FileOutputStream("thewing.txt");
    // 생략
} catch (FileNotFoundException e) {
    e.printStackTrace();
} finally {
    if (out != null) { 
        try {
            out.close(); //close 예외가 발생할 수 있다.
        } catch(IOException e) {
                e.printStackTrace();
        }
}
```

### try - with - resources 예제

```jade
try(FileOutputStream out = new FileOutputStream("thewing.txt")) { 
        //생략
} catch(IOException e){ 
    e.printStackTrace(); 
}
```

### Multi Catch

- try 블록내에 예외처리를 다양하게 구현할 때 중복 코드 발생을 줄여 주기 위해 사용합니다.
- 자바 7에서 추가

###### 주의사항

- Multi Catch 문에 사용된 예외들은 예외의 상속관계에서 부모와 자식 관계에 있으면 안 된다.

##### 예제

```c
try {
    //생략
} catch ( NoSuchElementException | RuntimeException e) {

}
Exception in thread "main" java.lang.Error: Unresolved compilation problem:
    The exception NoSuchElementException is already caught by the alternative RuntimeException
```

- NoSuchElementException 은 RuntimeException 의 자식 클래스 이기 때문에 RuntimeException 하나만 처리가 가능하다

## 자바가 제공하는 예외 계층 구조

http://www.tcpschool.com/java/java_exception_class

Object - Throwable - Error - IOError

Object - Throwable - Exception - IOException

## RuntimeException 과 RE가 아닌 것의 차이는?

- RuntimeException 클래스를 상속받는 자식 클래스들은 주로 치명적인 예외 상황을 발생시키지 않는 예외들로 구성
- try / catch 문을 사용하기 보다는 프로그램을 작성하면서 예외가 발생 하지 않도록 주의 하는 것이 좋다.
- 예외 발생 시 트랜잭션 rollback 한다.

## CheckedException

- CheckedExcepton 클래스인 Exceptino 클래스에 속하는 자식 클래스들은 치명적인 예외 상황을 발생시키기 때문에 반드시 try / catch 문을 사용하여 예외 처리를 해야한다.
- 자바 컴파일러는 RuntimeException 클래스 이외의 Exception 클래스의 자식 클래스에 속하는 예외가 가능성이 있는 구문에는 반드시 예외 처리 .
- 만약 예외처리 하지 않으면 컴파일 시 오류 발생.

## 커스텀한 예외 만드는 방법

- Throwable 을 직접 상속 받는 클래스는 Exception과 Error가 있다.

- Error 와 관련된 클래스는 개발자가 손대서는 절대 안 됨.

- 직접 만들 땐 Exception 을 처리하는 클래스라면 java.lang.Exception 클래스의 상속을 받는 것이 좋다.

  ```java
  public class MyException extends Exception{
      public MyException(){
          super();
      }
  
      public MyException(String message){
          super(message);
      }
  }
  ```

#### super() 메소드

- this()  메소드가 같은 클래스의 다른 생성자를 호출할 때 사용된다면, `super()` 메소드는 부모 클래스의 생성자를 호출할 때 사용한다.

- 자식 클래스의 인스턴스를 생성하면, 해당 인스턴스는 자식 클래스의 고유 맴버뿐만 아니라 부모 클래스의 모든 맴버 포함

- 부모 클래스의 멤버를 초기화하기 위해서는 자식 클래스의 생성자에서 부모 클래스의 생성자까지 호출해야 함

- 부모 클래스의 생성자 호출은 모든 클래스의 부모 클래스인 Object 클래스의 생성자까지 올라가며 수행

  ```java
  public class MyException extends Exception{
      public MyException(){
          super();
      }
  
      public MyException(String message){
          super(message);
      }
  }
  public class CustomException {
      public static void main(String[] args) {
          CustomException sample = new CustomException();
          try {
              sample.throwMyException(13);
          } catch (MyException mye) {
              mye.printStackTrace();
          }
      }
  
      private void throwMyException(int number) throws MyException{
          try {
              if(number > 12) {
                  throw new MyException("Number is over than 12");
              }
          } catch (MyException e) {
              e.printStackTrace();
          }
      }
  }
  ```

  > //출력 me.thewing.liveStudy._9week.MyException: Number is over than 12    me.thewing.liveStudy._9week.CustomException.throwMyException(CustomException.java:16)    me.thewing.liveStudy._9week.CustomException.main(CustomException.java:7)

  - MyException 을 던진다고 명시해 놓았지만, 이 메소드를 호출하는 메소드에서는 반드시  MyException 으로 catch 할 필요는 없다.

  - MyException 의 부모 클래스인 Exception 클래스로 catch 해도 무방하다. 그런데, 앞에서 MyException 이 예외 클래스가 되려면  Throwable 클래스의 자식 클래스가 되어야 한다고 이야기했다. 만약  MyException 을 선언할 때 관련된 클래스를 확장하지 않았을 때에는 이 부분에서 제대로 컴파일이 되지 않는다. 다시 말해서, 다음과 같이 MyException 이 아무런 상속을 받지 않고 선언되어있다면,

    ```java
    public class MyException { // extends Exception{
        public MyException(){
            super();
        }
    
        public MyException(String message){
    //        super(message);
        }
    }
    ```

    CustomException 클래스를 컴파일 할 때 에러 메시지들을 만든다.

    ```c
    public class CustomException {
        public static void main(String[] args) {
            CustomException sample = new CustomException();
            try {
                sample.throwMyException(13);
            } catch (MyException mye) {  <<error
                mye.printStackTrace();
            }
        }
    
        private void throwMyException(int number) throws MyException{
            try {
                if(number > 12) {
                    throw new MyException("Number is over than 12");  <<error
                }
            } catch (MyException e) { <<error
                e.printStackTrace();
            }
        }
    }
    ```

    ## 자바 예외 처리 전략

    - 예외를 어떻게 처리할지를 알아두는 것이 좋다.

    - 실행시에 발생할 확률이 매우 높은 경우에는 런타임 예외로 만드는 것이 나을 수도 있다. 즉, 클래스 선언시 extends Exception 대신에 extends RuntimeException 으로 선언하는 것이다. 이렇게 되면 해당 예외를 throw 하는 메소드를 사용하더라도 try-catch 로 묶지 않아도 컴파일시에 예외가 발생하지 않는다. 

    - 이 경우, 예외가 발생할 경우 해당 클래스를 호출하는 다른 클래스에서 예외를 처리하도록 구조적인 안전장치가 있어야 한다.

    - 안전 장치란 try-catch 로 묶지 않은 메소드를 호출하는 메소드에서 예외를 처리하는 try-catch 해두는 것을 말한다. 

      ```java
      public void methodCaller() {
          try {
              methodCaller();
          } catch (Exception e) {
              // 예외처리
          }
      }
      
      public void methodCallee() {
          // RuntimeException 예외 발생 가능성 있는 부분
      }
      ```

      - 이처럼 unchecked exception 인 RuntimeException 이 발생하는 메소드가 있다면, 그 메소드를 호출하는 메소드는 try-catch 로 묶어주지 않더라도 컴파일할 때 문제가 생기지 않는다.
      - 예외가 발생할 확률이 높아, 위 methodCaller() 처럼 try-catch 로 묶어 주는 것이 좋다.

      ```
      try {
      	// 예외발생 가능한 코드
      } catch (SomeException e) {
      	// 여기 아무 코드없음
      }
      ```

    - 이렇게 catch  문장 작성은 피해야 함

    - SomeException 은 어떤 예외를 잡는다는 것을 의미할 뿐 실제 존재한다는 게 아니다. 
    - catch 에 아무런 작업을 하지 않으면 어디서 발생했는지 찾을 수 없다.

    ## 마무리

    - 임의의 예외 클래스를 만들 때에는, 반드시 `try-catch` 로 묶어줄 필요가 있을 경우에만 Exception 클래스를 확장한다.
    - 일반적으로 실행시 예외를 처리할 수 있는 경우에는 RuntimeException 클래스를 확장하는 것을 권장함.
    - catch 문 내에 아무런 작업 없이 공백을 놔두면 예외 분석이 어려워, 반드시 로그처리 같은 예외 처리를 해줘야한다.





---


>  백기선님의 도움으로 이렇게 공부할 수 있는 시간을 확보할 수 있는 기회를 만들기 위해 노력할 수 있어 행복합니다. 새해에도 항상 건강하시고 하는일 모두 잘 되시길 바랍니다.  

블로그 

https://sujl95.tistory.com/62
