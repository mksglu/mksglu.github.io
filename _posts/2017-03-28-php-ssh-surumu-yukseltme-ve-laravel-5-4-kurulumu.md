---
id: 3401
title: PHP SSH Sürümü Yükseltme ve Laravel 5.4 Kurulumu
date: 2017-03-28T03:12:03+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=3401
permalink: /php-ssh-surumu-yukseltme-ve-laravel-5-4-kurulumu
categories:
  - Laravel 5.4
  - Linux
  - PHP
---
Merhabalar, bugün **SSH** ile sunucuma **Laravel 5.4** kurmak isterken **Plesk** panelde **7.1** olan **PHP** sürümüm **SSH**&#8216;de **5.4** olarak gözükmekteydi. Bu yüzden kurmakta sorun yaşadım.

## SSH PHP Sürümünü Yükseltme

**SSH**&#8216;de aşağıdaki komutla çözüme geçelim.

<pre class="lang:php decode:true">which php</pre>

Eğer ki çıktımız **/usr/bin/php** ise devam edelim.

<pre class="lang:default decode:true ">sudo mv /usr/bin/php /usr/bin/php54
</pre>

<pre class="lang:default decode:true ">sudo rm -rf /usr/bin/php</pre>

<pre class="lang:default decode:true ">ln -s /opt/plesk/php/7.1/bin/php /usr/bin/php
</pre>

Ben kendi Plesk panelimden 7.1&#8217;in yolunu kısayol oluşturdum.

## Laravel 5.4 Kurulumu

Kurulumu gerçekleştirelim.

<pre class="lang:default decode:true ">composer create-project --prefer-dist laravel/laravel laravel
</pre>

Kurulumdan sonra gerekli izinleri verelim.

<pre class="lang:default decode:true ">chmod 755 -R laravel
chmod -R o+w storage</pre>

Şimdi dizin işlemlerine geçelim.

**Public klasörü**nde bulunan **server.php **dosyasının ismini **index.php **olarak değiştirelim ve yine **Public klasörü**nde bulunan **.htaccess** dosyası ile birlikte ana dizine taşıyalım.

Şu an hatasız Laravel ekranını görmeniz gerekmekte.

## Artisan Kullanımı

Öncelikle çalıştıralım.

<pre class="lang:default decode:true ">php artisan serve --host=&lt;HOST IP BURAYA&gt;--port=8125
</pre>

Şu an 8125 portunda çalışabilirsiniz.

<https://laravel.com/docs/5.4/artisan>

Murat Bastas&#8217;a teşekkürler.