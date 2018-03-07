---
id: 1716
title: CkEditor ile JQuery Ajax Kullanımı
date: 2013-07-20T11:46:40+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=1716
permalink: /ckeditor-ajax-post-php
views:
  - "127"
categories:
  - jQuery
tags:
  - Ckeditor Entegresi
  - Ckeditor Jquery Ajax Post İle Post Etme
---
Merhaba, bir metin editörü olan CkEditor&#8217;de yazdığımız girdileri JQuery&#8217;in Ajax kütüphanesi ile veritabanına kaydedeceğiz.

Buradan (<https://ckeditor.com/ckeditor-4/download>) CkEditor&#8217;ü indirelim ve HTML şablonumuzda HEAD tagları arasında tanımlayalım.

CkEditor&#8217;ü görüntülememi sağlayan bir HTML betiği içerisinde form oluşturuyorum. Metin alanı için Textarea etiketini kullanıyorum.

<pre class="lang:xhtml decode:true">&lt;form id="kaydet" name="kaydet" method="post"&gt;
 &lt;textarea name="ornek_1" id="ornek_1"&gt;&lt;/textarea&gt;&lt;br /&gt;
 &lt;input type="submit" id="tik" /&gt;
&lt;/form&gt;</pre>

Oluşturduğumuz formun name değerini kaydet olarak tanımlıyorum. HTML şablonumuzda BODY tagları arasında CkEditör&#8217;ü script tagları içerisinde çağırıyorum.

<pre class="lang:js decode:true">&lt;script type="text/javascript"&gt;
 CKEDITOR.replace( 'ornek_1' );
&lt;/script&gt;</pre>

Burada yer alan ornek_1 kullandığımız Textarea etiketinin name değeridir. JQuery Ajax kodlarımı yazmaya başlayabilirim.

<pre class="lang:js decode:true">$(document)
    .ready(function () {
        $('#tik')
            .click(function () {
                for (var kaydet in CKEDITOR.instances) 
                    CKEDITOR.instances[kaydet].updateElement();
                $.ajax({
                    type: 'POST',
                    url: 'kaydet.php',
                    cache: false,
                    data: $('#kaydet').serialize(),
                    success: function (hesapCevap) {
                        $('#sonuc').html(hesapCevap);
                    }
                });
                return false;
            });
    });</pre>

Burada yer alan <span class="lang:default highlight:0 decode:true crayon-inline ">for (var kaydet in CKEDITOR.instances)</span> satırındaki kaydet oluşturduğumuz formun name değeridir.

PHP üzerinde girdilerimi veritabanına kaydedebilirim artık.

<pre class="lang:php decode:true ">mysql_select_db("dersler",mysql_connect("localhost","root",""));
mysql_query("SET CHARACTER SET utf8");
mysql_query("SET COLLATION_CONNECTION = 'utf8_general_ci'");
mysql_query("INSERT INTO ck (dene) VALUES ('".$_POST['ornek_1']."')");</pre>