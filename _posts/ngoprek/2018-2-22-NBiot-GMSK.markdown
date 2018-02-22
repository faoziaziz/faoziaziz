---
layout: post
title: "NBiot GMSK"
date: 2018-2-22 13:39:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- TechneAndPraxis
tags:
- Modulasi
- Iot
- OFDM
excerpt_separator:  <!--more-->
---
*"Mengapa nb iot menggunakan modulasi GMSK?"* pertanyaan itu menjadi penting ketika OFDM hampir merajalela di dunia pertelekomunikasian. Walaupun sebenarnya kita juga bisa menggunakna GMSK-OFDM untuk mengoptimalkannya, karena memang OFDM tidaklah mirip dengan teknik modulasi, dan lebih cenderung mirip dengan teknik Multiplexing. OFDM memutar spectrum frequensi agar sinyal tidak berbenturan walau pada titik yang sama, kalau secara geometri ofdm akan membentu sinyal yang cenderung 3D kalau dilihat dengan Spectrum Analizer yang mampu mengukur dalam kerangka 3 Dimensi.

Lalu mengapa GMSK masih digunakan, yang jelas pada bagian modulator, Hilbert transform akan merubah bentuk sinyal yang kotak-kotak akan lebih cenderung bisa sinussoid, mengingat ketika kita mencoba membuat sinyal yang semakin kotak maka ada kecendrungan untuk melebarkan pita di domain frekuensi. Hilber transform ini akan lebih mengefisiensikan spektrum frekuensi namun memberikan dampak pada bentuk sinyal di domain waktu terlihat seperti sinusoid.

IoT membutuhkan transmini yang cukup cepat tapi dengan bandwith yang terbatas. Hal ini dikarenakan device paling hanya mengirimkan data sensor yang jika diukur palingan tidak menjapai kecepatan 1 Kbps. GMSK cukup bagus untuk efisiensi spektrum, inilah kenapa NBIoT memilih teknik modulasi ini ketimbang QAM yang notabennya bisa mengirimkan jumlah data yang lebih banyak. 
