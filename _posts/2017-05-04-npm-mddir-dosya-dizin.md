---
id: 3605
title: Npm Mddir Paketi ile Dosya Dizin Diyagramı
date: 2017-05-04T18:52:44+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3605
permalink: /npm-mddir-dosya-dizin
categories:
  - JavaScript
tags:
  - ASCII Dosya Dizini
  - Node.Js
  - Npm Mddir
---
Bilişim alanında kullanılan paket, eklenti ve uygulama dökümanlarında sıkça kullanılan dizin diyagramını Node Package Modules&#8217;in mddir paketi ile yapabiliriz. Laravel derslerine başladığımda ihtiyacım oldu.

## Kullanım

<pre class="lang:default decode:true">sudo npm install mddir -g
cd node_modules/mddir/src/
node mddir "../../../public/"
</pre>

## Çıktısı

Src dizinimizde directoryList.md dosyamızı açalım. Bulunduğu dizinde yazma izninin olduğuna emin olalım.

<pre class="lang:default decode:true ">|-- blog
    |-- .htaccess
    |-- favicon.ico
    |-- index.php
    |-- robots.txt
    |-- web.config
    |-- css
    |   |-- app.css
    |-- js
        |-- app.js
</pre>

&nbsp;