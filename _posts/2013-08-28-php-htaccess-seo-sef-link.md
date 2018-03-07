---
id: 1832
title: PHP Seo Dostu Link Yapıları
date: 2013-08-28T12:02:44+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=1832
permalink: /php-htaccess-seo-sef-link
views:
  - "232"
categories:
  - PHP
tags:
  - PHP
  - PHP Dersleri
  - PHP Sef Link
  - PHP Sef Link Fonksiyonu İle Seo Uyumlu Link Yapısı
---
Merhabalar, PHP Htaccess ile SEO uyumlu link yapıları elde edeceğiz.

<pre class="lang:php decode:true">require_once('config.php');

$baslik = mysql_query("SELECT * FROM tasarim ORDER BY id DESC");
while($gel=mysql_fetch_assoc($baslik)){
    echo '&lt;a href="detay/'.$gel['sef'].'.html"&gt;',$gel['Baslik'],"&lt;br/&gt;",'&lt;/a&gt;';
}</pre>

<pre class="lang:php decode:true">require_once('config.php');
$sef = mysql_escape_string($_GET['gel']);
$yazi = mysql_query("SELECT * FROM tasarim WHERE sef='$sef'");
$cek = mysql_fetch_assoc($yazi);
    switch($cek){
        case null;
            echo "&lt;center&gt;&lt;h1 style='font-size:500px'&gt;404&lt;/h1&gt;&lt;/center&gt;";
            break;
        default:
        echo $cek['icerik'];
}</pre>

<pre class="lang:php decode:true">mysql_select_db("calismalarim",mysql_connect("localhost","root"));</pre>

<pre class="lang:xhtml decode:true">Options +FollowSymLinks
RewriteEngine On
RewriteRule ^detay/([a-zA-Z0-9_-]+).html$ oku.php?gel=$1 [L]</pre>

<pre class="lang:php decode:true">require_once('config.php');
function sef_link($bas)
{	 
    $bas = str_replace(array("&quot;","&#39;"), NULL, $bas);
    $bul = array('Ç', 'Ş', 'Ğ', 'Ü', 'İ', 'Ö', 'ç', 'ş', 'ğ', 'ü', 'ö', 'ı', '-');
    $yap = array('c', 's', 'g', 'u', 'i', 'o', 'c', 's', 'g', 'u', 'o', 'i', ' ');
    $perma = strtolower(str_replace($bul, $yap, $bas));
    $perma = preg_replace("@[^A-Za-z0-9\-_]@i", ' ', $perma);
    $perma = trim(preg_replace('/\s+/',' ', $perma));
    $perma = str_replace(' ', '-', $perma);
    return $perma;
}
$baslik = "Başlık";
$icerik= "Başlık ile ilgili bir metin.";
$sef = sef_link($baslik);
$kaydet=mysql_query("INSERT INTO tasarim (Baslik,icerik,sef) VALUES ('".$baslik."','".$icerik."','".$sef."')");</pre>

<pre class="lang:mysql decode:true">CREATE TABLE IF NOT EXISTS `tasarim` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `Baslik` varchar(250) NOT NULL,
  `icerik` text CHARACTER SET utf32 NOT NULL,
  `sef` varchar(250) NOT NULL,
  PRIMARY KEY (`id`),
  KEY `Baslik` (`Baslik`),
  KEY `Baslik_2` (`Baslik`),
  KEY `Baslik_3` (`Baslik`)
) ENGINE=MyISAM  DEFAULT CHARSET=utf8 AUTO_INCREMENT=7 ;</pre>

<pre class="lang:xhtml decode:true ">/detay/www-mkoseoglu-com-php-htaccess-ile-sef-link-olusturma</pre>