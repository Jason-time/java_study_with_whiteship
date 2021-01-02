## 목표

자바의 패키지에 대해 학습하세요.

## 학습할 것 (필수)

- package 키워드
- import 키워드
- 접근제어자
- 클래스패스
- CLASSPATH 환경변수
- -classpath 옵션

## 마감일시

2021년 1월 2일 토요일 오후 1시까지.

# 패키지

package c.jaavapackage

- 마치 폴더로 파일들을 정리하고 묶어 주는 것처럼 클래스를 구분 짓는 개념
- 자바는 패키지의 가장 상위 디렉토리에서 실행함
- 소스 제일 윗줄에 있어야 함
- 패키지는 소스에 하나만 선언해야 함
- 폴더의 이름은 패키지의 이름과 동일해야 함
- 패키지의 이름을 정할 때 java로 시작하면 안 됨. 

### 패키지 이름 지정 규칙 ( 주로 사용하는 규칙 )

> java  (자바 기본 패키지)
> javax (자바 확장 패키지)
> org (일반적으로 비영리단체)
> com (일반적으로 영리단체 패키지)

### 패키지 이름 명명 규칙

- 모두 소문자만 가능
- 예약어는 사용 불가 

### import 키워드

import 패키지명.클래스명

다른패키지명에 있는 클래스를 찾지 못할 때 사용함

`import 패키지명.*` 으로 하위 모든 클래스를 가져올 수 있다.

> 인텔리제이, 윈도우 `Alt + Enter` 로 import 가능

import 할 때 `import static` 을 사용하면, static 한 변수, static한 메소드 사용가능

### impoprt를 하지 않아도 되는 패키지

- java.lang 패키지
- 같은 패키지

### 접근 제어자 ( Access Modifier)

public, protected, package-private (접근 제어자 없음), private 

> `public`  접근 가능(누구나)
>
> `protected` 같은 패키지에 있거나, 상속 받은 경우 사용 가능.
>
> `package-private` 특별하게 적어주지 않은 경우. 같은 패키지 내에서 접근 가능.
>
> `private` 해당 클래스 내에서만 접근 가능.

변수의 경우, 변수를 변경 못하게 하고, 메소드를 통해 변경이나 조회할 수 있도록 할 때, 접근 제어자를 사용함.

### 클래스패스

클래스패스란, 클래스를 찾기위한 경로입니다만.

JVM은 CLASSPATH의 경로를 확인하여 클래스 위치를 참조한다.

J2 JDK 버전부터는 /jre/lib/ext 폴더에 클래스 라이브러리들을 복사해서 사용하고 특별히 설정하지 않는다.

.class 파일에 포함된 명령을 실행하기 위해 classpath 에 지정한 경로를 사용한다.

classpath는 디렉토리와 파일을 ;으로 구분한 목록이지요.

classpath 를 지정하기 위해서는

- CLASSPATH 환경변수 사용
- java runtime 에 -classpath 옵션 사용.

### java runtime에 옵션을 사용할 수도 있어요.  -classpath

> javac <options> <source files>
>
> 컴파일하기 위해 참조할 클래스 파일들을 찾기 위해서 파일 경로 지정해주는 옵션이고요.

필요한 클래스 파일들이 C:\Java 에 있다면,

> javac -classpath c:\Java\Hello.java 로 함.

단축어 cp를 사용해도 되고요.

` javac -cp C:\Java\Hello.java`



참고 

https://kils-log-of-develop.tistory.com/430



>  백기선님의 도움으로 이렇게 공부할 수 있는 시간을 확보할 수 있는 기회를 만들기 위해 노력할 수 있어 행복합니다. 새해에도 항상 건강하시고 하는일 모두 잘 되시길 바랍니다.  
