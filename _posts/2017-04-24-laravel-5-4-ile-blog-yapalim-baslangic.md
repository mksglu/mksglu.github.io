---
id: 3458
title: 'Laravel 5.4 ile Blog Yapalım &#8211; Başlangıç'
date: 2017-04-24T21:13:50+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3458
permalink: /laravel-5-4-ile-blog-yapalim-baslangic
categories:
  - Laravel 5.4
tags:
  - Laravel 5.4
  - Laravel 5.4 Blog
  - Laravel 5.4 Dersleri
---
**Laravel** 5.4 çatısı ile Türkçe kaynak olması amacı ile en temel gereksinimleri barındıran bir blog çalışması yapacağız. Öncelikle **Laravel**&#8216;in evrensel tanımına bir göz atalım. Çalışma boyunca Laravel dökümanına sadık kalacağım. Siz de benimle birlikte takip edebilirsiniz.

[<img class="aligncenter size-full wp-image-3474" src="https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4.png" alt="" width="2220" height="1125" srcset="https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4.png 2220w, https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4-300x152.png 300w, https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4-768x389.png 768w, https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4-1024x519.png 1024w" sizes="(max-width: 2220px) 100vw, 2220px" />](https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4.png)

## Laravel

**Laravel**, MVC yapısında web uygulamaları geliştirme için tasarlanmış ücretsiz, açık kaynak PHP web uygulama iskeletidir. **Laravel**, GitHub sitesinde barındırılan kaynak kodu ile birlikte, MIT lisansı altında yayınlandı.

## Laravel Kurulumu

**Laravel** kullanımı için sunucumuzda bazı gereksinimlerin var olduğundan emin olmalıyız.

  * PHP >= 5.6.4
  * OpenSSL PHP Extension
  * PDO PHP Extension
  * Mbstring PHP Extension
  * Tokenizer PHP Extension
  * XML PHP Extension

Bu gereksinimleri sağladığınızdan emin iseniz kuruluma devam edebiliriz. Kurulumda <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">composer</span>  kullanacağız.

### Composer

Composer hakkında yine evrensel bilgi kaynağına başvuralım ve alıntılayalım.

Composer, PHP programlama dili için tasarlanmış çoklu platform (cross-platform) bir paket yönetim sistemidir. PHP uygulamaları ve uygulama içerisinde kullanılan kütüphaneler için bağımlılık yönetimi (dependency management) sağlar. Nils Adermann and Jordi Boggiano, tarafından geliştirilmiş olup ilk sürümü 1 Mart 2012 tarihinde yapılmıştır[1]. Composer geliştirilirken Node.js&#8217;in &#8220;npm&#8221; ve Ruby&#8217;nin &#8220;bundler&#8221; sistemlerinden esinlenilmiştir[2].

Composer komut satırından çalıştırılır ve uygulamanın bağımlı olduğu kütüphaneleri uygulama içerisine kurar. Kurulan kütüphanelerin bağımlı olduğu başka kütüphaneler varsa onlar da otomatik olarak kurulur. Composer ayrıca packagist adı verilen ortak bir kaynaktan izin verilen kütüphanelerin uygulama içerisine kolayca kurulmasına da imkan verir. Yüklenen kütüphanelerin uygulama içerisine otomatik olarak yüklenmesi (autoload) için bir altyapı da sunar.

### Composer Yükleyelim

Ben bir Linux kullacanıcısıyım. <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">Linux 4.10.8-1-MANJARO x86_64 GNU/Linux</span> Siz kendi işletim sisteminize göre [buradaki](https://getcomposer.org/download/) bağlantıyı takip ederek kurulumunu yapabilirsiniz.

Ben kendi paket yöneticimden yüklüyorum.

#### Linux Arch & Manjaro

<pre class="lang:c decode:true ">yaourt -S composer</pre>

Komutu ile birlikte composer kurulumunu başarılı bir şekilde gerçekleştirmiş bulunmaktayım. Siz de yüklemenin doğruluğunu öğrenmek isterseniz terminal ekranınızda <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">composer</span>  komutunu çalıştırabilir ve kullanabileceğiniz argüman listesine ulaşabilirsiniz.

#### Composer Create Project

Composer üzerinde create-project komutunu kullanabiliriz. Bu komut bizlere ilgili paketi yeni bir proje halinde indirmemizi sağlayacaktır.

Terminalde kurmak istediğiniz dizini açalım. Linux&#8217;ta <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">pwd</span>  komutu ile bulunduğunuz dizini görebilir, <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">cd</span> komutu ile farklı dizinlere geçiş yapabilir ve <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">ls</span> komutu ile de bulunduğunuz dizinde bulunan dosyaları görüntüleyebilirsiniz.

Terminalde kurulumu yapmak istediğiniz dizine geldiğinizde aşağıdaki komutu çalıştıralım:

<pre class="lang:default decode:true">composer create-project --prefer-dist laravel/laravel blog</pre>

Buradaki blog sizin projenizin ismi olacaktır. Siz bunu dilediğiniz şekilde değiştirebilirsiniz. Kurulumdan sonra ilgili dizinde blog isminde bir klasör oluştuğunu görüyoruz.

### Laravel 5.4 ile Geliştirmeye Hazırız

**Laravel** çalışmalarımızda bazı yetkilendirmeleri tanımlamamız gerekmektedir. Bunlar depolama alanı içerisindeki <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">storage</span>  ve <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">bootstrap/cache</span>  dizinleridir.

<pre class="lang:default decode:true  ">sudo chgrp -R www-data storage bootstrap/cache 
sudo chmod -R ug+rwx storage bootstrap/cache</pre>

#### PHP Artisan

Laravel&#8217;de projemizi geliştirirken sık sık artisan komutlarını kullanacağız. Bu konuya ileride daha çok değineceğiz. Şimdi projemizi çalıştıralım.

<pre class="lang:default decode:true ">php artisan serve</pre>

Bu komut bizlere varsayılan olarak 8000 portunda Laravel&#8217;i çalıştırmaktadır. Eğer farklı bir port üzerinde çalışmak isterseniz;

<pre class="lang:default decode:true ">php artisan serve --port=5050</pre>

Yukarıdaki kullanım gibi 5050 portunda da çalışabilirsiniz. Eğer buraya kadar sorunsuz bir şekilde kurulumu gerçekeştirdi iseniz bir sonraki dersimize geçebilirsiniz.

## GitHub:

Github üzerinden çalışmaya ulaşabilirsiniz.

  * https://github.com/mkoseoglu/laravel5.4-blog

## Kaynak:

  * https://laravel.com/docs/5.4/installation