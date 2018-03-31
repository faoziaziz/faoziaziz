---
layout: post
title: "Device Firmware Upgrade"
author: Aziz Amerul Faozi
date: 2018-3-29 00:24:16 +0700
comments: true
excerpt_separator:  <!--more-->
categories: 
- TechneAndPraxis
tags:
- TA
---

DFU = Device Firmware Upgrade, menjadi salah satu methode untuk mengupload data kedalam firmware. Lalu apa yang dimaksud firmware disini, firmware merupakan software yang di store kedalam perangkat Writable, volatile memory dengan perantara USB. Lalu kenapa dinamai Upgrade, jadi guys itu karena bisa melakukan overwrite pada perangkat firmware tersebut. Methode ini merupakan cara untuk mendownload (mengirim informasi ke perangkat dari host), dan mengupload (dari perangkat menuju host).

|bmRequestType|bRequest|wValue|wIndex|wLength|Data|
|-------------|--------|------|------|-------|----|
|00100001b|DFU_DETACH|wTimeout|Interface|Zero|None|
|00100001b|DFU_DNLOAD|wBlockNum|Interface|Length|Firmware|
|10100001b|DFU_UPLOAD|Zero|Interface|Length|Firmware|
|10100001b|DFU_GETSTATUS|Zero|Interface|6|Status|
|00100001b|DFU_CLRSTATUS|Zero|Interface|Zero|None|
|10100001b|DFU_GETSTATE|Zero|Interface|1|Status|
|00100001b|DFU_ABORT |Zero|Interface|Zero|None|

Diatas adalah table DFU Class Spesific Request

|bRequest|Value|Protocol|
|DFU_DETACH|0|1|
|DFU_DNLOAD|1|2|
|DFU_UPLOAD|2|2|
|DFU_GETSTATUS|3|1*, 2|
|DFU_CLRSTATUS|4|2|
|DFU_GETSTATUE|5|1*,2|
|DFU_ABORT|6|2|

\* artinya optional
