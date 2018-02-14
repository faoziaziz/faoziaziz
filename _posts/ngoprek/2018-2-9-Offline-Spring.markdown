---
layout: post
title: "Offline Spring"
date: 2018-2-9 23:59:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- TechneAndPraxis
tags:
- Heroku
- Java
- Maven
- Web
excerpt_separator:  <!--more-->
---

Bagi para pecinta bahasa pemrograman Java, mungkin dynamic web sudah tidak asing dengan tomcat dan servlet. Tapi kali ini kita akan mencoba untuk mengopreknya menggunakan CLI (Command Line Interface), karena komputer saya terlalu berat untuk memproses Eclipse.

Sayangnya dengan berbagai cara saya tidak bisa menggunakan settingan proxy untuk spring, walaupun maven masih bisa digunakan dengan mengedit [file m2/settings.xml](http:/techneandpraxis/filsafat/2018/02/05/Kopi-Jokowi.html) tapi saya membutuhkan kuota internet untuk bisa menjalankan perintah

```bash
spring init -dependencies=web faoziaziz
```

setelah itu jangan lupa rubah dalam mode offline supaya kita tidak perlu download lagi untuk me-run kode yang sudah kita buat dengan perintah

```bash
mvn -o install 
mvn dependency:go-offline
```

jangan lupa juga membuat Procfile dengan isi berikut agar nanti pas deploy pake heroku tidak susah.

```bash
web: java -jar target/*.jar
```

lalu buat repository git perintah berikut

```bash
git init
git add .
git commit -m "Ciye yang lagi development"
```

buat app heroku-nya, jangan lupa buat akun dulu, awas nama aplikasinya ganti jangan faoziaziz

```bash
heroku create faoziaziz
heroku git:remote -a faoziaziz

git push heroku master
```

edit file pada **src/main/java/com/example/faoziaziz/DemoApplication.java** dengan kode berikut, (lokasi folder faoziaziz akan terganti sesuai dengan init pada string yang kalian buat)

```java
/* 
  	bagian package jangan diganti jadi faoziaziz
  	pake yang bawaan ajah pas kamu lagi install 

*/
package com.example.faoziaziz;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;
import org.springframework.web.bind.annotation.*;
import org.springframework.stereotype.*;

@Controller
@SpringBootApplication
public class DemoApplication {
	@RequestMapping("/")
	@ResponseBody

	String home()
	{
		return "Hello World";
	}
	public static void main(String[] args) {
		SpringApplication.run(DemoApplication.class, args);
	}
}
```
untuk runnya tinggal 

```bash
heroku local web
```
lalu cek localhost:8080 anda.

