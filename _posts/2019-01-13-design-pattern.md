---
layout: post
title: 자바 디자인 패턴의 이해 (Gof Design Pattern)
---

이 노트는 아래의 강좌를 보면서 배운 내용을 정리한 것임
> [인프런 자바 디자인 패턴의 이해](https://www.inflearn.com/course/%EC%9E%90%EB%B0%94-%EB%94%94%EC%9E%90%EC%9D%B8-%ED%8C%A8%ED%84%B4/)

## 들어가기 전
#### Gof Design Pattern이란?
>"Gang of Four" design patterns describe how to solve recurring design problems to design flexible and reusable object-oriented software, that is, objects that are easier to implement, change, test, and reuse. (wikipedia)

- *유연하고 재사용성 높은* 객체지향 프로그램을 만드는 게 목표인데
- 그걸 방해하는 설계상의 문제를 반복적으로 만나게 된다.
- 그 전형적인 문제들을 해결하기 위한 솔루션을 gof design pattern이 제시하는 거고
- 이 디자인 패턴들을 적용하면 객체의 *구현*, *변경*, *테스트*, *재사용* 이 쉬워지게 된다.
- 유지보수성Maintainability이 올라가는 것이다.

## Section 1. Strategy Pattern
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

## Section 4. Factory Method Pattern
>keyword: object creation, template method pattern

#### What is Factory Method Pattern?
- The factory method pattern is `a creational pattern`.
- object 생성을 어떻게 할 지에 대한 패턴이다.
- 그리고 object 생성을 위해 `팩토리 메소드`를 사용한다.
- 어떤 객체를 생성할 때 직접 생성자를 호출하지 않고 팩토리 메소드를 호출한다는 말

```java
Item item = new HpPotion();
item.use();

Item item = new MpPotion();
item.use();
```
이렇게 하지 않고
```java
ItemCreator creator;
Item item;

creator = new HpCreator();
item = creator.create(); // 이 create()이 팩토리 메소드
item.use();

creator = new MpCreator();
item = creator.create();
item.use();
```
이렇게 객체를 생성한다. (Item객체의 *생성자역할* 인 ItemCreator가 있다.)
여기서 두번째 코드가 첫번째 코드보다 더 유연하다고 할 수 있다.

![W3sDesign_Factory_Method_Design_Pattern_UML](/assets/W3sDesign_Factory_Method_Design_Pattern_UML.jpg)

#### 어떻게 팩토리 메소드를 통한 객체 생성이 더 유연한 방법인가?
- 첫번째 코드처럼 생성자를 통해 객체들을 생성하면 Item 객체들이 추가, 수정, 삭제될 때 마다 전체 코드가 다시 수정되어야 한다.
- 그래서 생성될 객체의 타입을 구체적으로 명시할 필요 없이 객체를 생성하고 싶다면 팩토리 메소드를 호출해서 그 메소드 안에서 구체적으로 지정된 객체가 생성되고 리턴되게 할 수 있다.
- 그리고 팩토리 메소드에 객체생성을 맡기면 일련의 객체 생성 과정을 하나로 통일되게 묶을 수 있다.
- 아이템 생성자와 아이템을 *추상화해서* 각각 추상클래스, 인터페이스로 두고 상속을 통해 각 세부 아이템에 맞게 구현하면 실제 아이템 생성 부분(클라이언트)의 코드는 다형성을 이용해서 작성될 수 있고 그렇게되면 여러가지 아이템 생성에 유연하게 대처할 수 있는 코드가 된다.
- *객체 생성에 있어서도* 구조와 구현의 분리를 통해 결합도 낮은 유연한 프로그램 작성이 가능하게 하는 부분.

#### 템플릿 메소드 패턴과의 연관관계는?
- 팩토리 메소드 패턴에서 템플릿 메소드 패턴이 사용된다.
- 위의 예시에서 팩토리 메소드였던 ItemCreator의 `create()` 메소드는 아이템 객체 생성 및 전처리, 후처리 작업 등을 수행할 수 있다 (DB에 아이템 생성 로그를 남긴다든지)
- 그 처리 과정들(step)이 아이템별로 다르니까 template, skeleton에 해당하는 create()메소드는 템플릿 메소드로 하고 나머지 step들에 해당하는 메소드들은 아이템별 subclass에 구현을 맡기는 것이다. 즉, 템플릿 메소드 패턴이 그대로 쓰인다.
- 요약하면, 팩토리 메소드 패턴은 객체 생성의 템플릿 메소드 패턴이라 할 수 있겠다.

#### 팩토리 메소드 vs 팩토리 메소드 패턴
-

## Section 5. Singleton Pattern
![1920px-Singleton_UML_class_diagram.svg](/assets/1920px-Singleton_UML_class_diagram.svg.png)
*인스턴스 하나만 생성해야할 객체를 위한 패턴*

## Section 6. Prototype Pattern
>keyword: Cloneable

- 프로토타입 패턴을 이용해서 복잡한 인스턴스를 복사할 수 있다.
- **생산 비용이 높은 인스턴스** 를 복사를 통해서 쉽게 생성할 수 있도록 하는 패턴

#### 인스턴스 생산 비용이 높은 경우
1. 종류가 너무 많아서 클래스로 정리되지 않는 경우
2. 클래스로부터 인스턴스 생성이 어려운 경우

![900px-Prototype_UML.svg](/assets/900px-Prototype_UML.svg.png)

```java
// Prototype pattern
public abstract class Prototype implements Cloneable {
    public Prototype clone() throws CloneNotSupportedException{
        return (Prototype) super.clone();
    }
}

public class ConcretePrototype1 extends Prototype {
    @Override
    public Prototype clone() throws CloneNotSupportedException {
        return (ConcretePrototype1)super.clone();
    }
}

public class ConcretePrototype2 extends Prototype {
    @Override
    public Prototype clone() throws CloneNotSupportedException {
        return (ConcretePrototype2)super.clone();
    }
}
```
자바에서는 Object의 clone()메소드를 통해 프로토타입 패턴을 지원한다.

## Section 7. Builder Pattern
>keyword:

- 복잡한 단계가 있는 인스턴스 생성을 빌더 패턴을 통해서 구현할 수 있다.
