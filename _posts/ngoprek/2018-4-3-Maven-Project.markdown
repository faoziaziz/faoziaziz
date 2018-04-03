---
layout: post
title: "Maven Project"
date: 2018-4-3 04:18:00 +0700
author: Aziz Amerul Faozi
comments: true
categories: 
- TechneAndPraxis
tags:
- Maven
- Java
excerpt_separator:  <!--more-->
---

Hello guys untuk membuat project dengan java, alangkah bagusnya jika kita menggunakan builder maven. Tapi jika anda bermasalah dengan proxy itb anda bisa mengakses [link berikut ini](http:/techneandpraxis/filsafat/2018/02/05/Kopi-Jokowi.html). Pertama-tama kita deklarasikan dulu projectnya bernama apa, 


```bash
mvn archetype:generate -DgroupId=org.labseni.app -DartifactId=PlotJavaBaru -DarchetypeArtifactId=maven-archetype-quickstart -DinteractiveMode=false 
```
Nama dari aplikasi yang akan kita buat adalah PlotJavaBaru dan ini akan menghadirkan direktory beserta content dasar untuk membuat sebuah project dengan menggunakan Java.

Seperty biasa kita gunakan perintah mvn package untuk membuild code project tadi.

Lalu kita akan punya file App.java dalam direktory src/main/org/labseni/app/. Untuk itu kita akan masukkan kode berikut untuk membuat plotting berjalan

```java
package org.labseni.app;

import java.awt.BorderLayout;
import java.awt.Component;
import java.awt.event.WindowAdapter;
import java.awt.event.WindowEvent;
import java.io.IOException;
import java.util.ArrayList;
import java.util.List;

import javax.swing.BorderFactory;
import javax.swing.JFrame;
import javax.swing.JPanel;
import javax.swing.border.Border;

import net.miginfocom.swing.MigLayout;

import org.jzy3d.chart.Chart;
import org.jzy3d.chart2d.Chart2d;
import org.jzy3d.colors.Color;
import org.jzy3d.plot2d.primitives.Serie2d;
import org.jzy3d.plot3d.primitives.ConcurrentLineStrip;
import org.jzy3d.plot3d.primitives.axes.layout.IAxeLayout;
import org.jzy3d.plot3d.primitives.axes.layout.providers.PitchTickProvider;
import org.jzy3d.plot3d.primitives.axes.layout.renderers.PitchTickRenderer;
import org.jzy3d.ui.LookAndFeel;

/**
 * Showing a pair of 2d charts to represent pitch and amplitude variation of an
 * audio signal.
 * 
 * Noticed problems on chart resize. Suspect "wrong stuffs" around miglayout or jogl.
 * 
 * FIXME : use ChartGroup to build interface. Miglayout/JOGL interaction causes problem when downsizing windows
 * 
 * @author Martin Pernollet
 */
public class App {
    public static float duration = 60f;
    /** milisecond distance between two generated samples*/
    public static int interval = 50;
    public static int maxfreq = 880;
    public static int nOctave = 5;

    public static void main(String[] args) throws Exception {
        PitchAmpliControlCharts log = new PitchAmpliControlCharts(duration, maxfreq, nOctave);
        new TimeChartWindow(log.getCharts());

        generateSamplesInTime(log);
        // generateSamples(log, 500000);
    }

    public static void generateSamples(PitchAmpliControlCharts log, int n) throws InterruptedException {
        System.out.println("will generate " + n + " samples");

        for (int i = 0; i < n; i++) {
            // Random audio info
            double pitch = Math.random() * maxfreq;
            double ampli = Math.random();

            // Add to time series
            log.seriePitch.add(time(n, i), pitch);
            log.serieAmpli.add(time(n, i), ampli);
        }
    }

    public static double time(int n, int i) {
        return ((double) i / n) * duration;
    }

    public static void generateSamplesInTime(PitchAmpliControlCharts log) throws InterruptedException {
        System.out.println("will generate approx. " + duration * 1000 / interval + " samples");

        start();

        while (elapsed() < duration) {
            // Random audio info
            double pitch = Math.random() * maxfreq;
            double ampli = Math.random();

            // Add to time series
            log.seriePitch.add(elapsed(), pitch);
            log.serieAmpli.add(elapsed(), ampli);

            // Wait a bit
            Thread.sleep(interval);
        }
    }

    /** Hold 2 charts, 2 time series, and 2 drawable lines */
    public static class PitchAmpliControlCharts {
        public Chart2d pitchChart;
        public Chart2d ampliChart;
        public Serie2d seriePitch;
        public Serie2d serieAmpli;
        public ConcurrentLineStrip pitchLineStrip;
        public ConcurrentLineStrip amplitudeLineStrip;

        public PitchAmpliControlCharts(float timeMax, int freqMax, int nOctave) {
            pitchChart = new Chart2d();
            pitchChart.asTimeChart(timeMax, 0, freqMax, "Time", "Frequency");

            IAxeLayout axe = pitchChart.getAxeLayout();
            axe.setYTickProvider(new PitchTickProvider(nOctave));
            axe.setYTickRenderer(new PitchTickRenderer());

            seriePitch = pitchChart.getSerie("frequency", Serie2d.Type.LINE);
            seriePitch.setColor(Color.BLUE);
            pitchLineStrip = (ConcurrentLineStrip) seriePitch.getDrawable();

            ampliChart = new Chart2d();
            ampliChart.asTimeChart(timeMax, 0, 1.1f, "Time", "Amplitude");
            serieAmpli = ampliChart.getSerie("amplitude", Serie2d.Type.LINE);
            serieAmpli.setColor(Color.RED);
            amplitudeLineStrip = (ConcurrentLineStrip) serieAmpli.getDrawable();
        }

        public List<Chart> getCharts() {
            List<Chart> charts = new ArrayList<Chart>();
            charts.add(pitchChart);
            charts.add(ampliChart);
            return charts;
        }
    }

    /** A frame to show a list of charts */
    public static class TimeChartWindow extends JFrame {
        private static final long serialVersionUID = 7519209038396190502L;

        public TimeChartWindow(List<Chart> charts) throws IOException {
            LookAndFeel.apply();
            String lines = "[300px]";
            String columns = "[500px,grow]";
            setLayout(new MigLayout("", columns, lines));
            int k = 0;
            for (Chart c : charts) {
                addChart(c, k++);
            }
            windowExitListener();
            this.pack();
            show();
            setVisible(true);
        }

        public void addChart(Chart chart, int id) {
            Component canvas = (java.awt.Component) chart.getCanvas();

            JPanel chartPanel = new JPanel(new BorderLayout());
            /*chartPanel.setMaximumSize(null);
            chartPanel.setMinimumSize(null);
            canvas.setMinimumSize(null);
            canvas.setMaximumSize(null);*/
            
            Border b = BorderFactory.createLineBorder(java.awt.Color.black);
            chartPanel.setBorder(b);
            chartPanel.add(canvas, BorderLayout.CENTER);
            add(chartPanel, "cell 0 " + id + ", grow");
        }

        public void windowExitListener() {
            addWindowListener(new WindowAdapter() {
                @Override
                public void windowClosing(WindowEvent e) {
                    TimeChartWindow.this.dispose();
                    System.exit(0);
                }
            });
        }
    }

    /** Simple timer */
    protected static long start;

    public static void start() {
        start = System.nanoTime();
    }

    public static double elapsed() {
        return (System.nanoTime() - start) / 1000000000.0;
    }
}
```

