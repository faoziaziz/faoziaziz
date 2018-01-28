---
layout: post
title: "FPGA dan Osilator"
date: 2018-1-5 22:56:32 +0700
comments: true
categories: [TechneAndPraxis]
---

## Apakah osilator mempengaruhi kecepatan prosesing dari sebuah fpga?

Entah jawaban berikut benar atau tidak, yang jelas ini jawaban saya hari ini. Osilator memang diperlukan untuk mengatur kecepatan bit dalam proses komputasi, mengingat osilator bisa menghasilkan clock yang nantinya dimasukkan kedalam logic gate semisal flip-flop atau shift register untuk mengontrol kecepatan prosesing. Tapi sebenarnya kecepatan FPGA sendiri ditentukan oleh karakteristik Switching Time yang muncul akibat nilai capasitansi dari transistor logic yang membentuk FPGA tersebut, jadi FPGA memang bisa melakukan prosesing tanpa menggunakan osilator, tapi hal ini berdampak pada bit serial yang keluar akan sebanding dengan total delay dari nilai jumlah sinyal yang melewati logic gate tersebut. Wah, baru sadar aku dengan apa yang disampaikan Pak Aldo waktu itu. Kalau kita lihat prosesing serial dari FPGA spartan 6 slx-9 bisa mencapai 3.6 GHz, hal ini memang menarik untuk dijadikan sebagai digital prosesing. Tapi untuk keluar dan diproses semisal dengan mikrokontroler kecepatan data harus disesuaikan dengan clock dari mikrokontroler, dan inilah fungsi dari osilator sebagai clock di FPGA. Walohualam
