---
#permalink : 
title : "객체지향언어의 특징"
excerpt : 기초 문법 중 내가 몰랐던, 혹은 까먹었던 부분들만 적어보겠다.

categories : 
 - CS
tags :
 - Java
 - OOP

toc : true
toc_sticky : true

date: 2022-01-20
last_modified_at: 2022-01-21
---

<span style="color : gray">처음 써보는 기술블로그이자 첫 번째 포스트...!!  
두서없이 막 쓸 것 같다.</span>  

## **OOP is A PIE** - 객체지향의 특징 4가지<br>
추상화(Abstraction)<br>다형성(Polymorphism)<br>상속(Inheritance)<br>캡슐화(Encapsulation)

## 1. 추상화(Abstraction)
현실의 <span style="color: blue">객체</span>가 갖는 속성과 기능은 <span style="color: blue">추상화</span> 되어 <span style="color: blue">클래스</span>에 정의된다.  
클래스는 <span style="color: blue">구체화</span>되어 프로그램의 <span style="color: blue">객체</span>가 된다.

## 2. 다형성(Polymorphism)
+ 항상 헷갈리는 <strong>오버로딩(overloading)</strong>과 <strong>오버라이딩(overriding)</strong>.<br>  
    **오버로딩**은 과적재. 한 클래스 내에서 이름은 같지만 다르게 동작하는 메서드를 여러개 작성하는 것.  

     **오버라이딩**은 over-writting. 부모클래스의 메서드를 자식 클래스에서 동일한 이름으로  
     자신의 특징에 맞게 재작성하는 것.  
     + 오버라이딩한 자식의 접근 제한자는 부모보다 같거나 더 넓어야 한다.
        > static: 정적인 != 고정된  
        ⇒ 바뀔수는 있지만 거의 안바뀌는(ex: 학명)  
        <br> 
        멤버 변수 중 static이 붙는 클래스 멤버는 <span style="color: red">객체와 무관</span>하며  
        클래스 로딩 시 클래스 영역에 메모리가 할당된다.
     + 모든 클래스에는 Object 클래스에 정의된 메서드가 있다.
     + 메서드가 오버라이드 된 경우, 무조건 자식 클래스의 메서드가 호출된다.

<br>

+ 부모 객체는 자식을 담을 수는 있지만(메모리에 있음) 자식의 내용에 접근할 수 없다.  
이 때 필요한게 참조형 객체의 형 변환(캐스팅).  

    **묵시적 캐스팅**은 자손 타입의 객체를 조상 타입으로 참조하는 것으로, 형변환 생략이 가능하다.  

    **명시적 캐스팅**은 조상 타입을 자손 타입으로 참조하는 것으로, 형변환 생략이 불가능하고 명시적 캐스팅 이후에는 자식의 내용에 접근할 수 있다.  

<br>

+ 다형성을 사용하는 이유 : 관리는 편리하게, 기능은 원하는대로!
    > Person 클래스 하나로 스파이더맨, 배트맨, 슈퍼맨, 일반인, 직장인.. 등등을 한번에 관리할 수 있다.
    

## 3. 상속(Inheritance)
부모 클래스와 자식 클래스 간에 is a 관계가 성립될 때 구현한다.  
~~딱히 쓸게 없네~~

## 4. 캡슐화(Encapsulation)
+ Singleton 디자인 패턴  
객체의 인스턴스가 오직 1개만 생성되는 패턴(객체의 생성을 제한한다).

    <span style="color: gray">아직 singleton 패턴을 사용해보지 않아서 이후에 추가 작성하겠다.</span>


참고 : [velog.io/@sungsuzi/oop의-4가지-특징](https://velog.io/@sungsuzi/oop%EC%9D%98-4%EA%B0%80%EC%A7%80-%ED%8A%B9%EC%A7%95)


