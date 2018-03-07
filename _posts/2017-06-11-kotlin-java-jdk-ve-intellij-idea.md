---
id: 3662
title: 'Kotlin: JAVA JDK ve IntelliJ IDEA Yükleyelim'
date: 2017-06-11T15:04:13+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3662
permalink: /kotlin-java-jdk-ve-intellij-idea
categories:
  - Kotlin
tags:
  - Kotlin Dersleri
  - Kotlin IntelliJ IDEA Yükleme
  - Kotlin JAVA JDK Yükleme
---
[Kotlin](https://www.mkoseoglu.com/etiket/kotlin-dersleri/) için ihtiyacımız olan yazılımları yükleyelim. **JAVA JDK** ve **Intellij IDEA** kurulumlarını gerçekleştireceğiz.

## Java JDK

Google&#8217;da JAVA JDK araması yaptığımda karşıma çıkan [ilk sonuc](http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html)a tıklıyorum. Buradan kendi işletim sisteminizi göz önünde bulundurarak <span class="lang:default highlight:0 decode:true crayon-inline ">Java SE Development Kit</span> &#8216;i indirelim.

Linux&#8217;ta indirilen klasörde uçbirim açalım.

<pre class="lang:default decode:true ">sudo mv jdk1.8.0_131 /usr/lib/jvm/oracle_jdk8
</pre>

Eğer ki <span class="lang:default highlight:0 decode:true crayon-inline ">lib</span>  dizini altında <span class="lang:default highlight:0 decode:true crayon-inline ">jvm</span>  dizini yok ise mkdir komutu ile oluşturabilirsiniz.

<pre class="lang:default decode:true ">cd /usr/lib && sudo mkdir jvm</pre>

JDK dizinimizin yollarını tanımlayalım. Uçbirimde <span class="lang:default highlight:0 decode:true crayon-inline ">/etc/profile</span> dosyasını metin editörü ile açalım ve aşağıdaki komutları dosyanın en sonuna ekleyelim.

<pre class="lang:default decode:true ">export J2SDKDIR=/usr/lib/jvm/oracle_jdk8
export J2REDIR=/usr/lib/jvm/oracle_jdk8/jre
export PATH=$PATH:/usr/lib/jvm/oracle_jdk8/bin:/usr/lib/jvm/oracle_jdk8/db/bin:/usr/lib/jvm/oracle_jdk8/jre/bin
export JAVA_HOME=/usr/lib/jvm/oracle_jdk8
export DERBY_HOME=/usr/lib/jvm/oracle_jdk8/db</pre>

Cihazımızı yeniden başlatalım. Uçbirimde java -version komutunu girelim. Çıktımız aşağıdakine benzer olmalıdır.

<pre class="lang:default decode:true ">java version "1.8.0_131"
Java(TM) SE Runtime Environment (build 1.8.0_131-b11)
Java HotSpot(TM) 64-Bit Server VM (build 25.131-b11, mixed mode)
</pre>

<h2 class="download-page__title" data-product-name="IntelliJ IDEA">
  IntelliJ IDEA
</h2>

Kotlin için kullanacağımız IntelliJ IDEA yazılımını kendi sitesinden [indirelim](https://www.jetbrains.com/idea/download). **Community **sürümü ücretsiz olarak yayınlanmakta.

Linux için, <span class="lang:default highlight:0 decode:true crayon-inline ">bin</span>  dizini içerisinde <span class="lang:default highlight:0 decode:true crayon-inline ">idea.sh</span>  dosyasını uçbirimde çalıştırmak yeterlidir.

Kotlin için ihtiyacımız olan her şeye sahibiz.

&nbsp;