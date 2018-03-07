---
id: 1427
title: PHP Random Kullanımı ve Örnekleri
date: 2013-06-27T09:09:32+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=1427
permalink: /php-rastgele-random
views:
  - "56"
categories:
  - PHP
tags:
  - PHP
  - PHP Degiskenler
  - PHP Dersleri
  - PHP Rand Fonksiyonu Kullanımı
  - PHP Random Örnekleri
  - Wordpress Rastgele Yazılar
---
Blogumun headeri için **her sayfa yenilenmesinde** değişen **rastgele sözleri** göstermek için kod aramaktaydım. **PHP de rand** fonksiyonunu araştırırken ve tabii biraz da yardım alarak internette kolay kolay bulamadıgım **PHP rastgele** sözler kodunun **4 farklı çeşidini yazdım.**

İstediğinizi kullanabilirsiniz. Umarım birilerinin işine yarar.

<pre class="lang:php decode:true">$yazi=array("söz1","söz2","söz3","söz4","söz5");
$karissin =mt_rand(0,4); // mt_rand'ın rand'a göre daha performanslı oldugunu duymustum.
echo "$yazi[$karissin]";</pre>

Burada dikkat edilmesi gereken en önemli nokta **PHP&#8217;de diziler** her zaman **** dan başlar. Eğer ben bunu **mt_rand(0,5)** yapsaydım **6** tane söz arıyacaktı ve bir noktadan sonra hata vermesine neden olacaktı. O yüzden **mt_rand(0,4)** olarak başlatıyoruz.

<pre class="lang:php decode:true">$yazi=array("söz1","söz2","söz3","söz4","söz5");
$kactane = count($yazi);
echo $yazi[rand(0,$kactane-1)];</pre>

PHP de **count array&#8217;**ı daha çok nesneleri saydırmak için kullanırız. Ama burada saydığı nesneleri **rand fonksiyonu** rastgele sözler kodumuzu tamamladı.

&nbsp;

<pre class="lang:php decode:true">$soz[1] = "soz1"; // Söz 1
$soz[2] = "soz2"; // Söz 2
$soz[3] = "soz3"; // Söz 3
$soz[4] = "soz4"; // Söz 4
$soz[5] = "soz5"; // Söz 5
$karistir = rand(1,5); // Sözleri karıştıralım.
echo "$soz[$karistir]"; // Ekrana basalım.</pre>

<pre class="lang:php decode:true">$sozler = array("1","2","3","4");	
shuffle($sozler); // rastgele
echo $sozler[0];</pre>