# 4주차 과제: 제어문

### 목표

자바가 제공하는 제어문을 학습하세요.

### 학습할 것

선택문
반복문



## 제어문

코드의 순차적인 흐름을 제어하는 명령문



## 조건문

주어진 조건식의 결과에 따라 별도의 명령을 수행하도록 제어하는 명령문



### if 문

조건식의 결과가 참(true)이면 주어진 명령문을 실행하며, 거짓(false)이면 아무것도 실행하지 않는다.

<img src="week_004.assets/image-20201203232446205.png" alt="image-20201203232446205" style="zoom:80%;" />

```
<문법>
if (조건식) {
	조건식의 결과가 참일 때 실행할 명령문;
}
```

```java
public class Main {
    public static void main(String[] args) {
        char ch1 = 'B';
        char ch2 = 'd';

        if (ch1 >= 'a' && ch1 <= 'z') {
            System.out.println("ch1은 소문자 입니다.");
        }
        if (ch2 >= 'a' && ch2 <= 'z') {
            System.out.println("ch2은 소문자 입니다.");
        }
    }
}
```

```
<실행 결과>
ch2은 소문자 입니다.
```

제어문에 속하는 명령문들은 중괄호로 감싸주어야 하며, 이러한 중괄호 영역을 블록(block)이라고 한다.

위의 예시에서는 ``ch1``은 대문자 이기 때문에 위의 if문은 실행되지 않았고, ``ch2``가 소문자 이기 때문에 아래 if문이 실행되었다.



### if - else문

조건식의 결과가 참(true)이면 if 다음에 주어진 명령문을 실행하고, 거짓(false)이면 else 뒤에 명령문을 실행한다.

<img src="week_004.assets/image-20201203232416388.png" alt="image-20201203232416388" style="zoom:80%;" />

```
<문법>
if (조건식) {
	조건식의 결과가 참일 때 실행할 명령문;
} else {
	조건식의 결과가 거짓일 때 실행할 명령문;
}
```

```java
public class Main {
    public static void main(String[] args) {

        int n1 = 100;

        if (n1 % 3 == 0) {
            System.out.println("100은 3의 배수 입니다.");
        } else {
            System.out.println("100은 3의 배수가 아닙니다.");
        }
    }
}
```

```
<실행결과>
100은 3의 배수가 아닙니다.
```

위의 예시에서는 ``n1``은 3의 배수가 아니기 때문에 if 뒤에 있는 명령문은 실행되지 않고, else 뒤의 명령어가 실행된 것을 확인할 수 있다.



### if - else if - else 문

두 개의 if - else 문을 연달아 작성한 형태이며, 중첩된 if문을 좀 더 간결하게 표현할 수 있다. 

<img src="week_004.assets/image-20201203232416388.png" alt="image-20201203232416388" style="zoom:80%;" />

```
<문법>
if (조건식1) {
	조건식1의 결과가 참일 때 실행할 명령문;
} else if (조건식2) {
	조건식2의 결과가 참일 때 실행할 명령문;
} else {
	조건식1과 조건식2의 결과가 모두 거짓일 때 실행할 명령문;
}
```

```java
public class Main {
    public static void main(String[] args) {

        int n1 = 100;

        if (n1 % 3 == 0) {
            System.out.println("100은 3의 배수 입니다.");
        } else if (n1 % 5 == 0){
            System.out.println("100은 5의 배수 입니다.");
        } else {
            System.out.println("100은 3의 배수도 5의 배수도 아닙니다.");
        }
    }
}
```

```
<실행 결과>
100은 5의 배수 입니다.
```



### switch문

if - else 문과 마찬가지로 주어진 조건 값의 결과에 따라 다른 명령을 수행하는 조건문이며, if - else 문 보다 가독성이 더 좋다는 장점이 있다.

하지만 switch문의 조건 값으로는 ``byte``, ``short``, ``char``, ``int``형의 변수나 리터럴만 사용이 가능하다. (래퍼 클래스 포함) 그리고 ``enum`` 키워드를 사용한 열거체와 ``String`` 클래스의 객체도 사용할 수 있다.

<img src="week_004.assets/image-20201203232321310.png" alt="image-20201203232321310" style="zoom:80%;" />

```
<문법>
switch (조건 값) {
	case 값1:
		조건 값이 값1일 때 실행할 명령문;
		break;
    case 값2:
    	조건 값이 값2일 때 실행할 명령문;
    	break;
    ...
    default:
    	조건 값이 어떠한 case 절에도 해당하지 않을 때 실행할 명령문;
    	break;
}
```

