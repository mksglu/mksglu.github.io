---
id: 3061
title: CodeIgniter 3 Insert Kullanımı
date: 2016-08-24T07:07:27+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=3061
permalink: /codeigniter-dersleri-insert-islemleri
categories:
  - CodeIgniter 3.x
tags:
  - CI
  - CodeIgniter
  - CodeIgniter Dersleri
  - CodeIgniter Veri Ekleme
  - MVC
  - PHP
---
[**CodeIgniter**](http://www.mkoseoglu.com/etiket/codeigniter/) ile veritabanına veri ekleme işlemini gerçekleştirelim. Öncelikle _models _klasörümüzde **YeniProje **isminde bir [PHP](http://www.mkoseoglu.com/etiket/php/) dosyası oluşturalım. Dosyanın içerisine aşağıda yer alan kodları yazalım.

### models/YeniProje

<pre class="lang:php decode:true">class YeniProje extends CI_Model		
	{

		function Insert(){

		$data = array(
			'alanBir'	=&gt; 'Ben alanBire eklenecek veriyim.',
			'alanIki'	=&gt; 'Ben alanIkiye eklenecek veriyim.',
		);

		$query = $this-&gt;db-&gt;insert('tablo',$data);
		echo $query	? "&lt;h1&gt;veri eklendi..&lt;/h1&gt;" : FALSE;

		/*
		SQL = INSERT INTO tablo (alanBir, alanIki) VALUES ('Ben alanBire eklenecek veriyim.', 'Ben alanIkiye eklenecek veriyim.')

		*/

		}

	}</pre>

**CodeIgniter **üzerinde kullanılan **insert** fonksiyonunda birinci parametre işlem yapmak istediğimiz tablo ismi, ikincisi ise verilerimizi gönderdiğimiz dizi değişkenimizdir. Hemen alt satırında yaptığımız if bloğunda da işlem hakkında çıktı alabiliyoruz.

### controllers/Uygulama

<pre class="lang:php decode:true ">defined('BASEPATH') OR exit('No direct script access allowed');

	class Uygulama extends CI_Controller {

		function __construct() 
		{
			parent::__construct();
		}

		function insert()
		{
		$this-&gt;load-&gt;model('yeniproje');
		$query = $this-&gt;yeniproje-&gt;Insert();
   		}
	  
	}
</pre>

**Uygulama** dosyamızda ise **insert** isminde bir fonksiyon oluşturduk ve **Model** dosyamızdan gelen işlem mekanizmamızı tanımladık.

Tarayıcımızda, _localhost/index.php/uygulama/insert_ adresini çalıştırdığımızda işlemin başarılı olduğunu görebilirsiniz.