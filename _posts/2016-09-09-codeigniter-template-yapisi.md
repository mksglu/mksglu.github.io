---
id: 3075
title: CodeIgniter 3 Template Yapısı
date: 2016-09-09T02:27:17+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=3075
permalink: /codeigniter-template-yapisi
categories:
  - CodeIgniter 3.x
tags:
  - CodeIgniter
  - CodeIgniter Dersleri
  - CodeIgniter Kütüphane Oluşturma
  - CodeIgniter Tema Kullanımı
  - CodeIgniter Template
  - CodeIgniter Template Kullanımı
  - CodeIgniter Template Sistemi
  - PHP
---
[**CodeIgniter**](http://www.mkoseoglu.com/php-mysql/) öğrenmeye yeni başladığım sıralarda **template** yapısına gerek duymamıştım fakat **blog** sistemi yazmaya karar verdiğimde ne kadar elzem bir ihtiyaç olduğunu anlamam uzun sürmedi. Birkaç döküman ve video taramasından sonra amacıma ulaştım. Bu konuda pek **Türkçe** kaynak olmamasından mütevellit blogumda paylaşmaya karar verdim. Olay şöyle ki;

Öncelikle **kütüphane**mizi oluşturalım. [**CodeIgniter**](http://www.mkoseoglu.com/etiket/codeigniter/) dizininde **libraries** klasöründe &#8220;**TempK**&#8221; isminde bir **PHP** dosyası oluşturalım.

## TempK

<pre class="lang:php decode:true">&lt;?php 

class tempK {

        protected $CI;

        public function __construct()
        {
                $this-&gt;CI =& get_instance();
        }

        public function get($temp, $data=null)
        {
               
       		$data['header']  = $this-&gt;CI-&gt;load-&gt;view('template/header',$data,true);
       		$data['sidebar'] = $this-&gt;CI-&gt;load-&gt;view('template/sidebar',$data,true);
       		$data['content'] = $this-&gt;CI-&gt;load-&gt;view('content/'.$temp,$data,true);
       		$data['footer']  = $this-&gt;CI-&gt;load-&gt;view('template/footer',$data,true);
       		$this-&gt;CI-&gt;load-&gt;view('template/index',$data);
       		       		

        }

}

?&gt;
</pre>

Yukarıda yer alan kodlarımızda, [**template**](http://www.mkoseoglu.com/etiket/codeigniter-template/) klasörümüzde bulunan _header.php_, _sidebar.php_, _footer.php_ ve **content** klasöründe bulunan dosya ismi dinamik olan _home.php_ dosyamıza veri gönderelim. En alt satırda da _index.php_ dosyamızda gösterelim.

## Template

**View** klasörümüzün içerisine [**Template**](http://www.mkoseoglu.com/etiket/codeigniter-template-kullanimi/) isminde bir klasör daha oluşturalım ve içerisinde _header.php_, _sidebar.php_, _footer.php_ ve _index.php_ dosyaları oluşturalım.

### Footer

<pre class="lang:xhtml decode:true">&lt;div class="footer"&gt;
	&lt;span&gt;footer&lt;/span&gt;
&lt;/div&gt;
&lt;/body&gt;
&lt;/html&gt;</pre>

### Header

<pre class="lang:xhtml decode:true">&lt;!DOCTYPE html&gt;
&lt;html lang="en"&gt;
&lt;head&gt;
	&lt;meta charset="UTF-8"&gt;
	&lt;title&gt;&lt;?php echo $title; ?&gt;&lt;/title&gt;
&lt;/head&gt;
&lt;body&gt;
	&lt;div class="header"&gt;
	     &lt;span&gt;header&lt;/span&gt;
	&lt;/div&gt;</pre>

### Sidebar

<pre class="lang:xhtml decode:true">&lt;div class="sidebar"&gt;
		&lt;span&gt;sidebar&lt;/span&gt;
&lt;/div&gt;</pre>

### Index

<pre class="lang:php decode:true">&lt;?php

	echo $header;
	echo $sidebar;
	echo $content;
	echo $footer;

?&gt;</pre>

## Content

[**Template**](http://www.mkoseoglu.com/etiket/codeigniter-tema-kullanimi/) yapımızda içerik kısmımızda yer alacak [**PHP**](http://www.mkoseoglu.com/etiket/php/) dosyalarını oluşturalım. Ben, _single.php_ ve _home.php_ olarak iki farklı sayfa oluşturdum.

### Home

<pre class="lang:php decode:true">&lt;div class="content-home"&gt;
		&lt;span&gt;&lt;?php echo $a; ?&gt;&lt;/span&gt;
		&lt;ul id="conU"&gt;
			&lt;?php for($x = 1; $x &lt;= 10; $x++){ ?&gt;	

			&lt;li&gt;&lt;a href="#"&gt;&lt;/a&gt;&lt;?php echo $x; ?&gt;&lt;/li&gt;
						
			&lt;?php } ?&gt;	
		&lt;/ul&gt;
	&lt;/div&gt;
</pre>

### Single

<pre class="lang:php decode:true">&lt;div class="content-single"&gt;
		&lt;span&gt;&lt;?php echo $a; ?&gt;&lt;/span&gt;
		&lt;ul id="conU"&gt;
			&lt;?php for($x = -5; $x &lt;= 10; $x++){ ?&gt;	

			&lt;li&gt;&lt;a href="#"&gt;&lt;/a&gt;&lt;?php echo $x; ?&gt;&lt;/li&gt;
						
			&lt;?php } ?&gt;	
		&lt;/ul&gt;
	&lt;/div&gt;
</pre>

## Controllers

Şimdi de **controller** için kodlarımızı yazalım. **Template** isminde bir **PHP** dosyası oluşturuyorum.

<pre class="lang:php decode:true">&lt;?php

defined('BASEPATH') OR exit('No direct script access allowed');

class Template extends CI_Controller {
	function __construct() 
	{
		parent::__construct();
	 	$this-&gt;load-&gt;library('tempK');
	}

	public function index()
	{
		 $data['title'] ="Ben home başlığım.";
		 $data['a'] ="Ben home içeriğim.";
		 $this-&gt;tempK-&gt;get('home',$data);
		 
	}
	public function single()
	{
 		 $data['title'] ="Ben single başlığım.";
		 $data['a'] = "Ben single içeriğim.";
		 $this-&gt;tempK-&gt;get('single',$data);
		 
	}

}
 
?&gt;</pre>

## Sonuç

Genel anlamda yapımız bu şekilde. _template/index_&#8216;e ya da _template/single_ adreslerine baktığımızda başarılı bir şekilde çalıştığını görebilirsiniz. Bu şekilde devam ettiğinizde temeli sağlam bir yapı çıkartabilirsiniz.

> Paylaşın, sevin, mutlu olun.