# 2주차 과제: 자바 데이터 타입, 변수 그리고 배열

### 목표

자바의 프리미티브 타입, 변수 그리고 배열을 사용하는 방법을 익힙니다.

### 학습할 것
- 프리미티브 타입 종류와 값의 범위 그리고 기본 값
- 프리미티브 타입과 레퍼런스 타입
- 리터럴
- 변수 선언 및 초기화하는 방법
- 변수의 스코프와 라이프타임
- 타입 변환, 캐스팅 그리고 타입 프로모션
- 1차 및 2차 배열 선언하기
- 타입 추론, var



## 1. 기본형 타입

#### 데이터 타입(Data type)

데이터가 메모리에 어떻게 저장되고 프로그램에서 어떻게 처리되어야 하는지를 명시적으로 알려주는 것



![img](https://mblogthumb-phinf.pstatic.net/20150117_213/highkrs_1421425975864eM6G8_PNG/%B1%D7%B8%B21.png?type=w2)

*< 이미지 출처: https://blog.naver.com/highkrs/220242895539 >*



#### 프리미티브 타입(Primitive type)

- 기본 값이 있기 때문에 Null이 존재하지 않지만, 기본형 타입에 Null을 넣고 싶다면 래퍼 클래스를 활용할 수 있음
- **스택** 메모리에 **실제 값이 직접 저장**됨
- 컴파일 시점에 데이터 크기가 할당 메모리 범위를 넘어서면 에러가 발생

| 타입                     | 할당 메모리           | 범위                                             | 기본값   | Wrapper class |
| ------------------------ | --------------------- | ------------------------------------------------ | -------- | ------------- |
| boolean                  | 1 byte                | true, false                                      | false    | Byte          |
| byte                     | 1 byte                | -128 ~ 127                                       | 0        | Short         |
| short                    | 2 byte                | -32,768 ~ 32,767                                 | 0        | Integer       |
| **int**<br />(기본형)    | 4 byte                | -2,147,483,648<br />~ 2,147,483,647              | 0        | Long          |
| long                     | 8 byte                | -2^63 ~ 2^63 - 1                                 | 0L       | Float         |
| float                    | 4 byte                | (3.4 X 10^-38) <br />~ (3.4 X 10^38) 의 근사값   | 0.0F     | Double        |
| **double**<br />(기본형) | 8 byte                | (1.7 X 10^-308) <br />~ (1.7 X 10^308) 의 근사값 | 0.0      | Boolean       |
| char                     | 2 byte<br />(UniCode) | 0 ~ 65,535                                       | '\u0000' | Char          |



부동 소수점 실수 변수(float, double)는 정확한 계산을 해야할 때(예)금액)에는 사용하지 않는 것이 좋음. 왜냐하면 정확한 값을 보장받을 수 없기 때문

정확한 계산이 필요할 때엔 JAVA API인 **BigDecimal**을 사용하자.

> 해당 내용 참고: https://reference-m1.tistory.com/105



## 2. 프리미티브 타입과 레퍼런스 타입

#### Reference 타입

- 8개의 기본형 변수를 사용하여 사용자가 직접 만들어 사용하는 데이터 타입을 의미
- 값이 저장된 공간을 참조하는 **주소값**을 **힙(Heap)에 저장**
- 빈 객체를 의미하는 Null이 존재, 그러나 해당 데이터를 Null 값으로 받으면 NullPointException이 발생하므로 변수값을 넣어야 함.

| 타입                  | 할당 메모리<br />(객체의 주소값) | 기본값 | 선언 예시                     |
| --------------------- | -------------------------------- | ------ | ----------------------------- |
| 배열(Array)           | 4 byte                           | Null   | int[] arr = new int[7];       |
| 열거(Enumeration)     | 4 byte                           | Null   |                               |
| 클래스(Class)         | 4 byte                           | Null   | Member member = new Member(); |
| 인터페이스(Interface) | 4 byte                           | Null   |                               |



## 3. 리터럴

#### 리터럴(literal)

변수에 넣은 데이터 그 자체를 의미하며 변하지 않음(메모리 안에 위치한 값)

​	※ **상수(Constant)**: 변하지 않는 변수(한 번 값을 입력하면 다시는 바꿀 수 없음), final 지시자 사용
​		 예) ``final int DAY_OF_WEEK = 7``

