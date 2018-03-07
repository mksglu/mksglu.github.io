---
id: 2565
title: PHP Data Objects (PDO) Kullanımı
date: 2014-07-07T00:36:07+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=2565
permalink: /php-data-objects-pdo-kullanimi
categories:
  - PHP
tags:
  - PHP Data Objects (PDO) Kullanımı
---
Merhabalar,

Bu dersimizde PHP PDO Kullanımı hakkında bilgiler vereceğim. Daha sonra **UPDATE**, **DELETE**, **INSERT**, **Veri Çekme** ve **Veritabanı Bağlantısı** işlemlerini örneklerle açıklayacağız.

## **PDO Nedir?**

**PDO** (**PHP Data Objects / PHP Veri Objeleri**) özetle; hafif ve tutarlı bir şekilde **veritabanına erişimi sağlayan bir arayüz.** Adından da anlayacağınız üzerie “**Object Oriented Programming**” arayüzüne sahip, onlarca veritabanı sürücüsü destekliyor.

## **PDO Veritabanı Bağlantısı**

&nbsp;

<pre class="lang:php decode:true">try{
		        $db = new PDO('mysql:host=localhost;dbname=VeritabanıIsmi;charset=utf8','Kullanıcı Adı','Sifre');
			}catch(PDOException $e){
				echo 'Hata: '.$e-&gt;getMessage();
			}</pre>

Veritabanı bağlantısında olası hataları yakalamak için **try cacth** kullandık**. Karakter Setini UTF-8 **olarak belirledik.

## **PDO prepare() Methodu Kullanımı**

prepare() Çalıştırılmak üzere bir SQL deyimini hazırlar. Metot **bindparam(),** **execute(), bindColumn(), bindValue()** metotları ile beraber çalışır. Dışarıdan **SQL sorgularına** dahil edilecek veriler için iki tür tanım yapmayı sağlar. Bunlardan birisi **soru işaretidir**. Diğeri ise önünde **iki nokta üst üste olan herhangi bir isimdir.**

## **PDO Hata Mesajlarını Yakalama errorInfo() Kullanımı**

**Mysql** kullandığımızda sorgularımızın sonuna **mysql_error();** ekleyerek **hata mesajlarını** yakalayabiliyoruz.

**PDO** kullanırken bu durum biraz değişiyor ve yerini **errorInfo();** fonksiyonuna bırakıyor. Bu fonksiyon bize **3 elemanlı bir array** döndürür. **** ve **1**. eleman ilgili sorgunun **hata kodu,** **3. elemanı ise hata mesajıdır.**

Ben hata mesajlarını yakalarken **empty();** fonksiyonunu kullanıyorum. Eğer **hata mesajı** boş ise işlem başarılıdır şeklinde. Bunu **rowCount();** fonksiyonu kullanarak veya sorgu **false** dönüyorsa hata vardır şeklinde yapanlarda var.

## **PDO DELETE Sorgusu Kullanımı**

<pre class="lang:php decode:true">$del = $db-&gt;prepare("DELETE FROM pdotablo WHERE id = ?");
			$del-&gt;execute(array(
				'1'
			));
			$hata = $del-&gt;errorInfo();
			echo empty($hata[2]) ?  "Başarılı Bir Şekilde Çalıştı." : $hata[2];</pre>

**Delete** sorgumuzda **ID degeri 1** olan verimizi başarılı bir şekilde sildik.

## **PDO UPDATE Sorgusu Kullanımı**

<pre class="lang:php decode:true">$guncelle = $db-&gt;prepare("UPDATE pdotablo SET baslik=? WHERE id = ?");
			$guncelle-&gt;execute(array('Mert Köseoğlu','5'));
			$hata = $guncelle-&gt;errorInfo();
			echo empty($hata[2]) ?  "Başarılı Bir Şekilde Çalıştı." : $hata[2];</pre>

**Update** sorgumuzda **ID degeri 5** olan **baslik** sütunumuzda ki verimizi &#8220;**Mert Köseoğlu**&#8221; olarak başarılı bir şekilde güncelledik.

## **PDO SELECT Kullanımı TEK (Verileri Listeletmek) **

<pre class="lang:php decode:true">$sql = $db-&gt;prepare("SELECT * FROM pdotablo WHERE id= ?");
			$sql-&gt;execute(array(
				'5'
			));

			$row=$sql-&gt;fetch(PDO::FETCH_ASSOC);
			echo $row['baslik'];

 			$hata = $sql-&gt;errorInfo();
			echo empty($hata[2]) ?  "Başarılı Bir Şekilde Çalıştı." : $hata[2];</pre>

## **PDO SELECT Kullanım Döngü (Verileri Listeletmek)**

<pre class="lang:php decode:true">$sql = $db-&gt;prepare("SELECT * FROM pdotablo");
			$sql-&gt;execute();

			while($row=$sql-&gt;fetch(PDO::FETCH_ASSOC)) {
				echo $row['baslik'];
			}


 			$hata = $sql-&gt;errorInfo();
			echo empty($hata[2]) ?  "Başarılı Bir Şekilde Çalıştı." : $hata[2];</pre>

## **PDO INSERT Sorgusu Kullanımı (Veri Eklemek)**

<pre class="lang:php decode:true">$baslik = "Deneme Baslik";
			$icerik = "Deneem İçerik";
			$footer = "Deneme Footer";

			$sql = $db-&gt;prepare('INSERT INTO pdotablo (baslik,icerik,footer) VALUES (?,?,?)');
			$ekle = $sql-&gt;execute(array(

				$baslik,
				$icerik,
				$footer,

				));
			
	 		$hata = $sql-&gt;errorInfo();
			echo empty($hata[2]) ?  "Başarılı Bir Şekilde Çalıştı." : $hata[2];</pre>

## **PDO Eklenen Verinin ID Degerini Almak**

<pre class="lang:php decode:true">$id = $db-&gt;lastInsertId();
			echo $id;</pre>

## **PDO quote() Methodu Kullanımı**

<pre class="lang:php decode:true ">$id=$db-&gt;quote($_POST["id"]);
$bag-&gt;query("SELECT * FROM okul WHERE id ='$id'");</pre>

**PDO** ile **mysql\_escape\_string** ve türevlerinin yerini **quote()** methodu aldı.