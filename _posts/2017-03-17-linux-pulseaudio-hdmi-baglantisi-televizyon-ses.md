---
id: 3329
title: 'Linux Mint PulseAudio &#8211; HDMI Bağlantısı'
date: 2017-03-17T02:19:21+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=3329
permalink: /linux-pulseaudio-hdmi-baglantisi-televizyon-ses
categories:
  - Linux
tags:
  - HDMI Televizyondan Ses Gelmiyor Linux
  - Linux
  - Linux HDMI Bağlantısı
  - PulseAudio
---
Merhabalar, bir [**Linux**](http://www.mkoseoglu.com/etiket/linux/) **kullanıcısı** olarak daha önce bir ses denetim aracına ihtiyaç duymamıştım. Taki dizüstü bilgisayarımı **HDMI** bağlantısı ile televizyonuma bağlamak isteyene kadar. Ekranımda bir sorun yoktu fakat **sesi bir türlü televizyona veremedim**. Tam da burada **PulseAudio** derdime derman oldu.

Terminalden **PulseAudio** ses denetim aracını çalıştırdıktan sonra üst menüden **Configuration** sekmesine tıklayınız. Burada size uygun ses kanalını seçerek televizyonunuzdan ses çıkışının keyfini sürebilirsiniz.

<a href="https://apps.ubuntu.com/cat/applications/pavucontrol/" target="_blank">Ubuntu PulseAudio</a>

### Arch

<pre class="lang:default decode:true ">sudo pacman -S pulseaudio pavucontrol</pre>

&nbsp;