- 프리미티브 타입 데이터를 리터럴이라고 칭함
- 클래스 데이터인 인스턴스는 리터럴이 될 수 없으나(인스턴스는 값을 동적으로 사용하기 위해 작성되기 때문), 데이터가 변하지 않도록 설계가 가능함. 이를 불변 클래스(immutable class)라고 칭함. 
  예) 자바의 String, Color 같은 클래스
- 종류: 정수형, 실수형, 문자형, 논리형, 문자열 리터럴이 존재함

![img](https://t1.daumcdn.net/cfile/tistory/99ADC13E5C8F8F6626)

*< 이미지 출처: https://mine-it-record.tistory.com/100 >*

##### 1) 정수 리터럴

- 정수 리터럴은 int 형으로 컴파일
- long(혹은 Long) 타입 리터럴은 숫자 뒤에 l 또는 L을 붙여서 표시

``` java
int a = 15;		// 10진수 리터럴 15
int b = 015;	// 8진수(0으로 시작), 10진수 값으로 13
int c = 0x15;	// 16진수(0x로 시작), 10진수 값으로 21
int d = 0b0101;	// 2진수(0b로 시작), 10진수 값으로 5

long l = 10000L;
```



##### 2) 실수 리터럴

- 소수점 형태나 지수 형태로 표현한 값, double 타입으로 컴파일
- 숫자 뒤에 f(float)나, d(double)을 명시적으로 붙이기도 하며, f(혹은 F)를 붙이면 float 타입, d(혹은 D)를 붙이면 double 타입으로 강제적으로 변환됨. (float은 f를 꼭 붙여줘야 하고, double은 생략이 가능함)

``` java
double f = 0.1234;
double g = 1234E-4; // 1234*10*(-4) 이므로 0.1234와 동일

float h = 0.1234f;
double i = .1234D;
```



##### 3) 문자 리터럴

- 단일 인용부호('')로 문자를 표현하거나, '\u' 다음에 유니코드 값을 입력해 표현할 수 있음

```java
char a = 'H';
char b = "한";
char c = '\uac00';	// '가'라는 문자 표현, 유니코드 값(\u다음에 4자리 16진수로, 2바이트의 유니코드)
```

| 특수문자 리터럴 | 의미                  | 특수문자 리터럴 | 의미                         |
| --------------- | --------------------- | --------------- | ---------------------------- |
| '\b'            | 백스페이스(backspace) | '\r'            | 캐리지 리턴(carriage return) |
| '\t'            | 탭(tab)               | '\ "'           | 이중 인용부호(double quote)  |
| '\n'            | 라인피드(line feed)   | '\ ''           | 단일 인용부호(single quote)  |
| '\f'            | 폼피드(form feed)     | '\\\\\'         | 백슬래시(backslash)          |



##### 4) 논리 타입 리터럴과 그 외 리터럴

- boolean 타입 변수에 치환하거나 조건문을 이용
- 자바에서는 1,0을 true, false로 사용할 수 없음, ``boolean b = 1``이라는 코드를 입력했을 때 오류 발생

``` java
boolean b1 = true;
boolean b2 = 5 < 3;	// 결과는 false이므로 b2에 false라는 값이 저장됨
```

- null 리터럴은 레퍼런스에 대입해서 사용
- 기본타입에는 사용이 불가하고 String 같은 경우에는 사용이 가능함

``` java
int a = null; // 에러
String str = null;
str="JAVA";
```



##### 5) 문자열 리터럴

- 큰 따옴표( "" )로 문자열을 묶어서 표현, 참고로 문자열은 기본 데이터 타입에 포함되지 않음

  ※ **문자열**:기본 데이터 타입에는 속하지 않으며, 'String' 클래스를 이용해 선언할 수 있다.
  	문자열과 문자열 간의 연결은 '+'연산을 이용해 연결

``` java
String str = "Hello!";
```



## 4. 변수 선언 및 초기화

#### 변수(variable)

데이터를 저장하기 위해 프로그램에 의해 이름을 할당받은 메모리 공간을 의미함, 
즉, 변수란 데이터를 저장할 수 있는 메모리 공간을 의미하며, 이렇게 저장된 값은 변경될 수 있음



##### 변수의 이름 생성 규칙

1. 변수의 이름은 영문자(대소문자), 숫자, 언더스코어(_), 달러($)로만 구성할 수 있음
2. 변수의 이름은 숫자로 시작할 수 없음
3. 변수의 이름 사이에는 공백을 포함할 수 없음
4. 변수의 이름으로 자바에서 미리 정의된 키워드(keyword)는 사용 불가

변수의 이름은 해당 변수에 저장될 데이터의 의미를 잘 나타내도록 짓는 것이 좋다



#### 변수의 선언

변수를 사용하기 전에 반드시 먼저 변수를 선언하고 초기화 해야 함. 변수를 선언하는 방법에는 두 가지가 있음

##### 1) 변수 선언만 하는 방법

먼저 변수를 선언하여 메모리 공간을 할당받고, 나중에 변수를 초기화 하는 방법.
이렇게 선언만 된 변수는 초기화되지 않았으므로 해당 메모리 공간에는 알 수 없는 쓰레깃값만이 들어가 있음

따라서, 선언만 된 변수는 반드시 초기화 한 후에 사용해야함

자바에서는 프로그램의 안전성을 위해 초기화하지 않은 변수는 사용할 수 없도록 하고 있음. 
만약 초기화되지 않은 변수를 사용하려고 하면 , 자바 컴파일러는 오류를 발생시킴

```java
/* 
변수 선언만 하는 방법: 타입 변수이름; 
*/
int num;				// 변수 선언
System.out.println(num); // 오류 발생
num = 20;
System.out.println(num); // 20
```



##### 2) 변수 선언과 동시에 초기화 하는 방법

변수의 선언과 동시에 그 값을 초기화 할 수 있으며, 선언하고자 하는 변수들의 타입이 같다면 이를 동시에 선언할 수 있음

```java
/*
변수의 선언과 동시에 초기화 하는 방법
1) 타입 변수이름[, 변수이름];
2) 타입 변수이름 = 초기 설정 값[, 변수이름 = 초기 설정 값]
*/
int num1, num2;					// 같은 타입의 변수를 동시에 선언
double num3 = 3.14;				// 선언과 동시에 초기화
double num4 = 1.23, num5 = 4.56;// 같은 타입의 변수를 동시에 선언하면서 초기화
```

선언하고자 하는 변수의 타입이 서로 다르면 동시에 선언할 수 없음

또한 다음 예제처럼 여러 변수를 동시에 초기화 할 수 없음

```java
double num1, num2;			// 같은 타입의 변수를 동시에 선언
...
num1 = 1.23, num2 = 4.56;	// 하지만 이미 선언된 여러 변수를 동시에 초기화 할 수없음
```



## 5. 변수의 스코프와 라이프타임

#### 스코프(Scope)

변수에 대한 접근과 변수가 존재할 수 있는 영역, 사용 가능한 범위

{} 안에서 변수를 선언했을 경우 영역이 끝나기 전까지는 어디서든 사용이 가능함

``` java
public class ValableScopeExam {	// Class 영역
    int globalScope = 10;		// Class 영역에서 선언한 변수(Global Variable)
    
    public void scopeTest(int value){	// 메소드 영역
        int localScope = 10;			// 메소드 영역 안에서 선언한 변수(Local Variable)
        System.out.println(globalScope);// 사용 가능
        System.out.println(localScope);	// 사용 가능
        System.out.println(value);		// 사용 가능
    }
    
    public static void main(String[] args){
        // 메인 메소드는 static 변수가 아닐 경우 객체화해야 클래스 변수를 사용할 수 있음
        System.out.println(globalScope);	// 사용 불가
        System.out.println(localScope);		// 사용 불가
        System.out.println(value);			// 사용 불가
    }
}
```



##### static

static한 변수(변수 앞에 static 키워드를 붙힘)나, 메소드는 Class를 인스턴스화 하지 않아도 사용할 수 있음.

``` java
public class VariableScopeExam {
    int globalScope = 10; 
    static int staticVal = 7;

    public void scopeTest(int value){
        int localScope = 20;        
    }

    public static void main(String[] args) {
        System.out.println(globalScope);	// 사용 불가
        System.out.println(staticVal);      // 사용 가능
        
        VariableScopeExam v1 = new VariableScopeExam();
        System.out.println(v1.globalScope); // 사용 가능
    }

}
```



static 변수는 값을 저장할 수 있는 공간이 하나만 생성되므로, 인스턴스가 여러개 생성되어도 static 변수는 하나로 공유됨

``` java
public class VariableScopeExam {
    int globalScope = 10; 
    static int staticVal = 7;

    public static void main(String[] args) {
        ValableScopeExam v1 = new ValableScopeExam();
        ValableScopeExam v2 = new ValableScopeExam();
        v1.globalScope = 20;
        v2.globalScope = 30; 

        System.out.println(v1.globalScope);  // 20 출력 
        System.out.println(v2.globalScope);  // 30 출력 

        v1.staticVal = 10;
        v2.staticVal = 20; 

        System.out.println(v1.staticVal);  // 20 출력
        System.out.println(v2.staticVal);  // 20 출력
    }
}
```

- ``globalScope`` 같은 변수는 인스턴스가 생성될 때 생성되기 때문에 인스턴스 변수라고 함

- `` staticVal`` 같이 static한 변수는 클래스 변수라고 함

- 클래스 변수는 ``레퍼런스.변수명`` 으로 사용하기 보다는  ``클래스.변수명``으로 사용하는 것이 바람직함
  예) ``VariableScopeExam.staticVal``



