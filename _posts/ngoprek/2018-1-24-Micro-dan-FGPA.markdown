---
layout: post
title: "Micro x dan FPGA"
date: 2018-1-24 20:23:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: [TechneAndPraxis]
---
Untuk komunikasi antara SPI dan Spartan FPGA

Pin :

## Methode Serial Master Mode


1. FPGA   <==>     Plarform Flash Prom
- DIN  <= DO
- CCLK => clk
2. FPGA <==> SPI Serial Flash
- MOSI => DATA_IN
- DIN <= DATA_OUT
- CSO_B => SELECT
- CCLK => CLOCK

## Slave Modes
1. Slave Serial Mode, Processor, Microcontroller <==> FPGA
- SERIAL => DIN
- CLOCK => CCLK
2. JTAG (JTAG tester, processor, Microcontroller <==> Spartan FPGA)
- DATA_OUT => TDI
- MODE_SELECT => TMS
- CLOCK => TCK
- DATA_IN <= TDO


Hal yang aneh :
1. pin antara JTAG Headaer dan FPGA
- TDO <==> TDO
- TDI <==> TDI
- TMS <==> TMS
- TCK <==> TCK
2. JIka pada boundary chain komunikasi antar device FPGA, 
- TDO <==> TDI
- TDI <==> TDO
- TMS <==> TMS
- TCK <==> TCK


FPGA juga memiliki alamat permanent yang bisa diakses dengan menggunakan perintah
{% highlight bash %}
 readDna -p <position>
{% endhighlight %}
