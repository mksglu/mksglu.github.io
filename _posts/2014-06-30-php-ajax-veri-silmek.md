---
id: 2557
title: JQuery Ajax ile Veri Silmek
date: 2014-06-30T00:33:13+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=2557
permalink: /php-ajax-veri-silmek
categories:
  - jQuery
tags:
  - PHP
  - PHP Ajax İle Veri Silmek
  - Sayfa Yenilenmeden Veri Silmek Ajax
---
Merhabalar, PHP ve JQuery kullanarak veritabanından anlık veri silme işlemini gerçekleştireceğiz.

<pre class="lang:mysql decode:true">CREATE TABLE IF NOT EXISTS `ajaxsil` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `mesaj` text NOT NULL,
  PRIMARY KEY (`id`)
) ENGINE=MyISAM  DEFAULT CHARSET=utf8 AUTO_INCREMENT=7 ;</pre>

<pre class="lang:php decode:true">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
    &lt;script src="http://code.jquery.com/jquery-1.11.1.js"&gt;&lt;/script&gt;
    &lt;script src="ajax.js"&gt;&lt;/script&gt;
&lt;/head&gt;
&lt;body&gt;
    &lt;?php 
        $sql = mysql_query("SELECT * FROM ajaxsil ORDER BY id DESC") or die(mysql_error());
        while($a   = mysql_fetch_assoc($sql)) { 
        $mesaj = $a['mesaj']; 
        $id    = $a['id'];
    ?&gt;
    &lt;div class="silinen"&gt;
        &lt;p class="metin"&gt;&lt;?php echo $mesaj; ?&gt;&lt;/p&gt;
        &lt;a href="#" id="&lt;?php echo $id ?&gt;" class="silbeni"&gt;x&lt;/a&gt;
    &lt;/div&gt;
    &lt;?php } ?&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>

<pre class="lang:php decode:true">mysql_select_db("ajax",mysql_connect("localhost","root","")) or die ('Veritabanı Bağlanamadık !');
mysql_query("SET NAMES utf8");
mysql_query("SET CHARACTER SET utf8");
mysql_query("SET COLLATION_CONNECTION = 'utf8_general_ci'");</pre>

<pre class="lang:js decode:true">$(document)
    .ready(function () {
        $('.silbeni')
            .click(function () {

                var degisken = $(this);
                var silbeni = degisken.attr('id');
                var veri = 'id=' + silbeni;
                if (confirm("Silmek İstediğinizden Emin misiniz ?")) {
                    $.ajax({type: "GET", url: "islem.php", data: veri, success: function () {}});
                }
                $(this)
                    .parents(".silinen")
                    .animate({
                        backgroundColor: "#fbc7c7"
                    }, "fast")
                    .animate({
                        opacity: "hide"
                    }, "slow");
                return false;
            });
    });</pre>

<pre class="lang:php decode:true">&lt;?php 

require_once('db.php'); 
$id = $_GET['id'];
if($id) {
$sql = mysql_query("DELETE FROM ajaxsil WHERE id = '$id' ") or die(mysql_error());
}

?&gt;</pre>

&nbsp;