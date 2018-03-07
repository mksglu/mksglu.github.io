---
id: 3396
title: 'Linux Manjaro Steam Failed To Load Driver: Swrast'
date: 2017-03-28T02:54:04+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=3396
permalink: /linux-manjaro-steam-failed-to-load-driver-swrast
categories:
  - Linux
---
Merhabalar, Manjaro sistemimde bir hata aldım. Çözümü şu şekilde yaptım.

<blockquote class="wp-embedded-content" data-secret="zSekbsShXZ">
  <p>
    <a href="https://www.mkoseoglu.com/linux-manjaro-failed-to-initialize-the-nvidia-gpu-at-pci100">Linux Manjaro Failed to initialize the NVIDIA GPU at PCI:1:0:0</a>
  </p>
</blockquote>



Sorunu çözdükten sonra, **optirun steam** yazdığımda şu şekilde hata aldım.

## Linux Manjaro Optirun Steam

<pre class="lang:default decode:true ">Installing breakpad exception handler for appid(steam)/version(0)
libGL error: No matching fbConfigs or visuals found
libGL error: failed to load driver: swrast</pre>

Çözümü ise **primusrun steam** komutu ile çalıştırarak buldum. Terminalde gerekli paketleri kuralım.

<pre class="lang:default decode:true ">yaourt primusrun</pre>

Size uygun paketi yükledikten sonra Terminalde Steam&#8217;ı çalıştıralım.

<pre class="lang:default decode:true ">primusrun steam</pre>

## Fatal Error: failed to load steamui.so

Eğer ki yukarıdaki gibi çalıştırmak istediğinizde **Fatal Error: failed to load steamui.so **hatası alıyorsanız terminalde şu şekilde çalıştırın:

<pre class="lang:default decode:true ">LD_PRELOAD='/usr/$LIB/libstdc++.so.6 /usr/$LIB/libgcc_s.so.1 /usr/$LIB/libxcb.so.1' primusrun steam</pre>

Ya da;

<pre class="lang:default decode:true ">mv .local/share/Steam{,.old} 
</pre>

Bir diğer çözüm olarak <span class="lang:default highlight:0 decode:true  crayon-inline ">~/.bashrc </span> dosyasına da tanımlayabiliriz.

<pre class="lang:default decode:true " title="~/.bashrc">export LD_PRELOAD='/usr/$LIB/libstdc++.so.6 /usr/$LIB/libgcc_s.so.1 /usr/$LIB/libxcb.so.1'
</pre>

&nbsp;