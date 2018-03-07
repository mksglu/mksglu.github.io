---
id: 3446
title: 'Linux Arch &#038; Manjaro CodeIgniter Kurulumu'
date: 2017-04-19T08:38:34+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3446
permalink: /linux-arch-manjaro-codeigniter
categories:
  - CodeIgniter 3.x
  - Linux
  - PHP
tags:
  - CodeIgniter
  - Linux Arch Sistem Dili Türkçe
  - Linux Arch TR Locale
  - Linux Manjaro CodeIgniter
  - PHP
  - PHP CodeIgniter
  - PHP CodeIgniter ::$input
  - PHP CodeIgniter ::$uri
---
**CodeIgniter** kurulumunda GitHub üzerinden ya da resmi siteden son sürümü indirdiğinizde ve çalıştırdığınızda sizi bir <span class="font:monaco lang:default highlight:0 decode:true crayon-inline">Welcome</span> ekranı karşılayacaktır. Bu ekranı gördüğünüzde sorunsuz çalıştığını varsayabilirsiniz; tabii bir **Arch&Manjaro** kullanıcısı değilseniz. Eğer ki **sistem dili Türkçe** olan Linux Arch ya da bir Manjaro kullanıcısı iseniz; muhtemelen CodeIgniter ya da ZN Framework çalışmayacaktır.  Bunun nedeni PHP&#8217;nin standart str fonksiyonlarının çalışmamasıdır. Konunun başlığını bu şekilde belirledim çünkü sorunun kaynağını bilen birisi zaten çözüme de rahatlıkla ulaşabilir. Önemli olan sorunun nereden kaynaklandığını bilemeyen arkadaşları konuya çekebilmek. Gerekli hata kodları etiket olarak dahil edilmiştir.

Şöyle anlatmak gerekirse <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">$this-uri->segment(1)</span> ve <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">$this->input->get(&#8216;q&#8217;)</span> kodları hata verecektir. Burada dikkat ettiğiniz bir nokta var mı? Evet, bildiniz! Burada <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">this</span> anahtarı ile eriştiğimiz sınıf özelliklerinin ikisinde de **i** harfi bulunmakta. Peki, bununla ne ilgisi var? Öncelikle [şurada](https://bugs.php.net/bug.php?id=18556) bu konu ile ilgili açılmış bir bug report bulunmakta. Ona göz atmanızı rica ediyorum. Şimdi biraz daha oturdu gibi konu. Bir dizi içerisinde **URI** ya da **INPUT** anahtarı ilgili PHP fonksiyonlarınca küçültülmek istenilmektedir. Fakat bunu başaramaz ve bu anahtarlar bize **urI** ve **Input **olarak döner ve hata verir.

## Olası Hata Çıktıları:

<pre class="lang:default decode:true">Message: Undefined property: Welcome::$uri

Message: Undefined property: Welcome::$input

Message: Call to a member function segment() on null</pre>

Yukarıdaki hatalardan normal zamanlarda bir çözüm yolu aransaydı <span class="font:monaco lang:default highlight:0 decode:true crayon-inline">$this->load->helper(&#8216;uri&#8217;);</span> satırını _Controller_ dosyamıza dahil etmeyi düşünürdük. Bu tarz bir hatanın olabileceğini kimse düşünemezdi.

## Çözüm Yolları:

Linux sistem dilinde bu tarz dönüşüm ve işlemlerin kontrol merkezinde **CTYPE** bulunmakta. Bizler, **CTYPE**&#8216;ı <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">en_US.UTF8</span>  yaparsak bu sorun çözülecektir.

[<img class="aligncenter size-full wp-image-3448" src="https://www.mkoseoglu.com/wp-content/uploads/17966903_1912078435695629_7955392821469594039_o.jpg" alt="" width="1366" height="768" srcset="https://www.mkoseoglu.com/wp-content/uploads/17966903_1912078435695629_7955392821469594039_o.jpg 1366w, https://www.mkoseoglu.com/wp-content/uploads/17966903_1912078435695629_7955392821469594039_o-300x169.jpg 300w, https://www.mkoseoglu.com/wp-content/uploads/17966903_1912078435695629_7955392821469594039_o-768x432.jpg 768w, https://www.mkoseoglu.com/wp-content/uploads/17966903_1912078435695629_7955392821469594039_o-1024x576.jpg 1024w" sizes="(max-width: 1366px) 100vw, 1366px" />](https://www.mkoseoglu.com/wp-content/uploads/17966903_1912078435695629_7955392821469594039_o.jpg)

Bir diğer çözüm yolu ise <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">en_US.UTF8</span>  yüklü olmak koşulu ile; **LC_CTYPE** veya **LC_ALL** değerini değiştirerek de sorun çözülebiliyor.

## Ek Olarak:

Çözümde benimle birlikte uğraş veren [AnkaraPHP](https://twitter.com/ankaraphp) ekibine ve Eray Aydın&#8217;a teşekkürlerimi iletiyorum.

## Kaynak:

  * https://wiki.archlinux.org/index.php/locale