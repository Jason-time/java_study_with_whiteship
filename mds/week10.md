# 10주차 : 멀티쓰레드 프로그래밍

## 목표

자바의 멀티쓰레드 프로그래밍에 대해 학습하세요.

## 학습할 것 (필수)

- Thread 클래스와 Runnable 인터페이스
- 쓰레드의 상태
- 쓰레드의 우선순위
- Main 쓰레드
- 동기화
- 데드락

## 마감일시

2021년 1월 23일 토요일 오후 1시까지.

---

## Thread 클래스와 Runnable 인터페이스

#### Process 란

- 실행중인 프로그램
- 프로그램이 운영체제에 의해 메모리 공간을 할당 받아 실행 중인 상태
- 프로세스는 다음으로 구성된다.
  - 데이터와 메모리 등의 자원.
  - 쓰레드로 구성

#### Thread란

- 프로세스 내에서 작업을 수행하는 주체를 의미
- 프로세스는 1개 이상의 쓰레드가 존재
- 두 개 이상 쓰레드를 가진 프로세스를 멀티 쓰레드 프로세스라고 한다.
- 경량 프로세스라고 불리며 가장 작은 실행 단위이다

### Thread 클래스와 Runnable 인터페이스

- 쓰레드를 생성하는 방법은 크게 두 가지 
  1. Runnalbe 인터페이스를 사용
  2. Thread 클래스를 사용
- Thread 클래스는 Runnable 인터페이스를 구현한 클래스. 

> 둘 중 어떤 것을 적용하느냐 차이이다.

- Runnable 과 Thread 모두 java.lang 패키지에 포함되어있다.

### Thread 클래스

```java
package java.lang;
class Thread implements Runnable {
	private static native void registerNatives();
	static {
	registerNatives();
	}
}
```

#### Runnable 인터페이스

```java
package java.lang;
@FunctionalInterface
public interface Runnable {
	public abstract void run();
}
```

### 사용 선택하는 기준은

- Thread 클래스가 다른 클래스를 확장할 필요가 있을 경우는 Runnable 인터페이스를 구현하면 된다. 

- 확장할 필요가 없는 경우에는 Thread 클래스를 사용하는 것이 편하다.

  ##### ThreadSample

  ```java
  public class ThreadSample extends Thread{
  	@Override
  	public void run(){
  		System.out.println("This is ThreadSample's run() method.");
  	}
  }
  ```

  ##### RunnableSample

  ```java
  public class RunnableSample immplements Runnable{
  	@Override
  	public void run(){
  		System.out.printtln("This is RunnableSample's run() method.");
  	}
  }
  ```

  ##### RunThreads

  ```java
  public class RunThreads {
  	public static void main(String[] args) {
  		runBasic();
  	}
  	public static void runBasic() {
  		RunnableSample runnable = new RunnableSample();
  		new Thread(runnable).start();
  		ThreadSample thread = new ThreadSample();
  		thread.start();
  		System.out.println("RunThreads.runBasic() method is ended.");
  	}
  }
  ```

  결과

  > This is RunnableSample's run() method.
  >
  > RunThreads.runBasic() method is ended.
  >
  > This is ThreadSample's run() method.

  - `start() ` 메소드가 끝날 때까지 기다리지 않고, 그 다음줄 `thread` 라는 객체의 `start()` 메소드를 실행.
  - 새로운 쓰레드가 시작하여 `run()` 메소드가 종료하는 것을 기다리지 않고 다음 줄로 넘어감.

### Thread는 순서대로 동작할까.

예제

#### RunMultiThreads

```java
public class RunMultiThreads {
	public static void main(String[] args) {
		runMultiThread();
	}
	public static void runMultiThread() {
		RunnableSample[] runnable = new RunnableSample[5];
		ThreadSample[] thread = new ThreadSample[5];
		for (int loop = 0; loop < 5; loop++) {
			runnable[loop] = new RunnableSample();
			thread[loop] = new ThreadSample();
			
			new Thread(runnable[loop]).start();
			thread[loop].start();
		}
		System.out.println("RunMultiThreads.runMultiThread() method is ended");
	}
}
```

결과

> This is RunnableSample's run() method.
> This is ThreadSample's run() method.
> This is RunnableSample's run() method.
> This is ThreadSample's run() method.
> This is ThreadSample's run() method.
> This is ThreadSample's run() method.
> This is ThreadSample's run() method.
> This is RunnableSample's run() method.
> This is RunnableSample's run() method.
> RunMultiThreads.runMultiThread() method is ended
> This is RunnableSample's run() method.

- 결과처럼 순서대로 실행 하지 않는다.
- 매번 결과가 다르다.ㄷ
- `run()` 메소드가 끝나지 않으면 애플리케이션은 종료하지 않는다.

### Thread sleep 메소드

- `sleep` 메소드는 주어진 시간 만큼 대기 한다.

### sleep 예제

```java
public class EndlessThread extends Thread{
	public void run() {
		while (true) {
			try {				System.out.println(System.currentTimeMillis());
				Thread.sleep(1000);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
		}
	}
}
```

