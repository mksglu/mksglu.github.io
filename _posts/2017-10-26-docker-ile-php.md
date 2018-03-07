---
id: 3910
title: Docker ile PHP Geliştirelim
date: 2017-10-26T03:10:40+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3910
permalink: /docker-ile-php
categories:
  - Docker
tags:
  - Docker
  - Docker ile PHP
  - Docker Kullanımı
---
Merhaba,

**Docker** ile **PHP geliştirmek** isteyenlere yönelik kullandığım bir paketten bahsedeceğim. GitHub&#8217;ta [webdevops.io](http://webdevops.io) bünyesinde geliştirilen paket ile **Docker Hub**&#8216;ta bulunan tüm imajları dilediğiniz gibi kullanabilirsiniz.

&nbsp;

Öntanımlı olarak gelen birden fazla seçenek bulunmakta. **PHP ile proje geliştirenler**den şunu duyar gibiyim. Bende çalışıyor, ama arkaşımda çalışmıyor. Çok ciddiyim. Bu anahtar kelimelerle bile Google&#8217;da araştırma yaptığınızda karşınıza birçok konu başlığı çıkmakta.

Ben de bu sorunu bloğumda yazmışım hatta. Linux Mint kullanıcısı iken karşılaştığım bir PHP ortam sorunu ve çözümü: <https://www.mkoseoglu.com/linux-php-composer-hatasi-ve-cozumu>

Birgün CI ile geliştirme yaparken Laravel 5.5 ile çözmem gereken bir sorun vardı. Fakat şöyle bir durum var. Laravel 5.5 ile birlikte PHP 7 bağımlılığı da beraberinde gelmekte. Bu durumda, Arch Linux&#8217;a yeni bir PHP sürümü yapılandırmak ya da XAMP&#8217;ın PHP 7 sürümünü kurmak görünürde en mantıklı gelen çözümlerdi. Fakat ilerleyen zamanlarda bunun aslında ne kadar da saçma ve sığ bir süreç olduğunu fark ettim.

**Docker**, bizlere bu sorunu çözmeyi vaad ediyor. Bir sanallaştırma teknolojisi olan **Docker** üzerine teorik bilgilerden ziyade geliştirme paketinden söz etmeyi tercih ediyorum.

GitHub alanlarında ekledikleri açıklama satırında Symfony, WordPRess, Joomla ve diğer PHP projelerini (NGINX, Apache HTTPd, PHP-FPM, MySQL, Solr, Elasticsearch, Redis, FTP) desteklediklerinden söz etmişler._ _PHP sürümleri ve servisleri elinizin altında, tek yapmanız gereken Docker Compose ile birden fazla konteynırı ayağa kaldırmak.

## Docker Kurulumu

Ben Arch Linux kullanıcısıyım. Pacman kullanarak ihtiyacım olan uygulamaları yüklüyorum.

<pre class="lang:default decode:true ">sudo pacman -S docker docker-compose</pre>

Yükledikten sonra **Docker** servisimi başlatıyorum.

<pre class="lang:default decode:true ">sudo systemctl start docker.service</pre>

Linux kullanıcılarının dikkat etmesi gereken bir nokta var. Docker&#8217;ın her komutunda sudo kullanmak ya da **Docker**&#8216;ı kullanıcı grubuna eklemek zorundasınız. Ben eklemeyi tercih ediyorum.

<pre class="lang:default decode:true ">sudo groupadd docker
sudo usermod -aG docker $USER</pre>

Bu işlemden sonra oturumumu yeniden başlatıyorum. Uçbirimde <span class="lang:default highlight:0 decode:true crayon-inline ">docker version</span> komutunu çalıştırıyorum. Eğer sizin de çıktınız aşağıdakine benzer ise her şey yolunda demektir.

<pre class="lang:default decode:true ">Client:
 Version:      17.10.0-ce
 API version:  1.33
 Go version:   go1.9.1
 Git commit:   f4ffd2511c
 Built:        Wed Oct 18 23:08:56 2017
 OS/Arch:      linux/amd64

Server:
 Version:      17.10.0-ce
 API version:  1.33 (minimum version 1.12)
 Go version:   go1.9.1
 Git commit:   f4ffd2511c
 Built:        Wed Oct 18 23:09:11 2017
 OS/Arch:      linux/amd64
 Experimental: false
</pre>

## PHP Docker Boilerplate

Git clone komutu ile paketimizi yerele çekelim. Paketimizin içerisinde yer alan app dizini bizim Linux&#8217;taki mount, **Docker**&#8216;daki Volumes dizinidir. Bir anlamda yerel bilgisayarınızdaki çalışma dosyalarınızdır. Biz, app dizini üzerinde çalışacağız.

Gerekli dökümanlara buradan ulaşabilirsiniz: <https://github.com/webdevops/php-docker-boilerplate/tree/master/documentation>

