---
id: 2112
title: Google Analytics İle Grafiksel Olarak Anlık Ziyaretçi Görüntüleme
date: 2013-12-03T01:36:54+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=2112
permalink: /google-analytics-ile-grafiksel-olarak-anlik-ziyaretci-goruntuleme
views:
  - "6"
categories:
  - PHP
tags:
  - Google Analytics Api Kullanımı
  - Google Analytics Charts kullanımı
---
Merhabalar, Bu** Google Analytics** İle **Anlık** Veri Çekimini Göreceğiz. Bu Olay Sayesinde **Google Analytics** Ziyaret Etmeden Yazdığınız Scriptlerde Anlık **Ziyaretçi Akışını** Görebilirsiniz.

  * <span style="font-size: 1rem; line-height: 1.846153846;">NOT: Localhost&#8217;da Çalışırsanız Muhtemelen cURL Hatası Alacaksınız. Bu Yüzden Hostunuzda Çalışın. Hostunuz da Çalışabilmek Gibi Bir İmkanınız Yok İse php.ini Dosyasında İlgili Satırlarda cURL Ayarlarını Yapılandırın. Google&#8217;den Arastırabılırsınız.</span>

## Profil ID

Ben Aylık Olarak Çekmek İstedim Verilerimi. Öncelikle **Google Analytics** Sitesine Girin. Amacımız **Profil ID** Öğrenmek. Hangi Sitenin Ziyaretçi Verilerini Çekmek İstiyorsanız Ona Tıklayın. URL Kısmında  &#8220;**p**&#8221; Den Sonra Gelen 8 Haneli Numara Sizin **Profil ID**&#8216;niz.

### Örneğin Benim URL Yapım Aşağıda. PROFİL ID:71662332

<pre class="lang:xhtml decode:true">https://www.google.com/analytics/web/?hl=tr&pli=1#realtime/rt-overview/a40380513w69547240p&lt;strong&gt;71662332&lt;/strong&gt;/</pre>

## Düzenlenecek Tek Dosya: &#8216;ayar.php&#8217;

**ayar.php** dosyasında,

<pre class="lang:php decode:true"># Giriş Yaptıgınız Gmail Hesabı ve Şifresi.
		$analytics = new analytics("&lt;strong&gt;info@mkoseoglu.com&lt;/strong&gt;", "&lt;strong&gt;sifre&lt;/strong&gt;");
		$analytics-&gt;useCache();

		# Profil id'sini ayarlayalım
		$analytics-&gt;setProfileById('ga:&lt;strong&gt;71662332&lt;/strong&gt;');</pre>

**Gmail Hesabı**nızı ve **Şifre**nizi. Alt Satırda ga: **PROFİL ID**&#8216;nizi Yazınız.

### Buraya Kadar Tamam. Sıra Geldi Dosyaları İndirmeye.

## Dosyaları İndirin

## <a href="http://yadi.sk/d/QYopf6JrDokVk" target="_blank">http://yadi.sk/d/QYopf6JrDokVk</a>

<span style="color: #ff0000;">Rar Şifresi: mkoseoglu.com</span>

## Ek Olarak Grafik Yapısını Değiştirmek İstersek

#### Düzenlenmesi Gereken Dosya &#8216;index.php&#8217;

**index.php** Dosyasında ,

  * **<span style="color: #ff0000;"><strong>line </strong></span>Yazan Kısmı**** <span style="color: #ff0000;">area</span> **Olarak Değiştirirseniz Farklı Bir Görünüm Elde Edebilirsiniz.

<pre class="lang:php decode:true">plotOptions: {
               &lt;strong&gt; area&lt;/strong&gt;: {
                    pointStart: 1,
                    marker: {
                        enabled: false,
                        symbol: 'circle',
                        radius: 2,
                        states: {
                            hover: {
                                enabled: true
                            }
                        }
                    }
                }
            },</pre>

  * **Yine index.php Dosyamda type: line satırını type:area olarak değiştiriyorum.**

<pre class="lang:php decode:true ">chart: {
                renderTo: 'sayac',
                type: '&lt;strong&gt;area&lt;/strong&gt;'
            }</pre>

## Demo: <a href="http://mkoseoglu.com/depo/api/" target="_blank">http://mkoseoglu.com/depo/api/</a>

#### Kaynaklar:

  * <span style="font-size: 1rem; line-height: 1.846153846;"> </span><a style="font-size: 1rem; line-height: 1.846153846;" href="http://www.hayatikodla.com/google-analytics-api-kullanimi/" target="_blank">http://www.hayatikodla.com/google-analytics-api-kullanimi/</a>
  * <a href="http://www.erbilen.net/347-google-analytics-verileri-ve-grafiksel-gosterimi.html" target="_blank">http://www.erbilen.net/347-google-analytics-verileri-ve-grafiksel-gosterimi.html</a>