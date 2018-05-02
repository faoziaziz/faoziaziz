---
layout: post
title: "OVA TA : Installing JHipster"
date: 2018-5-1 23:11:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- Hobby
- TechneAndPraxis

tags:
- SAR
- MIT
- OVA TA
excerpt_separator:  <!--more-->
---

Oke guys, untuk edisi OVA TA kali ini sekaligus melanjutkan sinetron berjudul *"Mengejar MIT epiode 6 : Install JHipster"*. Pertama kita install dulu yarnnya yah.

```bash
npm install --global yarn
```

lalu install Yeoman dengan yarn

```bash
yarn global add yo
```

kemudian install JHipster

```bash
yarn global add generator-jhipster
```

buat direktory untuk membuat aplikasinya, semisal namanya aplikasiku

```bash
mkdir aplikasiku
cd aplikasiku
yo jhipster
```
Sayangnya react tidak tersedia di JHipster yang telah kita install tadi.


# Credit
1. [Installing Jhipster](https://www.jhipster.tech/installation/).
2. [Repo Sarahtustra](https://github.com/faoziaziz/sarahtustra.git)
