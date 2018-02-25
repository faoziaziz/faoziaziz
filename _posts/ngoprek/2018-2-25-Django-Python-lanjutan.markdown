---
layout: post
title: "Django Python lanjutan"
date: 2018-2-25 22:46:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- TechneAndPraxis
tags:
- Python
- Django
excerpt_separator:  <!--more-->
---

Oke guys setelah menginstall django admin di [Django](http:/techneandpraxis/2018/02/20/Django.html) sekarang kita mencoba untuk memperbaiki file untuk bisa di hosting dengan heroku. Kita buat project-nya dahulu dengan template dari heroku dengan perintah berikut ini, project tersebut saya beri nama faoziaziz.

```bash
django-admin.py startproject --template=https://github.com/heroku/heroku-django-template/archive/master.zip --name=Procfile faoziaziz

```
lalu masuk kedalam direktory faoziaziz

```bash
cd faoziaziz
```

lalu install pipenv

```bash
pipenv install
```

kemudian coba kita masuk ke dalam virtual environment

```bash
pipenv shell
```

kemudian kita coba run servernya dengan perintah

```bash
heroku local 
```
cek ke dalam webbrowser dengan alamat localhost:5000,

jika anda ingin menguploadnya ke heroku server anda

```bash
heroku create faoziaziz
heroku git:remote -a faoziaziz
git init .
git commit -m "Push ke heroku"
git push heroku master
```

lalu coba cek ke alamat https://faoziaziz.herokuapp.com, gunakan alamat kesukaan anda untuk bisa dipakai sesuai kebutuhan.
