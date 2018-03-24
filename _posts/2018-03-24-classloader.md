---
layout: post
title: 자바의 클래스로더 시스템
tags: Java
category: blog
date: 2018-03-24
modify_date: 
picture_frame: shadow
---
  
## Java의 클래스로더 시스템과 리플렉션 기능  

자바는 ***동적 로드*** 특징이 있다.   
이 동적 로드를 담당하는 부분이 JVM의 ***클래스 로더***다.  
  
 
## 자바에서 동적 로드란?  
자바는 모든 클래스를 한꺼번에 메모리에 로딩하고 실행되는 게 아니라 실행 도중 어떠한 클래스를 처음 참조할 때 해당 클래스를 로드하고 링크하는 특징이있다. 프로그램 실행 흐름 상 필요한 클래스만 그 때 그 때 로딩되어서 메모리 공간을 효율적으로 사용할 수 있다.  
만약 프로그램 실행 중 전혀 참조되지 않는 클래스라면 메모리에 로딩되지 않는다.  
그리고 그 클래스 로딩을 담당하는 것이 자바의 클래스 로더이다.  
클래스 로더는 자바어플리케이션이 실행될 때 가장 먼저 **부트스트랩 클래스로더**가 클래스들을 로드하고 나머지 클래스 로더들이 각각 다른 범위의 클래스들을 로드한다.  

* 부트스트랩 클래스 로더 ( Bootstrap class loader ) - JVM을 가동할 때 생성되며, __Object클래스를 비롯해 자바 API__를 로드한다. 다른 클래스 로더와 달리 네이티브 코드(기계가 알아듣는 코드)로 구현돼 있다. 

* 확장 클래스 로더 ( extension class loader ) - 기본 자바API를 제외한 확장 클래스(?)를 로드한다. 보안 기능.

* 시스템 클래스 로더 ( system class loader ) - 애플리케이션의 클래스를 로드한다. 사용자가 지정한 클래스 패스 내의 클래스를 로드한다. 사용자가 만든 클래스들.

* 사용자 정의 클래스 로더( user-defined class loader )  - 어플리케이션 사용자가 직접 코드 상에서 생성해서 사용하는 클래스 로더 -> Class.forName(클래스이름)

  
  
## Class.forName(클래스이름)의 원리와 용도  
한 객체의 인스턴스를 만드는 방법에는 키워드 new를 이용한 방법만 있는 것이 아니다. 자바의 동적인 클래스 로드의 특징을 활용한 Class.forName이란 클래스로더를 이용할 수도 있다.  
만약에 어떠한 클래스의 이름만 알고 있을 경우 그 클래스를 프로그래머가 클래스로더를 사용해서 동적으로 로드할 수 있다.  
ex)  
```
String className = "Hello3"; ----> 클래스 이름이 이러할 때  
Class clazz = Class.forName(className); ----> 이렇게 Class.forName이란 메소드의 인자값으로 클래스 이름을 주면 이 클래스로더 메소드는 className에 해당하는 클래스 정보를 읽어들여서 메모리에 올리고  
해당 클래스 정보를 리턴한다. 그 값을 clazz라는 변수에 저장.  
``
여기까지는 클래스의 정보를 가지고 온 것이고 인스턴스로 만드려면 clazz.newInstance() 메소드를 호출해야 한다.  
클래스명이 Hello3 이라면 (Hello3)clazz.newInstance()로 형변환을 해주면 된다.  
  
일반적인 인스턴스 생성이라면 키워드 new를 이용하면 되지만 만약에 아직 정해지지 않은 클래스를 가정해놓고 코드를 구현해야 한다면 Class.forName이 유용하다.  왜냐하면 클래스이름에 해당하는 String className 변수만 나중에 바꿔치기 하면 되기 때문이다.  
이렇게 Class clazz라는 변수에 클래스정보를 담으면 clazz.newInstance()를 통해서 인스턴스화 할 수 있는데 위의 예시처럼 형변환을 (Hello3)으로 하는 일은 거의 없을 것이다. 왜냐하면 애초에 아직 안정해진 클래스를 가지고 코드를 구현해 놓고자 클래스로더를 활용하는 건데  
형변환을 뭘로 할지도 당연히 모르는 상태일 것이기 때문이다. 그래서 보통 Hello3이 구현하고 있는 인터페이스를 정의해서 그 인터페이스로 형변환을 시켜서 가져오는 방법으로 사용한다.  
Hello3가 interface Hello 를 구현하는 클래스라면 (Hello)clazz.newInstance()로 인스턴스화 시킬 수 있고 이렇게 하면 메소드는 Hello3이 오버라이딩 한 것으로 호출될 것이니까 Hello3에서 구현한 대로 인스턴스를 쓸 수 있다.  
  
## 자바의 리플렉션 기능  
Class clazz에 클래스 정보들이 담긴다고 했는데 클래스의 필드와 메소드도 이를 통해 알아낼 수 있다.  
이처럼 메모리에 로딩되어 있는 클래스의 정보를 프로그래머가 코딩하면서 알아낼 수 있게 하는 기능이 바로 자바의 리플렉션 기능이다.  
clazz 변수를 이용해서 그 클래스가 가진 모든 메소드와 필드를 알아낼 수 있는데 예를 들어  
```
Method[] method = clazz.getMethod();
Field[] field = claszz.getFields();
```
이런식으로 메소드와 필드들을 배열로 가져올 수 있고 배열에 하나씩 접근해서 getName메소드를 사용하면 메소드의 이름과 필드 이름을 알아낼 수 있다.  
이렇게 객체를 통해(위의 Method, Field 같은 - 이것들은 java.lang.reflect에 속하는 클래스들이다.) 메모리에 적재된 클래스의 정보를 이용해 분석하는 방법이 바로 자바의 Reflection 기능이다.  

이클립스같은 IDE에서 객체이름뒤에 점.을 찍으면 메소드목록이 주르륵 나오는 것도 그냥 나오는 것이 아니라 IDE 내부적으로 리플렉션 기능을 구현하고 있기 때문에 가능한 일인 것이다.  
  