- 중단할 수가 없어서 무한 실행. 직접 실행 중지해야함.
- `Thread.sleep()` 메소드를 사용할 때는 항상 `try-catch` 로 묶어야 한다. 
- 적어도 `InterruptedException` 으로 예외 처리를 해줘야 한다. `sleep()` 메소드는 `InterruptedException` 예외를 던질 수도 있다고 선언 되어 있기 때문이다.

## 쓰레드의 상태

- 쓰레드의 현재 상태를 나타낸다.

| 상태          | 의미                                                         |
| ------------- | ------------------------------------------------------------ |
| NEW           | 쓰레드 객체는 생성되었지만, 아직 시작하지 않음.              |
| RUNNABLE      | 쓰레드가 실행중                                              |
| BLOCKED       | 쓰레드가 실행 중지 상태이며, 모니터 락(monitor lock)이 풀리기를 기다리는 상태 |
| WAITING       | 쓰레드가 대기중인 상태                                       |
| TIMED_WAITING | 특정 시간만큼 쓰레드가 대기중인 상태                         |
| TERMINATED    | 쓰레드가 종료된 상태                                         |

### Thread.join()

- join(), join(0)
  - 해당 쓰레드가 종료될때 까지 기다린다.
- join(60000)
  - 60초 동안 기다린다.
- 매개변수에 음수를 넣으면 `*IllegalArgumentException* ` 예외 발생

### interrupt()

- 현재 수행중인 쓰레드를 중단시킨다.
- 그냥 중지 시키지는 않고 InterruptedException 예외를 발생시키면서 중단함

### stop()

- 안정상의 이유로 deprecated 되었다. 이 메소드 사용금지

```java
public void checkJoin() {
	SleepThread thread = new SleepThread(2000);
	try {
		thread.start();
		thread.join(5000);
		thread.interrupt();
		System.out.println("thread state(after join) ="+thread.getState());
	} catch (Interruptedexception ie) {
		ie.printStackTrace();
	}
}
```

결과

> Sleeping Thread-0
>
> Stopping Thread-0
>
> thread state(after join)=TERMINATED

### Thread 상태확인  메소드

| 리턴 타입      | 메소드 이름 및 매개변수 | 설명                                                         |
| -------------- | ----------------------- | ------------------------------------------------------------ |
| void           | checkAccess()           | 현재 수행중인 쓰레드가 해당 쓰레드를 수정할 수 있는 권한이 있는지를 확인. 권한이 없다면 SecurityException 예외 발생 |
| boolean        | isAlive()               | 쓰레드가 살아 있는지 확인. 해당 쓰레드의 run() 멤소드가 종료되었는지 확인 |
| boolean        | isInterrupted()         | run() 메소드가 정상적으로 종료하지 않고, interrupt() 메소드의 호출을 통해 종료되었는지 확인 |
| static boolean | interrupted()           | 현재 쓰레드가 중지되었는지 확인                              |

### Thread static 메소드 목록

| 리턴 타입     | 메소드 이름 및 매개 변수 | 설명                                                         |
| ------------- | ------------------------ | ------------------------------------------------------------ |
| static int    | activeCount()            | 현재 쓰레드가 속한 쓰레드 그룹의 쓰레드 중 살아 있는 쓰레드의 갯수 반환 |
| static Thread | currentThread()          | 현재 수행중인 쓰레드의 객체를 리턴                           |
| static void   | dumpStack()              | 콘솔 창에 현재 쓰레드의 스택 정보 출력                       |

## 쓰레드의 우선순위

- Java에서 각 쓰레드는 우선순위(priority)에 관한 자신만의 필드를 가진다.

- 이러한 우선순위에 따라 특정  쓰레드가 더 많은 시간 동안 작업을 할 수 있도록 설정한다.

  | 필드                     | 설명                                        |
  | ------------------------ | ------------------------------------------- |
  | static int MAX_PRIORITY  | 스레드가 가질 수 있는 최대 우선 순위를 명시 |
  | static int MIN_PRIORITY  | " 최소 우선순위 명시                        |
  | static int NORM_PRIORITY | 쓰레드 생성 시 기본 우선순위 명시           |

  - `getPriority()` 와 `setPriority()` 메소드를 통해 쓰레드의 우선순위를 반환하거나 변경할 수 있다.

  - 쓰레드 우선순위는 1부터 10까지이며  숫자가 높을수록 우선순위도 높다.
  - 쓰레드의 우선순위는 상대적인 값이다.
  - 우선순위 10인 쓰레드는 우선순위 1 쓰레드 보다 좀 더 많이 실행 큐에 포함.
  - 우선순위가 높으면 좀 더 많은 작업 시간을 할당 받는다.

## MAIN 쓰레드

### Main Thread

