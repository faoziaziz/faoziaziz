---
layout: post
title: "Maven Project"
date: 2018-4-3 04:18:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- TechneAndPraxis
tags:
- Maven
- Java
excerpt_separator:  <!--more-->
---

Hello guys untuk membuat project dengan java, alangkah bagusnya jika kita menggunakan builder maven. Tapi jika anda bermasalah dengan proxy itb anda bisa mengakses [link berikut ini](). Pertama-tama kita deklarasikan dulu projectnya bernama apa, 


```bash
mvn archetype:generate -DgroupId=org.labseni.app -DartifactId=PlotJavaBaru -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false 
```
Nama dari aplikasi yang akan kita buat adalah PlotJavaBaru dan ini akan menghadirkan direktory beserta content dasar untuk membuat sebuah project dengan menggunakan Java.

Seperty biasa kita gunakan perintah mvn package untuk membuild code project tadi.

# Referensi
1. [Maven in 5 Minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) 

