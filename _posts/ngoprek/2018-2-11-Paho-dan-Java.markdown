---
layout: post
title: "Paho dan Java"
date: 2018-2-11 23:09:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- TechneAndPraxis
tags:
- Paho
- Maven
- Java
- IoT
- Heroku
- MQTT
excerpt_separator:  <!--more-->
---

Oke guys sekarang kita mencoba untuk menaruh server MQTT di heroku, walaupun sepertinya susah untuk mengakses port 1883 dari ITB tapi kita akan coba menggunakan perantara HTTP/HTTPS protokolnya untuk bisa men-subscribe dan post topik dari dashboard swing yang akan kita buat nanti.

# Arsitekturnya
![Arsitekturnya](https://raw.githubusercontent.com/faoziaziz/IdiotBGT/master/images/pic1.png)

mungkin kita akan mencoba JSON untuk bisa dipakai mengakses ke server Moquette di heroku.

# Progres Sementara
Untuk sementara kita coba codenya di komputer local.

## Install 
Untuk installasi cukup dengan mengeklone kode dan membuildnya dengan maven.
```bash
git clone https://github.com/faoziaziz/IdiotBGT.git tutLabseni
cd tutLabseni/idiotBGT
mvn exec:java -Dexec.mainClass=org.labseni.App
```

# Referensi 
1. [Playing around MQTT](http://www.hascode.com/2016/06/playing-around-with-mqtt-and-java-with-moquette-and-eclipse-paho/)

