---
layout: post
title: 자바 디자인 패턴의 이해 (Gof Design Pattern)
---
Section 1. Strategy Pattern
---
>keyword: Interface, Delegation, Strategy Pattern

### Interface
- 기능의 선언과 구현을 분리할 수 있게 해준다
- 기능의 사용 통로 역할도 한다 (쓰고자 하는 기능의 접근점을 제공)

### Delegation
- 아웃소싱같은
- 어떤 기능의 구현을 다른 객체에게 위임하고 그 객체의 기능을 자기 기능처럼 갖다쓰는 것

### Strategy Pattern
- 다양한 여러가지 알고리즘을 `하나의 추상적인 접근점`을 통해서 사용한다
- 이렇게 하면 그 알고리즘은 변경가능해진다.
- 전략을 바꿔치기할 수 있게 된다.

위임Delegation과 전략패턴Strategy Pattern은 서로 비슷해보이지만 전략패턴은 말 그대로 하나의 확고한 소프트웨어 디자인 패턴인거고 위임은 패턴이라기 보단 소프트웨어 개발의 기초적인 지침인 "낮은 결합도와 높은 응집도"를 가능하게 하는 어떤 보편적인 하나의 테크닉이라고 보면 될 것 같다.