#### 라이프타임(Lifetime)

변수 혹은 레퍼런스의 생존 기간, 즉 생성된 후 부터 폐기될 때 까지의 기간을 의미함



##### 객체의 생명주기

1. Created (생성)

2. In use or reachable (사용중)

3. Invisible (사용 중이며 접근불가)

4. Unreachable (사용되지 않음)

5. Collected (GC 대상이 되는 상태)

6. Finalized (Finalize 를 거친 상태)

7. Deallocated (메모리 해제된 상태)



**1) Created**

객체를 위한 메모리 공간을 Heap 에 할당. 그 다음 Super class의 생성자를 호출 하면서 initializer 및 instance variable의 initialize를 수행한 후에 객체의 생성자를 실행

**2) In use or reachable (사용중)**

객체가 생성되어 다른 객체에 의해 참조되어 있는 상태. 이 상태를 Strongly referenced 상태라고 함.

**3) Invisible (사용 중이며 접근불가)**

Invisible 상태는 Strongly referenced는 되어 있지만 직접 접근할 수 없는 상태이며, 바로 GC의 대상이 되지 않음
모든 객체가 이 상태를 거치지는 않음

``` java
public void run(){
  Object foo = new Object();
  foo.doSomething();
  while( true ){
​    // do something.
  }
}
```

