4주차 과제
==========
``` 자바가 제공하는 제어문을 학습하세요 ```

> **제어문(control statement)** 은 프로그램의 흐름을 바꾸는 역할을 하는 문장들을 말한다. 

#### 선택문
---
- if
	- 기본형식

	```
		if (조건식) { 
			// 조건식이 true 일 때 실행하는 문장을 적는다.
		}
	```
	- 위의 예처럼 조건식을 적고 조건식이 참이면 실행할 문장을 {} 안에 적습니다.
	- 예제
	```
		package com.example;
		class Main {
			public static void main(String[] args){
				int age;
				age = 20;
				if (age > 18){
					System.out.println("성인입니다");
				}
			}
		}
	```
	
	- 결과


 	```
		"C:\Program Files\Java\jdk-12.0.2\bin\java.exe" "-javaagent:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2020.2.4\lib\idea_rt.jar=3549:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2020.2.4\bin" -Dfile.encoding=UTF-8 -classpath C:\Users\coop\IdeaProjects\ch02\out\production\ch02 com.example.Main
		성인입니다

		Process finished with exit code 0

	```
	
- if else
	- 기본형식
	```
		if (조건식) { 
				// 조건식이 true 일 때 실행하는 문장을 적는다.
		} else {
			//조건식이 거짓이면 실행할 문장을 적습니다.
			}
	```
	조건식이 거짓일 경우 실행할 문장을 적어서 조건식이 참일 경우와 거짓일 경우 모두 작동하는 프로그램을 만들 수 있어요.
	- 예제
	```
		package com.example;

		class Main {
			public static void main(String[] args){
				int age;

				age = 10;
				if (age > 18){
					System.out.println("성인입니다");
				} else {
					System.out.println("미성년자");
				}
			}
		}
	```
	- 결과
	```
		"C:\Program Files\Java\jdk-12.0.2\bin\java.exe" "-javaagent:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2020.2.4\lib\idea_rt.jar=3654:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2020.2.4\bin" -Dfile.encoding=UTF-8 -classpath C:\Users\coop\IdeaProjects\ch02\out\production\ch02 com.example.Main
		미성년자

		Process finished with exit code 0

	```
- switch 

>하나의 조건식으로 많은 경우의 수를 처리하고자 할 때 사용하면 좋습니다.

	- 예제 
	```
		package com.example;
		class Main {
			public static void main(String[] args){
				int num;
				num = 1;
				switch (num) {
					case 1:
						System.out.println("숫자1");
						break;
					case 2:
						System.out.println("숫자2");
						break;
					default:
						System.out.println("숫자1이아님");
				}
			}
		}
	```
	
	- 결과
	```
		"C:\Program Files\Java\jdk-12.0.2\bin\java.exe" "-javaagent:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2020.2.4\lib\idea_rt.jar=3694:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2020.2.4\bin" -Dfile.encoding=UTF-8 -classpath C:\Users\coop\IdeaProjects\ch02\out\production\ch02 com.example.Main
		숫자1

		Process finished with exit code 0

	```

#### 반복문
---
- for
	- for 문은 반복 횟수를 알고 있을 때 사용하면 좋습니다.
	- 예제
	```
		package com.example;
		class Main {
			public static void main(String[] args){
			   for(int i=1; i<=2; i++){
				   System.out.println("잘했어요.");
				}
			}
		}
	```
	결과
	```
		"C:\Program Files\Java\jdk-12.0.2\bin\java.exe" "-javaagent:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2020.2.4\lib\idea_rt.jar=3722:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2020.2.4\bin" -Dfile.encoding=UTF-8 -classpath C:\Users\coop\IdeaProjects\ch02\out\production\ch02 com.example.Main
		잘했어요.
		잘했어요.

		Process finished with exit code 0
	```
	- i의 초깃값을 1로 설정하고, i의 값이 2가 될 때까지 반복합니다. 그래서 두번 반복합니다.
- while
	- for문 보다 간결합니다. 조건식이 true 일때 계속 실행시키고자 할 때 사용합니다.
	- 예제
	```
		package com.example;
		class Main {
			public static void main(String[] args){
				int i=1;
				while (i<=2) {
				   System.out.println("잘했어요.");
				   i++;
				}
			}
		}

	```
	- 결과
	```
		"C:\Program Files\Java\jdk-12.0.2\bin\java.exe" "-javaagent:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2020.2.4\lib\idea_rt.jar=3736:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2020.2.4\bin" -Dfile.encoding=UTF-8 -classpath C:\Users\coop\IdeaProjects\ch02\out\production\ch02 com.example.Main
		잘했어요.
		잘했어요.

		Process finished with exit code 0
	```
	- 주의 할 점은 i++를 제외하면 무한반복에 빠진다는 것입니다. 반드시 종결조건을 만들기 위해서 i++을 표기해야 합니다.
- do while
	- 반드시 한 번은 실행하는 반복문입니다. 자주 사용하지는 않습니다.
	- 예제
	```
		package com.example;
		class Main {
			public static void main(String[] args){
				int i=1;
				do {
					System.out.println("잘했어요.");
					i++;
				} while (i<=2);
			}
		}
	```
	- 결과
	```
		"C:\Program Files\Java\jdk-12.0.2\bin\java.exe" "-javaagent:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2020.2.4\lib\idea_rt.jar=3753:C:\Program Files\JetBrains\IntelliJ IDEA Community Edition 2020.2.4\bin" -Dfile.encoding=UTF-8 -classpath C:\Users\coop\IdeaProjects\ch02\out\production\ch02 com.example.Main
		잘했어요.
		잘했어요.

		Process finished with exit code 0

	```
