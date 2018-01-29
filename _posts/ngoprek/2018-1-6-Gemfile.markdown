---
layout: post
title: "Gemfile"
date: 2018-1-6 04:03:32 +0700
comments: true
categories: 
- TechneAndPraxis
tags:
- Heroku
---

*"Jadi apa itu gemfile?"*, buat anda yang baru dalam dunia per-ruby-an, Gemfile menjadi sering kita jumpai. Sebenarnya jika anda seorang developer android, Gemfile mirip dengan gradle.build yang ada dalam file android. Gemfile bekerja sebagai file untuk list dependency dari sesuatu yang akan anda development seperti jika anda menggunakan postgres maka akan muncul 
{%highlight ruby%}
gem 'pg', '0.18.4'
{%endhighlight%}

jika kita menggunakan perintah 
{%highlight bash%}
bundle install
{%endhighlight%}

maka kita akan menginstall dependency tersebut. 

Namun dalam proses pengerjaan ruby rail sering kita temukan code grup seperti development, test, atau production. Namun menurut hipotesa yang belum terverifikasi saya, grup tersebut digunakan untuk keperluan pemilihan teknik development, seperti kebiasaan localhost yang dijadikan sebagai test, atau hosting seperti heroku yang dijadikan sebagai production. 