``default``절은 조건 값이 위에 나열된 어떠한 case 절에도 해당하지 않을 때만 실행된다. 이 절은 반드시 존재해야 하는 것은 아니고 필요할 때만 선언할 수 있다. 하지만 이는 case가 어떤 조건을 다 커버할 경우에만 해당하며, 조건 값이 case절에 해당이 안될 때 ``default`` 절이 없으면 에러가 발생한다.

```java
public class Main {
    public static void main(String[] args) {
        int n = 2;

        switch (n){
            case 1:
                System.out.println("1 입니다");
                break;
            case 2:
                System.out.println("2 입니다");
                break;
            case 3:
                System.out.println("3 입니다");
                break;
            default:
                System.out.println("그 외의 숫자 입니다.");
        }
    }
}
```

```
<실행 결과>
2 입니다
```

각 case 절 및 default 절은 반드시 ``break``키워드를 포함하고 있어야 한다. ``break``는 조건 값이 해당하는 case 절이나 default 절이 실행된 뒤에 전체 switch 문을 빠져나가게 해준다. 

만약에 ``break`` 키워드가 없다면, 조건에 해당하는 switch 문의 case 절 이후의 모든 case 절이 전부 실행될 것이기 때문이다.

```java
public class Main {
    public static void main(String[] args) {
        int n = 2;

        switch (n){
            case 1:
                System.out.println("1 입니다");
            case 2:
                System.out.println("2 입니다");
            case 3:
                System.out.println("3 입니다");
            default:
                System.out.println("그 외의 숫자 입니다.");
        }
    }
}
```

```
<실행 결과>
2 입니다
3 입니다
그 외의 숫자 입니다.
```

위와 같이 ``break`` 키워드가 없으면, 2에 해당하는 절 이후의 모든 case 안에 있는 명령문이 실행된 것을 확인할 수가 있다.

그리고 switch 문의 조건으로 여러 개의 case 절을 사용하여 여려 개의 조건 값을 한 번에 검사할 수 있다.

```java
public class Main {
    
    public enum DayOfWeek{
        MON, TUE, WED, THU, FRI, SAT, SUN
    }
    
    public static void main(String[] args) {        
        DayOfWeek day = DayOfWeek.FRI;

        switch (day){
            case MON:
            case TUE:
            case WED:
            case THU:
            case FRI:
                System.out.println("평일 입니다");
                break;
            case SAT:
            case SUN:
                System.out.println("휴일 입니다");
                break;
        }
    }
}
```

```
<실행 결과>
평일 입니다
```



## 반복문

반복문이란 똑같은 명령을 일정 횟수만큼 반복하여 수행하도록 제어하는 명령문이다.



### while 문

while 문은 특정 조건을 만족할 때 까지 게속해서 주어진 명령문을 반복 실행한다.

<img src="week_004.assets/image-20201203232253115.png" alt="image-20201203232253115" style="zoom:80%;" />

```
<문법>
while (조건식){
	조건식의 결과가 참일 동안 반복적으로 실행할 명령문;
}
```

while문은 우선 조건식이 참(true)인지를 판단하여, 참이면 내부의 명령문을 실행한다. 내부의 명령문을 전부 실행하고 나면, 다시 조건식으로 돌아와 또 한번 참인지를 판단하게 된다. 이 때 내부의 명령문에는 조건식의 결과를 변경하는 명령문이 존재해야 한다.

이렇게 조건식의 검사를 통해서 반복해서 실행되는 반복문을 루프라고 한다.

```java
public class Main {
    public static void main(String[] args) {
        int i = 0;

        while (i < 5){
            System.out.println( i + "번째 출력 중");
            i++; // 이 문장이 없으면 무한 루프
        }
        System.out.println("while문이 종료 된 후 i의 값 :"+ i );
    }
}
```

```
<실행 결과>
0번째 출력 중
1번째 출력 중
2번째 출력 중
3번째 출력 중
4번째 출력 중
while문이 종료 된 후 i의 값 :5
```

while 문 내부에 조건식의 결과를 변경하는 명령문이 존재하지 않을 때 프로그램이 영원히 반복되게 되는데, 이것을 **무한 루프**에 빠졌다고 한다. 무한 루프는 특별히 의도한 경우가 아니라면 반드시 피해야 하는 상황이다.

따라서, while문을 작성할 때는 조건식의 결과가 어느 순간 거짓(false)을 갖도록 조건식의 결과가 변경되는 명령문을 반드시 포함시켜야 한다.



### do - while문