- Java는 실행 실행 환경인 JVM 에서 구동된다. 이것이 하나의 프로세스이고 JAVA를 실행하기 위해 우리가 실행하는 `main()` 메소드가 메인 쓰레드이다.

  ```java
  public class MainMethod {
  	public static void main(String[] args) {
  	
  	}
  }
  ```

  - `public static void main (string[] args) {}` 이것이 메인  쓰레드이고 메인 쓰레드의 시작점을 선언하는 것이다.
  - 따로 쓰레드를 실행하지 않고 `main()` 메소드만 실행하는 것을 싱글 쓰레드 애플리케이션 이라고 한다. 

### 멀티 쓰레드 애플리케이션

- 메인 쓰레드에서 쓰레드를 생성하여 실행하는 것을 쓰레드 애플리케이션이라 함.

### Daemon Thread

- Main 쓰레드의 작업을 돕는 보조적인 역할을 하는 쓰레드
- Main 쓰레드가 종료하면 데몬 쓰레드도 강제적으로 자동 종료 한다. 
  - Main 쓰레드의 보조 역할을 하기 때문에, Main 쓰레드가 없어지면 의미가 없어지기 때문.

### Daemon Thread 사용

- Main 쓰레드가 Daemon 이 될 쓰레드의 `setDaemon(true)'  를 호출하면 Daemon 쓰레드가 된다. 

- 예제

- ```java
  DaemonThread
  
  public class DaemonThread extends Thread{
      public void run() {
          try {
              Thread.sleep(Long.MAX_VALUE);
          } catch (Exception e){
              e.printStackTrace();
          }
      }
  }
  public void runCommonThread() {
      DaemonThread thread = new DaemonThread();
      thread.start();
  }
  ```

  - long 최댓값 만큼 대기한다.

#### runDaemonThread

```java
public void runDaemonThread() {
    DaemonThread thread = new DaemonThread();
    thread.setDaemon(true);
    thread.start();
}
```

- 프로그램이 대기하지 않고 그냥 끝난다. 데몬 쓰레드는 해당 쓰레드가 종료되지 않아도 다른 실행중인 일반 쓰레드가 없다면 멈춘다.

### 데몬 쓰레드를 만든 이유?

- 모니터링하는 쓰레드를 별도로 띄어 모니터링을 하다가, Main 쓰레드가 종료하면, 관련된 모니터링 쓰레드가 종료되어야 프로세스가 종료될 수 있다. 
- 모니터링 쓰레드를 데몬 쓰레드로 만들지 않으면 프로세스가 종료할 수 없다. 
- 이렇게 부가적인 작업을 수행하는 쓰레드를 선언할 때 데몬 쓰레드를 만든다.

## 동기화(Synchronize)

- 여러 개의 쓰레드가 한 개의 리소스를 사용하려고 할 때 사용 하려는 쓰레드를 제외한 나머지들을 접근하지 못하게 막는 것.
- 쓰레드에 안전하다고 한다. (Thread-safe)
- 자바에서 동기화 하는 방법은 3가지
  - Synchronized 키워드
  - Atomic 클래스
  - Volatile 키워드

#### Synchronized 키워드

- Java 예약어 중 하나이다
- 변수명이나, 클래스명으로 사용이 불가능하다

####  Synchronized 사용방법

- 메소드 자체를 synchronized로 선언하는 방법(synchronized methods)
- 다른 하나는 메소드 내의 특정 문장만 synchronized로 감싸는 방법(synchronized statements)이다.

## Atomic

- Atomicity(원자성)의 개념은 '쪼갤 수 없는 가장 작은 단위'를 뜻한다
- 자바의 Atomic Type은 Wrapping 클래스의 일종으로, 참조 타입과 원시 타입 두 종류의 변수에 모두 적용이 가능하다. 사용시 내부적으로 CAS(Compare-And-Swap) 알고리즘을 사용해 lock 없이 동기화 처리를 할 수 있다.
- Atomic Type경우 `volatile`과 `synchronized` 와 달리 `java.util.concurrent.atomic` 패키지에 정의된 클래스이다
- CAS는 특정 메모리 위치와 주어진 위치의 value를 비교하여 다르면 대체하지 않는다.
- 사용법은 변수를 선언할때 타입을 Atomic Type으로 선언해주면된다
  - ex) AtomicLong

## 데드락(교착상태, Deadlock)

### Thread Deadlock

- Deadlock(교착상태) 란 , 둘 이상의 쓰레드가 lock을 획득하기 위해 대기하는데, 이 lock을 잡고 있는 쓰레드들도 똑같이 다른 lock을 기다리면서 서로 block 상태에 놓이는 것을 말한다. 
- Deadlock은 다수의 쓰레드가 같은 lock을 동시에, 다른 명령에 의해 획득하려 할 때 발생할 수 있다.



------



해당 블로그 가기 :

https://sujl95.tistory.com/63



---


>  백기선님의 도움으로 이렇게 공부할 수 있는 시간을 확보할 수 있는 기회를 만들기 위해 노력할 수 있어 행복합니다. 새해에도 항상 건강하시고 하는일 모두 잘 되시길 바랍니다.  

블로그 

https://sujl95.tistory.com/62
