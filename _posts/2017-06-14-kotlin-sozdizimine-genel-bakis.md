---
id: 3667
title: 'Kotlin: Temel Sözdizimine Genel Bakış'
date: 2017-06-14T01:45:53+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3667
permalink: /kotlin-sozdizimine-genel-bakis
categories:
  - Kotlin
tags:
  - Kotlin
  - Kotlin Class Yapısı
  - Kotlin Dersleri
  - Kotlin Fonksiyonlar
  - Kotlin Veri Tipleri
  - Kotlin Yorum Satırları
---
[Kotlin](https://www.mkoseoglu.com/etiket/kotlin-dersleri/) ile ilk uygulamamızı yazalım ve temel seviyede Kotlin sözdizimine genel bir göz gezdirelim.

## Merhaba Dünya

Yazılım dillerinin başlangıç klasiği &#8220;Hello World&#8221; ile başlayalım uygulamamıza. Öncelikle Intellij IDEA yazılımını çalıştıralım.

<span class="lang:default highlight:0 decode:true crayon-inline ">Create New Project</span> &#8216;e tıklayalım ve açılan arayüzde <span class="lang:default highlight:0 decode:true crayon-inline ">Java</span> sekmesi altında <span class="lang:default highlight:0 decode:true crayon-inline ">Kotlin (Java)</span> seçeneğini işaretleyerek <span class="lang:default highlight:0 decode:true crayon-inline ">next</span> diyelim.

Bir sonraki aşamada <span class="lang:default highlight:0 decode:true crayon-inline ">Project name</span>  alanına ilkuygulama yazarak <span class="lang:default highlight:0 decode:true crayon-inline ">finish</span>  diyorum.

Gerekli modüller yüklendiğinde bizleri sade bir arayüz karşılamakta.

<img class="aligncenter size-large wp-image-3668" src="https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-154652_1366x768_scrot-e1497185250578-1024x533.png" alt="" width="700" height="364" srcset="https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-154652_1366x768_scrot-e1497185250578-1024x533.png 1024w, https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-154652_1366x768_scrot-e1497185250578-300x156.png 300w, https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-154652_1366x768_scrot-e1497185250578-768x400.png 768w, https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-154652_1366x768_scrot-e1497185250578-700x364.png 700w, https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-154652_1366x768_scrot-e1497185250578.png 1345w" sizes="(max-width: 700px) 100vw, 700px" />

<span class="lang:default highlight:0 decode:true crayon-inline ">Project</span>  sekmesi altında yer alan uygulama dizininin altında yer alan src dizinine sağ tıklayalım ve <span class="lang:default highlight:0 decode:true crayon-inline ">New</span>  ve <span class="lang:default highlight:0 decode:true crayon-inline ">Kotlin File/Class</span>  yönergelerini takip edelim.

Öncelikle JAVA&#8217;da bunu nasıl yaparız ona bakalım, hemen ardından [Kotlin](https://www.mkoseoglu.com/etiket/kotlin-dersleri/) ile yazalım.

### Java ile &#8220;Merhaba Dünya&#8221;

<pre class="lang:default decode:true ">public static void main(String[] args) {
    System.out.println("Merhaba Dünya!");
}</pre>

### Kotlin ile &#8220;Merhaba Dünya&#8221;

<pre class="lang:default decode:true">fun main(args: Array&lt;String&gt;) {
    println("Merhaba Dünya!")
}</pre>

Kotlin&#8217;de bir diğer yazım biçimi olarak da <span class="lang:default highlight:0 decode:true crayon-inline ">{}</span> kullanmak yerine <span class="lang:default highlight:0 decode:true crayon-inline ">=</span>  operatörü ile daha kısa ifadeler elde edebiliriz. Intellij IDEA üzerine ilgili satırın üzerine <span class="lang:default highlight:0 decode:true crayon-inline ">alt+enter</span>  kombinasyonları ile karşınıza çıkan seçenekte &#8220;_Conver to expression body_&#8221; seçeneği ile bu düzenlemeyi otomatik olarak gerçekleştirebilirsiniz.

### Kotlin ile &#8220;Merhaba Dünya&#8221;

<pre class="lang:default decode:true ">fun main(args: Array&lt;String&gt;) = println("Merhaba Dünya!")</pre>

<img class="aligncenter size-large wp-image-3671" src="https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-170324_1366x768_scrot-e1497189836561-1024x526.png" alt="" width="700" height="360" srcset="https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-170324_1366x768_scrot-e1497189836561-1024x526.png 1024w, https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-170324_1366x768_scrot-e1497189836561-300x154.png 300w, https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-170324_1366x768_scrot-e1497189836561-768x395.png 768w, https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-170324_1366x768_scrot-e1497189836561-700x360.png 700w, https://www.mkoseoglu.com/wp-content/uploads/2017-06-11-170324_1366x768_scrot-e1497189836561.png 1362w" sizes="(max-width: 700px) 100vw, 700px" />

## Kotlin&#8217;de Veri Tipleri

Kotlin&#8217;de veri tiplerinde ondalık sayı, tam sayı ve string ifadeleri inceleyelim. Burada ek anektod olarak değişken tanımlamalarında kullanacağımız <span class="lang:default highlight:0 decode:true crayon-inline ">val</span> ve <span class="lang:default highlight:0 decode:true crayon-inline ">var</span> farkına da değineceğim.

<pre class="lang:default decode:true ">fun main(args: Array&lt;String&gt;) {
    var myDecimal = 0.1  
    var myNumber  = 1    
    var myString: String  
    myString = "Her Şey Çok Güzel Olacak!"
    myString = "En azından hayattayız bu da bir şey be abi."
    val myAnotherString:String
    myAnotherString = "Blog yazmak güzeldir."
}</pre>

Burada <span class="lang:default highlight:0 decode:true crayon-inline ">myDecimal</span> **ondalık** veri tipimizi, <span class="lang:default highlight:0 decode:true crayon-inline ">myNumber</span> **tam sayı** veri tipimizi ve <span class="lang:default highlight:0 decode:true crayon-inline ">myString</span> **string** veri tipimizi temsil etmektedirler.

Bir değişkeni tanımlarken <span class="lang:default highlight:0 decode:true crayon-inline ">var</span> kullandığımızda **mutable** (değişken/değişebilir), <span class="lang:default highlight:0 decode:true crayon-inline ">val</span> kullandığımızda ise **immutable** (değişmez) olmaktadır.

Kod bloğumuzun en sonunda, <span class="lang:default highlight:0 decode:true crayon-inline ">print(myString)</span>  dediğimizde bizlere &#8220;_En azından hayattayız&#8230;_&#8221; çıktısını verir. Fakat böyle bir şeyi <span class="lang:default highlight:0 decode:true crayon-inline ">val</span>  ile yapamayız.

Burada noktalı virgül kullanımı opsiyoneldir.

## Kotlin&#8217;de Class ve Fonksiyon Yapısı

[Kotlin](https://www.mkoseoglu.com/etiket/kotlin-dersleri/) üzerinde basit bir örnek bloğu yazdım. Eminim, zihninizde sözdizimi ve işleyiş biçimi adına faydası olacaktır. Bir class içerisinde fonksiyon tanımladım.

<pre class="lang:default decode:true ">fun main(args: Array&lt;String&gt;) {
    val name:String = "Mert Köseoğlu"
    var obj = Person().Disp(name)
}

class Person {
    fun Disp(name:String) = print("Bu kişinin ismi ${name}")
}</pre>

Burada **Inmutable (değişmez)** <span class="lang:default highlight:0 decode:true crayon-inline ">val</span> ile name değişkenimin **String** bir ifade olduğunu belirttim ve değerine ismimi yazdım. Bir satır altında **obj** değişkenimin içerisinde **Person** classının içerisinde bulunan **Disp** fonksiyonuna değer gönderdik.

**Class Person**&#8216;ın içerisinde tanımladığımız **Disp** fonksiyonunda ise gelen değeri <span class="lang:default highlight:0 decode:true crayon-inline ">print</span>  fonksiyonu ile yazdırdık.

Burada dikkat ederseniz <span class="lang:default highlight:0 decode:true crayon-inline ">${name}</span> tarzında bir ifade kullandım. **String** bir ifade içerisinde değişken tanımlamanız için <span class="lang:default highlight:0 decode:true crayon-inline ">$</span> kullanmanız gerekmektedir. Peki, <span class="lang:default highlight:0 decode:true crayon-inline ">{}</span> kullanmamızın amacı nedir?

<span class="lang:default highlight:0 decode:true crayon-inline">${}</span> ifadesini <span class="lang:default highlight:0 decode:true crayon-inline ">name.lastname</span> tarzında birden fazla dizinin yazılmasında kullanıyoruz.

<pre class="lang:default decode:true ">fun main(args: Array&lt;String&gt;) {
 val b = 10
 val a = 5
 
 print("Bir $a sayısı ile bir $b sayının toplamı ${a+b} dir.")

}</pre>

### Bir Class Oluşturalım

Peki, harici bir **Class** nasıl oluşturabiliriz? Proje dizinimizde <span class="lang:default highlight:0 decode:true crayon-inline ">src</span> üzerinde **New** diyelim ve yeni bir **Package** oluşturalım. Oluşturduğumuz Package&#8217;nin ismi <span class="lang:default highlight:0 decode:true crayon-inline ">com.persons</span> olsun.

Oluşturduğumuz <span class="lang:default highlight:0 decode:true crayon-inline ">com.persons</span> &#8216;ın içerisine yine **New** diyerek **Kotlin File/Class** diyelim ve **Kind** seçeneğinde **Class**&#8216;ı seçelim.

Person içerisinde bulunan Person Class&#8217;ımızı bu dosyanın içerisinde tanımlayalım ve Person içerisinde import edelim.

<pre class="lang:default decode:true ">package com.persons

class Person {
    fun Disp(name:String) = print("Bu kişinin ismi ${name}")
}</pre>

<pre class="lang:default decode:true">import com.persons.Person
import java.awt.PrintJob

fun main(args: Array&lt;String&gt;) {
    val name:String = "Mert Köseoğlu"
    var obj = Person().Disp(name)
}</pre>

Bu sayede harici **Class**&#8216;lar üzerinde de çalışabiliriz.

## Kotlin&#8217;de Yorum Satırları

Birçok yazılım dilinde de kullandığımız sözdizimi burada da geçerli. Burada iki farklı şekilde <span class="lang:default highlight:0 decode:true crayon-inline">// Yorum</span> ve <span class="lang:default highlight:0 decode:true crayon-inline">/* Yorum */</span> olmak üzere yorum satırlarını tanımlayabiliriz.