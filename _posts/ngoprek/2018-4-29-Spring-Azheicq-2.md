---
layout: post
title: "Spring Azheicq 2 : Membuat War"
date: 2018-4-29 02:44:00 +0700
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

Oke guys sekarang masuk ke memburu MIT episode 5 kali ini kita akan membuat file war agar lebih packageable. Untuk itu kita edit bagian pom.xml pada [Azheicq 1](https://faoziaziz.herokuapp.com/techneandpraxis/2018/04/21/Spring-Azheicq.html) menjadi seperti ini. Jangan lupa yang diedit cuma bagian buildnya sajah yah guys.

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>org.labseni</groupId>
  <artifactId>SpringMITcode</artifactId>
  <packaging>war</packaging>
  <version>1.0-PERCOBAAN</version>
  <name>SpringMITcode</name>
  

  <parent>
     <groupId>org.springframework.boot</groupId>
     <artifactId>spring-boot-starter-parent</artifactId>
     <version>2.0.1.RELEASE</version>
  </parent>

  <properties>
    <java.version>1.8</java.version>
  </properties>

  <dependencies>
    <dependency>
      <groupId>org.springframework.boot</groupId>
      <artifactId>spring-boot-starter-web</artifactId>
    </dependency>

    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>javax.servlet-api</artifactId>
      <version>3.1.0</version>
      <scope>provided</scope>
    </dependency>

    <dependency>
      <groupId>org.springframework</groupId>
      <artifactId>spring-webmvc</artifactId>
      <version>4.3.0.RELEASE</version>
      <scope>compile</scope>
    </dependency>

    <dependency>
        <groupId>jstl</groupId>
        <artifactId>jstl</artifactId>
        <version>1.2</version>
        <scope>compile</scope>
    </dependency>

    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>
  </dependencies>

  <build>

  		<!-- yang diedit bagian build doang yah guys-->
         <plugins>
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-compiler-plugin</artifactId>
                <version>2.3.2</version>
                <configuration>
                    <source>1.6</source>
                    <target>1.6</target>
                </configuration>
            </plugin> 
            
          
            <plugin>
                <groupId>org.apache.maven.plugins</groupId>
                <artifactId>maven-war-plugin</artifactId>
                <configuration>
                  <failOnMissingWebXml>false</failOnMissingWebXml>
                </configuration>
            </plugin>

            <!-- bagian ini saya buat untuk bisa di deploy tanpa harus menginstall server tomcat di localhost atau menginstall plugin deploy cli di heroku-->
            <plugin>
            
            <groupId>org.apache.maven.plugins</groupId>
            <artifactId>maven-dependency-plugin</artifactId>
            <version>3.0.2</version>
            <executions>
                <execution>
                    <phase>package</phase>
                    <goals><goal>copy</goal></goals>
                    <configuration>
                        <artifactItems>
                            <artifactItem>
                                <groupId>com.github.jsimone</groupId>
                                <artifactId>webapp-runner</artifactId>
                                <version>8.5.27.0</version>
                                <destFileName>webapp-runner.jar</destFileName>
                            </artifactItem>
                        </artifactItems>
                    </configuration>
                </execution>
            </executions>
        </plugin>


        </plugins>
    </build>
</project>


```

setelah itu kembali pada build dengan perintah

```bash
mvn package
```

nanti dalam direktory target akan muncul file war-nya. Dengan file war itu kita bisa run dalam tomcat atau heroku.

```bash
java -jar target/dependency/webapp-runner.jar target/SpringMITcode-1.0-PERCOBAAN.war
```

lalu cek di dalam localhost:8080/crot anda.

Untuk yang ingin deploy di heroku, buat procfile dengan nama Procfile dengan isinya sebagai berikut

```bash
web: java $JAVA_OPTS -jar target/dependency/webapp-runner.jar --port $PORT target/SpringMITcode-1.0-PERCOBAAN.war
```

Misalkan anda ingin memberi nama domainnya lontongtahuisi

```bash
heroku create lontongtahuisi
git init 
git add .
git commit -m "Commit pertama"
heroku git:remote -a lontongtahuisi
git push heroku master
```

sekarang coba masuk ke https://lontongtahuisi.herokuapp.com/crot maka akan muncul tampilan seperti localhost:8080/crot anda

# Credit

1. Agung Setiawan. 2013. [Cara jalankan war dengan Tomcat](https://agung-setiawan.com/cara-gampang-deploy-war-ke-tomcat-windows/). Diakses tanggal 29 April 2018 jam 03.47
2. Repo [Lontong Tahu Isi](https://github.com/faoziaziz/lontongtahuisi)