---
layout: post
title:  "[Spring] Spring Basic"
subtitle:   "[Spring] Spring Basic"
categories: study
tags: spring
---



## Spring

- #### Framework

  - 특정한 목적에 맞게 프로그래밍을 쉽게 하기 위한 약속 

- #### Spring

  - JAVA 언어를 기반으로, 다양한 어플리케이션을 제작하기 위한 약속된 프로그래밍 틀 
  - 코드의 경량화
  - 개발 중 테스트가 쉬움 

## DI(Dependency Injection) 와 IOC 컨테이너

### A 객체에서 B/C 객체 이용하는 방법

<img src="https://github.com/minheeson/minheeson.github.io/blob/master/assets/img/spring/2_DI.png" width=500/>

- 방법 1) A 객체가 B/C 객체를 new 생성자를 통해 직접 생성 

  ```java
  MyCalculator myCalculator = new MyCalculator();
  myCalculator.setCalculator(new Calculator());

  myCalculator.setFirstNum(10);
  myCalculator.setSecondNum(2);
  		
  myCalculator.add();
  ```

- 방법 2) __외부에서 생성된 객체를 setter() 나 생성자를 통해__ 사용하는 방법 (_DI_)


- #### IOC 컨테이너

  <img src="https://github.com/minheeson/minheeson.github.io/blob/master/assets/img/spring/2_IOC.png" width=250/>

  - 외부(IOC 컨테이너)에서 생성된 B/C 객체를 조립(주입)시켜 setter() 나 생성자를 통해 사용
  - 각각의 객체는 인터페이스를 통해 부품화 
  - 결국, 스프링은 부품을 __생성하고 조립하는 라이브러리의 집합체라__ 할 수 있음 

## Spring property

### Spring Property Configuration

```java
// xml파일 위치 지정
String configLocation = "classpath:applicationCTX.xml";
		
// IOC 컨테이너 생성 (부품들 생성) 
// 지정한 위치를 참고하여 설정파일을 얻어옴 
AbstractApplicationContext ctx = new GenericXmlApplicationContext(configLocation);
		
// 스프링 컨테이너에서 컴포넌트(bean) 가져옴
// 외부에서 얻어옴 (=주입)
MyInfo myInfo = ctx.getBean("myInfo", MyInfo.class);
		
myInfo.getInfo();
ctx.close();
```

```xml
<!-- ".BMICalculator"클래스를 bmiCalculator라는 id를 지정해서 객체(bean) 생성 -->
<bean id="bmiCalculator" class="spring_ex_4.BMICalculator">
  	<!-- 클래스 내의 필드의 값을 설정 -->
  	<!-- 기초 데이터 -->
	<property name="lowWeight" value="18.5" />
	<property name="normal" value="23" />
	<property name="overWeight" value="25" />
	<property name="obesity" value="30" />
</bean>

<!-- ".MyInfo"클래스를 myInfo라는 id를 지정해서 객체(bean) 생성 -->
<bean id="myInfo" class="spring_ex_4.MyInfo">
	<property name="name" value="홍길동" />
	<property name="height" value="187" />
	<property name="weight" value="84" />
  	<!--  List 타입 -->
	<property name="hobby">
		<list>
			<value>수영</value>
			<value>요리</value>
			<value>독서</value>
		</list>
	</property>
  	<!-- 다른 빈 객체 참조 -->
  	<!-- bean "bmiCalculator"를 참조함 -->
	<property name="bmiCalculator">
		<ref bean="bmiCalculator" />
	</property>
</bean>
```

- xml 파일을 쓰기 위해서는 반드시 클래스에서 setter() 만들어줘야 가능 
- 생성, 조립 모두 컨테이너의 역할 