위와 같이 실행했을 때, foo의 역할이 이미 종료되었어도 run() 이 리턴될 때까지 strong reference를 가진다.
이 상태가 바로 invisible 상태인데, strong reference를 가졌지만 foo를 다시 접근할 수 없는 상태이며 while 문이 끝날 때까지 계속 메모리가 유지되는 것임

그래서 memory leak 을 유발할 수 있기 때문에 명시적으로 null 을 만들어주는 것이 좋다.
null이 되면 strong reference가 해지되면서 Unreachable 상태가 되기 때문

**4) Unreachable (사용되지 않음)**

strong reference 가 존재하지 않을 경우이며 이 상태의 객체는 GC의 후보가 됨. 
후보가 된다고 해서 바로 GC가 되는 것은 아니지만 GC 대상 큐에 들어 간다. 이러한 객체들은 GC의 루트가 가지는 체인에 참조되는 형태이며 GC가 수행될 때 이 루트의 체인을 따라가며 메모리를 해제함

**5) Collected (GC 대상이 되는 상태)**

메모리 해제단계 도입부. 이 상태에서는 GC가 객체의 finlize( 가 정의되어 있는지 판단하게 되고 finlize 가 있다면 finalizer 라는 queue에 넣고 없다면 바로 다음 단계인 finalized 상태로 전환 시킴

**6) Finalized (Finalize 를 거친 상태)**

finalizer를 통해 finalize가 실행된 후의 상태.
finalize는 Collected 상태라고 해서 바로 수행되는 것이 아니라 finalizer의 Queue에 들어가는 것이기 때문에 finalize가 호출되는 시간이 보장되지 않음. 또한 JVM에 따라 수행시간도 다름. 
그래서 finalize 가 구현되어 있다면 객체의 반환시간은 그만큼 더 늦어지게 되고, finalize를 위한 객체의 메모리도 그만큼 증가하게 됨

**7) Deallocated (메모리 해제 된 상태)**

