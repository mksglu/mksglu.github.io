---
id: 3690
title: Linux Mouse Konfigürasyonu (xinput,xev)
date: 2017-06-18T18:30:50+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3690
permalink: /linux-mouse-konfigurasyonu
categories:
  - Linux
tags:
  - Linux
  - Linux Logitech M720 Triathlon
  - Linux Xev Komutu
  - Linux Xinput Komutu
---
Kullandığınız farenin buton işlevlerini değiştirebilir, farklı görevler atayabilir ve tuş görevlerini yer değiştirebilirsiniz. [Logitech M720 Triathlon](https://www.mkoseoglu.com/etiket/linux-logitech-m720-triathlon/) kullanırken ileri ve geri tuşlarının yerlerini değiştirmem gerekti. Bunun için Linux&#8217;ta **xinput** komutu üzerinde <span class="lang:default highlight:0 decode:true crayon-inline ">lists</span> ve <span class="lang:default highlight:0 decode:true crayon-inline ">set-button-map</span> parametrelerini kullanarak seçili aygıt üzerinde tanımlama yaparken **xev** komutu ile de ilgili butonların hangi ID değerlerini öğreneceğiz.

Öncelikle **xinput** komutunun sözdizimine bir göz gezdirelim:

<pre class="lang:sh decode:true">xinput --lists</pre>

<pre class="lang:sh decode:true">usage :
	xinput get-feedbacks &lt;device name&gt;
	xinput set-ptr-feedback &lt;device name&gt; &lt;threshold&gt; &lt;num&gt; &lt;denom&gt;
	xinput set-integer-feedback &lt;device name&gt; &lt;feedback id&gt; &lt;value&gt;
	xinput get-button-map &lt;device name&gt;
	xinput set-button-map &lt;device name&gt; &lt;map button 1&gt; [&lt;map button 2&gt; [...]]
	xinput set-pointer &lt;device name&gt; [&lt;x index&gt; &lt;y index&gt;]
	xinput set-mode &lt;device name&gt; ABSOLUTE|RELATIVE
	xinput list [--short || --long || --name-only || --id-only] [&lt;device name&gt;...]
	xinput query-state &lt;device name&gt;
	xinput test [-proximity] &lt;device name&gt;
	xinput create-master &lt;id&gt; [&lt;sendCore (dflt:1)&gt;] [&lt;enable (dflt:1)&gt;]
	xinput remove-master &lt;id&gt; [Floating|AttachToMaster (dflt:Floating)] [&lt;returnPointer&gt;] [&lt;returnKeyboard&gt;]
	xinput reattach &lt;id&gt; &lt;master&gt;
	xinput float &lt;id&gt;
	xinput set-cp &lt;window&gt; &lt;device&gt;
	xinput test-xi2 [--root] &lt;device&gt;
	xinput map-to-output &lt;device&gt; &lt;output name&gt;
	xinput list-props &lt;device&gt; [&lt;device&gt; ...]
	xinput set-int-prop &lt;device&gt; &lt;property&gt; &lt;format (8, 16, 32)&gt; &lt;val&gt; [&lt;val&gt; ...]
	xinput set-float-prop &lt;device&gt; &lt;property&gt; &lt;val&gt; [&lt;val&gt; ...]
	xinput set-atom-prop &lt;device&gt; &lt;property&gt; &lt;val&gt; [&lt;val&gt; ...]
	xinput watch-props &lt;device&gt;
	xinput delete-prop &lt;device&gt; &lt;property&gt;
	xinput set-prop &lt;device&gt; [--type=atom|float|int] [--format=8|16|32] &lt;property&gt; &lt;val&gt; [&lt;val&gt; ...]
	xinput disable &lt;device&gt;
	xinput enable &lt;device&gt;
</pre>

Biz, <span class="lang:default highlight:0 decode:true crayon-inline ">xinput set-button-map</span> komutunu kullanacağız.

<pre class="lang:sh decode:true">xinput --list</pre>

Komutumuzun çıktısı şuna benzer olmalıdır:

<pre class="lang:sh decode:true">⎡ Virtual core pointer                    	id=2	[master pointer  (3)]
⎜   ↳ Virtual core XTEST pointer              	id=4	[slave  pointer  (2)]
⎜   ↳ Logitech M720 Triathlon                 	id=11	[slave  pointer  (2)]
⎜   ↳ Logitech K360                           	id=12	[slave  pointer  (2)]
⎜   ↳ Elan Touchpad                           	id=14	[slave  pointer  (2)]
⎣ Virtual core keyboard                   	id=3	[master keyboard (2)]
    ↳ Virtual core XTEST keyboard             	id=5	[slave  keyboard (3)]
    ↳ Power Button                            	id=6	[slave  keyboard (3)]
    ↳ Asus Wireless Radio Control             	id=7	[slave  keyboard (3)]
    ↳ Video Bus                               	id=8	[slave  keyboard (3)]
    ↳ Video Bus                               	id=9	[slave  keyboard (3)]
    ↳ Sleep Button                            	id=10	[slave  keyboard (3)]
    ↳ USB2.0 VGA UVC WebCam                   	id=13	[slave  keyboard (3)]
    ↳ Asus WMI hotkeys                        	id=15	[slave  keyboard (3)]
    ↳ AT Translated Set 2 keyboard            	id=16	[slave  keyboard (3)]
</pre>

**Logitech M720 Triathlon **cihazımın Id değeri 11 gözükmekte. Şimdi, değiştirmek istediğimiz butonların hangi Id değerlerine sahip olduklarını öğrenelim.

<pre class="lang:default decode:true">xev | grep button</pre>

Komutu çalıştırdıktan sonra değiştirmek istediğimiz butonlara tıklayalım ve uçbirime bakalım. Çıktımız şuna benzer olmalıdır:

<pre class="lang:sh decode:true ">state 0x0, button 8, same_screen YES
state 0x0, button 8, same_screen YES
state 0x0, button 9, same_screen YES
state 0x0, button 9, same_screen YES
</pre>

Ben burada Id değeri 8 olan butonum ile Id değeri 9 olan butonumu yer değiştireceğim. Bu sayede işlevleri de yer değiştirmiş olacaktır.

<pre class="lang:default decode:true">xinput set-button-map 11 1 2 3 4 5 6 7 9 8 10 11 12 13 14</pre>

Yukarıdaki komutu uçbirimde çalıştırdığımızda butonların işlevlerinin başarılı bir şekilde yer değiştirdiğini görebiliriz.

Oturumu her yeniden başlattığımızda seçili aygıtın Id değeri değişebilir. Şu anki oturumda Id değeri 11 olan aygıt üzerinde bu işlemi gerçekleştirdik. Bu komutu bir session dosyasında açılışta çalıştırmak istediğinizde hata alma olasılığınız çok yüksek çünkü her zaman Id değeri 11 olmayacaktır.

Bunun için basit bir script kullanalım.

<pre class="lang:sh decode:true">#!/bin/sh
for id in `xinput --list|grep 'Logitech M720 Triathlon'|perl -ne 'while (m/id=(\d+)/g){print "$1\n";}'`; do
    echo "setting device ID $id"
    notify-send -t 10  'Mouse ayarları yapıldı.'
    xinput set-button-map $id 1 2 3 4 5 6 7 9 8 10 11 12 13 14
done</pre>

Burada _Logitech M720 Triathlon _olarak yazdığım aygıt ismi için siz kullanmak istediğiniz aygıtı yazabilirsiniz. For döngüsünde bu aygıtı bulur ve bir regex kuralı ile ilgili satırı parçalayarak bizlere Id değerini verir.

Bu dosyayı dosya.sh olarak kaydedebilir ve başlangıçta çalıştırabilirsiniz.