dan jangan lupa bagian pom.xml diedit seperti berikut 

```xml
<project xmlns="http://maven.apache.org/POM/4.0.0" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
  <modelVersion>4.0.0</modelVersion>
  <groupId>org.labseni.app</groupId>
  <artifactId>PlotJavaBaru</artifactId>
  <packaging>jar</packaging>
  <version>1.0-SNAPSHOT</version>
  <name>JavPlotMan</name>
  <url>http://maven.apache.org</url>
  <repositories>
    <repository>
      <id>jzy3d-snapshots</id>
      <name>Jzy3d Snapshots</name>
      <url>http://maven.jzy3d.org/snapshots</url>
    </repository>
 
    <repository>
       <id>jzy3d-releases</id>
       <name>Jzy3d Releases</name>
       <url>http://maven.jzy3d.org/releases</url>
    </repository>
  </repositories>

  <dependencies>
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>3.8.1</version>
      <scope>test</scope>
    </dependency>

    <dependency>
    <groupId>org.jzy3d</groupId>
      <artifactId>jzy3d-api</artifactId>
      <version>1.0.0</version>
    </dependency>

   <dependency>
     <groupId>org.jzy3d</groupId>
     <artifactId>jzy3d-api</artifactId>
     <version>1.0.1-SNAPSHOT</version>
   </dependency>
  

  </dependencies>
</project>
```
lihat yang terpenting bagian dependency sama repositorynya, ada nambahin beberapa. Lalu run dengan perintah

```bash
mvn package
```

kemudian 
```bash
mvn exec:java -Dexec.mainClass=org.labseni.app.App
```
lalu akan muncul frame seperti dibawah ini.

![Frame](https://raw.githubusercontent.com/faoziaziz/JavPlotMan/master/runingsignal.png)

# Referensi
1. [Maven in 5 Minutes](https://maven.apache.org/guides/getting-started/maven-in-five-minutes.html) 
2. [Repo JavPlotMan](https://github.com/faoziaziz/JavPlotMan)

