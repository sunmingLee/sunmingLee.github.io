---
#permalink : 
title : "자바 기초문법(2)"
excerpt : 기초 문법 중 내가 몰랐던, 혹은 까먹었던 부분들만 적어보겠다.

categories : 
 - CS
tags :
 - Java
 - OOP

toc : true
toc_sticky : true

last_modified_at: 2022-01-31
---
<span style="color:gray">이번주까지 해서 자바의 기초 문법을 모두 끝냈다.  
이번주는 내가 모르는 부분이 많았어서 양이 좀 더 많아질 것 같다. </span>

## 추상클래스
**사용 이유 : 구현의 강제를 통한 프로그램의 안정성 향상**  
메서드의 재정의가 무조건 이루어져야하는 경우, 부모 클래스를 추상 클래스로 만들어 재정의 없이는 컴파일 에러가 나도록 하여 **실수를 미연에 방지한다.**  

## 인터페이스
모든 멤버변수는 public static final 이며 생략가능하다.  
모든 메서드는 public abstract 이며 생략가능하다. (JDK 1.8부터는 default method가 추가됨)  
클래스와 마찬가지로 extends로 상속이 가능하며, 다중 상속이 가능하다. (*Why? 동작의 충돌이 일어나지 않기 때문*)

### 사용 이유
+ **손쉬운 모듈 교체 지원**

아래의 예시를 살펴보자.  

```java
public interface Pay {
	public void payment();
}


public class CardPay implements Pay {
	@Overriding
	public void payment() {
	}
}

public class CashPay implements Pay {
	@Overriding
	public void payment() {
	}
}


public class PaymentService {
    Pay pay;
    private final Stirng CREDIT_CARD = "카드결제";
    private final String CASH = "현금결제";
    
    public void process(String option) {
        if(option.equals(CREDIT_CARD) {
        	pay = new CardPay();
        }
        else if(option.equals(CASH) {
        	pay = new CashPay();
        }
    	pay.payment();
    }
}
```
결제 방식에는 여러 가지가 있다. 이 때, Pay 인터페이스를 생성하고 다른 결제 방법들이 이를 구현하도록 하면 결제 방식이 CardPay에서 CashPay가 되더라도 클래스의 이름만 바꿔주면 손쉽게 모듈 교체가 가능하다. 로직의 변화는 전혀 없다.  

만약 새로운 결제방식이 추가 된다면 Pay 인터페이스를 구현하는 또다른 클래스를 만들기만 하면 된다. 해당 클래스에 대한 특별한 설계나 공부가 필요없는 것이다.  
<br>

+ **서로 상속 관계가 없는 클래스들간의 관계 부여를 통한 다형성 확장**  

Phone과 Camera 클래스가 있다고 가정하자.  
두 제품 모두 충전이 가능한(Chargeable) 모델이지만 서로 상속 관계가 없다.  
charge 메서드를 사용하기 위해서는 객체가 충전 가능한 모델인지 하나하나 확인해야 한다.  
이 때, 두 클래스 모두 Chargeable 이라는 인터페이스를 구현하게 한다면 간단하게 충전 가능성을 확인할 수 있다.  
<br>

+ **모듈 간 독립적 프로그래밍을 통한 개발 기간 단축**

계산기를 구현하기 위해 두 팀이 협업한다고 가정하자.  
A팀은 클라이언트를 위한 UI를, B팀은 계산 로직의 구현을 담당한다.  
계산기에 필요한 add라는 메서드를 담은 Calculator 인터페이스를 만들고 A팀과 B팀 모두 이를 implements 한다.  
A팀에서는 해당 메서드를 호출과 리턴 타입만 맞춰 대략적으로 구현해두고 B팀에서는 정확한 비지니스 로직을 구현하여 나중에 이를 A팀의 코드와 교환하기만 하면 된다.  
<br>

### 디폴트 메서드(default method)

인터페이스에 선언된 구현부가 있는 일반 메서드.  
디폴트 메서드는 abstract가 아니기 때문에 해당 메서드를 반드시 구현해야 할 필요가 없어진다.  
JDK 1.8부터 디폴트 메서드가 생기면서 메서드 간 충돌이 생겼다. 이때 메서드의 우선 순위는  
+ interface vs super class? >> super class win!  
+ interface vs interface? >> 두 인터페이스를 구현한 클래스에서 반드시 오버라이딩을 해서 충돌을 해결해야 한다.  
<br>

## Generics

다양한 타입의 객체를 다루는 메서드로, 컬렉션 클래스에서 **컴파일 시에** 타입을 체크한다.  
미리 사용할 타입을 명시해서 객체의 타입에 대한 안전성을 향상시키고 형 변환의 번거로움을 감소시킨다.  
<> 안에 타입 파라미터(참조형 타입)를 표시한다.  
객체 생성 시 타입 파라미터가 정해지면 해당 타입의 자식까지만 허용이 된다.  
구체적인 타입 제한이 필요할 때는 타입 파라미터 선언 뒤 extends 와 함께 상위 타입을 명시한다.  
```java
class NumberBox<T extends Number>{...}
NumberBox<Integer> intBox = new NumberBox<Integer>();
NumberBox<String> strBox = new NumberBox<String>(); // 컴파일 에러 발생
```
<br>

## Exception Handling

+ Error : 메모리 부족, stack overflow 등 프로그램의 비정상적 종료를 막을 수 없는 상황으로 디버깅이 필요하다.  
+ Exception : 읽으려는 파일이 없거나 네트워크 연결이 안되는 등 프로그램 코드에 의해 수습될 수 있는 상황이다.  

예외 클래스의 계층  

<img width="489" alt="exception" src="https://user-images.githubusercontent.com/47583202/151790543-dbc93c11-ac10-4c46-bbdd-c33ace565ee2.PNG">  

 
+ Checked Exception : 예외에 대한 대처 코드가 없으면 컴파일이 진행되지 않는다.  
+ Unchecked Exception(RuntimeException의 하위 클래스) : 예외에 대한 대처 코드가 없더라도 컴파일은 진행된다.  
<br>

try ~ catch ~ finally 구문은 주로 try 블록에서 사용한 리소스를 반납할 때 사용된다.(resource leak 발생 가능)  

객체가 AutoCloseable 인터페이스를 구현한 경우(I/O Stream, socket, connetion 등), try 선언문에 선언된 객체들에 대해 자동 close 호출이 가능하다.
```java
try(FileInputStream fileInput = new FileInputStream("input.txt");){
    fileInput.read();
} catch (IOException e){
    e.printStackTrace();
}
```

메서드 재정의 시 부모의 예외보다 더 넓은 예외를 사용할 수 없다.  
<br>
<br>

<span style="color:gray">수업 들으면서 메모식으로 정리해둔거라 뭔가 정리가 잘 안된 느낌이지만...  
다시 봤을 때 기억 안나는 부분만 나중에 더 추가해야지.</span>  
<br>

> 참고 : [인터페이스를 사용하는 이유](https://syundev.tistory.com/225)