<pre class="lang:default decode:true">git clone https://github.com/webdevops/php-docker-boilerplate.git docker
</pre>

Uçbirimde paket dizininde aşağıdaki komut ile birlikte çalışma ortamımızı seçelim. Geliştirme ortamında development olanını seçmekte fayda var. Gerekli hata ayıklama gösterimleri açık olarak gelmekte.

<pre class="lang:default decode:true ">cp docker-compose.development.yml docker-compose.yml
</pre>

Şimdi, <span class="lang:default highlight:0 decode:true crayon-inline ">docker-compose.yml</span> dosyamızın içeriğine bir göz atalım. Burada yer alan komutların açıklama ve anlatımları için <span class="lang:default highlight:0 decode:true crayon-inline ">Dockerfile</span> oluşturma üzerine araştırma yapabilirsiniz. Ben kullanmayacağım için <span class="lang:default highlight:0 decode:true crayon-inline ">links</span> altında belirtilen <span class="lang:default highlight:0 decode:true crayon-inline">mail servisi</span>ni siliyorum.

MySQL veritabanı olarak 5.7 sürümünü kullanmayı tercih ettiğim için başındaki yorum satırını kaldırarak ilgili satırı aktif ediyorum. Hemen yukarısında kalan 5.6 sürümünün başına yorum satırı koyarak geçersiz hale getiriyorum.

<pre class="lang:default decode:true ">dockerfile: MySQL-5.7.Dockerfile</pre>

Ve son olarak phpMyAdmin kullanmak istediğim için dosyanın aşağında bulunan yorum satırlarını silerek aktif hale getiriyorum ve görebilmek için bir port tanımlıyorum.

<pre class="lang:default decode:true">phpmyadmin:
  image: phpmyadmin/phpmyadmin
  links:
    - mysql
  ports:
    - 3000:80
  environment:
    - PMA_HOSTS=mysql
    - VIRTUAL_HOST=pma.boilerplate.docker
    - VIRTUAL_PORT=80
  volumes:
    - phpmyadmin:/sessions</pre>

Buna göre, phpMyAdmin&#8217;in 3000&#8217;inci portumda çalışmasını beklerim.

Kullandığımız paketin dökümantasyonunda ortam değişkenleri ve daha birçok konuda anlatım bulunmakta. Kendi ihtiyaçlarınıza göre inceleyerek yapılandırabilirsiniz.

## Docker Compose

Docker Compose birden fazla konteynırı ayağa kaldırmaya yarar. Öncelikle bu paketimizi build etmemiz gerekli.

<pre class="lang:default decode:true ">docker-compose build</pre>

Yukarıdaki komut ile inşaa ederek ihtiyaçlarımıza yönelik yapılandırdığımız Dockerfile dosyamız bizlere ilgili servislerin imajını indirmekle görevlidir.

Gerekli işlemler tamamlandığında <span class="lang:default highlight:0 decode:true crayon-inline">docker image ls</span> komutu ile tamamlanan imajlarımızı görüntüleyebiliriz. Sol kısımda yer alanlar ise ID değerleridir.

Şimdi buradaki imajlarımızı ayağa kaldıralım, çalıştıralım.

<pre class="lang:default decode:true ">docker-compsoe up -d</pre>

Buradaki <span class="lang:default highlight:0 decode:true crayon-inline ">-d</span> parametresi detached&#8217;ten gelmektedir. Türkçesi ile bağımsız, tarafsız anlamlarına gelmekte ve olan detached&#8217;in bizler için asıl amacı Docker komutlarını arka planda çalıştırmasıdır.

Komutumuzu çalıştırdıktan sonra adres çubuğumuza <span class="lang:default highlight:0 decode:true crayon-inline ">localhost:8000</span> yazarak **Apache** sunucumuza, <span class="lang:default highlight:0 decode:true crayon-inline ">localhost:3000</span> yazarak da **phpMyAdmin** ekranımıza ulaşabilirsiniz.

Buradaki app dizininde Laravel, CI ve WordPress gibi yukarıda da sözünü ettiğimiz Framework&#8217;leri (çatı) kullanabilir farklı PHP sürümleri ve servisleri ile ihtiyacına göre çalışma ortamınızı yapılandırabilirsiniz.

Çalışmalarınızı GitHub&#8217;a, Dockerfile dosyanızı ise imaj haline getirerek Docker Hub hesabınıza atabilirsiniz.

## Sonuç

**Docker**&#8216;in Türkçe kaynak eksikliği herkesçe bilindiği için bu makaleyi oluşturmaya karar verdim. Kısa da olsa bir **PHP geliştirici**sinin hangi süreçlerden geçmesi ve hangi adımları izleyerek işlevsel bir Docker kullanıcısı olabileceğini anlatmayı hedefledim.