메모리 반환이 끝난 상태로 GC의 동작이 마무리 된 상태



## 6. 타입 변환, 캐스팅 그리고 타입 프로모션

#### 타입 변환(Type conversion)

어떤 데이터 하나의 타입을 다른 타입으로 바꾸는 것
자바에서는 boolean형을 제외한 나머지 기본 타입 간의 타입 변환을 자유롭게 수행할 수 있음

자바에서 연산은 동일한 데이터 타입에서 가능
하지만, 서로 다른 데이터 타입끼리의 연산이 필요할 때가 있음. 이 때 변수의 데이터 타입을 바꿔주는 작업이 필요

메모리에 할당받은 바이트의 크기가 사대적으로 작은 타입에서 큰 타입으로의 타입 변환은 생략할 수 있음
하지만, 메모리에 할당받은 바이트의 크기가 큰 타입에서 작은 타입으로의 타입 변환은 데이터의 손실이 발생함
따라서 상대적으로 바이트의 크기가 작은 타입으로 타입 변환을 할 경우 컴파일 오류가 발생.

데이터 타입 변환의 종류는 자동 타입 변환(묵시적 타입 변환, Type Promotion), 강제 타입 변환(명시적 타입 변환, Type Casting)이 있음



##### 1) 자동 타입 변환(Type Promotion)

대입 연산이나 산술 연산에서 컴파일러가 자동으로 수행해주는 타입 변환
자바에서는 데이터의 손실이 발생하지 않거나, 데이터의 손실이 최소화되는 방향으로 자동 타입 변환을 진행
또한, 자바에서는 데이터의 손실이 발생하는 대입 연산은 허용하지 않음

``` java
double num1 = 10;	// int형 데이터인 10이 double형으로 자동 타입 변환
int num2 = 3.14;	// 데이터의 손실이 발생(데이터 표현 범위: double > int)하여 컴파일 오류 발생
double num3 = 7.0f + 3.14;	// float형 데이터가 double형으로 자동 타입 변환되며 산술 진행

System.out.println(num1);	// 10.0 출력
System.out.println(num3);	// 10.14 출력
```

다음과 같이 자바 컴파일러가 자동으로 수행하는 타입 변환은 언제나 데이터의 손실이 최소화 되는 방향으로 이루어지며, 다음과 같은 방향으로 자동 타입 변환이 이루어짐

- byte -> short, char -> int -> long -> float -> double

``` java
byte num1 = 100;        // 자동 타입 변환(byte형 변수가 표현할 수 있는 범위내에 있음)
byte num2 = 200;        // 오류 발생(byte형 변수가 표현할 수 있는 범위를 벗어남)

int num3 = 9876543210;  // 오류 발생(int형 변수가 표현할 수 있는 최대 범위(2,147,483,647) 초과)
long num4 = 9876543210; // 오류 발생(int형 변수가 표현할 수 있는 최대 범위(2,147,483,647) 초과)

float num5 = 3.14;      // 오류 발생(float형 변수가 표현할 수 있는 범위를 벗어남)

int num3 = 9876543210L;  // 오류 발생(int형 변수가 표현할 수 있는 범위를 벗어남)
long num4 = 9876543210L; // 자동 타입 변환(리터럴의 마지막에 L이나 l 접미사를 추가하여 long형 리터럴로 명시)
```



##### 2) 강제 타입 변환(Type Casting)

사용자가 타입 캐스트 연산자()를 사용하여 강제적으로 수행하는 타입 변환

자바에서는 다음과 같이 명시적 타입 변환을 수행할 수 있음

``` java
(변환할 타입) 변환할데이터
```

변환시키고자 하는 데이터의 앞에 괄호를 넣고 그 괄호 안에 변환할 타입을 작성하면 됨
자바에서는 괄호를 타입 캐스트(Type cast) 연산자라고 함

``` java
int num1 = 1, num2 = 4;

// 나눗셈의 결과로 0 출력(int형으로 자동타입 변환), 그리고 자동 형변환 실행(0.0)
double result1 = num1 / num2; 

// num1을 double형으로 강제 타입 변환, 따라서 연산 수행을 위해 num2도 double형으로 자동 형변환 실행
double result2 = (double) num1 / num2;

System.out.println(result1);	// 0.0 출력
System.out.println(result2);	// 0.25 출력
```



