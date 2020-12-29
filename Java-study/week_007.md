# 7주차 과제: 패키지

## 목표

자바의 패키지에 대해 학습하세요.

## 학습할 것 (필수)

- package 키워드
- import 키워드
- 클래스패스
- CLASSPATH 환경변수
- -classpath 옵션
- 접근지시자



## 패키지(package)

자바에서 패키지(package)란 서로 관련 있는 클래스와 인터페이스의 집합을 의미한다.

자바에서 패키지는 물리적으로 하나의 **디렉터리**를 의미한다. 따라서 하나의 패키지에 속한 클래스나 인터페이스 파일은 모두 해당 패키지 이름의 디렉터리에 포함되어 있다.

#### 패키지의 특징

- 서로 관련이 있는 클래스나 인터페이스를 함께 묶음으로써 파일을 효율적으로 관리할 수 있다.

- 클래스들이 필요할 때만 사용될 수 있도록 해준다.

- 클래스를 패키지 이름과 함께 계층적인 형태로 사용함으로써 다른 그룹에 속한 클래스와 발생할 수 있는 클래스 이름간의 충돌을 막아준다.

#### 패키지 선언

클래스나 클래스가 속하는 패키지는 ``package``라는 키워드와 함께 지정된다. 패키지 선언은 다음과 같이 할 수 있다.

```java
package study.week07;
```

패키지의 선언은 클래스나 인터페이스의 소스파일``(.java)``의 맨 첫 줄에 위와 같은 명령문을 적어주면 된다. 디렉토리의 계층 구조는 점(.)으로 구분 된다.

원칙적으로 모든 클래스는 반드시 하나의 패키지에 속해있어야 하지만, 패키지를 선언하지 않는다고 해서 컴파일 단계에서 에러가 발생하지는 않는다. 왜냐하면 클래스에서 따로 패키지를 선언해주지 않으면, 그 클래스는 기본적으로 **default package**에 속하게 되기 때문이다. 

#### 패키지 제약사항

1. 소스의 가장 첫 줄에 위치해야 한다. 
2. 하나의 소스파일에는 단 한 번의 패키지 선언만을 허용한다.
3. 패키지 이름과 클래스가 위치한 폴더 이름은 같아야 한다.
4. 패키지 이름은 java로 시작해서는 안된다. java 패키지는 자바의 기본 패키지로 JVM 개발자들만이 생성할 수 있는 패키지이기 때문.
   - **패키지 이름 작성시 유의사항**
     - 패키지 이름은 모두 소문자로 지정해야한다.(권장사항)
     - 자바의 에약어를 사용해서는 안된다. 패키지 이름에 중간에라도 ``int``와 같은 예약어가 위치하면 컴파일 시 에러가 발생한다.
     - 패키지 이름은 숫자로 시작할 수 없다.



## import

위와 같이 선언한 패키지에 속한 클래스를 다른 파일에서 사용하기 위해서 사용되는 것이 ``import`` 키워드다.

패키지에 속한 클래스를 사용하기 위해서는 클래스의 패키지명을 모두 적어줘야 하는데, ``import``문은 이를 쓰지 않고도 이용할 수 있도록 만들어 준다. 

``import`` 문은 자바 컴파일러와 JVM에게 코드에서 사용할 클래스의 패키지에 대한 정보를 미리 제공하는 역할을 한다.

#### import 문 선언

import 문은 다음과 같이 선언할 수 있으며, ``package``와 ``Class`` 선언 사이에 위치해야 한다.

```java
import java.awt.event.*;			// import 패키지명.*; 패키지 내 모든 클래스
```

위와 같이 선언하면 ``java.awt.event`` 패키지 내에 있는 모든 클래스들을 가져오는 것이며,

```java
import java.awt.event.ActionEvent;	// import 패키지명.클래스명; 패키지 내 특정 클래스
```

이렇게 선언하면 ``java.awt.event`` 패키지 내에 있는 ``ActionEvent`` 클래스만 가져온다.

만약에 ``import`` 선언 없이 클래스를 직접 사용하려면, 패키지 전체 주소를 가져와 다음과 같이 사용할 수 있다.

```java
java.awt.event.ActionEvent myEvent = new java.awt.event.ActionEvent(); 
```

#### static import

``import`` 문은 ``static`` 클래스, 메소드, 데이터 필드들에도 적용이 가능하다.

자주 사용하는 클래스나 메소드를 ``static``으로  ``import``하면 코드를 간소화하여 작성할 수 있다.

```java
package example.week07;

import static java.lang.System.out;

public class statictest {
    public static void main(String[] args){
//        System.out.println("Hello");        
        out.println("Hello");
    }
}
```









클래스패스 개념 자체

클래스패스 환경변수 사용방법, 

접근지시자



### Reference URL

> https://programmers.co.kr/learn/courses/5/lessons/172
>
> https://blog.naver.com/29java/70188825312
>
> https://muckycode.blogspot.com/2017/07/java-package.html
>
> https://ko.wikipedia.org/wiki/자바_패키지