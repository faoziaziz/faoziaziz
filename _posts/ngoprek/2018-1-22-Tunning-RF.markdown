---
layout: post
title: "Tunning RF UI"
date: 2018-1-22 01:52:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- TechneAndPraxis
tags:
- TA
---
Oke gus sembari mengerjakan tugas akhir di bagian user interface sekarang kita mencoba untuk membuat slider untuk tunning RF kita kali ini.

{% highlight java %}
package com.herokuapp.faoziaziz;

import javax.swing.JFrame;
import javax.swing.JSlider;
import javax.swing.JLabel;
import java.awt.Container;
import java.util.Hashtable;

public class SliderBuatTunning {

	public static void main(String[] args) {
		// Membuat frame
		JFrame frem = new JFrame("Ngetes JSlider");
		frem.setDefaultCloseOperation(JFrame.EXIT_ON_CLOSE);
		// Create the value-label pairs in a hashtable
		Hashtable labelTable = new Hashtable();
		Container contentPane = frem.getContentPane();
		JSlider dds_tuner = new JSlider(0, 10, 5);
		labelTable.put(new Integer(0), new JLabel("Cupu"));
		labelTable.put(new Integer(5), new JLabel("Menengah"));
		labelTable.put(new Integer(10), new JLabel("Advance"));
/*		
		dds_tuner.setMinorTickSpacing(1);
		dds_tuner.setMajorTickSpacing(2);
		dds_tuner.setPaintTicks(true);
		contentPane.add(dds_tuner);
*/
		dds_tuner.setLabelTable(labelTable);
		dds_tuner.setPaintLabels(true);
		contentPane.add(dds_tuner);
		
		frem.setVisible(true);

	}

}

{% endhighlight %}

Oke guys itulah code yang nanti akan menjadi salah satu bahan untuk user Interface TA-Cantik kali ini.