## 7. 1차 및 2차 배열 선언

#### 배열(array)

배열은 같은 타입의 변수들로 이루어진 유한 집합

- 배열 요소(element): 배열을 구성하는 각각의 값

- 인덱스(index): 배열에서의 위치를 가리키는 숫자, 자바에서 인덱스는 언제나 0부터 시작하며, 0을 포함한 양의 정수만을 가질 수 있음

같은 타입의 데이터를 많이 다뤄야 하는 경우에 사용할 수 있는 가장 기본적인 자료구조

배열은 선언되는 형식에 따라 1차원 배열, 2차원 배열 그리고 그 이상의 다차원 배열로 선언할 수 있음



##### 1차원 배열

타입은 배열 요소로 저장되는 변수의 타입을 명시

배열 이름은 배열이 선언된 후에 배열에 접근하기 위해 사용됨

자바에서는 배열 선언 방법으로 두 가지 방법을 모두 사용할 수 있지만, 첫 번째 방법 `` 타입[] 배열이름 ``만을 사용하는 것이 좋다.

자바에서는 배열도 모두 객체이므로, 각각의 배열은 모두 자신만의 필드와 메소드를 가지고 있음.

**선언 및 생성 방법**

```
***선언 방법***
1) 타입[] 배열이름;
2) 타입 배열이름[];

***생성 방법***
배열이름 = new 타입[배열길이];

***선언과 생성을 동시에 하는 방법***
타입[] 배열이름 = new 타입[배열길이];
```

```java
int[] grade1;
int grade2[];

grade1 = new int[5];

int[] grade3 = new int[7];
```



다음과 같이 인텍스를 이용하면 각각의 배열요소에 따로 접근할 수 있음
또한, grade2 배열 처럼 배열의 길이보다 적은 수의 배열 요소만을 초기화할 경우, 나머지 배열 요소들은 배열의 타입에 맞게 자동으로 초기화 됨

```java
int[] grade1 = new int[3]; // 길이가 3인 int형 배열의 선언 및 생성
int[] grade2 = new int[3]; // 길이가 3인 int형 배열의 선언 및 생성 

grade1[0] = 85; // 인덱스를 이용한 배열의 초기화
grade1[1] = 65;
grade1[2] = 90; 

grade2[0] = 85; // 배열의 길이보다 적은 수의 배열 요소만 초기화 

for (int i = 0; i < grade1.length; i++) {
    System.out.print(grade1[i] + " "); // 인덱스를 이용한 배열로의 접근, 85 65 90 출력
}

for (int i = 0; i < grade2.length; i++) {
    System.out.print(grade2[i] + " "); // 인덱스를 이용한 배열로의 접근, 85 0 0 출력 
}
```



하지만 다음과 같이 해당 배열의 길이를 초과하는 인덱스를 사용하면, ArrayIndexOutOfBounds 예외가 발생

``` java
int[] grade = new int[3];   // 길이가 3인 int형 배열의 선언 및 생성
grade[0] = 85;              // 인덱스를 이용한 배열의 초기화
grade[1] = 65;
grade[2] = 90;

System.out.print(grade[4]); // ArrayIndexOutOfBounds 예외 발생
```



**배열의 초기화**

배열도 선언과 동시에 초기화가 가능하며, 다음과 같이 {} 괄호(초기화 블록, initialization block)를 사용하여 초깃값을 나열할 수 있음

``` 
***선언 및 초기화 방법***
1. 타입[] 배열이름 = {배열요소1, 배열요소2, ...};
2. 타입[] 배열이름 = new 타입[]{배열요소1, 배열요소2, ...};
```

두 가지 방법 모두 초기화 블록에 맞춰 자동으로 배열의 길이가 설정됨

그러나 다음과 같은 경우에는 2번째 방법만을 사용하여 초기화 해야 함.

1. 배열의 선언과 초기화를 따로 진행해야 할 경우
2. 메소드의 인수로 배열을 전달하면서 초기화해야 할 경우

``` java
int[] grade1 = {70, 80, 90};		// 선언과 동시에 초기화 방법1
int[] grade2 = new int[]{70, 90, 80};// 선언과 동시에 초기화 방법2

int[] grade3;
grade3 = {70, 90, 80};			// 이미 선언된 배열을 해당 방법으로 초기화하면 오류가 발생

int[] grade4;
grade4 = new int[]{70, 90, 80};	// 이미 선언된 배열은 이 방법으로만 초기화 할 수 있음
```



