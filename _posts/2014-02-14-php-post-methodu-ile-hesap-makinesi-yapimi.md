---
id: 2205
title: PHP POST Methodu İle Hesap Makinesi Yapımı
date: 2014-02-14T04:06:55+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=2205
permalink: /php-post-methodu-ile-hesap-makinesi-yapimi
categories:
  - PHP
tags:
  - PHP
  - PHP Dersleri
  - PHP eval() Fonksiyonu
  - PHP Hesap Makinesi Yapımı
---
Merhabalar, **geometri** ödevimi **&#8220;programlama ile hesap makinesi&#8221;** olarak seçtim. İnternette örnekleri incelediğim de istediğim tarzda yapılmışını bulamadım. Tek bir input içine yazılan veriler ile işlem yapmak istedim. Sonuçta PHP nin zaten **matematik** işlemleri için bir esnekliği var bir de neden biz çarpma, toplama, çıkarma.. şeklinde seçip işlem yaptıralım ?

Bu yüzden tek bir **input** a değerleri girdim. Fakat PHP ifadeyi **string** olarak aldıladı. Bunu **eval()**; fonksiyonu ile çözdüm. Ben bunu **Ajax** kullanarak tamamlayacağım. Siz istediğiniz gibi kullanırsınız.

Çarpma : **x**

Toplama : **+**

Çıkarma : **&#8211;**

Bölme: **/**

Demo : <a href="http://www.mkoseoglu.com/hesap" target="_blank">www.mkoseoglu.com/hesap</a>

<pre class="lang:php decode:true ">error_reporting(0);

		// Hatalar Gizlensin.

	$x = $_POST['islem'];

		// name degeri islem olan inputumuzun değerini POST methodu ile alıyoruz.

		// Verimizi X adında bir değişkene atıyoruz.

function hesapla($degerler)
{
	$degerler = preg_replace("/[^0-9+\-.x\/()%]/","",$degerler);
	$degerler = preg_replace("/([+-])([0-9]{1})(%)/","*(1\$1.0\$2)",$degerler);
	$degerler = preg_replace("/([+-])([0-9]+)(%)/","*(1\$1.\$2)",$degerler);
	$degerler = preg_replace("/([0-9]+)(%)/",".\$1",$degerler);
 $degerler = preg_replace("/x/","*",$degerler);
		// preg_replace() fonksiyonu ile sadece kullanacağımız karakterlere izin verdik.

	if ($degerler == "" OR $degerler == NULL)
	{
		$returnHata = "hata";
		return $returnHata;

		// Hata izin verdiğimiz karakterlerin dışında karakter olursa boş olarak gözükecek. 
		// Bu durumda degerler boş ise hata mesajımızı yazdırıyoruz.		

	}else {
		eval("\$return=" . $degerler . ";" );
	}

		// eval(); fonksiyonu ile string ifademizin PHP kodu olarak yorumlanmasını sağladık.

	if(strlen($return) &gt;= 4) {
		$ayirma = number_format($return, 0, '', '.');
			return $ayirma;
	}else {
			return var_dump($return);

	}

		// Girilen karakter sayısı 4 den büyükse number_format(); fonksiyonu ile ayırıp, değeri döndürüyoruz.
		// Girilen karakter sayısı 4 den küçük ise return değişkenini döndürüyoruz.

}
		Echo hesapla($x);

		// Sonuç</pre>