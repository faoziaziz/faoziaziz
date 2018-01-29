---
layout: post
title: "Pin arm-m0 Nouvton"
date: 2018-1-22 18:37:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- TechneAndPraxis
tags:
- TA
---

Oke Guys sekarang kita mencoba untuk membuat sebuah downloader untuk arm-cortex-M0 sebagai controller dari SDR yang akan kita buat beberapa pin disini akan menjadi notes, untuk percobaan yang nanti akan kita download ke arm-cortex Nouton yang sudah diintegrasi dengan beragam tambahan seperti osilator dan lainnya.

untuk LQFP-48. M058-M05162


- pin 4  : rst 
- pin 6  : avss
- pin 34 : mosi_1
- pin 33 : miso_1

**Untuk fungsi pin SPI**
- pin 1  : mosi_0
- Pin 2  : miso_0 
- pin 47 : SPISS0 
- pin 3  : SPICLK0
 
- pin 42 : AVDD (pin untuk analog supply operations)
- pin 6  : AVSS (pin untuk analog ground operation)
- pin 41 : VDD  ( untuk digital supply)
- pin 17 : VSS (untuk digital ground)
- pin 16 : XTAL1
- pin 15 : XTAL2

