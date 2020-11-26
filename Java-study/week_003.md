# 3주차 과제: 연산자

### 목표

자바가 제공하는 다양한 연산자를 학습하세요.

### 학습할 것

- 산술 연산자
- 비트 연산자
- 관계 연산자
- 논리 연산자
- instanceof
- assignment(=) operator
- 화살표(->) 연산자
- 3항 연산자
- 연산자 우선 순위
- (optional) Java 13. switch 연산자

---

### 연산자

연산에서 사용되는 표시나 기호



#### 연산자와 연산식에 대한 정리

| 연산자<br />종류 | 연산자                                                 | 연산<br />방향     | 피연산자수     | 산출값<br />타입  | 기능 설명                             |
| ---------------- | ------------------------------------------------------ | ------------------ | -------------- | ----------------- | ------------------------------------- |
| 산술             | +, -, *, /, %                                          | →                  | 이항           | 숫자              | 사칙연산 및 나머지 계산               |
| 부호             | +, -                                                   | ←                  | 단항           | 숫자              | 음수와 양수의 부호                    |
| 문자열           | +                                                      | →                  | 이항           | 문자열            | 두 문자열을 연결                      |
| 대입             | =, +=, -=, *=, /=, %=, <br />&=,^=, \|=, <<=, >>= >>>= | ←                  | 이항           | 다양              | 우변의 값을 좌변의 변수에 대입        |
| 증감             | ++, --                                                 | ←                  | 단항           | 숫자              | 1만큼 증가/감소                       |
| 비교             | ==, !=, >, <, >=, <=, <br />instanceof                 | →                  | 이항           | boolean           | 값의 비교                             |
| 논리             | !, &, \|, &&, \|\|                                     | →<br />*( ! : ← )* | 단항<br />이항 | boolean           | 논리적 NOT, AND, OR 연산              |
| 조건             | (조건식) ? A : B                                       | →                  | 삼항           | 다양              | 조건식에 따라 A 또는 B 중 하나를 선택 |
| 비트             | ~, &, \|, ^                                            | →<br />*( ~ : ← )* | 단항<br />이항 | 숫자<br />boolean | 비트 NOT, AND, OR, XOR 연산           |
| 쉬프트           | >>, <<, >>>                                            | →                  | 이항           | 숫자              | 비트를 좌측/우측으로 밀어서 이동      |

*< 내용 참고 URL: https://medium.com/@katekim720/연산자부터-조건-반복문까지-3d5cec6513d4 >*
(이것이 자바다 | 신용권의 Java 프로그래밍 정복_1 책에서 발췌한 내용인 듯 하다)



연산자는 피연산자의 수에 따라 단항, 이항, 다항 연산자로 구분함

예시)

```java
++x;		// 단항 연산자
x + y;		// 이항 연산자	
(sum > 90) ? "A" : "B";	// 삼항 연산자
```

연산식은 반드시 **하나의 값 만을 산출**함, 연산자 수가 아무리 많아도 두개 이상의 값을 산출하지 않음



## 1. 산술 연산자

산술 연산자는 사칙연산을 다루는 연산자
모두 두 개의 피연산자를 가지는 **이항 연산자**이며, 피연산자들의 결합 방향은 왼쪽에서 오른쪽임

| 산술 연산자 | 설명                                                         |
| ----------- | ------------------------------------------------------------ |
| +           | 왼쪽의 피연산자에 오른쪽의 피연산자를 **더함**               |
| -           | 왼쪽의 피연산자에서 오른쪽의 피연산자를 **뺌**               |
| *           | 왼쪽의 피연산자에 오른쪽의 피연산자를 **곱함**               |
| /           | 왼쪽의 피연산자를 오른쪽의 피연산자로 **나눔**               |
| %           | 왼쪽의 피연산자를 오른쪽의 피연산자로 **나눈 후, 그 나머지를 반환**함 |

```java
class operator_study{
    public static void main (String[] args){
        int num1 = 8, num2 = 4;
        
        System.out.println("num1 + num2 = " + (num1 + num2));
        System.out.println("num1 - num2 = " + (num1 - num2));
        System.out.println("num1 * num2 = " + (num1 * num2));
        System.out.println("num1 / num2 = " + (num1 / num2));
        System.out.println("num1 % num2 = " + (num1 % num2));
    }
}
```

```
<실행 결과>
num1 + num2 = 12
num1 - num2 = 4
num1 * num2 = 32
num1 / num2 = 2
num1 % num2 = 0
```



