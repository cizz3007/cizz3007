---
title: thymeleaf 문법
date: 2018-04-09 19:00:00
description: <center>Thymeleaf 문법 1</center>

categories:
- 타임리프
- SYNTAX
- THYMELEAF

tags:THYMELEAF, SYNTAX

---

# THYMELEAF 설정
---

> 스프링부트 + thymeleaf로 작업 중인데, 작업하면서 잊지 않기 위해 기록해둔다. 
템플릿엔진 언어 중 하나인 타임리프를 사용하기 위해 아래와 같이 해주자. html태그에 xmlns:th="http://www.thymeleaf.org"를 추가해주고, /로 테그를 잘 닫아주자.

```
<!DOCTYPE HTML>
<html xmlns:th="http://www.thymeleaf.org">
<head>
    <title>Thymeleaf syntax</title>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8"/>
</head>
<body>

</body>
</html>

```
<br>
<br>
<br>

> 메이븐 환경이라면 아래의 의존성을 추가하자.
```
  <!-- thymeleaf 의존성추가-->
        <dependency>
        	<groupId>org.springframework.boot</groupId>
        	<artifactId>spring-boot-starter-thymeleaf</artifactId>
        </dependency>
```
<br>
<br>
<br>

> application.properties에 추가해주자
```
spring.thymeleaf.prefix=/WEB-INF/views/ 본인의 경로에 맞게 수정
spring.thymeleaf.suffix=.html //마찬가지로 현재 본인의 템플릿엔진언어의 확장자로 변경후 사용.
spring.thymeleaf.cache=false //true or false 자신의 환경에 맞게 설정
spring.thymeleaf.enabled=true
spring.thymeleaf.mode=LEGACYHTML5 // legacy모드 사용시 입력 
spring.thymeleaf.encoding=UTF-8 

```
<br>
<br>
<br>

> Thymeleaf는 반드시 태그를 닫아줘야 오류가 없다, 이러한 방식은 나한테는 불편함으로 느껴졌다. 다행히 해결방법은 아주 간단했다.
  아래의 의존성을 추가해주자.  
  thymeleaf-html5-legacy는 태그를 닫지 않아도 thymeleaf가 정상적으로 태그들을 인식하게 해준다.

```
 <!--thymelead-html5 legacy(메이븐)-->
        <dependency>
             <groupId>net.sourceforge.nekohtml</groupId>
             <artifactId>nekohtml</artifactId>
         </dependency>

```
