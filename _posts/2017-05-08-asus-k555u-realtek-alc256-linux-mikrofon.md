---
id: 3610
title: ASUS K555U Realtek ALC256 Linux Mikrofon Sorunu
date: 2017-05-08T00:50:36+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3610
permalink: /asus-k555u-realtek-alc256-linux-mikrofon
categories:
  - Genel
  - Linux
tags:
  - Asus K555
  - ASUS K555U Linux
  - ASUS K555U Realtek ALC256 Linux
  - Establishing connection toPulseAudio. Please wait ..
  - Linux Arch Hda Jack Retask
  - Linux Realtek ALC 256
  - Pioneer SE-MJ591 Tanıtımı
---
## Güncelleme: Linux Kernel 4.12

Linux Kernel 4.12 ile birlikte ses ve mikrofon sorunlarının tamamı giderildi.

* * *

Esenlikler herkese. Eğer bu yazıya Google&#8217;da yaptığınız araştırmalar sonucunda geldi iseniz; Tanrı şimdiden sabır versin. Belirtmek isterim ki bu yazıda umduğunuzu bulamayacaksınız, zira ben de çaresizim.

Bilgisayarımı ilk aldığımda blogumda [Windows 10&#8217;da yaşanan uyku sorunu](https://www.mkoseoglu.com/asus-uyku-modu-siyah-ekran-cozumu)ndan bahsetmiştim. Bu yazıdan kısa bir süre sonra **Linux** kullanmaya başladım. Ubuntu, Mint, OpenSUSE, Linux Lite, Arch Linux ve Manjaro dağıtımlarını kullandım. KDE, XFCE ve Gnome masaüstü ortamları ile çalıştım. Şu an sabit olarak Manjaro I3WM kullanmaktayım. Sözün özü şu ki; **Linux&#8217;ta Realtek ALC256 ses kartının mikrofon ayarlarında sorun oluşmakta** maalesef.

Bu konu ile ilgili Google ve diğer arama motorlarında yaptığınız araştırmalarda sayısız forumda sayısız konu okuyacak ama çözüme yüksek ihtimal ulaşamayacaksınız. Jack girişinden ve dahili kemara mikrofonundan bir türlü ses kaydedemeyeceksiniz. Alsamixer, PulseAudio gibi binbir çeşit araç deneyecek, paket depolarında sörf yapacaksınız. Biliyorum, biliyorum çünkü ben bunları yaşadım. Tüm Facebook gruplarına konu açtım. Farklı dağıtımlarda uzman kişilerden görüş aldım. Bu sorunun bir çözümü yok ve kronik bir sorun.

Geçici ve ideal olmayan bir çözüm buldum neyse ki. Çok içime sinmese de paylaşmak istedim. Bir Jack dönüştürücüye ihtiyacımız var. Google&#8217;da [U](https://www.google.com.tr/search?q=USB+Ses+Kart%C4%B1&oq=USB+Ses+Kart%C4%B1&aqs=chrome..69i57j69i65&sourceid=chrome&ie=UTF-8)[SB](https://www.google.com.tr/search?q=USB+Ses+Kart%C4%B1&oq=USB+Ses+Kart%C4%B1&aqs=chrome..69i57j69i65&sourceid=chrome&ie=UTF-8) [Ses](https://www.google.com.tr/search?q=USB+Ses+Kart%C4%B1&oq=USB+Ses+Kart%C4%B1&aqs=chrome..69i57j69i65&sourceid=chrome&ie=UTF-8) [Ka](https://www.google.com.tr/search?q=USB+Ses+Kart%C4%B1&oq=USB+Ses+Kart%C4%B1&aqs=chrome..69i57j69i65&sourceid=chrome&ie=UTF-8)[rtı](https://www.google.com.tr/search?q=USB+Ses+Kart%C4%B1&oq=USB+Ses+Kart%C4%B1&aqs=chrome..69i57j69i65&sourceid=chrome&ie=UTF-8)** **olarak arama yaptığınınızda görebilirsiniz. Ben denemek için en kalitesiz olanlarından bir tane aldım. Bu arada  mikrofon olarak da Snopy&#8217;nin [Sn-330M](http://www.hepsiburada.com/snopy-sn-330m-siyah-masaustu-mikrofon-p-BSUCZLKCSN-330M?magaza=Abtek&wt_gl=cpc.elk.bilgisayar-diger.pla&gclid=Cj0KEQjwi7vIBRDpo9W8y7Ct6ZcBEiQA1CwV2HhBX4I01rjNpumNDw1b9blMPoYtTkJVHaGqle0SvFoaAgVP8P8HAQ) mikrofonunu satın aldım. Uygun fiyatına nazaran harika verim aldım. Satın aldığım kalitesiz Jack dönüştürücü biraz daha sağlam olsa çok daha güzel bir ses kalitesi alacağımı tahmin ediyorum. Eğer ciddi anlamda bu konuda bir çalışmanız olacaksa Creative&#8217;nin [X-Fi Go Pro](http://www.hepsiburada.com/creative-x-fi-go-pro-usb-ses-karti-p-BD304452) modelini tavsiye ederim. Henüz denemedim ama okuduğuma göre alınası bir cihaz.

Bir diğer alternatif ise USB çıkışlı bir mikrofon satın almanız. Ses kalitesi ne kadar iyi olur orası tartışılır, bilemeyeceğim.

Bu arada yeri gelmişken yeni bir kulaklık almayı düşünüyorum. Pioneer&#8217;in [SE-MJ591](http://www.hepsiburada.com/pioneer-se-mj591-siyah-kulakustu-kulaklik-p-BD802315) modelini beğendim. Satın aldığımda deneyimimi burada güncellerim.

## Güncelleme

Uzun bir aradan sonra beni tam olarak tatmin etmese de bir çözüm buldum. Linux Arch tabanlı dağıtımlarda <span class="lang:default highlight:0 decode:true crayon-inline">hda-jack-retask-bz</span> paketini yükleyelim ve üçbirimde <span class="lang:default highlight:0 decode:true crayon-inline ">hda-jack-retask</span>  komutu ile çalıştıralım.

Muhtemelen her cihazda farklı olacaktır bu sorun ve çözümü. Ben deneyerek buldum. **Select a codec** menüsünden ses kartım olan **Realtek ALC256**&#8216;yı seçtim. Sağ menüden ise **show unconnected pins** seçeneğini işaretledim.

Pin ID:0x18 olanı override olarak işaretledim ve Microfone seçtim. Install boot override seçeneği ile başlangıçta ayarların yapılandırılmasını sağladım.

Uçbirimde bir metin editörü ile aşağıdaki dosyayı görüntüleyelim.

<pre class="lang:default decode:true ">/etc/modprobe.d/alsa-base.conf</pre>

İçerisinde bulunan satırları silelim ve aşağıdaki komutla değiştirelim.

<pre class="lang:default decode:true ">options snd-hda-intel model=laptop-dmic,headset-mic</pre>

Yedeklemeyi unutmayın.

Bilgisayarımı yeniden başlattığımda uçbirimde pavucontrol ile ses ayarlarımı görüntüledim. Çıkış ayarlarından dahili mikrofonumu seçtim.

Bu yöntemle dizüstü bilgisayarınızdaki dahili mikrofonu kullanabilirsiniz. Bazılarında Pin ID:0x19 çalışmış. Siz denemelisiniz kendiniz için.

## Olası Sorunlar

Uçbirimde <span class="lang:default highlight:0 decode:true crayon-inline ">pavucontrol</span>  yazdığınızda _&#8220;_**Establishing connection toPulseAudio. Please wait ..**_&#8221; _hatası alabilirsiniz.

Çözüm olarak <span class="lang:default highlight:0 decode:true crayon-inline ">rm -r ~/.pulse</span> komutunu uçbirimde çalıştırın. Bunun ardından <span class="lang:default highlight:0 decode:true crayon-inline ">pulseaudio -k</span> komutu ile servisi durduralım ve <span class="lang:default highlight:0 decode:true crayon-inline ">pulseaudio &#8211;start</span> ile yeniden başlatalım.

Uçbirimde tekrar <span class="lang:default highlight:0 decode:true crayon-inline ">pavucontrol</span> komutunu girdiğinizde gerekli ses ayarlarınızı yapabilirsiniz.

## Pioneer SE-MJ591

**Piooner SE-MJ591** modelini Idefix üzerinden satın aldım. Yanınızda taşımak için harika bir taşıma kutusu mevcut. Müzikleri tüm detayları ile hissedebilirsiniz.

Uzun kullanımda rahatsız etmekte. Ben en fazla iki saat aralıksız kullanabildim. Biraz çıkartıp dinlenmek gerekiyor.

Onun dışında çok memnunum.