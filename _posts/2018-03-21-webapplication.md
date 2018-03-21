---
layout: post
title: 웹어플리케이션 구조
tags: WebProgramming
category: blog
date: 2018-03-21
modify_date: 
picture_frame: shadow
---
  
**클라이언트가 웹서버에 접속하는 과정**  
1. ip접속하면 OS가 80포트갖고있는 웹서버에 연결해준다. (Nginx, Apache)  
2. 웹서버가 path정보 읽는다. path를 읽어서 해당 WAS로 요청 전달 (웹서버에 어떤 path면 어떤 WAS로 갈지 설정해둔다)  
path앞부분이 contextRoot다.  웹 어플리케이션마다 고유의 contextRoot값이 있어야한다. contextRoot다르면 다른 어플리케이션이다.    
3. WAS는 path정보를 통해 어떤 어플리케이션인지 알아내고 해당 자원 꺼낸뒤 응답한다. 그리곤 접속이 종료된다.  
   
 
*왜 앞단에 웹서버를 두지?*--> 장애가 발생했을 때 대응이 편하다. (그리고 웹서버는 간단하게 만들어져있어서 잘 안죽음)  
보통 웹서버랑 WAS는 분리해놓는다(IP다름)   
WAS 하나에 장애생기면 WAS만 바꿔치기 하면 손쉽게 장애에 대응 할 수 있다 (failover)    
    

  
**WAS와 웹어플리케이션의 관계**  
하나의 WAS에 여러개의 application 배치deploy할 수 있다. (각 어플리케이션은 contextRoot 다름)  
각각의 어플리케이션은 서로가 정보를 공유하지 못한다.  
  
    

**웹어플리케이션**

웹어플리케이션에는 반드시 WEB-INF라는 폴더가 있다. 여기 안에는 web.xml이 있고 classes폴더, lib폴더 존재   

* web.xml: 배치기술자, 배포기술자 deployment descriptor. 어떤 path가 오면 어떤 서블릿이 실행되느냐 의 정보를 담고있다.

* classes 폴더: 클래스파일, 패키지

* lib: *.jar

그 외 WEB-INF폴더와 같은 레벨에 각종파일, 폴더들 존재

*위의 디렉토리를 통째로 압축하면 war 파일이고 이 war를 WAS에 설치하면 웹어플리케이션이 비로소 동작하기 시작한다.*

