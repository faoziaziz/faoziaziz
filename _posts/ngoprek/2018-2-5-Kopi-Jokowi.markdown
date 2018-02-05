---
layout: post
title: "Kopi Jokowi"
date: 2018-2-5 15:29:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- TechneAndPraxis
- Filsafat
tags:
- IoT
- Jokowi
- Kopi
- Gratis
- MQTT

excerpt_separator:  <!--more-->
---
Sembari melepas kesedihan karena ide Multiplexing Polarisasi pernah dibahas oleh NASA. Saya mencoba melepas kesedihan dengan melakukan tindakan tidak jelas. Ah bukan hanya karena malu karena multiplexing polarisasi yang sudah pernah ditemukan, tapi alih-alih menambahkannya kedalam TA supaya keren, malah membuat saya susah move on dari kesedihan gagal meraih nobel. Kali ini saya mencoba untuk menginstall Paho, salah satu platform yang disediakan untuk memanfaatkan MQTT. Sayangnya untuk menginstall ini tidak bisa saya lakukan dengan menggunakan WiFI ITB karena terhalang oleh proxy yang mengeblock port 443. Karena saya lagi sedih, saya memaksakan diri untuk menginstallnya dan nebeng ke Coffice Bandung dekat dengan Unpad DU. Tapi karena tidak enak dengan baristanya saya mesen saja kopi yang murah, akh jika harga kopi espresso segitu pasti tubruk lebih murah, dan sayangnya harganya sama 17 ribu. Alih-alih ingin berhemat untuk memanfaatkan wifi gratis malah jadi hedon, ya sudahlah yang penting saya bisa mengoprek dengan bebas tanpa dibatasi proxy, dan coba untuk mengeksploitasi WiFi-nya supaya uang 17 ribu itu bisa kembali dengan bentuk lain seperti untuk download buku, atau untuk install Paho Dikomputer saya supaya bisa ngoprek, wkwkwkkwk.

## Install Paho
Buat yang ingin ngoprek dengan paho anda bisa mendownloadnya [di sini](https://codeload.github.com/eclipse/paho.mqtt.java/zip/master)
setelah berhasil di download anda lalu mengekstraknya. Kalau mau terlihat keren anda bisa mengekstraknya dengan terminal dengan perintah berikut 

```bash
unzip paho.mqtt.java.zip
```
setelah itu masuk kedirektorinya dan menginstall dengan maven jangan lupa edit bagian pom.xml nya dari kepler menjadi oxygen.

```
cd paho.mqtt.java
mvn package -Dskiptests
```

## Kopi 
Kopi tubruk mengingatkan saya pada masa lalu yang sok iye pada pengetahuan kopi. Tapi memang begitulah kopi rasanya seperti itu, seperti Jokowi yang memang mirip dengan kopi tubruk. Semakin lama maka kopinya akan semakin robustam tapi memang saya memesan kopi lampung. Padahal dulu pas aku mesen kopi lampung rasanya kayak rasa coklat, wkwkwk mungkin beda tempat beda rasa. Kopi tubruk memang kopi yang simple dan memang hanya butuh roasting dan digiling lalu diseduh dengan air panas. 
