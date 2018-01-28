---
layout: post
title: "Masalah npm dan Proxy"
date: 2018-1-5 23:54:32 +0700
comments: true
categories: [TechneAndPraxis]
---

***npm*** atau node package manager merupakan salah satu hal yang cukup menarik untuk para developer heroku. Mengingat node.js disediakan oleh heroku untuk mendevelop aplikasi disana untuk para pengoprek heroku yang mengalami masalah dengan proxy itb semoga ini bisa menjadi solusi.

{%highlight bash%}
npm config set proxy http://<username>:<password>@cache.itb.ac.id:8080
npm config set https-proxy http://<username>:<password>@cache.itb.ac.id:8080
{%endhighlight%}

sumber [NPM behind Proxy](https://forum.freecodecamp.org/t/npm-behind-a-proxy-server/19386)
untuk mendeaktifasi proxy semisal anda menggunakan wifi tether berikut codenya

{%highlight bash%}
npm config delete http-proxy
npm config delete https-proxy

npm config rm proxy
npm config rm https-proxy

set HTTP_PROXY=null
set HTTPS_PROXY=null
{%endhighlight%}
