---
id: 3380
title: Linux Manjaro Gnome 3.22 Çözümleri
date: 2017-03-22T04:48:57+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=3380
permalink: /linux-manjaro-gnome-3-22-cozumleri
full_width_featured_image_disabled:
  - "1"
categories:
  - Linux
tags:
  - Linux
  - Linux Arch
  - Linux Arch Manjaro
---
Merhabalar, uzun zaman sonra **Ubuntu Mint**&#8216;ten ayrılarak **Arch Manjaro**&#8216;ya geçiş yaptım. Sisteminiz en temel gereksinimlere işlevsel bir şekilde yanıt vermediğinde sizler de tıpkı benim yaptığım gibi farklı dağıtımlara yönelebilirsiniz.

Bu yazımda, Manjaro üzerinde karşılaştığım sorunları listeleyeceğim. Bu sorunları tek tek yazmaktansa tek bir yazıda toplamak daha mantıklı geldi. SEO&#8217;nun canı cehenneme, önemli olan okuyucular diyorum ve karşılaşmanız muhtemel sorunları klavyem yazdığınca açıklamaya çalışacağım.

[<img class="aligncenter size-large wp-image-3385" src="http://www.mkoseoglu.com/wp-content/uploads/2017-03-22-05-49-27-ekran-görüntüsü-1024x576.png" alt="" width="700" height="394" srcset="https://www.mkoseoglu.com/wp-content/uploads/2017-03-22-05-49-27-ekran-görüntüsü-1024x576.png 1024w, https://www.mkoseoglu.com/wp-content/uploads/2017-03-22-05-49-27-ekran-görüntüsü-300x169.png 300w, https://www.mkoseoglu.com/wp-content/uploads/2017-03-22-05-49-27-ekran-görüntüsü-768x432.png 768w, https://www.mkoseoglu.com/wp-content/uploads/2017-03-22-05-49-27-ekran-görüntüsü.png 1366w" sizes="(max-width: 700px) 100vw, 700px" />](http://www.mkoseoglu.com/wp-content/uploads/2017-03-22-05-49-27-ekran-görüntüsü.png)

## Nvidia Çözünürlük Ayarları

Meraktan, terminalde sudo nvidia-xconfig komutunu çalıştırdım. Kendisi bana xorg.conf dosyasını oluşturdu. Oluşan dosyada çözünürlüğüm 864x olarak gözükmekteydi.

Terminalde dosyamızı açalım.

<pre class="lang:default decode:true ">sudo nano /etc/X11/xorg.conf
</pre>

Ve ilgili kısmı şu şekilde güncelleyelim.

<pre class="lang:default decode:true ">Section "Monitor"
  Identifier   "CRT1"
  ModelName    "PANEL"
  Option       "DPMS"
  VendorName   "LCD"
  HorizSync    31-60
  VertRefresh  40-60
EndSection</pre>

Kaynak:

  * [https://wiki.archlinux.org/index.php/SiS#SiS\_671\_card](https://wiki.archlinux.org/index.php/SiS#SiS_671_card)
  * <http://www.randomshouting.com/2012/12/09/How-to-override-the-screen-resolution.html>

## Bumblebee Kurulumu

Öncelikle kartımızın **hibrit** olduğunu teyit edelim.

<pre class="lang:default decode:true ">lspci | grep -E "VGA|3D"
</pre>

**Multilip** deposu etkin değil ise etkinleştirelim.

<pre class="lang:default decode:true ">sudo nano /etc/pacman.conf
</pre>

<pre class="lang:default decode:true ">[multilib]
SigLevel = PackageRequired
Include = /etc/pacman.d/mirrorlist
</pre>

Sistemi güncelleyelim.

<pre class="lang:default decode:true ">sudo pacman -Syyu
</pre>

Sistemi güncelledikten sonra **xf86-video-intel** sürücüsü kurulu ise kaldıralım.

<pre class="lang:default decode:true ">sudo pacman -Ss xf86-video-intel</pre>

Yukarıdaki kod ile yüklü olup olmadığını kontrol edelim. Terminal çıktınızda **[installed]** ya da **[kurulu]** yazıyorsa kaldıralım.

<pre class="lang:default decode:true ">sudo pacman -R xf86-video-intel
</pre>

Kurulum paketlerini yükleyelim.

<pre class="lang:default decode:true ">sudo pacman -S bumblebee mesa xf86-video-intel nvidia lib32-nvidia-utils bbswitch nvidia-utils
</pre>

Kullanıcımızı **bumblebee** grubuna ekleyelim.

<pre class="lang:default decode:true ">sudo gpasswd -a $USER bumblebee
</pre>

**Bumblebee** servisini sistem açılırken etkinleştirelim.

<pre class="lang:default decode:true ">sudo systemctl enable bumblebeed.service
</pre>

#### Bilgisayarı yeniden başlatalım.

Terminal çıktısında **bumblebee** yer alıyorsa başarıyla gruba dahil etmişizdir.

<pre class="lang:default decode:true ">groups</pre>

**Bumblebee** servisinin durumunu görüntüleyelim. **active (running)** ve **enabled** ibarelerini görüyorsanız sorunsuz çalışıyor demektir.

<pre class="lang:default decode:true">systemctl status bumblebeed
</pre>

&nbsp;

Sizde kurulu olabilir ama bende değildi. [**VirtualGL**](https://cdn.rawgit.com/VirtualGL/virtualgl/2.5/doc/index.html#hd006) kuralım.

<pre class="lang:default decode:true ">yaourt -S virtualgl</pre>

Şimdi test edelim. **Nvidia** ekran kartı ile çalıştırmak istediğiniz uygulamaları terminalde çalıştırmadan önce başına **optirun** yazıyoruz ve ikinci argüman olarak da uygulamanın ismini yazıyoruz. **VGA** ve **Nvidia** farkını **FPS** ile test edebilirsiniz.

<pre class="lang:default decode:true ">glxspheres64
optirun glxspheres64
</pre>

#### Steam Yükleme

Yine **optirun steam** yazarak başarılı bir şekilde Steam kurabilirsiniz.

Ek Olarak:

  * https://forum.manjaro.org/t/optirun-cannot-access-secondary-gpu-error-xorg-ee-nouveau-0-drm-failed-to-set-drm-interface-version/15651
  * https://forum.manjaro.org/t/bumblebee-could-not-enable-discrete-graphics-card/16728/6

## PCIe Bus Error

Bu sorunu Mint ile de yaşamıştım. Boot ekranında bir dizi tekrar eden &#8220;PCIe bus error&#8230;&#8221; hatası görebilirsiniz. Genelde hibrit ekran kartı kullananlardan sık karşılaşılan bir sorun.

Boot ekranında e tuşuna basarak grub düzenleyici üzerinden de yapabilirsiniz ama ben manuel olanını göstereceğim. Çünkü onu beceremedim. Bilen bana da öğretsin, vardır bir olayı onun da.

<pre class="lang:default decode:true ">sudo nano /etc/default/grub</pre>

Karşımıza çıkan nano düzenleyicide ilgili satırı aşağıdaki gibi güncelliyoruz.

<pre class="lang:default decode:true">GRUB_CMDLINE_LINUX_DEFAULT="quiet splash pci=nomsi"</pre>

Şimdi **Grub güncelleyelim**.  Burası önemli Grub üzerinde yaptığınız her değişiklikten sonra güncellemeniz gerekmekte.

<pre class="lang:default decode:true ">grub-mkconfig -o /boot/grub/grub.cfg</pre>

Şimdi yeniden başlatabilirsiniz.

<pre class="lang:default decode:true">reboot</pre>

Eğer ki hata almaya devam ederseniz **pci=noaer **olarak deneyin.

Kaynak:

  * <http://askubuntu.com/questions/771899/pcie-bus-error-severity-corrected>
  * <https://wiki.archlinux.org/index.php/kernel_parameters>

#### Bluetooth

Yine boot ekranında Bluetooth sürücüsü hakkında bir hata satırı vardı. Bunun üzerine yaptığım araştırmalarda bir çözüm buldum. Boot ekranında sorun çözüldü bende. Sizinle de paylaşayım hemencecik.

<pre class="lang:default decode:true ">sudo nano /etc/pacman.conf</pre>

Yine  nano düzenleyicimizde;

<pre class="lang:default decode:true "># Pacman won't upgrade packages listed in IgnorePkg and members of IgnoreGroup
IgnorePkg   = bluez,bluez-qt,bluedevil,bluez-libs</pre>

Yukarıda yer alan satırı bulduktan sonra IgnorePkg taşıyıcısına **bluez,bluez-qt,bluedevil,bluez-libs **parametrelerini girin.

CTRL+x kombinasyonu ile kaydediyoruz.

Kaynak:

  * <https://forum.manjaro.org/t/bluetooth-won-t-receive-files-but-sends-them-ok/10540/3>

## Teamviewer

Şimdi dürüst olmak gerekirse tam olarak verdiği hatayı hatırlamıyorum. Yalnız şunu iyi biliyorum ki çalışmayacak abi.

Öncelikle, önceden kurduysanız Teamviewer&#8217;i silelim.

<pre class="lang:default decode:true ">sudo rm -rf /etc/teamviewer*
rm -rf ~/.config/teamviewer*</pre>

AUR paket yükleyici ile Teamviewer&#8217;in son sürümünü yükleyelim.

<pre class="lang:default decode:true ">sudo systemctl enable teamviewerd.service
sudo systemctl start teamviewerd.service</pre>

Ve sonra yukarıdaki komutları terminalde çalıştıralım.

Kaynak:

  * <https://aur.archlinux.org/packages/teamviewer/>

## Redshift

Gece çalışanlar için özellikle gözleri almasın diye kullanılan bir araç var. F.lux olarak geçmekte ismi. Ubuntu&#8217;da bunu kullanırdım ama Manjaro&#8217;da yükleyemedim. Buna istinaden bir alternatif buldum. O da Redshift! Kendisi gayet başarılı.

AUR paket yöneticimizden yükledikten sonra &#8220;Trying location provider `geoclue2'... Using provider`geoclue2&#8242;&#8221; şeklinde hata alacaksınız.

<pre class="lang:default decode:true ">sudo nano /etc/geoclue/geoclue.conf</pre>

Terminalde yukarıdaki kodu çalıştırdıktan sonra açılan düzenleyicide aşağıdaki kodları ekliyoruz:

<pre class="lang:default decode:true ">[redshift]
allowed=true
system=false
users=</pre>

Tamamdır. Şimdi kullanabilirsiniz. Başlangıçta çalıştır demeyi de unutmayın, kullanın. Göz sağlığı önemli.

Kaynak:

  * <https://github.com/jonls/redshift/issues/158>

## Keyring Chrome

Chrome her açtığımda keyring diyalog penceresinde benden root şifremi istiyordu. Muazzam topluluk buna da bir çözüm bulmuş.

<pre class="lang:default decode:true ">sudo mv /usr/bin/gnome-keyring-daemon /usr/bin/gnome-keyring-daemon-old 
sudo killall gnome-keyring-daemon</pre>

Kaynak:

  * <https://forum.manjaro.org/t/keyring-for-chromium-is-pointless/4328>

## PHP 7 + Apache2 + MySQL (XAMPP)

Şimdi önce kendimden gayet emin bir şekilde Apache&#8217;yi manuel olarak kurdum. Gerekli birkaç ayar çektim. Sonra PHP kurdum. Gayet güzel. Sunucuya PHP tanıtamadım. Uğraş uğraş, dedim yeter. XAMPP getirin bana. Çok güzel çare oldu.

Öncelikle buradan indirin:

  * <https://www.apachefriends.org/index.html>

Kurulum adımlarını [bu](https://wiki.archlinux.org/index.php/xampp) sayfadan takip edebilirsiniz. Autostart yapmayı unutmayın, üşenenlere büyük güzellik.

## Dil Ayarları

**Manjaro Settings Manager **aracı ile dil seçeneklerini özelleştirebilirsiniz.

## Masaüstü Ayarları

**Tweak Tools **aracı ile masaüstüne ikon ekleyebilirsiniz.