## 2. 비트 연산자

비트(bit) 단위로 논리 연산을 할 때 사용하는 연산자
비트 단위로 왼쪽이나 오른쪽으로 전체 비트를 이동하거나, 1의 보수를 만들 때도 사용함

| 비트 연산자 | 설명                                                         |
| ----------- | ------------------------------------------------------------ |
| &           | **비트 AND 연산**: 대응되는 비트가 모두 1이면 1을 반환       |
| \|          | **비트 OR 연산**: 대응되는 비트 중에서 하나라도 1이면 1을 반환 |
| ^           | **비트 XOR 연산**: 대응되는 비트가 서로 다르면 1을 반환      |
| ~           | **비트 NOT 연산**: 비트를 1이면 0으로, 0이면 1로 반전 (1의 보수) |
| <<          | **Left shift 연산**: 명시된 수만큼 비트들을 전부 왼쪽으로 이동 |
| >>          | **Right shift 연산**: 부호를 유지하면서 지정한 수만큼 비트를 전부 오른쪽으로 이동 |
| >>>         | 지정한 수만큼 비트를 전부 오른쪽으로 이동, 새로운 비트는 전부 0이 됨 |

```java
class operator_study{
    public static void main (String[] args){
        int num1 = 0b10101;	// 21, 0B는 2진수시작부호
        int num2 = 0b01100;	// 12
        
        System.out.println("num1 & num2 = " + Integer.toBinaryString(num1 & num2));
        System.out.println("num1 | num2 = " + Integer.toBinaryString(num1 | num2));
        System.out.println("num1 ^ num2 = " + Integer.toBinaryString(num1 ^ num2));
        System.out.println("~num1 = " + (~num1));
        System.out.println("~num2 = " + (~num2));
    }
}
```

```
<연산 결과>
num1 & num2 = 100
num1 | num2 = 11101
num1 ^ num2 = 11001
~num1 = -22
~num2 = -13

~num1 = 11111111111111111111111111101010
~num2 = 11111111111111111111111111110011
```

|                                                              |                                                              |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| ![비트 AND 연산](http://www.tcpschool.com/lectures/img_php_bitwise_and.png) | ![비트 OR 연산](http://www.tcpschool.com/lectures/img_php_bitwise_or.png) |
|                                                              |                                                              |
| ![비트 XOR 연산](http://www.tcpschool.com/lectures/img_php_bitwise_xor.png) | ![비트 NOT 연산](http://www.tcpschool.com/lectures/img_php_bitwise_not.png) |

```java
class operator_study{
    public static void main (String[] args){
        int num1 = 0b10101;	// 21, 0B는 2진수시작부호
        
        System.out.println("num1 << 2 = " + Integer.toBinaryString(num1 << 2));
        System.out.println("num1 >> 2 = " + Integer.toBinaryString(num1 >> 2));
        System.out.println("num1 >>> 2 = " + Integer.toBinaryString(num1 >>> 2));
        
        int num2 = 8;
        int num3 = -8;
        
        System.out.println("num2 >>> 2 =" + (num2 >>> 2));
        System.out.println("num3 >>> 2 =" + (num3 >>> 2));
    }
}
```

```
<실행 결과>
num1 << 2 = 1010100
num1 >> 2 = 101
num1 >>> 2 = 101

num2 >>> 2 =2
num3 >>> 2 =1073741822
```

shift 연산자를 이용하면 비트가 지정한 자리수만큼 이동

 ``<<``연산자 이용 시 한 비트씩 왼쪽으로 이동할 때마다 값이 2배 증가하며 (비트 이동 횟수 * 2)  만큼의 결과 값이 나옴

``>>``연산자 이용 시 한 비트씩 오른쪽으로 이동할 때 마다 값이 2배 감소하며 (비트 이동 횟수 / 2) 만큼의 결과 값이 나옴



## 3. 관계 연산자



## 4. 논리 연산자



## 5. instanceof



## 6. assignment(=) operator (대입)



## 7. 화살표(->) 연산자



## 8. 3항 연산자



## 9. 연산자 우선 순위

연산자의 우선 순위는 수식 내에 여러 연산자가 함께 등장할 때, 어느 연산자가 먼저 처리될 것인가를 결정함



## 10. optional) Java 13. switch 연산자



### 참조 URL

---

> https://medium.com/@katekim720/연산자부터-조건-반복문까지-3d5cec6513d4
>
> http://www.tcpschool.com/java/java_operator_arithmetic