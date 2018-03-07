---
id: 3488
title: 'Laravel 5.4 ile Blog Yapalım &#8211; Bölüm 1'
date: 2017-04-30T22:49:08+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3488
permalink: /laravel-5-4-blog-bolum-1
categories:
  - Laravel 5.4
tags:
  - Laravel
  - Laravel 5.4
  - Laravel 5.4 Blade Kullanımı
  - Laravel 5.4 Dersleri
  - PHP
---
Bir önceki yazımızda **Laravel** ve **Laravel kurulumu** hakkında bilgi vermiştik. Bkz: [laravel başlangıç](https://www.mkoseoglu.com/laravel-5-4-ile-blog-yapalim-baslangic). **Blog** projemizin için Bootstrap 4 ile geliştirilmiş ücretsiz bir **blog** teması beğendim ben. Bu bölümde genel olarak **Blade şablon yapısı**nı inceleyeceğiz. Siz de hazırsanız dersimize başlayalım. Noktalı virgülünüz bol olsun.

[<img class="aligncenter size-full wp-image-3474" src="https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4.png" alt="" width="2220" height="1125" srcset="https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4.png 2220w, https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4-300x152.png 300w, https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4-768x389.png 768w, https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4-1024x519.png 1024w" sizes="(max-width: 2220px) 100vw, 2220px" />](https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4.png)

## Birinci Bölüm:

  * Clean Blog şablonunu inceleyelim ve konfigüre edelim.
  * HTML arayüzümüzü parçalayalım. 
      * Parçalar
      * Bölümler
  * Blade şablon yapısını ve kullanımını inceleyelim. 
      * include
      * yield
      * extends
      * section
  * Route düzeni hakkında bilgi edinelim.
  * Laravel&#8217;de Clean Blog şablonumuzu görüntüleyelim.

## Clean Blog Teması

Start Bootstrap&#8217;ın ücretsiz olarak paylaştığı **Clean Blog** şablonunu sadeliği için tercih ettim. Bizim çalışmamız için uygun olacağını düşünüyorum. Gereksiz kodlardan arınmış bir şablon ile **Laravel** mantığını daha net anlayabiliriz. Toplamda dört ana HTML sayfasından oluşan Clean Blog şablonu **Bootstrap 4** Framework ile geliştirilmiştir.

### Clean Blog Bağlantısı:

Clean Blog şablonunu edinmek için aşağıda yer alan bağlantıya tıklayabilirsiniz. Ben bu seride **Bootstrap 4 Alpha **sürümünü kullanacağım. Siz dilediğiniz sürümü indirebilirsiniz.

  * [startbootstrap.com/template-overviews/clean-blog](https://startbootstrap.com/template-overviews/clean-blog/)

Şablon dosyalarımızı kendi işletim sisteminize uygun bir arşiv yöneticisi ile dışarıya çıkartalım.

<img class="aligncenter size-full wp-image-3489" src="https://www.mkoseoglu.com/wp-content/uploads/ilk-hali.png" alt="" width="902" height="174" srcset="https://www.mkoseoglu.com/wp-content/uploads/ilk-hali.png 902w, https://www.mkoseoglu.com/wp-content/uploads/ilk-hali-300x58.png 300w, https://www.mkoseoglu.com/wp-content/uploads/ilk-hali-768x148.png 768w" sizes="(max-width: 902px) 100vw, 902px" />

### Şablon Dosyalarını Konfigüre Edelim:

Laravel&#8217;de arayüz bileşenlerimiz **public** dizininde, HTML kodlarımız ise **resources** dizini altında bulunan **views** klasöründe; **Blade** şablon yapısı ile yer almalıdır.

Ben, **Clean Blog**&#8216;un dosyalarını, **Laravel**&#8216;de işlevsel biçimde kullanmamı sağlayacak şekilde konfigüre ettim.

<pre class="lang:default decode:true">|-- clean-blog
    |-- about.html
    |-- contact.html
    |-- index.html
    |-- post.html
    |-- css
    |   |-- bootstrap.min.css
    |   |-- clean-blog.css
    |-- font-awesome
    |   |-- css
    |   |   |-- font-awesome.css
    |   |   |-- font-awesome.min.css
    |   |-- fonts
    |       |-- FontAwesome.otf
    |       |-- fontawesome-webfont.eot
    |       |-- fontawesome-webfont.svg
    |       |-- fontawesome-webfont.ttf
    |       |-- fontawesome-webfont.woff
    |       |-- fontawesome-webfont.woff2
    |-- img
    |   |-- about-bg.jpg
    |   |-- contact-bg.jpg
    |   |-- home-bg.jpg
    |   |-- post-bg.jpg
    |   |-- post-sample-image.jpg
    |-- js
        |-- bootstrap.min.js
        |-- clean-blog.js
        |-- contact_me.js
        |-- jqBootstrapValidation.js
        |-- jquery.min.js
</pre>

## Parçalayalım ve Bölümleri Tanıyalım

**Clean Blog** arayüzümüzü **Laravel&#8217;**de dinamik bir yapıda kullanmak için kodlarımızı parçalamamız gerekmektedir. Bu düzenin mantığı başlarda karışık gelse de aslında çok basit. Tüm önyargılarımızdan arınalım ve şevkle okumaya devam edelim. Uykusu gelenler, mayışanlar, esneyenler; kendinize bir kahve alın!

Kullanılan arayüzlerde dinamik olması istenilen her bir bölüm, bir parça olmak zorundadır. Bunu görsel bir şekilde ifade etmeye çalışayım zira bu şekilde tam anlaşılmadı.

[<img class="aligncenter size-full wp-image-3559" src="https://www.mkoseoglu.com/wp-content/uploads/Clean-Blog-Start-Bootstrap-Theme-1.png" alt="" width="1351" height="1636" srcset="https://www.mkoseoglu.com/wp-content/uploads/Clean-Blog-Start-Bootstrap-Theme-1.png 1351w, https://www.mkoseoglu.com/wp-content/uploads/Clean-Blog-Start-Bootstrap-Theme-1-248x300.png 248w, https://www.mkoseoglu.com/wp-content/uploads/Clean-Blog-Start-Bootstrap-Theme-1-768x930.png 768w, https://www.mkoseoglu.com/wp-content/uploads/Clean-Blog-Start-Bootstrap-Theme-1-846x1024.png 846w" sizes="(max-width: 1351px) 100vw, 1351px" />](https://www.mkoseoglu.com/wp-content/uploads/Clean-Blog-Start-Bootstrap-Theme-1.png)

GIMP konusundaki yeteneksizliğim sizi &#8220;Bu da ne şimdi?&#8221; tarzında sorulara yöneltmiş olabilir. Biliyorum. Şu şekilde açıklayayım bunu da. **Kırmızı** bölgemiz şablonumuzun **alt bölüm**ünü oluşturacak ve **footer** ismini alacaktır. **Sarı** bölgelerimiz, şablonumuzun **içerik bölümü**nü oluşturacak ve **content** ismini alacaktır. Son olarak; **parlak turkuaz** bölgemiz şablonumuzun **üst bölümü**nü oluşturacak ve header ismini alacaktır. Şimdi zihninizde şablon parçalama olayının örtüştüğüne inanıyorum. Bunu yapıyoruz ki; şablonumuzu dinamik bir tema haline getirebilelim ve **MVC** deseninde sağlıklı bir sistem kurabilelim. Eğer halen sorularınız varsa bu konuda araştırmalar yapabilirsiniz.

Blade şablon yapısı ile bölümlendirmeyi hedeflediğimiz alanların kodlarını ayrıştıracağız. Sabırla devam edelim.

## Blade Şablon Yapısı

Öncelikle genel bir tanım yapalım. Ben **Blade şablon yapısı** olarak adlandırıyorum. Türkçe karşılığı &#8220;Tema motoru&#8221; anlamlarına da gelmektedir. Front-End (arayüz) çalışmalarımızda kodlarımızın okunabilirliğini sağlar. Yukarıda da bahsetmiştim. **Laravel**&#8216;de resources dizini altında views klasöründe yer almaktadırlar. Önemli bir nokta ise dosya uzantılarımızı &#8220;_**.blade**_&#8221; olarak belirlemeliyiz. **Blade** şablon motoruna yazdığımız tüm kodlar **PHP** üzerinden yorumlanır. **Blade** sözdizimine kısaca değineceğim. Konudan fazla sapmak istemiyorum. **Blade** hakkında daha fazla detayı dökümandan bulabilirsiniz.

### Blade Sözdizimi

**Blade şablon motoru** ile ekrana bir veri basmak istediğinizde **PHP**&#8216;deki print fonksiyonunun yerini küme parantezi almakta. Bir diğer deyişle süslü parantez.

Kısaca örnek verelim:

<pre class="lang:default decode:true ">{{ "Merhaba" }}</pre>

Yukarıdaki komutumuz Blade ile yorumlandığında şu şekilde algılayacaktır:

<pre class="lang:default decode:true ">&lt;? echo "Merhaba"; ?&gt;</pre>

Peki.. XSS açıklarından korunmak için PHP&#8217;de <span class="lang:default highlight:0 decode:true crayon-inline ">htmlspecialchars</span> fonksiyonunu kullanıyoruz. Blade ile bu fonksiyon varsayılan olarak kullanılır. Bazı istisnai durumlarda ise bunu devre dışı bırakmak isteyebiliriz. Bunun için küme parantezleri arasına ünlem işareti tanımlıyoruz.

<pre class="lang:php decode:true ">{!! "Merhaba" !!}</pre>

Bunun yanısıra bazı **JavaScript** çatıları da **küme parantezi** kullanmakta. Bu tarz bir çatıyı **Blade şablon motoru** ile kullanmak istersek ne yapmalıyız? Çözüm pek tabii basit. **@** bizim kaçış operatörümüz olacak. **Tekil kullanımlarda @** kullanırken, **uzun kod bloklarında @verbatim** kullanacağız.

<pre class="lang:default decode:true ">Merhaba, @{{ name }}</pre>

<pre class="lang:default decode:true ">@verbatim
    &lt;div class="container"&gt;
        Merhaba, {{ name }}.
    &lt;/div&gt;
@endverbatim</pre>

### Blade Include

**PHP**&#8216;de kullandığımız **include** ya da **require_include** fonksiyonlarını hatırladınız mı? **Blade** üzerinde **include** kullanımından hiçbir farkı yok. Belirlenen dosyayı, hedef dosyaya dahil eder.

<pre class="lang:default decode:true ">@include('nav.menu')</pre>

### Blade Extends

**Extends** kullanımı ile **@section** mirasına erişir, **@yield** tutucusu ile alanlarımızı bölümlendirebiliriz. Yukarıda açıkladığım bölümlendirme kısmının kod üzerindeki mantığı burada başlar.

<pre class="lang:default decode:true">@extends('layouts.app')</pre>

### Blade Yield

**Yield** ile oluşturduğumuz bölümlerde belirli alanları dinamikleştiririz. **Yield**, bir yer tutucudur. Bizim için o bölümü tutar ve dilediğimiz sayfada farklı değerlerde kullanmamıza imkan verir. En temel örnek site başlığımızdır.

<pre class="lang:default decode:true ">@yield('Başlığım',$title)</pre>

Kısaca **Blade** kullanımından söz ettiğimize göre **Clean Blog** şablonumuzu Blade şablon motorumuza entegre edebiliriz.

## Blade üzerinde Clean Blog

Öncelikle hazırladığım dizin yapısını diyagram ile görelim.

<pre class="lang:default decode:true">|-- view
    |-- about.blade.php
    |-- contant.blade.php
    |-- detail.blade.php
    |-- index.blade.php
    |-- layouts
    |   |-- master.blade.php
    |-- partials
        |-- footer.blade.php
        |-- header.blade.php
        |-- header
            |-- head.blade.php
            |-- masthead.blade.php
            |-- nav.blade.php</pre>

Biz çalışmalarımızda genelde **Türkçe** kullanmayı tercih etsek de yazılım sektörü global bir alandır. Buna dayanarak klasör ve dizin isimlerimiz herkesin anlayabileceği standartlarda olmalıdır. Buna dayanarak isimlendirme ve konfigüre işlemlerimize devam edeceğiz.

**Laravel**&#8216;de, **Layouts** klasörümüz içerisinde şablonumuzun **master** dosyası bulunmalıdır. **Master** dosyasından kastımın ne olduğunu kodları paylaştığımda daha net anlayacaksınız. **Partials** klasörümüzde ise şablonumuzun bölümleri bulunmalıdır. Bu bölümleri sizlerle yukarıda parçalamıştık. Unutmayın, ne kadar düzenli ve parçalı ilerlerseniz ilerde o kadar rahat edersiniz. Blog gibi basit içerikli çalışmalarda sorun olmasa da büyük projelerde çalışırken bu alışkanlığı edinmeniz size artı kazandıracaktır.

**Partials** içerisinde oluşturduğum **header** klasöründe ise şablonumuzun üst bölümünü parçaladım. Şablon iskeletimizde **head** bölümünü, menu bölümünü ve şablonumuza ait olan **masthead** bölümünü ayrıştırdım.

#### Kodlarımızı GitHub üzerinden görüntüleyebilirsiniz

  * <https://github.com/mkoseoglu/laravel-5-4-blog-yapalim/tree/master/resources/views>

## Route Yapılandırması

Tema dosyalarımızı konfigüre ettiğimize göre şimdi yönlendirmelerimizi yapalım.

**Laravel**&#8216;de yönlendirme kodlarımız web dosyasında düzenlenmektedir. Yine ilerleyen derslerde yeri geldiğinde detaylı olarak göreceğiz. **Laravel** dökümanlarından daha geniş bilgilere erişebilirsiniz.

  * <https://laravel.com/docs/5.4/routing>

<pre class="lang:default decode:true ">Route::get('/', function () {
    return view('index');
});
Route::get('about', function () {
    return view('about');
});
Route::get('detail', function () {
    return view('detail');
});
Route::get('contant', function () {
    return view('contant');
});
</pre>

## PHP Artisan ve Laravel&#8217;de Görüntüleme

PHP Artisan komutlarını yine Route gibi ilerleyen derslerde detaylı olarak göreceğiz. Şimdilik sadece sanal sunucumuzu başlatalım. **Laravel**&#8216;in kurulu olduğu dizine terminal kullanarak gelelim ve php artisan serve komutunu çalıştıralım.

<pre class="lang:default decode:true">[mksglu@mksglu blog]$ php artisan serve
Laravel development server started: &lt;http://127.0.0.1:8000&gt;</pre>

Bu çıktıyı gördükten sonra tarayıcıda

  * localhost:8000**/**
  * localhost:8000**/about**
  * localhost:8000**/detail**
  * localhost:8000**/contant**

Bağlantılarını kullanarak şablonumuzun çalıştığını görebilirsiniz. **Laravel** ders serisinde bölümleri daha kısa tutarak daha çok bilgi vermeyi amaçlıyorum. Her şey iç içe gözükse de dikkatle takip ettiğinizde üstesinden geleceğinize eminim.

## GitHub

  * <https://github.com/mkoseoglu/laravel-5-4-blog-yapalim>