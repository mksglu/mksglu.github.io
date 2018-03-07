---
id: 3603
title: Linux Manjaro XFCE Spotify Kurulumu
date: 2017-05-04T18:18:13+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3603
permalink: /linux-manjaro-xfce-spotify-libcurl-openssl-1-0
categories:
  - Linux
tags:
  - Linux
  - Linux Manjaro
---
Linux Manjaro XFCE sistemimde son güncellemeden sonra Spotify kurulumunda hata aldım.

## Olası Hata Çıktısı

<pre class="lang:default decode:true ">could not satisfy depenencies: libcurl-openssl-1.0: requires openssl-1.0 spotify: requires libcurl-openssl-1.0</pre>

Bulunamayan bağımlılıkları yalın halde yüklemek istediğimde ise paket hatası aldım.

## Çözüm

Manjaro forumunda konu ile ilgili bir çözüm buldum.

<pre class="lang:default decode:true">git clone https://aur.archlinux.org/spotify.git
cd spotify
git checkout 28698fb
makepkg -sri</pre>

## Olası Hata Çıktısı

<pre class="lang:default decode:true ">/usr/share/spotify/spotify: /usr/lib/libssl.so.1.0.0: version `OPENSSL_1.0.0' not found (required by /usr/share/spotify/spotify)
/usr/share/spotify/spotify: /usr/lib/libcrypto.so.1.0.0: version `OPENSSL_1.0.0' not found (required by /usr/share/spotify/spotify)
/usr/share/spotify/spotify: /usr/lib/libcurl.so.3: no version information available (required by /usr/share/spotify/spotify)</pre>

## Çözüm

<pre class="lang:default decode:true ">sudo -Rsnc spotify
sudo -Syyuu
sudo pacman -Scc
yaourt -S --m-arg --skippgpcheck --noconfirm libopenssl-1.0-compat
yaourt -S --m-arg --skippgpcheck --noconfirm libcurl-openssl-1.0
yaourt -S spotify</pre>

&nbsp;

## Kaynak

  * <https://forum.manjaro.org/t/trouble-updating-spotify/21723/10>