##### 2차원 배열(Two dimensional array)

2차원 배열이란 배열의 요소로 1차원 배열을 가지는 배열

```
***선언 방법***
1. 타입[][] = 배열이름;
2. 타입 배열 이름[][];
3. 타입[] 배열이름[];
```

![2차원 배열](http://www.tcpschool.com/lectures/img_java_array23.png)

​		*<이미지 출처: http://www.tcpschool.com/java/java_array_twoDimensional>*

``` java
int[][] arr = new int[2][3];	// 2차원 배열 선언 및 생성 방법

int k = 10;
for (int i = 0; i < arr.length; i++) {
    for (int j = 0; j < arr[i].length; j++) {
        arr[i][j] = k; // 인덱스를 이용한 초기화
        k += 10;
    }
} 

for (int i = 0; i < arr.length; i++) {
    for (int j = 0; j < arr[i].length; j++) {
        System.out.print(arr[i][j] + " ");
    }
    System.out.println();	// 10 20 30(줄바꿈)40 50 60 출력
}
```



**배열의 선언과 동시에 초기화**

``` 
***선언 및 초기화 방법***
타입 배열이름[열의길이][행의길이] = {
	{배열요소[0][0], 배열요소[0][1], 배열요소[0][2], ...},
	{배열요소[1][0], 배열요소[1][1], 배열요소[1][2], ...},
	{배열요소[2][0], 배열요소[2][1], 배열요소[2][2], ...},
	...
};
```

``` java
int[][] arr = {
    {10, 20, 30},
    {40, 50, 60}
};
```



**가변 배열(dynamic array)**

자바에서는 2차원 배열을 생성할 때 열의 길이를 명시하지 않음으로써, 행마다 다른 길이의 배열을 요소로 저장할 수 있음. 

이렇게 행마다 다른 길이의 배열을 저장할 수 있는 배열을 가변배열이라고 함

또한 가변 배열도 초기화 블록을 사용하여 배열을 선언과 동시에 초기화할 수 있음

``` java
int[][] arr = new int[3][];
arr[0] = new int[2];
arr[1] = new int[4];
arr[2] = new int[1];

int[][] arr2 = {
    {10, 20},
    {10, 20, 30, 40},
    {10}
};
```



## 8. 타입 추론, var

#### 타입 추론(Type Inference)

코드 작성 당시 타입이 정해지지 않았지만, 컴파일러가 그 타입을 유추하는 것

**Java 10 이상**에서 ```var```라는 Local Variable Type-Inference가 추가됨
(Java 9 버전 이하에서는 일반 변수에 대해 타입 추론을 지원하지 않으며, 이 때의 타입 추론은 Generic과 Lambda에 대한 타입 추론을 의미함)



#### var

var는 local variable이면서 선언과 동시에 초기화가 필수적으로 요구됨

``` java
// java 9 이하
String message = "Good bye, Java 9";
// java 10 이상
var message = "Hello, Java 10";
```

데이터 타입을 명시하지 않아도 컴파일러는 변수에 대입한 오른쪽에 있는 리터럴의 유형으로 부터 타입을 유추하여 주입함

이 기능은 초기화값이 있는 로컬 변수에만 사용할 수 있음

var는 키워드가 아니고 int와 같은 타입의 이름임, 변수의 유형은 컴파일 후 추론되며 나중에 변경할 수 없음





##### 참조 URL

> https://gbsb.tistory.com/6
>
> https://blog.naver.com/highkrs/220242895539
>
> https://blog.naver.com/brickbot/220511845770
>
> 
>
> https://mine-it-record.tistory.com/100
>
> https://roseee.tistory.com/entry/Java-변수-선언하기-데이터-타입과-타입-변환
>
> 
>
> http://www.tcpschool.com/java/java_datatype_variable
>
> https://programmers.co.kr/learn/courses/5/lessons/231
>
> 
>
> https://wakestand.tistory.com/179
>
> https://lemontia.tistory.com/649
>
> 
>
> http://www.tcpschool.com/java/java_datatype_typeConversion
>
> https://stage-loving-developers.tistory.com/8
>
> 
>
> https://velog.io/@bk_log/Java-타입-추론
>
> https://www.baeldung.com/java-10-local-variable-type-inference