---
id: 3607
title: 'Linux Arch &#038; Manjaro Yaourt Onay Kaldırma'
date: 2017-05-04T21:30:14+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3607
permalink: /linux-arch-manjaro-yaourt-onay-kaldirma
categories:
  - Linux
---
**Linux Arch** ve **Manjaro** kullanıcıları uçbirimden paket yüklemek istediklerinde paketin düzenlenmesi ve derlenmesine yönelik bir dizi soru ile karşılaşmakta. Bunu seri bir hale getirmek için birkaç parametrede değişiklik yapmak gerek. Ben kullanıyorum ve çok memnun kaldım.

<pre class="lang:default decode:true ">sudo nano /etc/yaourtrc</pre>

Uçbirimde yukarıdaki komutu çalıştıralım ve aşağıdaki yönergeleri takip edelim.

<pre class="lang:default decode:true">NOCONFRIM=1
</pre>

<span class="lang:default highlight:0 decode:true crayon-inline ">Nano</span>  için konuşuyorum, **CTRL+W** ile <span class="lang:default highlight:0 decode:true crayon-inline ">NOCONFRIM</span>  satırını bulalım. 0 olan değerini bir yapalım.

<pre class="lang:default decode:true ">EDİTFILES=O
</pre>

Ve yine <span class="lang:default highlight:0 decode:true crayon-inline ">EDİTFILES</span>  satırını bulalım; <span class="lang:default highlight:0 decode:true crayon-inline ">1</span>  olan değerini <span class="lang:default highlight:0 decode:true crayon-inline "></span>  ile güncelleyelim.

**CTRL+X** ile kaydedip kapatalım.

## Kaynak

  * <https://basarmert.blogspot.com.tr/2015/12/aur-depo-ve-yaourt-onay-istegini.html>