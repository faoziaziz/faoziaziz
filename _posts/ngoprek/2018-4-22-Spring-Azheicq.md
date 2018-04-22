---
layout: post
title: "Spring Azheicq 1"
date: 2018-4-22 06:54:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- TechneAndPraxis
tags:
- Spring
- Java
- MVC
- MIT
excerpt_separator:  <!--more-->
---

Oke guys, masih bersama saya dalam acara berburu MIT episode 3, kali ini kita akan memanfaatkan MVC Spring sebagai midle-end dari *Zuhandene* yang akan kita gunakan untuk melaukan perburuan ini. Yang pertama buat dulu project maven-nya iyah, sebenernya bisa sih pake 

```bash 
spring init 
``` 
tapi biar agak keren kita build dari maven awalnya guys. Perintahnya seperti biasa 

```bash
mvn archetype:generate -DgroupId=com.labseni.app -DartifactId=springts -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false 
```
lalu edit bagian pomnya dan sesuaiakan dengan kebutuhan, ah He he he, berikut code **pom.xml** nya.

```xml 
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>com.labseni.app</groupId>
  <artifactId>springts</artifactId>
  <packaging>war</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>springts</name>
  <url>http://maven.apache.org</url>

  <properties>
         <java-version>1.8</java-version>
         <springframework.version>4.3.0.RELEASE</springframework.version>
         <jackson.version>2.7.5</jackson.version>
   </properties>


  <dependencies>
    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>${springframework.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-aop</artifactId>
      <version>${springframework.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-beans</artifactId>
      <version>${springframework.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-context</artifactId>
      <version>${springframework.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-core</artifactId>
      <version>${springframework.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-expression</artifactId>
      <version>${springframework.version}</version>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-web</artifactId>
      <version>${springframework.version}</version>
    </dependency>

    <dependency>
        <groupId>jstl</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
    </dependency>

    <dependency>
      <groupId>com.fasterxml.jackson.core</groupId>
      <artifactId>jackson-databind</artifactId>
      <version>${jackson.version}</version>
    </dependency>

    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>
    </dependency>

    <dependency>
        <groupId>commons-logging</groupId>
        <artifactId>commons-logging</artifactId>
        <version>1.2</version>
    </dependency>
  </dependencies>

  <build>
        <!-- plugin jadul
        <plugins>
            <plugin>
                <groupId>org.springframework.boot</groupId>
                <artifactId>spring-boot-maven-plugin</artifactId>
            </plugin>
        </plugins>
        -->
    <finalName>goMIT</finalName>
      <pluginManagement>
      <plugins>
        <plugin>
          <groupId>org.apache.tomcat.maven</groupId>
          <artifactId>tomcat7-maven-plugin</artifactId>
          <version>2.2</version>
          <configuration>
            <path>/goMIT</path>
          </configuration>
        </plugin>
      </plugins>
    </pluginManagement>
  </build>
</project>

```

lalu buat file DispatcherServletInitializer.java, HomeController.java, dan WebApplicationContextConfig.java, dalam direktory 

```bash
src/main/java/com/labseni/app
```
setelah itu buat direktory juga, di 

```bash
 springts/src/main/webapp/WEB-INF/jsp
```

lalu buat file dengan nama welcome.jsp dalam direktory diatas, berikut codenya.

```html
<!-- springts/src/main/webapp/WEB-INF/jsp/welcome.jsp -->
<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core"%>
<!DOCTYPE html>
<html lang="en">
	<head>
		<meta charset="utf-8">
		<meta http-equiv="X-UA-Compatible" content="IE=edge">
		<meta name="viewport" content="width=device-width, initial-scale=1">
		<title>Welcome</title>
		<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.5/css/bootstrap.min.css">
	</head>
	<body>
		<div class="jumbotron">
			<h1>${greeting}</h1>
			<p>${tagline}</p>
		</div>
		
	</body>
</html>
```

setelah itu kita edit beberapa file javanya,  yang ke

- bikin file DispatcherServletInitializer.java

```java
/*
	filename : springts/src/main/java/com/labseni/app/DispatcherServletInitializer.java
*/
package com.labseni.app.config;

import org.springframework.web.servlet.support.AbstractAnnotationConfigDispatcherServletInitializer;

public class DispatcherServletInitializer extends AbstractAnnotationConfigDispatcherServletInitializer{

	@Override
	protected Class<?>[] getRootConfigClasses(){
		return null;
	}
	@Override
	protected Class<?>[] getServletConfigClasses(){
		return new Class[]
		{
			WebApplicationContextConfig.class
		};
	}

	@Override
	protected String[] getServletMappings(){
		return new String[]{"/"};
	}
}
```
- bikin file HomeController.java

```java
/*
	filename : springts/src/main/java/com/labseni/app/HomeController.java
*/

package com.labseni.app.controller;

import org.springframework.stereotype.Controller;
import org.springframework.ui.Model;
import org.springframework.web.bind.annotation.RequestMapping;

@Controller
public class HomeController{
	@RequestMapping("/")
	public String welcome(Model model)
	{
		model.addAttribute("greeting", "Welcome to MIT!");
		model.addAttribute("tagline", "Only faoziaziz can pass MIT");
		return "welcome";
	}
}
```
- WebApplicationContextConfig.java

```java
/*
	filename : springts/src/main/java/com/labseni/app/WebApplicationContextConfig.java
*/
package com.labseni.app.config;

import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.ComponentScan;
import org.springframework.context.annotation.Configuration;
import org.springframework.web.servlet.config.annotation.DefaultServletHandlerConfigurer;
import org.springframework.web.servlet.config.annotation.EnableWebMvc;
import org.springframework.web.servlet.config.annotation.WebMvcConfigurerAdapter;
import org.springframework.web.servlet.view.InternalResourceViewResolver;
import org.springframework.web.servlet.view.JstlView;

@Configuration
@EnableWebMvc
@ComponentScan("com.labseni.app")
public class WebApplicationContextConfig extends WebMvcConfigurerAdapter{
	@Override
	public void configureDefaultServletHandling(DefaultServletHandlerConfigurer configurer){
		configurer.enable();
	}
	@Bean
	public InternalResourceViewResolver getInternalResourceViewResolver(){
		InternalResourceViewResolver resolver = new InternalResourceViewResolver();
		resolver.setViewClass(JstlView.class);
		resolver.setPrefix("/WEB-INF/jsp/");
		resolver.setSuffix(".jsp");
		return resolver;
	}
}
```

lalu kita jalankan dalam server tomcat 7 dengan perintah berikut guys.

```bash
mvn -o tomcat7:run
```
Cek di browser, dengan mengetikan alamat localhost:8080. Oke guys, nanti akan ada tampilan seperti berikut.

[gambar]

Spring merupakan MVC dan reactJS merupakan bagian V dari MVC, jadi code ini nanti kita akan pakai untuk kombinasikan AWS sebagai BackEnd, Spring sebagai Midle End, dan ReactJS sebagai Front-End-nya guys. Biar bisa dapet Huge Recommendation ke SMART Guys.

# Kredit
1. Ganeshan, Amuthan. 2016.*Spring MVC Beginner's Guide Second Edition*. Birmingham : Packt Publishing.
2. Github : [SpringAzheicq](https://github.com/faoziaziz/SpringAzheicq) 



