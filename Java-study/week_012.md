# 12주차 과제: 애노테이션

### 목표

자바의 애노테이션에 대해 학습하세요.

### 학습할 것 (필수)

- 애노테이션 정의하는 방법
- [@retention](https://github.com/retention)
- [@target](https://github.com/target)
- [@documented](https://github.com/documented)
- 애노테이션 프로세서



## 애노테이션

주석처럼 프로그래밍 언어에 영향을 미치지 않으며 유용한 정보(설정 정보)를 특정 프로그램에게 제공하는 것

예전에는 현업에서 프로그램을 작성할 경우 소스코드와 설정파일(예: .xml)을 분리하여 관리했었다고 한다. 그런데 소스코드를 여러사람이 공유해야 하는 점과 소스코드가 변경될 때마다 설정파일도 동시에 변경해야하는 번거로움과 버전 불일치 등의 문제가 빈번하였는데, 이를 합치기로 하면서 애노테이션이 생겼다고 한다.

애노테이션은 코드에 설정에 대한 정보를 넣기로 한 것이며, 기존 문법을 바꾸지 않아도 되는 장점이 있다. 

사용 예) ``@Test`` 라는 어노테이션의 경우 ``JUnit``이라는 특정 프로그램에서만 유효하며, 테스트 대상이 될 메소드에 이 애노테이션 하나만 추가하면 따로 테스트 될 대상을 지정해주지 않아도 된다.

또한, 예를 들어 스프링의 경우 스프링 컨테이너에게 관리할 대상인 빈에 대한 정보를 XML 파일(``application.xml``)로 작성였는데 지금은 자바코드로 설정파일을 만들어 ``@Bean``이라는 애노테이션을 사용하여 쉽게 빈을 관리할 수 있다.

설정파일의 경우 함부로 수정할 수 없는 것





소스코드 + 소스코드 프로그램에 대한 문서-> 버전문제 때문에 관리를 용이하게 하기 위해 주석으로 바뀌게 됨

``/* .... */ `` : Javadoc 주석(Javac.exe를 위한 주석)



### 표준 애노테이션

Java에서 제공하는 애노테이션



**1) @Override**

오버라이딩을 올바르게 했는지 컴파일러가 체크, javac.exe가 사용하는 애노테이션

오버라이딩을 할 때 메서드 이름을 잘못 적는 실수를 하는 경우가 많음

![image-20210201234024221](week_012.assets/image-20210201234024221.png)

이런 실수를 방지하고자 나온 애노테이션으로, 오버라이딩할 때는 메서드 선언부 앞에 @Override를 붙이면 된다.

이렇게 하면 컴파일 단계에서 오류가 발생하기 때문에 오타 여부를 쉽게 파악할 수 있다. 그래서 메서드 상속 시 이 애노테이션을 붙이는 습관을 들이는 것이 좋다.



**2) @Deprecated**

앞으로 사용하지 않을 것을 권장하는 필드나 메서드를 표시하는 용도로 쓰임

![image-20210201234052576](week_012.assets/image-20210201234052576.png)

자바는 하위호환성을 중요시 여겨서 구 버전의 메서드를 없애지는 않으나, 사용을 권장하지 않는다는 표시로 이 애노테이션을 사용한다.

해당 어노테이션이 붙은 메서드를 사용하여 코드를 컴파일할 경우 다음과 같은 메시지가 나타나는 것을 확인할 수 있다.

![image-20210201234526559](week_012.assets/image-20210201234526559.png)



**3) FunctionalInterface**

함수형 인터페이스에 붙이는 애노테이션으로, 이 인터페이스가 제대로 작성(함수형 인터페이스는 하나의 추상메서드만 가져야 함)이 되었는지 컴파일러가 체크하는 용도로 사용됨

![image-20210201232534517](week_012.assets/image-20210201232534517.png)



**4) SuppressWarnings**

컴파일러의 경고메시지가 나타나지 않게 억제하는 용도로 사용하는 애노테이션

괄호() 안에 억제하고자하는 경고의 종류를 문자열로 지정하여 사용하며, 다음과 같은 방식으로 작성하면 된다.

![image-20210201232956994](week_012.assets/image-20210201232956994.png)



컴파일러가 알려주는 경고를 코드작성자가 이미 파악하여 확인했다는 표시의 의미로 사용됨

둘 이상의 경고를 동시에 억제하려면 괄호 안에 중괄호{}를 사용하여 경고의 종류를 배열 선언하는 것처럼 나열해주면 됨

그리고 `` -Xlint`` 옵션으로 컴파일하면, 경고메시지를 확인할 수 있음

