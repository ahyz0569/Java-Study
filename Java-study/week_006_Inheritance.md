# 6주차 과제: 상속

## 목표

자바의 상속에 대해 학습하세요.

## 학습할 것 (필수)

- 자바 상속의 특징
- super 키워드
- 메소드 오버라이딩
- 다이나믹 메소드 디스패치 (Dynamic Method Dispatch)
- 추상 클래스
- final 키워드
- Object 클래스



## 상속(Inheritance)

상속이란 기존의 클래스에 기능을 추가하거나 재정의하여 새로운 클래스를 정의하는 것이다.

상속을 이용하면 기존에 정의되어 있는 클래스의 모든 필드와 메소드를 물려받아, 새로운 클래스를 생성할 수 있다. 이 때 기존에 정의되어 있던 클래스를 **부모 클래스(parent class)** 또는 **상위 클래스(super class)**라고도 한다.

그리고 상속을 통해 새롭게 작성되는 클래스를 **자식 클래스(child class)** 또는 **하위 클래스(sub class)** 라고도 한다.

![상속 다이어그램](http://www.tcpschool.com/lectures/img_java_inheritance_diagram.png)

#### 상속 구현 예시

```java
class Person{
    private int age = 40;
    public int year = 1980;
}

class Child extends Person{
    public int height = 140;
    void display(){
        System.out.println(age);        
        System.out.println(year);
        System.out.println(height);
    }
}

public class Week06{
    public static void main(String[] args){
        Child ch = new Child();
        ch.display();
    }
}
```



#### 상속의 장점

1. 기존에 작성된 클래스를 재활용할 수 있어 클래스가 간결해진다.
2. 자식 클래스 설계 시 중복되는 멤버를 미리 부모 클래스에 작성해 놓으면, 자식 클래스에서는 해당 멤버를 작성하지 않아도 된다. 즉, 멤버 중복 선언이 필요없다.
3. 클래스 간의 계층적 관계를 구성함으로써 다형성의 문법적 토대를 마련한다.



#### 상속의 특징

1. 다중 상속을 지원하지 않는다. 즉, **단일 상속(Single Inheritance)**만 가능하다.
   - 다중 상속의 단점
     - 메소드 출처의 모호성: 여러 부모 클래스들 중에서 이름이 같은 메소드가 있을 경우 어떤 메소드를 상속받아야 하는지 모호하여 문제(충돌)가 생김
     - 필요 없는 부분까지 상속을 받아야 하기 때문에 매우 무거워진다.
   - 대신 자바는 **Interface 다중 구현**을 제공한다.
2. 선택적 상속이 불가능 하다. All or Not 만 가능
   - 상속되는 클래스의 속성이나 기능을 선택적으로 상속받을 수 없다. 전부 다 받거나, 아예 받지 않거나 둘 중 하나만 가능하다.
   - 상속을 받게 되면 부모 클래스의 모든 속성과 기능을 상속받아 사용할 수 있다.
     - 하지만, 생성자와 초기화 블록은 상속되지 않는다.
     - 부모 클래스에서 ``private``으로 정의된 멤버 변수는 상속은 가능하지만, **접근은 불가능**하다. 그래서 ``public``으로 선언한 ``setter``또는 ``getter``를 이용해 접근한다.
   - 상속 받은 기능 중 수정을 원하는 기능은 다시 재정의 할 수 있고**(Overriding)**, 필요한 속성이나 기능은 추가하여 작성할 수 있다. ~~객체 생성의 경우에는 재사용만 가능하고 변경,추가는 불가능 하다.~~
   - 자손의 멤버 개수는 조상보다 적을 수 없다.(같거나 많다.)
3. 생성자는 상속되지 않는다.
   - 생성자는 반드시 클래스 이름과 동일하게 써야 하는데, 상속하면 클래스 이름이 달라지기 때문
   - 그러나 재사용을 위해 하위 클래스에서 상위 클래스의 생성자를 호출할 수 있는데, 이는 ``super`` 키워드를 사용하면 가능하다. 단, 반드시 첫 줄에서만 가능하다.
4. 상속의 횟수에 제한을 두지 않는다.
5. 자손의 변경은 조상에 영향을 미치지 않는다.
6. 계층 구조의 최상위에 있는 클래스는 Object 클래스이다.





## Super

``super`` 키워드는 부모 클래스로부터 상속받은 필드나 메소드를 자식 클래스에서 참조할 때 사용하는 키워드다.

부모 클래스의 멤버와 자식 클래스의 멤버 이름이 같을 경우 ``super`` 키워드를 사용하여 접근할 수 있으며, ``this`` 키워드와 사용방법이 비슷하다.

또한, ``super`` 참조 변수를 사용할 수 있는 대상도 인스턴스 메소드뿐이며, 클래스 메소드에서는 사용할 수 없다.

```java
class Person{
    public int a = 4;
    public int b = 10;
}

class Child extends Person{
    public int b = 100;
    void display(){
        System.out.println(a);
        System.out.println(this.a);
        System.out.println(super.a);
        
        System.out.println(b);
        System.out.println(this.b);
        System.out.println(super.b);
    }    
}

public class Week06{
    public static void main(String[] args){
        Child ch = new Child();
        ch.display();
    }
}
```



#### super() 메소드

``this()`` 메소드가 같은 클래스의 다른 생성자를 호출할 때 사용된다면, ``super()`` 메소드는 부모 클래스의 생성자를 호출할 때 사용된다.

자식 클래스의 인스턴스를 생성하면, 해당 인스턴스에는 자식 클래스의 고유 멤버뿐만 아니라 부모 클래스의 모든 멤버까지도 포함되어 있다. 따라서, 부모 클래스의 멤버를 초기화하기 위해서는 자식 클래스의 생성자에서 부모 클래스의 생성자까지 호출해야 한다. 





## 다형성(Polymorphism)

여러 가지 형태를 가질 수 있는 능력으로 자바에서는 조상타입 참조 변수로 자손 타입 객체를 다루는 것이다.

```java
class Tv {
    boolean power;
    int channel;
    
    void power(){	power = !power;	}
    void channelUp(){	++channel;	}
    void channelDown(){	--channel;	}
}
class SmartTv extends Tv {
    String caption;
    void caption(){	... }
}

/* 참조 변수와 인스턴스의 타입이 일치 */
Tv t = new Tv();
SmartTv s = new SmartTv();

/* 다형성 */
Tv t = new SmartTv();	// 타입 불일치 OK

SmartTv s = new Tv();	// 에러, 허용 안됨.
```

``Tv t = new SmartTv();`` 코드와 같이 조상 타입(Tv)의 참조 변수인 ``t``에 자손 타입 클래스 SmartTv의 인스턴스 (``new SmartTv()``)를 담을 수 있는 것을 다형성이라고 한다.

이와 반대로 자손 타입의 참조변수로 조상 타입의 객체를 가리킬 수 없다.

참조변수가 조상타입일 때와 자손타입일 때는 참조변수로 사용할 수 있는 멤버의 갯수가 달라지는 차이가 있다.





## 메서드 오버라이딩(Method Overriding)

상속 관계에 있는 부모 클래스에서 이미 정의된 메서드를 자식 클래스에서 재정의하는 것을 의미한다.

```java
class Point {
    int x;
    int y;
    
    String getLocation(){
        return "x: " + x + ", y: " + y;
    }
}
class Point3D extends Point {
    int z;
    
    String getLocation(){	// 메서드 오버라이딩
        return "x: " + x + ", y: " + y + ", z: " + z;
    }
}
```

메서드 오버라이딩에서 주의할 점은 선언부는 바꿀 수 없고 구현부(내용)만 변경이 가능하다는 것이다.



### 오버라이딩의 조건

1. 선언부가 조상 클래스의 메서드와 일치해야 한다. 

   선언부가 일치한다는 것은 메서드의 반환 타입, 메서드 이름, 매개변수 목록이 모두 일치해야 한다는 것이다.

2. 접근 제어자를 조상 클래스의 메서드보다 좁은 범위로 변경할 수 없다.

3. 예외는 조상 클래스의 메서드보다 많이 선언할 수 없다.

   ```java
   class Parent {
       void parentMethod() throws IOException, SQLException { ... }
   }
   class Child extends Parent {
       void parentMethod() throws IOException { ... }
   }
   ```

   자식 클래스에서 오버라이딩한 메서드에 선언된 예외는 부모클래스의 메서드에 선언된 예외보다 적거나 같아야 한다.





## 다이나믹 메소드 디스패치(Dynamic Method Dispatch)

메소드 오버라이딩은 자바의 런타임 다형성을 지원하는 방법 중 하나다. 다이나믹 메소드 디스패치(Dynamic Method Dispatch)는 컴파일 타임이 아닌 런타임에 업캐스팅(Upcasting)된 자식 클래스의 오버라이딩 된 메서드를 호출하는 것이다.

- 오버라이딩 된 메서드가 조상 클래스의 참조를 통해 호출될 때, 자바는 호출이 발생할 때 참조되는 객체의 유형에 기초하여 그 메서드의 어떤 버전(조상클래스/자손클래스)을 실행할 것인지를 결정한다. 따라서, 이러한 결정은 실행 시간에 이루어진다.
- 런타임 시, 오버라이딩 된 메서드의 어떤 버전이 실행될 지는 참조되는 객체의 유형 (참조 변수의 유형이 아님)에 따라 달라진다.
- 조상클래스의 참조 변수는 자손클래스 객체를 참조할 수 있다. 이것은 업캐스팅이라고도 한다. 자바는 이 사실을 사용하여 런타임에 재지정된 메소드에 대한 호출을 해결한다.

다음과 같이 ``Super`` 클래스와 이를 상속받아 구현된 ``Sub1``과 ``Sub2`` 클래스가 있다고 가정하자.

```java
static class Super {
    void print(){
        System.out.println("super's print");
    }
}
static class Sub1 extends Super {
    @Override
    void print(){
        System.out.println("Sub1's print");
    }
}
static class Sub2 extends Super {
    @Override
    void print(){
        System.out.println("Sub2's print");
    }
}

public static void main(String[] args) {
    Super refer = new Super();
    refer.print();
    
    refer = new Sub1();
    refer.print();
    
    refer = new Sub2();
    refer.print();
}
```

이 코드의 실행결과는 다음과 같다.

```
super's print
Sub1's print
Sub2's print
```

``Super`` 타입의 참조 변수인 ``refer``에 자손 클래스 객체인 ``Sub1``과 ``Sub2``를 대입하면 업캐스팅이 이루어지고, ``refer``에는 각각의 객체가 대입될 때마다 자손 객체의 주소를 가리키게 된다.

따라서, 조상클래스가 자손클래스에 의해 오버라이딩 된 메서드를 포함하는 경우, 다른 타입의 객체가 조상클래스 참조 변수를 통해 참조될 때, 다른 버전의 메소드가 실행된다. 





## 제어자(modifier)

클래스와 클래스의 멤버(멤버 변수, 메서드)에 부가적인 의미를 부여한다.

- 접근 제어자: public, protected, (default), private
- 그 외: static, final, abstract, synchronized, native, transient, volatile 등

하나의 대상에 여러 제어자를 같이 사용할 수 있지만, 접근 제어자는 하나만 사용한다. 

```java
public class Modifier{
    public static final int WIDTH = 200;
    public static void main(String[] args) { ... }
}
```

접근제어자를 제일 왼쪽에 쓰는 것이 관례다.

### static

| 사용 가능 대상 | 의미                                                         |
| -------------- | ------------------------------------------------------------ |
| 멤버변수       | - 모든 인스턴스에 공통적으로 사용되는 클래스 변수가 된다.<br />- 클래스 변수는 인스턴스를 생성하지 않고도 사용 가능하다.<br />- 클래스가 메모리에 로드될 때 생성된다. |
| 메서드         | - 인스턴스를 생성하지 않고도 호출이 가능한 static 메서드가 된다.<br />- static 메서드 내에서는 인스턴스 멤버(변수, 메서드)들을 직접 사용할 수 없다. |

### final

변경될 수 없음

| 대상                   | 의미                                                         |
| ---------------------- | ------------------------------------------------------------ |
| 클래스                 | 변경될 수 없는 클래스, 확장될 수 없는 클래스가 된다.<br />그래서 final로 지정된 클래스는 다른 클래스의 **조상이 될 수 없다**. |
| 메서드                 | 변경될 수 없는 메서드, <br />final로 지정된 메서드는 오버라이딩을 통해 **재정의 될 수 없다**. |
| 멤버변수<br />지역변수 | 변수 앞에 final이 붙으면, 값을 변경할 수 없는 **상수**가 된다. |

![Final Keyword in Java | Final Variable, Method & Class - Scientech Easy](https://www.scientecheasy.com/wp-content/uploads/2019/01/final-keyword-in-java.png)

​												*< 이미지 출처: https://www.scientecheasy.com/ >*

![image-20210303224559632](week_006.assets/image-20210303224559632.png)

> final class의 사용 예시: ``String``

### abstract

| 대상   | 의미                                                         |
| ------ | ------------------------------------------------------------ |
| 클래스 | 클래스 내에 추상 메서드가 선언되어 있음을 의미한다.          |
| 메서드 | 선언부만 작성하고 구현부는 작성하지 않은 추상 메서드임을 알린다. |

```java
abstract class AbstractTest{	// 추상 클래스(추상 메서드를 포함한 클래스)
    abstract void move();		// 추상 메서드(구현부가 없는 메서드)
}
AbstractTest a = new AbstractTest(); 	// 에러 발생(추상 클래스의 인스턴스 생성 불가)
```





## 추상 클래스

미완성(추상) 메서드를 갖고 있는 클래스

주로 다른 클래스 작성에 도움을 주기 위한 클래스로 사용되며, 인스턴스 생성이 불가능 하다.

상속을 통해 추상 메서드를 완성해야 인스턴스를 생성할 수 있다.

```java
abstract class Player {
    abstract void play(int pos);
    abstract void stop();
}

Player p = new Player();	// 에러

class AudioPlayer extends Player {
    void play(int pos){ ... }
    void stop(){ ... }
}

AudioPlayer ap = new AudioPlayer();
Player p = new AudioPlayer();	// 가능 (다형성)
```



### 추상 메서드

미완성 메서드, 구현부(``{}``)가 없는 메서드

```java
abstract 리턴타입 메서드이름();
```

추상메서드의 선언은 ``abstract``라는 제어자를 맨 앞에 붙여줘야 하며, 메서드 이름 마지막에는 반드시 세미콜론``;``을 붙여주어야 한다.

추상메서드는 꼭 필요하지만 자손마다 다르게 구현될 것으로 예상될 경우에 사용한다.

```java
abstract class Player {
    abstract void play(int pos);
    abstract void stop();
}

class AudioPlayer extends Player {
    void play(int pos){ ... }	// 추상 메서드 구현
    void stop(){ ... }			// 추상 메서드 구현
}

class AbstractPlayer extends Player{ 	// 에러
    void play(int pos){ ... }	// 추상 메서드 구현
}
```

``AudioPlayer`` 클래스의 경우에는 ``Player``라는 추상 클래스에 선언된 메서드를 구현하여 에러가 없는 것을 확인할 수 있다. 

반면, ``AbstractPlayer``의 경우에는 ``play()``라는 메서드를 정상적으로 구현하였지만 ``stop()``이라는 메서드를 구현하지 않았기 때문에 미완성 클래스로 클래스 선언부에서 오류가 생기게 된다.

때문에,  ``AbstractPlayer`` 클래스 선언부 맨 앞에 ``abstract`` 제어자를 붙여주어야 한다.

**추상 메서드를 사용하는 이유**는 무엇일까?

-> 필수 기능을 강제로 구현하게 하는 이점이 있다.



### 추상클래스의 작성

여러 클래스에 공통적으로 사용될 수 있는 추상클래스를 바로 작성하거나 기존 클래스의 공통 부분을 뽑아서 추상클래스를 만든다.

다음과 같은 클래스들이 선언되었다고 하자.

```java
class Marine {
    int x, y;						// 현재 위치
    void move(int x, int y){ ... }	// 지정된 위치로 이동
    void stop(){ ... }				// 현재 위치에 정지
    void stimPack(){ ... }			// 스팀팩 사용
}
class Tank {
    int x, y;						// 현재 위치
    void move(int x, int y){ ... }	// 지정된 위치로 이동
    void stop(){ ... }				// 현재 위치에 정지
    void changeMode(){ ... }		// 공격모드 변환
}
class Dropship {
    int x, y;						// 현재 위치
    void move(int x, int y){ ... }	// 지정된 위치로 이동
    void stop(){ ... }				// 현재 위치에 정지
    void load(){ ... }				// 선택된 대상을 태움
    void unload(){ ... }			// 선택된 대상을 태움
}
```

``Marine``, ``Tank``, ``Dropship`` 이 세 클래스에는 현재 위치를 담고 있는 변수 ``x``, ``y``와 이동, 정지 기능을 담당하는``move()``, ``stop()`` 메서드(선언부가 일치해야 함)가 공통으로 포함되어 있는 것을 확인할 수 있다.

이와 같이 공통된 부분을 추출하여 ``Unit`` 클래스로 묶어서 정의해 다음과 같이 코드를 변경할 수 있다.

```java
abstract class Unit {
    int x, y;							// 현재 위치
    abstract void move(int x, int y);	// 지정된 위치로 이동
    void stop(){ ... }					// 현재 위치에 정지
}
class Marine extends Unit {    
    void move(int x, int y){ ... }	// 지정된 위치로 이동
    void stimPack(){ ... }			// 스팀팩 사용
}
class Tank extends Unit {    
    void move(int x, int y){ ... }	// 지정된 위치로 이동    
    void changeMode(){ ... }		// 공격모드 변환
}
class Dropship extends Unit {    
    void move(int x, int y){ ... }	// 지정된 위치로 이동    
    void load(){ ... }				// 선택된 대상을 태움
    void unload(){ ... }			// 선택된 대상을 태움
}
```

이와 같이 공통된 부분을 추상클래스로 묶어 정의한 후, 각 클래스에서 상속을 받아 필요에 따라 기능을 구현하는 형식으로 코드를 작성하면 코드가 간결해진다.

또한 다음과 같이 하나의 배열에 여러 객체를 넣어 사용 가능한 다형성의 장점을 활용할 수 있게 된다.

```java
Unit[] group = new Unit[3];
group[0] = new Marine();
group[1] = new Tank();
group[2] = new Dropship();

for(int i = 0; i < group.length; i++){
    group[i].move(100, 200);
}
```

#### 추상클래스의 장점

- 코드 작성이 쉽고 코드의 중복이 제거된다.
- 추상화된 코드는 구체화된 코드보다 유연하기 때문에 코드 관리(변경)가 용이하다.





## Object

모든 클래스의 최고 조상 클래스로, 부모가 없는 클래스는 자동적으로 Object 클래스를 상속받게 된다.

모든 클래스는 Object 클래스에 정의된 11개의 메서드를 상속받는다. 11개의 메서드 중 대표적인 것으로 ``toString()``, ``equals(Object obj)``, ``hashCode()`` 등이 있다.

다음과 같이 클래스가 정의되어 있다고 가정하면, 

```java
class Point { ... }
class Circle extends Point{ ... }
```

컴파일러가 다음과 같이 Circle 클래스에 ``extends Object`` 코드를 추가해준다.

```Java
class Point extends Object { ... }
class Circle extends Point{ ... }
```





#### Reference URL

> https://buddev.tistory.com/59
>
> http://www.tcpschool.com/java/intro
>
> https://www.youtube.com/channel/UC1IsspG2U_SYK8tZoRsyvfg
>
> https://www.geeksforgeeks.org/dynamic-method-dispatch-runtime-polymorphism-java/
>
> https://velog.io/@maigumi/Dynamic-Method-Dispatch