while 문은 루프에 진입하기 전에 먼저 조건식을 검사 하는 반면에, do-while문은 먼저 루프를 한 번 실행한 후에 조건식을 검사한다. 

즉, do-while 문은 표현식의 결과와 상관없이 무조건 한 번은 루프를 실행한다.

<img src="week_004.assets/image-20201203232234223.png" alt="image-20201203232234223" />

```
<문법>
do {
	조건식의 결과가 참인 동안 반복적으로 실행할 명령문;
} while (조건식);
```

```java
public class Main {
    public static void main(String[] args) {
        int i = 0, j = 0;

        while (i > 5){
            System.out.println( i + "번째 출력 중");
            i++;
        }
        System.out.println("while문이 종료 된 후 i의 값 :"+ i );

        do{
            System.out.println( j + "번째 출력 중");
            j++;
        } while (j > 5);
        System.out.println("while문이 종료 된 후 j의 값 :"+ j );
    }
}
```

```
<실행 결과>
while문이 종료 된 후 i의 값 :0
0번째 출력 중
while문이 종료 된 후 j의 값 :1
```

같은 조건이지만 while문 안에 있는 명령문으로 인한 출력은 한 번도 일어나지 않았다. 하지만 do-while문은 조건식의 결과와 상관없이 무조건 한 번의 실행이 있기 때문에 출력을 한 번 한 것을 확인할 수 있다.



### for 문

for문은 자체적으로 초기식, 조건식, 증감식을 모두 포함하고 있는 반복문이다. 따라서 while문 보다 좀 더 간결하게 반복문을 표현할 수 있다.

<img src="week_004.assets/image-20201203232234223.png" alt="image-20201203232234223" style="zoom:80%;" />

```
<문법>
for (초기식; 표현식; 증감식){
	표현식의 결과가 참일 동안 반복적으로 실행할 명령문;
}
```

```java
public class Main {
    public static void main(String[] args) {
        int i;
        for (i = 0; i < 5 ; i++){
            System.out.println( i + "번째 출력 중");
        }
        System.out.println("for문이 종료된 후 i의 값: " + i);
    }
}
```

```
<실행 결과>
0번째 출력 중
1번째 출력 중
2번째 출력 중
3번째 출력 중
4번째 출력 중
for문이 종료된 후 i의 값: 5
```

자바에서는 다음과 같이 for문 안에서만 사용하는 변수를 초기식에서 직접 선언할 수 있는데, 이렇게 for문 안에서 직접 선언된 변수는 for문이 종료되면 같이 소멸한다.

```java
public class Main {
    public static void main(String[] args) {
//        int i;
        for (int i = 0; i < 5 ; i++){
            System.out.println( i + "번째 출력 중");
        }

//        System.out.println("for문이 종료된 후 i의 값: " + i);
        
        for (int i = 0; i < 3 ; i++){
            System.out.println( i + "번째 출력 중");
        }
    }
}
```

```
<실행 결과>
0번째 출력 중
1번째 출력 중
2번째 출력 중
3번째 출력 중
4번째 출력 중
0번째 출력 중
1번째 출력 중
2번째 출력 중
```

위의 예제에서는 반복문을 종료시키기 위해 i라는 이름의 변수를 두 번이나 선언하고 있다. 하지만 이렇게 선언해도 오류가 나지 않는 이유는 i 라는 변수가 for 문이 종료되면 자동으로 소멸되기 때문이다.

따라서 첫번째 for문 아래에서 i라는 변수를 참조하려고 하면 다음과 같은 에러가 발생하는 것을 확인할 수 있다.

> java: cannot find symbol
>   symbol:   variable i



### Enhanced for 문

JDK 1.5 부터는 배열과 컬렉션의 모든 요소를 참조하기 위한 Enhanced for 문이라는 반복문이 새롭게 추가되었다고 한다. 

```
<문법>
for (타입 변수이름 : 배열이나 컬렉션 이름){
	배열의 길이만큼 반복적으로 실행할 명령문;
}
```

Enhanced for문은 명시한 배열이나 컬렉션의 길이만큼 반복되어 실행된다. 루프마다 각 요소는 for 문에서 명시한 변수의 이름으로 저장되며, 명령문에서는 이 변수를 사용하여 각 요소를 참조할 수 있다.
(파이썬을 배운 사람이라면 쉽게 사용할 수 있을 문법인 것 같다.)

```java
public class Main {
    public static void main(String[] args) {

        int[] arr = { 1, 3, 5, 7, 9};

        for(int i : arr){
            System.out.println(i);
        }
    }
}
```

