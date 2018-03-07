---
id: 3640
title: Linux Manjaro 17 I3WM Topluluk Sürümü Çözümleri
date: 2017-06-11T11:07:27+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3640
permalink: /linux-manjaro-17-i3wm
categories:
  - Linux
tags:
  - Linux I3WM Ekran Çözünürlüğü
  - Linux I3WM Ekran Yırtılması
  - Linux I3WM Klavye
  - Linux I3WM No GLX Extension
  - Linux I3WM Touchpad Tıklama
  - Linux I3WM Türkçe Kaynak
  - Linux Manjaro I3 Kullanımı
---
Esenlikler, [Linux Manjaro topluluğu](https://manjaro.org/2017/03/07/manjaro-i3-community-edition-17-0-released/)nun geliştirdiği ve konfigüre ettiği **I3WM** (pencere/dizin) yöneticisine dair çözümlerimi aktarmaya çalışacağım. Bu makale ben çözümler buldukça güncellenecektir.

<img class="aligncenter size-large wp-image-3654" src="https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-102941_1366x768_scrot-1024x576.png" alt="" width="700" height="394" srcset="https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-102941_1366x768_scrot-1024x576.png 1024w, https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-102941_1366x768_scrot-300x169.png 300w, https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-102941_1366x768_scrot-768x432.png 768w, https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-102941_1366x768_scrot-700x394.png 700w, https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-102941_1366x768_scrot.png 1366w" sizes="(max-width: 700px) 100vw, 700px" />

## Ekran Çözünürlüğü

Kullanıdığınız **dahili** ya da **harici monitör**ün çözünürlüğünü güncellemek ve tanımlamak için **[xrandr](https://wiki.archlinux.org/index.php/xrandr)** komutunu kullanacağız.

Klavyeden <span class="lang:default highlight:0 decode:true crayon-inline ">ctrl+enter</span>  kombinasyonunu kullanarak uçbirimi açalım.

<pre class="lang:default decode:true ">xrandr</pre>

Komutun çıktısı aşağıdakine benzer olmalıdır:

<pre class="lang:default decode:true ">Screen 0: minimum 8 x 8, current 1366 x 768, maximum 32767 x 32767
eDP1 connected primary 1366x768+0+0 (normal left inverted right x axis y axis) 340mm x 190mm
   1366x768      60.05*+
   1280x720      60.00  
   1024x768      60.00  
   1024x576      60.00  
   960x540       60.00  
   800x600       60.32    56.25  
   864x486       60.00  
   640x480       59.94  
   720x405       60.00  
   680x384       60.00  
   640x360       60.00  
DP1 connected 1366x768+0+0 (normal left inverted right x axis y axis) 410mm x 230mm
   1366x768      59.79*+
   1280x1024     75.02    60.02  
   1280x720      60.00  
   1024x768      75.03    60.00  
   800x600       75.00    60.32  
   640x480       75.00    72.81    66.67    59.94  
   720x400       70.08  
   1368x768_60.00  59.88  
HDMI1 disconnected (normal left inverted right x axis y axis)
HDMI2 disconnected (normal left inverted right x axis y axis)
VIRTUAL1 disconnected (normal left inverted right x axis y axis)</pre>

Şu an cihazımın tanımladığı iki adet aygıt bulunmaktadır. Bunlar yukarıda da görülebileceği üzere **DP1** ve **eDP1 (birincil)**&#8216;dir. Bizim tanımlamak ve konfigüre etmek istediğimiz aygıtın isminin <span class="lang:default highlight:0 decode:true crayon-inline ">DP1</span> olduğunu öğreniyoruz.

Ben harici ekranımın çözünürlüğü için <span class="lang:default highlight:0 decode:true crayon-inline ">1366&#215;768</span>  tercih ediyorum. Bu çözünürlüğü tanımlamak için yeni bir mod tanımlamamız gerekmektedir. Uçbirimden aşağıdaki komut ile devam edelim.

<pre class="lang:default decode:true ">cvt 1366 768 60</pre>

Komutun çıktısı aşağıdakine benzer olmalıdır:

<pre class="lang:default decode:true "># 1368x768 59.88 Hz (CVT) hsync: 47.79 kHz; pclk: 85.25 MHz
Modeline "1368x768_60.00"   85.25  1368 1440 1576 1784  768 771 781 798 -hsync +vsync
</pre>

Yeni modumu tanımlayalım.

<pre class="lang:default decode:true ">xrandr --newmode "1368x768_60.00"   85.25  1368 1440 1576 1784  768 771 781 798 -hsync +vsync</pre>

Tanımladığımız modu ekleyelim. Kullanılan <span class="lang:default highlight:0 decode:true crayon-inline ">addmore</span>  parametresinde **DP1** aygıtını tanımladım. Siz, **xrandr** çıktınızda hangi aygıtı kullanmak istiyorsanız onu yazmalısınız.

<pre class="lang:default decode:true ">xrandr --addmode DP1 1368x768_60.00</pre>

Ekrana çıkışını verelim. Bu kez <span class="lang:default highlight:0 decode:true crayon-inline ">output</span>  parametresini kullanalım.

<pre class="lang:default decode:true ">xrandr --output DP1 --mode 1368x768_60.00</pre>

Tanımladığımız harici monitörde görüntünün gelmesi gerekmektedir. Linux&#8217;ta **xrandr** komutunu kullanarak cihazımıza bağlı olan bir monitöre ilgili çözünürlüğü tanımladık ve görüntü çıkışı verdik.

Bu işlemi Linux Manjaro topluluğu I3WM sürümünde <span class="lang:default highlight:0 decode:true crayon-inline ">mod+ctrl+b</span> kombinasyonları ile kullanabileceğimiz bir menüde de gerçekleştirebiliriz.

## Otomatik Tanımlama

[Linux Manjaro Gnome 3.22 Çözümleri](https://www.mkoseoglu.com/linux-manjaro-gnome-3-22-cozumleri) yazımda da kullandığım bir yöntemi tercih edebiliriz. Yalnız fark ettiğim sorun şudur ki XFCE ve Gnome masaüstlerinde cihazı başlattıktan sonra harici monitörü taktığımızda tanımlama ve çözünürlük ayarları başarılı bir şekilde bize yansısa da **I3WM**&#8216;de yukarıdaki yöntemi kullanmanız gerekmektedir.

Uçbirimde aşağıdaki dosyayı görüntüleyelim.

<pre class="lang:default decode:true ">/etc/X11/xorg.conf</pre>

<pre class="lang:default decode:true ">Section "Monitor"
  Identifier   "CRT1"
  ModelName    "PANEL"
  Option       "DPMS"
  VendorName   "LCD"
  HorizSync    31-60
  VertRefresh  40-60
EndSection</pre>

Yukarıda yer alan komutları ekleyelim ve dosyamızı güncelleyelim. Orijinal yazıda ilgili konunun kaynakları yer almaktadır.

## Ekran Yırtılması

Genel ağ (internet) üzerinde bir tarayıcıda gezinirken farenizin tekerleği ile yukarı-aşağı yaptığınızda ekrandaki yırtılmaları fark edebilirsiniz. Bunun için **Compton** kullanacağız.

**Linux Manjaro topluluğu I3WM** sürümünde bizler için bir alias (takma ad) atamış. Uçbirimi açalım ve <span class="lang:default highlight:0 decode:true crayon-inline">comp</span> komutunu girelim. Karşımıza topluluğun yazdığı komutlar çıkmaktadır. Ben bunları kullanmak istemediğim için tamamını sildim ve sadece yırtılmaları önlemek için tanımlanan komutları kullandım.

Uçbirimde direkt olarak görüntülemek isterseniz <span class="lang:default highlight:0 decode:true crayon-inline">~/.config/compton.conf</span>  dosya uzantısını bir metin editörü olarak görüntülemeniz yeterlidir.

<pre class="lang:default decode:true ">backend = "glx";
paint-on-overlay = true;
glx-no-stencil = true;
vsync = "opengl-swc";
unredir-if-possible = true;</pre>

Yukarıda yer alan komutları dosyamıza ekleyelim ve yeniden başlatalım. Yırtılmaların düzeldiğini fark edeceksinizdir.

Klavyede <span class="lang:default highlight:0 decode:true crayon-inline ">mod+t</span>  ile **compton**&#8216;u devre dışı bırakabilir, <span class="lang:default highlight:0 decode:true crayon-inline ">mod+ctrl+t</span>  ile de tekrar devreye alabilirsiniz. Uçbirimde ise <span class="lang:default highlight:0 decode:true crayon-inline ">compton -b</span>  komutunu kullanarak başlatabilirsiniz.

Ve yine topluluğun geliştirdiği <span class="lang:default highlight:0 decode:true crayon-inline ">compton-conf</span>  paketini kurarak grafiksel bir arayüz ile de ayarlarınızı gerçekleştirebilirsiniz.

## Olası Sorunlar

Uçbirimde **compton** komutunu uyguladığınızda <span class="lang:default highlight:0 decode:true crayon-inline ">glx_init(): No GLX extension.</span>  çıktısını alabilirsiniz.

Çözümüne dair edindiğim bilgilere dayanarak söyleyebilirim ki; **Bumblebee** ve **ekran kartı** kulumunu başalarılı bir şekilde gerçekleştirdiğinizde sorun düzelecektir. Bu konuda daha ayrıntılı araştırma için ilgili kaynakları aşağıya bırakıyorum.

  * [Google araması](https://www.google.com.tr/search?q=compton+glx_init()%3A+No+GLX+extension.&oq=compto&aqs=chrome.2.69i59l3j69i57j69i61j69i60.1603j0j4&sourceid=chrome&ie=UTF-8#q=compton+glx+init():+No+GLX+extension.)
  * <https://forum.manjaro.org/t/glx-init-no-glx-extension-when-trying-to-start-compton/18645>
  * <https://bbs.archlinux.org/viewtopic.php?id=221539>

## Touchpad (dokunmatik fare)

Touchpad (dokunmatik fare) üzerinde XFCE ve Gnome masaüstlerinde grafiksel arayüz ile dokunmatik ayarlarını düzenleyebiliyorduk. Ben **I3WM**&#8216;de bunu bulamadığım için bazı düzenlemeler ile sorunu çözeceğiz.

Öncelikle uçbirimi açalım.

<pre class="lang:default decode:true">/usr/share/X11/xorg.conf.d/40-libinput.conf</pre>

<pre class="lang:default decode:true ">Section "InputClass"
Identifier "devname"
Driver "libinput"
MatchIsTouchpad "on"
Option "Tapping" "on"
Option "NaturalScrolling" "true"
Option "TapButton1" "1"
Option "TapButton2" "3"
Option "TapButton3" "2"
Option "VertEdgeScroll" "on"
Option "VertTwoFingerScroll" "on"
Option "HorizEdgeScroll" "on"
Option "HorizTwoFingerScroll" "on"
Option "CircularScrolling" "on"
Option "CircScrollTrigger" "2"
Option "EmulateTwoFingerMinZ" "40"
Option "EmulateTwoFingerMinW" "8"
Option "CoastingSpeed" "0"
Option "FingerLow" "30"
Option "FingerHigh" "50"
Option "MaxTapTime" "125"
EndSection</pre>

Yukarıdaki komutları ilgili dosyamızda tanımlayalım ve cihazı yeniden başlatalım. Tüm fonksiyonların başarılı bir şekilde çalıştığını görebilirsiniz.

Bununla ilgili birkaç kaynak bırakıyorum.

  * <https://wiki.archlinux.org/index.php/Libinput>
  * <https://forum.manjaro.org/t/changes-to-40-libinput-conf-not-working-for-touchpad-speed/22268/6>

## Harici Klavye Ayarları

Linux&#8217;ta klavye ayarları için <span class="lang:default highlight:0 decode:true crayon-inline ">setxkbmap</span> kullanılmaktadır. Benim dizüstü bilgisayarımda harici klavye kullanırken karakter hatası almaya başladım. Bu sorunu çözmek için uçbirimde <span class="lang:default highlight:0 decode:true crayon-inline ">setxkbmap tr</span>  komutunu çalıştırdım. Başarılı bir şekilde Türkçe karakter tanımlaması gerçekleştirildi. Bunu başlangıçta çalıştırmak için ise;

<pre class="lang:default decode:true ">~/.i3/config</pre>

I3WM için tanımlı config dosyamızı bir metin editörü ile görüntüleyelim ve dosyaya aşağıdaki komutu ekleyelim:

<pre class="lang:default decode:true ">exec --no-startup-id setxkbmap tr</pre>

Bilgisayarımızı yeniden başlatabiliriz. Klavye ayarlarımız Türkçe karakter seti ile güncellenmiştir.