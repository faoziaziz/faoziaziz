---
layout: post
title: "Plotting JFreeChart 1"
date: 2018-4-10 19:00:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- TechneAndPraxis
tags:
- Maven
- Java
- TA
excerpt_separator:  <!--more-->
---
Kelas ini merupakan bagian dari software TA, plotting dipakai untuk simulasi, look at [JavPlotMan](https://github.com/faoziaziz/JavPlotMan). Terus klick bagian alat dan SimCan

```java
package org.labseni;

import javax.swing.JFrame;
import org.jfree.chart.JFreeChart;
import org.jfree.chart.ChartUtils;
import org.jfree.chart.ChartFactory;
import org.jfree.data.general.DefaultPieDataset;
import java.io.File;

public class SimCantik {
	public SimCantik()
	{

	}
	public void Jalankan()
	{
		DefaultPieDataset pieDataset = new DefaultPieDataset();
		pieDataset.setValue("A", new Integer(75));
		pieDataset.setValue("B", new Integer(10));
		pieDataset.setValue("C", new Integer(10));
		pieDataset.setValue("D", new Integer(5));
	
		JFreeChart chart = ChartFactory.createPieChart("CSC408 Mark Distribution", //Title
				pieDataset, true, true, false);
	try {
		ChartUtils.saveChartAsJPEG(new File("chart.jpg"), chart, 500, 300);
	} catch (Exception e) {
		System.out.println("Problem occurred creating chart."); }
	
	}

}
```
