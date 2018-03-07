---
id: 3347
title: Linux Mint Steam Başlatma Sorunu
date: 2017-03-17T02:03:09+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=3347
permalink: /linux-steam-buton-baslatma-sorunu
categories:
  - Linux
tags:
  - Linux
  - Linux LC_ALL=C
  - Linux Steam Başlamıyor
  - Linux Steam Buton Yok
---
Merhabalar, geçenlerde sıkıntıdan ne yapacağımı bilemez halde iken **Steam**&#8216;dan CS:GO yüklemek istedim. Eskileri yad etmek kötü olmasa gerek diye düşündüm ve satın aldım. **Linux** desteğini bildiğim için de yüreğim ferahtı. Terminalden **Steam**&#8216;ı başlattığımda aşağıdaki gibi bir görünümde beni karşıladı. Maalesef arayüzde buton yok.

![Görüntünün olası içeriği: yazı](https://scontent-otp1-1.xx.fbcdn.net/v/t1.0-9/16708406_1877801635789976_8229237511256985033_n.jpg?oh=0535b1ae4302f9e63193601def963c76&oe=596BF328)

## Çözüm:

Çözüm olarak çok basit, bir satır kodumuz var.

<pre class="lang:default decode:true">LC_ALL=C steam</pre>

Terminalde **Steam**&#8216;ı bu şekilde çalıştırdığınızda başarı ile çalışacaktır.