---
layout: post
title: "Web Heroku Basa Jawa"
date: 2018-2-14 01:17:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- TechneAndPraxis
tags:
- Maven
- Java
excerpt_separator:  <!--more-->
---

Oke guys sebelumnya kita pernah ngoprek pake Spring, kali ini kita akan mencoba untuk membuatnya dari maven, buat yang belum install maven, silahkan install maven dulu yah. 

Untuk memulainya kita generate dulu direktorinya guys dengan perintah berikut

```bash
mvn archetype:generate -DgroupId=org.labseni.javalabseni -DartifactId=javalabseni -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false
```
masuk ke direktory project dengan perintah
```bash
cd javalabseni
```
edit file pom.xml nya dengan kode berikut
```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>org.labseni.javalabseni</groupId>
  <artifactId>javalabseni</artifactId>
  <packaging>jar</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>javalabseni</name>
  <url>http://maven.apache.org</url>
  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>   
    </dependency>
     <!--Ini tambahan dari pribadi, buat ngerun jadi webserver -->
     <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>jstl</artifactId>
      <version>1.2</version>
      <scope>compile</scope>   
    </dependency>

     <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>4.3.0.RELEASE</version>
      <scope>compile</scope>   
    </dependency>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>   
    </dependency>
  </dependencies>
</project>
```

Download dependencynya biar bisa dipake lagi sewaktu-waktu, dengan perintah mvn berikut
```bash
mvn dependency:go-offline
```
lalu install dengan mode offline biar hemat kuota
```bash
mvn -o install
```
buat direktory webapp dengan perintah berikut
```bash
mkdir -p src/main/webapp
```
buat file azizganteng.jsp
```bash
touch src/main/webapp/WEB-INF/azizganteng.jsp
```
