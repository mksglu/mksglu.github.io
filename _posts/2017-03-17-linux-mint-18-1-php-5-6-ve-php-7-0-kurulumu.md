---
id: 3342
title: Linux Mint 18.1 PHP 5.6 ve PHP 7.0 Kurulumu
date: 2017-03-17T02:55:23+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=3342
permalink: /linux-mint-18-1-php-5-6-ve-php-7-0-kurulumu
categories:
  - Linux
  - PHP
tags:
  - Linux
  - Linux PHP 5 Kurulumu
  - Linux PHP 7 Kurulumu
  - PHP
  - Ubuntu Linux Laravel
  - Ubuntu PHP 5 Kurulumu
  - Ubuntu PHP 7 Kurulumu
---
Merhabalar, **[Linux](http://www.mkoseoglu.com/linux/) Mint 18.1 Serena** üzerinde **PHP 5.6** ve **PHP 7.0** kurulumu birlikte inceleyelim. Öncelikle **Ubuntu 16**&#8216;dan sonra resmi depolarından PHP 5.x sürümünü kaldırdı ve yerine güncel olan PHP 7.0 kullandı. Fakat biz geliştiriciler için sürümler arasında sörf yapmak son derece mühim. Üzerinde çalıştığınız projenin sizden ne istediğini asla bilemezsiniz. Bu yüzden [Ondrej Sury](https://launchpad.net/~ondrej) isimli bir arkadaşımız kişisel paket arşivine PHP 5.x versiyonunu eklemiş. Bizler de bunu kullanacağız.

## PHP 5 Paketi

<pre class="lang:default decode:true">sudo apt-add-repository -y ppa:ondrej/php
sudo apt-get -y update</pre>

Paketimiz hazır.

## PHP 5.6 ve PHP 7.0 Kurulum

Şimdi her iki sürümü de **Apache2**, **MySQL** ve [**Laravel PHP Framework**](http://www.mkoseoglu.com/laravel-5-4/) destekli kurmaya hazırız.

<pre class="lang:default decode:true">sudo apt-get -y install php7.0 php5.6-mysql php5.6-cli php5.6-curl php5.6-json php5.6-sqlite3 php5.6-mcrypt php5.6-curl php-xdebug php5.6-mbstring libapache2-mod-php5.6 libapache2-mod-php7.0 mysql-server-5.7 apache2</pre>

## PHP 5.6 Kullanalım

<pre class="lang:default decode:true ">sudo a2dismod php7.0 ; sudo a2enmod php5.6 ; sudo service apache2 restart ; echo 1 | sudo update-alternatives --config php</pre>

## PHP 7.0 Kullanalım

<pre class="lang:default decode:true ">sudo a2dismod php5.6 ; sudo a2enmod php7.0 ; sudo service apache2 restart ; echo 2 | sudo update-alternatives --config php</pre>

## Son Olarak

<pre class="lang:default decode:true ">sudo a2dismod mpm_event
sudo a2enmod mpm_prefork
sudo service apache2 restart</pre>

* * *

**Ubuntu** ve **Debian** temel alınarak geliştirilen **Linux Mint 18.1 Serena** sürümünde başarıyla [PHP 5.6 ve PHP 7.0](http://www.mkoseoglu.com/php-mysql/) kurulumunu gerçekleştirdik.

Bol keyifli kodlar.