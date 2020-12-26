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
     - 메소드 출처의 모호성: 여러 부모 클래스들 중에서 이름이 같은 메소드가 있을 경우 어떤 메소드를 상속받아야 하는지 모호하여 문제가 생김
     - 필요 없는 부분까지 상속을 받아야 하기 때문에 매우 무거워진다.
   - 대신 자바는 **Interface 다중 구현**을 제공한다.
2. 선택적 상속이 불가능 하다. All or Not 만 가능
   - 상속되는 클래스의 속성이나 기능을 선택적으로 상속받을 수 없다. 전부 다 받거나, 아예 받지 않거나 둘 중 하나만 가능하다.
   - 상속을 받게 되면 부모 클래스의 모든 속성과 기능을 상속받아 사용할 수 있다.
     - 하지만, 생성자와 초기화 블록은 상속되지 않는다.
     - 부모 클래스에서 ``private``으로 정의된 멤버 변수는 상속은 가능하지만, **접근은 불가능**하다. 그래서 ``public``으로 선언한 ``setter``또는 ``getter``를 이용해 접근한다.
   - 상속 받은 기능 중 수정을 원하는 기능은 다시 재정의 할 수 있고**(Overriding)**, 필요한 속성이나 기능은 추가하여 작성할 수 있다. ~~객체 생성의 경우에는 재사용만 가능하고 변경,추가는 불가능 하다.~~
3. 생성자는 상속되지 않는다.
   - 생성자는 반드시 클래스 이름과 동일하게 써야 하는데, 상속하면 클래스 이름이 달라지기 때문
   - 그러나 재사용을 위해 하위 클래스에서 상위 클래스의 생성자를 호출할 수 있는데, 이는 ``super`` 키워드를 사용하면 가능하다. 단, 반드시 첫 줄에서만 가능하다.
4. 상속의 횟수에 제한을 두지 않는다.
5. 계층 구조의 최상위에 있는 클래스는 Object 클래스이다.



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







![Final Keyword in Java | Final Variable, Method & Class - Scientech Easy](https://www.scientecheasy.com/wp-content/uploads/2019/01/final-keyword-in-java.png)











#### Reference URL

> https://buddev.tistory.com/59
>
> 