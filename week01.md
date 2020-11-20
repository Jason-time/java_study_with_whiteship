백기선 선장님과 자바 온라인 스터디
https://github.com/whiteship/live-study/issues/1

1주차 과제 
=====
# JVM이란 무엇인가
- Java Virtual Machine '자바 가상 머신' 약자로 용어 그대로 가상 머신이다. 
- 한 번 코드를 작성하면 리눅스, 윈도우, 맥 등 사용할 수 있도록 해주는 다리 역할을 한다.
- 엄청난 장점이

# 컴파일 하는 방법

- 컴파일이란 .java 파일을 .class 파일로 만드는 것입니다.

		javac 파일이름.java  // 이 명령어로 컴파일 할 수 있다.
- 컴퓨터가 이해할 수 있는 바이트코드를 만드는 것입니다.

## 리눅스에서 컴파일하기 
- 먼저 설치하자.
- 왜 리눅스인가?
	+ 큰 의미가 있는 것은 아니다. 요즘 리눅스 연습하고 있어서 리눅스 환경에서 설치를 해보았고. 사용하는 리눅스는 centos 8 입니다.
- 내려 받기 참조 링크
	- [공식링크] https://www.javahelps.com/2019/04/install-latest-oracle-jdk-on-linux.html 
	- [블로그] https://rimkongs.tistory.com/86
	- [블로그] https://gdtbgl93.tistory.com/168
- 아래 코드로 내려 받는다.
~~~
	wget --no-check-certificate --no-cookies --header "Cookie: oraclelicense=accept-securebackup-cookie" https://download.oracle.com/otn-pub/java/jdk/15.0.1%2B9/51f4f36ad4ef43e39d0dfdbaf6549e32/jdk-15.0.1_linux-x64_bin.tar.gz
~~~
- 아래 내용을 그대로 실행하면 잘 설치가 됩니다.
	1. sudo mkdir /usr/lib/jvm		// 폴더 만들자, 만약 있다면 무시할 수 있다. 
	2. sudo tar -xvzf ~/Downloads/jdk-15_linux-x64_bin.tar.gz // 방금 받은 파일 풀기
	3. mv jdk-15.0.1 /usr/lib/jvm/	// 압축푼 폴더를 옮기자.
	4. sudo vim ~/.bash_profile	//편집하기 위에 파일을 열자
	5. PATH=$PATH:/usr/lib/jvm/jdk-15.0.1/bin	//입력하고, 아래도 입력하자.
	6. export JAVA_HOME=/usr/lib/jvm/jdk-15.0.1	// 입력하자.저장후 종료
- 아래 명령어를 실행.
	~~~
	sudo update-alternatives --install "/usr/bin/java" "java" "/usr/lib/jvm/jdk-15.0.1/bin/java" 0
	sudo update-alternatives --install "/usr/bin/javac" "javac" "/usr/lib/jvm/jdk-15.0.1/bin/javac" 0
	sudo update-alternatives --set java /usr/lib/jvm/jdk-15.0.1/bin/java
	sudo update-alternatives --set javac /usr/lib/jvm/jdk-15.0.1/bin/javac
	~~~
- 설정이 잘 되었는지 아래 명령어 입력해보자
~~~
	update-alternatives --list java
	update-alternatives --list javac
~~~
- 리눅스를 재로그인한다.

- 아래 명령어로 잘 설치되었는지 확인하자.

		java -version 

		vim hello.java		//vim으로 코드 작성해보자.파일 만들고.
- 드디어 코드를 작성하고 컴파일 해봅시다.
 ~~~
	 public class hello {
	         public static void main (String[] ar) {
	                 System.out.println("Hello, world");
	         }
	 }
~~~
- 저장하고 나온 후 

		javac hello.java	//컴파일 하고
		java hello 		//실행하자.

	
**질문**
- 쿠기 관련 이슈란?
	- 설치 명령어에 사용하는 --no-cookies 옵션의미 모르겠네요.

# 실행하는 방법

		java [파일이름]

<img src="/imgs/01_java.jpg" width="40%" title="자바실행" alt="자바실행화면"></img>
# 바이트코드란 무엇인가
- .java 파일은 사람이 이해할 수 있는 코드입니다. 
- 컴퓨터가 이해할 수 있는 코드로 바꿔야 하고 그 파일을 바이트코드 라고 부릅니다.
- JVM이 바이트코드를 컴퓨터가 읽을 수 있게 번역해줍니다.
- .class 파일이 바이트코드 입니다.

# JIT 컴파일러란 무엇이며 어떻게 동작하는지
- Just In Time 컴파일러.약자입니다.
- 동적 번역 이라고 합니다.
- 바이트코드를 바이너리코드로 변환해줍니다.
- 인터프리터와 정적 컴파일 방식을 혼합한 방식입니다.
- 인터프리터 방식의 단점을 보완하기 위해 도입했습니다.
- JIT컴파일러는 번역한 내용을 캐싱해 두어 동일한 메소드 실행시 캐싱된 내용을 실행합니다.
# JVM 구성 요소
- JVM은 크게 네가지 구성 요소를 가집니다.
	1. Class Loader
		- JRE가 바이트코드를 실행할 때 class 객체를 메모리에 생성한다.
		- 인스턴스를 생성하면 Class loader가 메모리에 로드한다.
	2. GC (Garbage Collector)
		- c언어와 달리 JVM이 메모리를 관리합니다.
		- 참조되지 않는 메모리를 정리해줍니다.
	3. Execution Engine
		- 메모리 로드 된 바이트코드를 실행합니다.
		- Class loader가 바이트코드를 메모리에 생성하면 Execution Engine이 실행합니다.
		- 인터프리터 방식이나 JIT 으로 실행합니다.
	4. Runtime Data Area
		- 클래스 영역 / 가비지 컬렉션 힙 영역 / 런타임 스택 영역 / 네이티브 메소드 스택 영역
# JDK와 JRE의 차이
- JDK : Java Development Kit (자바 개발 도구)
- JRE : Java Runtime Environment (자바 실행 환경)
- 개발하기 위해서는 JDK가 필요하고, 실행하기 위해서는 JRE가 필요합니다.
- JDK를 설치하면 JRE가 포함됩니다. 


다운 받을 때 --no-cookies 하는 이유는. 쿠키 이슈는 무엇인지 궁금합니다.
