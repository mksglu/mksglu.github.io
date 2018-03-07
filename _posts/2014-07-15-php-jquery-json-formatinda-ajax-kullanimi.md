---
id: 2578
title: PHP JQuery JSON Formatında Ajax Kullanımı
date: 2014-07-15T14:14:31+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=2578
permalink: /php-jquery-json-formatinda-ajax-kullanimi
categories:
  - PHP
tags:
  - Jquery
  - Jquery Ajax Data
  - Jquery Ajax Serialize
  - Jquery Json
  - PHP
  - PHP Json
---
Merhabalar,

PHP JQuery Ajax methodunu JSON formatında kullanalım.

## **Json Nedir ?**

jSON, object (nesne) ve array (dizi) olmak üzere 2 temel yapı içerir. Bu temel yapılar evrensel yapılardır ve tüm modern programlama dillerinde mevcuttur.

## **Kodlarımız &#8211; JQuery**

<pre class="lang:js decode:true">$(function(){
			$('input[type=submit]').click(function(){ // Type Submit Olana Tıklanıldığında.
				/* Input Name Degerlerine Göre Val() Methodunu Kullanarak Data Elde Ettik. */
				var x = $('input[name=x]').val();
				var q = $('input[name=q]').val();
				var a = $('input[name=a]').val();
				/* Verilerimizi 3 Farklı Sekilde Elde Edebiliriz. */
				var data = {"q" : q, "x" : x, "a" : a};
				var data =  "x=" + x + "&q=" + q + "&a=" + a;
				var data = $('form').serialize() + "&x=" + x + "&a=" + a;
				/* Ajax Baslasin */
				$.ajax({
					type:'POST', 						// - POST veya GET
					data:data,							// - Yukarıda data değişkenini tanımladık.
					dataType:'json', 					// - JSON Formatında Gönderilmesini Sağladık.
					url:'islem.php', 					// - Data Bilgisinin Gönderileceği Dosya Adresi.
					success:function(gelen){ 		 	// - Success, complete ve error Fonksiyonları vardır.
						$('.sonuc').html(gelen.veri);	// - Gelen Verimizi Sonuc Divinin İçerisine Yazdırdık.
					}
				});
				return false;
			});
		});</pre>

## **Kodlarımız &#8211; HTML**

<pre class="lang:xhtml decode:true">&lt;form method="POST"&gt;
		&lt;input type="text" name="q" id=""&gt;
		&lt;input type="submit" value="Ajax"&gt;
	&lt;/form&gt;
		&lt;input type="text" name="x" id=""&gt;
		&lt;input type="text" name="a" id=""&gt;
	&lt;div class="sonuc"&gt;&lt;/div&gt;</pre>

## **Kodlarımız &#8211; PHP**

<pre class="lang:php decode:true ">/*
		Mert Köseoğlu
		www.mkoseoglu.com
	*/

	$a = $_POST['a'];
	$q = $_POST['q'];
	$x = $_POST['x'];

	if($a == '' || $q== '' || $x=='') {
		$array['veri'] = "Hata Olustu.";
	}else{
		$array["veri"] = $_POST['q'].'&lt;br&gt;'.$_POST['x'].'&lt;br&gt;'.$_POST['a'];
	}

	
	echo json_encode($array);
</pre>