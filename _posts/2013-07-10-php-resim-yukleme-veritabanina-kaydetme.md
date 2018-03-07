---
id: 1568
title: PHP ile Görsel Yükleme
date: 2013-07-10T08:35:15+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=1568
permalink: /php-resim-yukleme-veritabanina-kaydetme
views:
  - "339"
categories:
  - PHP
tags:
  - PHP
  - PHP Dersleri
  - PHP Dosyayı Veritabanına Ekleme
---
Merhabalar, PHP ile görsellerimizi belirtilen dizine yüklerken aynı zamanda adreslerini veritabanına kaydedelim.

<pre class="lang:php decode:true">&lt;!DOCTYPE HTML&gt;
&lt;html lang="en-US"&gt;
&lt;body&gt;
	&lt;form enctype="multipart/form-data" action="yolla.php" method="POST"&gt;
        &lt;input type="file" name="resim" id="resim"&gt;
        &lt;input type="submit" name="gönder" value="gönder"&gt;
    &lt;/form&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>

<pre class="lang:php decode:true  ">&lt;?php

# Mert Köseoğlu
# www.mkoseoglu.com
# 10.07.2013

## Uzantı Kontrollerim
    $uzanti=    array('image/jpeg','image/jpg','image/png','image/x-png','image/gif');
## Aynı Dizinde Bulunan Resimler Klasörüne Kaydet
    $dizin=     "resimler";
     if(in_array(strtolower($_FILES['resim']['type']),$uzanti)){ 
     move_uploaded_file($_FILES['resim']['tmp_name'],"./$dizin/{$_FILES['resim']['name']}");
## Veritabanına Bağlanalım ##
     $baglan=   mysql_connect("localhost","root","") or die ('Sunucuya Bağlanamadım.');
     $asd=      mysql_select_db("mertk",$baglan) or die ('Veritabanı Bağlanamadık !');
## Dosya İsmimizi Veritabanına Yazdıralım. ##
    mysql_query("SET NAMES utf8");
    mysql_query("SET CHARACTER SET utf8");
    mysql_query("SET COLLATION_CONNECTION = 'utf8_general_ci'");
## Türkçe Karakter Hatası
    $db=       $_FILES['resim']['name'];    
## Resmimizin Adını Alalım
    $ekle=     mysql_query("INSERT INTO blog (resim) VALUES ('".$db."')") or die (mysql_Error());
# Blog Tablosu -&gt; Resim Sütununa Ekleyelim.
    echo "Başarılı !";
    }else{
     echo "Başarısız !";
    }

?&gt;</pre>