![image-20210201233432277](week_012.assets/image-20210201233432277.png)

대괄호 안에 있는 내용이 경고의 종류임

확인된 경고는 SuppressWarnings 애노테이션을 사용하여 경고를 억제해야, 다음에 발생할 수 있는 새로운 경고를 확인할 수 있기 때문에 이 애노테이션의 사용도 습관을 들이는 것이 좋다.





메타 애노테이션: 애노테이션을 만들 때 사용





## 애노테이션 정의하기

직접 애노테이션을 만들어서 사용할 수 도 있는데, 애노테이션을 정의하는 방법은 다음과 같다.

```java
@interface 애노테이션이름{
    타입 요소이름();	// 애노테이션의 요소를 선언
}
```

애노테이션의 요소는 추상 메서드며, 구현할 필요가 없다. 타입에는 배열, Enum, 다른 애노테이션이 올 수 있다. 

그리고 애노테이션을 적용할 때 요소들을 지정하여 작성해야 하며, 요소의 이름과 타입에 맞게 작성하되 순서는 상관이 없다.

```java
/* 애노테이션 정의 */
@interface Datetime{
    String yymmdd();
    String hhmmss();
}

@interface TestInfo{
    int count();
    String testedBy();
    String[] testTools();
    TestType testType(); // enum TestType { FIRST, FINAL }
    DateTime testDate(); // 자신이 아닌 다른 애노테이션 포함 (@DateTime)
}

/* 애노테이션 사용 */
@TestInfo(
	count = 3, testedBy="Yun", testTools={"Junit", "Mockito"},
    testType = TestType.FIRST,
    testDate = @DateTime(yymmdd="210203", hhmmss="041500")
)
public class Week12Class {}
```

애노테이션으로부터 정보를 얻는 프로그램은 추상메서드를 호출하여 코드 작성자가 지정한 값을 얻어서 사용하는 방식으로 동작한다.



애노테이션 정의 시에 요소에 기본값을 지정할 수 있다. 

애노테이션을 사용할 때 값을 지정하지 않으면 사용이 불가능하지만, 이 때는 값을 지정하지 않고 사용할 경우 기본값을 사용하게 된다.

```java
@interface TestInfo{
    int count() default 1;
}

@TestInfo	// @TestInfo(count=1)과 동일
public class Week12Class {}
```



애노테이션의 요소가 하나이고 이름이 ``value``일 때는 요소의 이름을 생략하고 지정할 수 있다.

```java
@interface TestInfo{
    String value();
}

@TestInfo("passed")	// @TestInfo(value = "passed")
public class Week12Class {}
```



애노테이션의 요소 타입이 배열인 경우에는, 값을 지정할 때 중괄호``{}``를 사용해야 한다.

```java
@interface TestInfo{
    String[] testTools();
}

@TestInfo(testTools={"Junit", "Mockito"}) // 값이 2개 이상일 때
@TestInfo(testTools="Junit")	// 값이 1개일 때는 중괄호 생략 가능
@TestInfo(testTools={})			// 값이 없을 때는 빈 중괄호{} 가 반드시 필요함
public class Week12Class {}
```



### 애노테이션 요소 선언 규칙

애노테이션의 요소를 선언할 때 아래와 같은 규칙을 반드시 지켜야 한다.

1. 요소의 타입은 기본형(primitive type), String, Enum, 애노테이션, Class(설계도 객체)만 허용된다. 

2. 괄호``()``안에 매개변수를 선언할 수 없다. 예) ``String major(int i, int j)``;

3. 예외를 선언할 수 없다. 예) ``String testlist() throws Exception;``

4. 요소를 타입 매개변수로 정의할 수 없다.

   예) ``ArrayList<T> list();``

상수는 가능하다.



### java.lang.annotation.Annotation

java.lang.annotation.Annotation은 모든 애노테이션의 조상이지만 상속은 불가능하다. 인터페이스 이기 때문이다.

Annotation에 정의되어 있는 추상메서드들은 구현되어 있지 않지만 컴파일러가 자동으로 구현해주기 때문에 사용이 가능하다.

그래서 모든 애노테이션들은 Annotation에 정의되어 있는 추상메서드들을 포함하고 있는 셈이며 다른 요소들처럼 구현하지 않고도 사용할 수 있다.





### 마커 애노테이션(Marker Annotation)

요소가 하나도 정의되지 않은 애노테이션이며, 대표적인 마커 애노테이션으로는 ``@Override``와 ``@Test``가 있다.





### Reference URL

> https://youtube.com/playlist?list=PLW2UjW795-f6xWA2_MUhEVgPauhGl3xIp