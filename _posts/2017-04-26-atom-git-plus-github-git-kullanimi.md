---
id: 3473
title: Atom Editör ile Git, GitHub ve Git Plus Kullanımı
date: 2017-04-26T21:44:44+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3473
permalink: /atom-git-plus-github-git-kullanimi
categories:
  - Genel
tags:
  - Git Kullanımı
  - Git Plus Kullanımı
  - Git ve GitHub Kullanımı
  - GitHub Kullanımı
---
Ekip halinde geliştirdiğiniz projelerde **Git** ve **GitHub** kullanımının önemini hatırlatmaya gerek duymadan konu başlığının içeriğinden bahsetmek istiyorum.

Bildiğiniz üzere; popüler metin editörlerinden birisi olan **Atom** şu sıralar çok revaşta. Ben de severek kullanıyorum kendisini. Bazı arayüz çalışan arkadaşlarım Sublime metin editöründen vazgeçmese de ben sunucu bazlı dillerde bir handikabını görmedim. Gerek paket deposu gerekse de pratik kullanımı ile vazgeçilmezimdir. Buna tema desteği de dahil tabii ki.

<img class="aligncenter size-full wp-image-3479" src="https://www.mkoseoglu.com/wp-content/uploads/g4.png" alt="" width="910" height="380" srcset="https://www.mkoseoglu.com/wp-content/uploads/g4.png 910w, https://www.mkoseoglu.com/wp-content/uploads/g4-300x125.png 300w, https://www.mkoseoglu.com/wp-content/uploads/g4-768x321.png 768w" sizes="(max-width: 910px) 100vw, 910px" />

Atom metin editöründe kullanılan işlevsel paketlerden birisi de **Git Plus**. Proje geliştirme aşamasında normal şartlarda uçbirimden uzak sunucu ile bağlantı kurmanız ve değişiklikleri bildirmeniz gerekmektedir. **Git Plus** sayesinde zorlanmadan uzak sunucu kullanabilir ve kolay kullanımı ile **Git** **GitHub** dünyasına adım atabilirsiniz.

Öncelikle **GIT** ve **GitHub**&#8216;ın genel ve evsensel tanımlarına değinelim ve alıntı yapalım.

## GitHub

**GitHub**, sürüm kontrol sistemi olarak **Git** kullanan yazılım geliştirme projeleri için web tabanlı bir depolama servisidir. **GitHub** özel depolar için ücretli üyelik seçenekleri sunarken, açık kaynaklı projeler için ücretsizdir.

**GitLab**&#8216;ta özel depoları da ücretsiz bir şekilde kullanabilirsiniz. Bu yazımızda uzak sunucu olarak **GitHub**&#8216;ı kullanacağız.

## Git

**GIT**; yazılım geliştirme süreçlerinde kullanılan, hız odaklı, dağıtık çalışan bir sürüm kontrol ve kaynak kod yönetim sistemidir. İlk sürümü Linux çekirdeği&#8217;nin geliştirilmesinde kullanılmak üzere geliştirilmiştir.

## 

### Git Kullanımı

Öncelikle uzak sunucuda bir depomuzun olması gerekli. Bunun için GitHub hesabımıza giriş yapalım ve <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">Create a new repository</span> bağlantısına tıklayarak yeni bir depo oluşturalım.

Depomuzun ismini oluştururken boşluk bırakmamaya özen gösterelim. Ben <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">git-plus-kullanimi</span> isminde bir depo oluşturdum kendime.

Bilgisayarınızda **GIT** yüklü değil ise yükleyelim. Ben Linux Manjaro kullanıcısıyım ve AUR&#8217;dan rahatlıkla indirip kurabiliyorum.

Yerel sunucumda **git-plus-kullanimi** isminde bir klasör oluşturdum ve içerisine PHP dosyamı ekledim.

Uçbirimimi açıyorum. Klasörün bulunduğu dizine geçiş yapıyorum. <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">pwd</span>  <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">ls</span>  ve <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">cd</span>  komutları yardımcı olabilir bu işlemde bizlere.

Şimdi aşağıda yeni bir depo oluşturalım.

<pre class="lang:default decode:true ">git init</pre>

Uçbirimde şuna benzer bir çıktı almanız gerek. &#8220;<span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">Initialized empty Git repository in /opt/lampp/htdocs/git-plus-kullanimi/.git/</span> &#8221;

Şimdi sistemimizde tanımladığımız **parola** ve **kullanıcı ismi**nin kaydedilmesini sağlamak için <span class="font:monaco lang:default highlight:0 decode:true crayon-inline ">git-credential-store</span> komutunu kullanacağız:

<pre class="lang:default decode:true ">git config credential.helper store</pre>

Güvenlik önlemi almak isterseniz; bir önbellekleme tanımlayabilirsiniz.  Biz devam edelim. Şu anki dalımızı güncelleyelim:

