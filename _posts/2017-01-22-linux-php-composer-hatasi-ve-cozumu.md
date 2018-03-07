---
id: 3263
title: Linux Mint PHP Composer Hatası ve Çözümü
date: 2017-01-22T23:33:29+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=3263
permalink: /linux-php-composer-hatasi-ve-cozumu
categories:
  - Linux
tags:
  - Laravel
  - Linux
  - Linux Mint 18 Composer
  - Linux Mint 18 Laravel 5
---
Esenlikler, **Linux** üzerinde **Laravel** kurmak isterken yaşadığım bir soruna çözüm olmak için bu satırlara emek vermekteyim.

## Olası hata çıktıları:

<pre class="lang:default decode:true ">You can also run `php --ini` inside terminal to see which files are used by PHP in CLI mode.</pre>

Terminalde bu şekilde bir çıktı aldığınızda aşağıdaki paketleri kurmalısınız. Kullandığınız **PHP** sürümüne ve ismine göre paket isminde değişiklik gösterebilir.

## Çözüm:

<pre class="lang:default decode:true">sudo apt-get update && sudo apt-get upgrade && sudo apt-get autoclean && sudo apt-get autoremove
sudo apt-get install php5.6-gd
sudo apt-get install php5.6-intl
sudo apt-get install php5.6-xsl
sudo apt-get update</pre>

Yukarıda yer alan komutları sırası ile terminal ekranınızda çalıştırın. Sonrasında **composer** işleminiz başarı ile çalışacaktır.