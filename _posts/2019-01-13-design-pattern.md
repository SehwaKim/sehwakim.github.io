---
layout: post
title: 자바 디자인 패턴의 이해 (Gof Design Pattern)
---

아래의 강좌를 보면서 배운 내용 정리
> [인프런 자바 디자인 패턴의 이해](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4/)

Section 1. Strategy Pattern
---
>keyword: Interface, Delegation, Strategy Pattern

#### Interface
>- 기능의 선언과 구현을 분리할 수 있게 해준다
- 기능의 사용 통로 역할도 한다 (쓰고자 하는 기능의 접근점을 제공)

#### Delegation
>- 아웃소싱같은
- 어떤 기능의 구현을 다른 객체에게 위임하고 그 객체의 기능을 자기 기능처럼 갖다쓰는 것

#### Strategy Pattern
>- 다양한 여러가지 알고리즘을 하나의 추상적인 접근점 을 통해서 사용한다
- 이렇게 하면 그 알고리즘은 변경가능해진다.
- 전략을 바꿔치기할 수 있게 된다.
- 전략 패턴을 쓰면 어떤 구체적인 알고리즘을 쓸 지에 대한 결정을 미룰 수 있게 됨으로써 런타임시 상황에 맞는 알고리즘을 선택해서 사용할 수 있게 된다.

![strategy](/assets/strategy.gif)

위임Delegation과 전략패턴Strategy Pattern은 서로 비슷해보이지만 전략패턴은 말 그대로 하나의 확고한 소프트웨어 디자인 패턴인거고 위임은 패턴이라기 보단 소프트웨어 개발의 기초적인 지침인 "낮은 결합도와 높은 응집도"를 가능하게 하는 어떤 보편적인 하나의 테크닉이라고 보면 될 것 같다.

## Section 2. Adapter Pattern
>keyword: Adapter, Adaptee, Target

연관성 없는 두 객체를 묶어 사용할 때 쓸 수 있다.
이미 주어진 알고리즘을 요구에 맞게 사용할 수 있게 된다.

<cite>https://en.wikipedia.org/wiki/Adapter_pattern</cite>
>The adapter design pattern solves problems like:
>> 1. How can a class be reused that does not have an interface that a client requires?
2. How can classes that have incompatible interfaces work together?
3. How can an alternative interface be provided for a class?

#### Target
>요구사항이 정의된 인터페이스

#### Adaptee
>이미 주어진 알고리즘이 있는 클래스 or 인터페이스

#### Adapter
>adaptee를 target의 요구에 맞게 변경하는 로직이 들어있는 클래스

![W3sDesign_Adapter_Design_Pattern_UML](/assets/W3sDesign_Adapter_Design_Pattern_UML.jpg)

요구하는 기능은 Target에 정의해놓고, 그것을 구현한 Adapter 클래스에서 Adaptee를 변환하는 로직을 구현하면 된다. 그렇게 되면 사용자는 Target을 갖다 쓸 때 Target의 구현체를 직접 쓰는건지 어댑터를 쓰는건지 모르게 되고, 알 필요도 없다. 요구사항이 변경되어 나중에 다른 Adaptee로 변경해야하는 경우엔 어댑터 내부의 로직만 다른 Adaptee를 쓰도록 변경해주면 된다. 어떤 새로운 요구사항이 있을 때 마다 새롭게 기능을 구현하는 게 아니라 기존에 비슷하게 쓰여질 수 있는 기능을 Adaptee로 삼아서 활용할 때 유용하게 쓰일 수 있는 패턴인 것 같다.

## Section 3. Template Method Pattern
>keyword: Template, Skeleton, Structure, Process, Step

<cite>https://en.wikipedia.org/wiki/Template_method_pattern</cite>
> the template method pattern defines the skeleton of an algorithm in an operation, deferring some steps to subclasses. It lets subclasses redefine certain steps of an algorithm without changing the algorithm's structure.

어떤 알고리즘이 일정한 프로세스를 가지고 있다면, 다른 말로 특정 순서(step)를 밟으며 동작해야 하는 요구사항이라면 이를 템플릿화해서 구현 할 수 있다.

즉 이런 경우에 템플릿 메소드 패턴을 쓸 수 있다.
>- 구현하려는 알고리즘이 일정한 프로세스가 있다 (순서, Step이 있다는 말)
- 구현하려는 알고리즘이 변경가능성이 있다

템플릿 메소드 패턴 구현 방법
>1. 알고리즘을 여러 단계로 나눈다.
2. 나눠진 알고리즘의 단계를 메소드로 선언한다.
3. 알고리즘을 수행할 템플릿 메소드를 만든다.
4. 하위 클래스에서 나눠진 메소드들을 구현한다.

![W3sDesign_Template_Method_Design_Pattern_UML](/assets/W3sDesign_Template_Method_Design_Pattern_UML.jpg)

서블릿을 보면 HttpServlet의 메소드인 `void service(HttpServletRequest req, HttpServletResponse resp)` 메소드가 전형적인 템플릿 메소드이다. 템플릿 역할을 하는 service 안에 분기에 따라 doGet, doPost 등의 메소드들이 사용되고 있고 그 do 메소드들의 세부 구현은 HttpServlet을 상속한 subclass에게 맡기는 형태이다. 이것을 템플릿 메소드 패턴이라고 할 수 있다.
템플릿 메소드 안의 step 들에 해당하는 메소드들은 요구사항 변경에 따라 언제든지 subclass에서 다르게 구현될 수 있다.
하지만 전체 프로세스, 템플릿 자체가 변경된다면? 그런 일이 있을 수도 있기에 이 부분은 설계 단계부터 항상 염두해 두어야 한다.