<pre class="lang:default decode:true ">git config --global push.default current</pre>

Uzak sunucumuzda bulunan depomuzun adresini keydedelim:

<pre class="lang:default decode:true ">git remote add origin https://github.com/mkoseoglu/git-plus-kullanimi.git
</pre>

Bulunduğumuz dizindeki tüm dosyaları ekleyelim:

<pre class="lang:default decode:true ">git add --all</pre>

Yerel sunucumuza teslim edelim:

<pre class="lang:default decode:true ">git commit -m "Git Plus Kullanımı Atom"</pre>

Uzak sunumuza gönderelim:

<pre class="lang:default decode:true ">git push -f origin master</pre>

Bizden kullanıcı adımızı ve parolamızı isteyecektir. Uçbirimde yazalım.

  * Username for &#8216;https://github.com&#8217;: mkoseoglu
  * Password for &#8216;https://mkoseoglu@github.com&#8217;: parolam

Uçbirimde parolamızı yazarken ekranda güvenlik önlemi olarak bir şey gözükmez. Siz yazın ve enter tuşu ile devam edin.

Şu şekilde bir çıktı aldım:

<pre class="lang:default decode:true">Counting objects: 3, done.
Delta compression using up to 4 threads.
Compressing objects: 100% (2/2), done.
Writing objects: 100% (3/3), 291 bytes | 0 bytes/s, done.
Total 3 (delta 0), reused 0 (delta 0)
To https://github.com/mkoseoglu/git-plus-kullanimi.git
 + b038c9d...c6a69fc master -&gt; master (forced update)
</pre>

Şimdi **GitHub** hesabında oluşturduğumuz depomuzu kontrol edelim. Başarılı bir şekilde dosyalarınızı gönderdiğinizi görebilirsiniz. **Atom Git Plus** kullanımı ile devam edelim.

## Git Plus Kullanımı

Atom metin editörüm ile git-plus-kullanimi ismindeki klasörümü açıyorum. Paket yükleme alanında git-plus olarak arama yapıyorum ve yüklüyorum. Paketi direkt indirmek ve kurmak isteyenler için bağlantı:

  * <https://atom.io/packages/git-plus>

Atom editörümü yeniden başlatıyorum. Şimdi oluşturduğum PHP dosyamda bir değişiklik yapıyorum.

<img class="aligncenter size-full wp-image-3476" src="https://www.mkoseoglu.com/wp-content/uploads/gg.png" alt="" width="685" height="209" srcset="https://www.mkoseoglu.com/wp-content/uploads/gg.png 685w, https://www.mkoseoglu.com/wp-content/uploads/gg-300x92.png 300w" sizes="(max-width: 685px) 100vw, 685px" />

Görselde de görüldüğü üzere; değişiklik yaptığım dosyanın rengi sol kısımdaki alanımda belirdi. Şimdi değişiklikleri uzak sunucumuza gönderelim.

Paketler sekmesinden **Git Plus**&#8216;a geliyorum ve **Add All + Commit + Push** seçeneğine tıklıyorum. Karşıma bir commit dosyası açıldı.

[<img class="aligncenter size-full wp-image-3477" src="https://www.mkoseoglu.com/wp-content/uploads/g2.png" alt="" width="693" height="240" srcset="https://www.mkoseoglu.com/wp-content/uploads/g2.png 693w, https://www.mkoseoglu.com/wp-content/uploads/g2-300x104.png 300w" sizes="(max-width: 693px) 100vw, 693px" />](https://www.mkoseoglu.com/wp-content/uploads/g2.png)

Yaptığım değişikleri yazdım ve **CTRL+S** kombinasyonu ile kaydettim. Başarılı bir şekilde uzak sunucuma gönderildi. Kontrol edelim hesabımızı tekrar.

[<img class="aligncenter size-full wp-image-3478" src="https://www.mkoseoglu.com/wp-content/uploads/g3.png" alt="" width="869" height="210" srcset="https://www.mkoseoglu.com/wp-content/uploads/g3.png 869w, https://www.mkoseoglu.com/wp-content/uploads/g3-300x72.png 300w, https://www.mkoseoglu.com/wp-content/uploads/g3-768x186.png 768w" sizes="(max-width: 869px) 100vw, 869px" />](https://www.mkoseoglu.com/wp-content/uploads/g3.png)

Evet. Git Plus sayesinde daha düzenli kod yazabilirsiniz. Herkese iyi çalışmalar.

## Kaynak:

  * https://git-scm.com/docs/git-credential-store
  * http://stackoverflow.com/questions/11403407/git-asks-for-username-everytime-i-push
  * https://makandracards.com/makandra/8039-git-how-to-configure-git-to-push-only-your-current-branch