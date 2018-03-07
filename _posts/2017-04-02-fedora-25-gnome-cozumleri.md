---
id: 3404
title: Linux Fedora 25 Gnome Çözümleri
date: 2017-04-02T05:00:35+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=3404
permalink: /fedora-25-gnome-cozumleri
categories:
  - Linux
tags:
  - Fedora
  - Linux
---
Merhabalar, Fedora 25 Gnome başlangıcında karşılaşmanızın olası olduğu bazı sorunlardan bahsetmek istiyorum. Fedora 25&#8217;e başlarken de diyebiliriz aslında.

[<img class="aligncenter size-large wp-image-3407" src="http://www.mkoseoglu.com/wp-content/uploads/2017-04-02-04-59-34-ekran-görüntüsü-1024x576.png" alt="" width="700" height="394" srcset="https://www.mkoseoglu.com/wp-content/uploads/2017-04-02-04-59-34-ekran-görüntüsü-1024x576.png 1024w, https://www.mkoseoglu.com/wp-content/uploads/2017-04-02-04-59-34-ekran-görüntüsü-300x169.png 300w, https://www.mkoseoglu.com/wp-content/uploads/2017-04-02-04-59-34-ekran-görüntüsü-768x432.png 768w, https://www.mkoseoglu.com/wp-content/uploads/2017-04-02-04-59-34-ekran-görüntüsü.png 1366w" sizes="(max-width: 700px) 100vw, 700px" />](http://www.mkoseoglu.com/wp-content/uploads/2017-04-02-04-59-34-ekran-görüntüsü.png)

## Sağ Tık İle Yeni Dosya Oluşturma

Bulunduğunuz konumda sağ tık yaparak yeni dosya oluşturabilirsiniz. Bunun için aşağıdaki yönergeleri takip edelim.

Terminalde -sizin dilinize göre değişkenlik gösterebilir- Tempaltes (Şablonlar) dizinine erişelim. Ve ilgili dizinde bir alt satırda yer alan komutu çalıştıralim. Yeniden başlattığınızda eklendiğini görebilirsiniz.

<pre class="lang:default decode:true">cd ~/Templates/
touch ‘New Text File.txt’ && touch ‘New Word File.doc’ && touch ‘New Excel File.xls’

</pre>

## Fedora&#8217;da Masaüstünü Etkinleştirme

Fedora&#8217;da  **Gnome Tweak Tool** yüklemelisiniz. Yüklediğinizde ki Türkçe kullanıyorsanız **İnce Ayar Aracı** olarak geçecektir ismi; masaüstü sekmesinden etkinleştirebilirsiniz. Eğer ki etkinleşmedi ise yazıyı takip edelim.

<pre class="lang:default decode:true ">sudo vi /etc/gdm/custom.conf</pre>

Yukarıdaki komutumuzla birlikte açılan terminalde **S** tuşuna basarak düzenleme moduna alıyoruz.

<pre class="lang:default decode:true ">WaylandEnable=false</pre>

**#WaylandEnable=false **satırının başındaki yorum etkisini kaldırın ve satırı etkinleştirin. Ve [daemon] etiketinin içerisinde, yine WaylandEnable satırının hemen altına aşağıdaki kodu ekleyelim.

<pre class="lang:default decode:true ">DefaultSession=gnome-xorg.desktop
</pre>

Son durumda aşağıdaki gibi olacaktır.

<pre class="lang:default decode:true"># GDM configuration storage

[daemon]
# Uncoment the line below to force the login screen to use Xorg
WaylandEnable=false
DefaultSession=gnome-xorg.desktop

[security]

[xdmcp]

[chooser]

[debug]
# Uncomment the line below to turn on debugging
#Enable=true</pre>

Bilgisayarınızı yeniden başlattığınızda kullanılabilir bir masaüstü sizi bekliyor olacak.

## XAMPP

Bu konuya Manjaro&#8217;da da değinmiştim aslında ama bu kez izin vermek zorunda kaldım. Belki Manjaro&#8217;da da vermişimdir, hatırlamıyorum ama ben yine de paylaşayım.

<blockquote class="wp-embedded-content" data-secret="LwY595so0r">
  <p>
    <a href="https://www.mkoseoglu.com/linux-manjaro-gnome-3-22-cozumleri">Linux Manjaro Gnome 3.22 Çözümleri</a>
  </p>
</blockquote>



<pre class="lang:default decode:true ">chown -hR mksglu:root /opt/lampp/htdocs
chmod 755 -R /opt/lampp/htdocs</pre>

&nbsp;