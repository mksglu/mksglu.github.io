---
id: 3697
title: 'Kotlin: Yineleyiciler &#038; Döngüler'
date: 2017-06-21T17:36:32+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3697
permalink: /kotlin-yineleyiciler-donguler
categories:
  - Kotlin
tags:
  - Kotlin
  - Kotlin Dersleri
  - Kotlin Döngüler
---
[Kotlin](https://www.mkoseoglu.com/etiket/kotlin-dersleri/)&#8216;de yineliyiciler ya da bir başka deyişle döngüler konusu ile devam ediyoruz. **Geleceğin Yazarları**, döngüleri şu şekilde tanımlamış:

&#8220;_Yazılan kodlarda belirli satırların birden fazla tekrar edilmesi istenebilir. Böyle durumlarda döngü yapıları kullanılır. Döngü yapılarında, döngünün kaç kere tekrar edeceği dinamik olarak belirlenebilir. Hatta döngünün tekrarlaması bir koşula bağlanabilir._&#8221;

Biz de bu tanıma bağlı kalarak **Kotlin** üzerinde genel kullanım mantığı ile örnekleme yapalım.

## For

For döngüsü, işlem koşullarının önceden belirli olduğu durumlarda kullanılır. Hemen bir genel kullanım örneği verelim ve sözdizime bakalım.

<pre class="lang:java decode:true ">for (i in 1..10) {
    println(i)
}</pre>

Bu ifadenin çıktısı şuna benzer olmalıdır:

<pre class="lang:default decode:true ">1
2
3
4
5
6
7
8
9
10</pre>

Burada kullanılan <span class="lang:default highlight:0 decode:true crayon-inline ">..</span> operatörü bir aralık belirtir. Buna <span class="lang:default highlight:0 decode:true crayon-inline ">rangeTo</span> fonksiyonu diyoruz. Tam anlamı şu şekilde aslında  <span class="lang:default highlight:0 decode:true crayon-inline ">1 <= i && i <= 10</span> ve yine burada kullanılan <span class="lang:default highlight:0 decode:true crayon-inline ">&&</span> operatörü ve anlamına gelmektedir.

Bir örnek daha verelim. Bu kez sadeleştirilmiş sözdizimi ile gelsin.

<pre class="lang:default decode:true ">for (i in 1..4) print(i)  

for (i in 4..1) print(i)</pre>

Birinci ifade için çıktımız <span class="lang:default highlight:0 decode:true crayon-inline ">1234</span> olurken ikinci ifade için tanımsız olacaktır. Peki, bu aralığın tersini almak mümkün mü? Gayet tabii.

<pre class="lang:default decode:true ">for (i in 4 downTo 1) print(i)</pre>

Burada çıktımızın <span class="lang:default highlight:0 decode:true crayon-inline ">4321</span> olmasını bekleriz.

Peki, **son eleman**ı içermeyen bir aralık oluşturmak istersek bunu nasıl yaparız? <span class="lang:default highlight:0 decode:true crayon-inline">Until</span> fonksiyonu ile.

<pre class="lang:default decode:true ">for (i in 1 until 10) { 
     println(i)
}</pre>

Tam olarak gösterimi ise şu şekilde olmaktadır: <span class="lang:default highlight:0 decode:true crayon-inline ">[1, 10)</span>

## WHILE

&#8220;_Döngüsel işlem veya tekrarlı işlem (iterasyon, İng. iteration), bilgisayarı aynı işlem grubunu belirli bir koşul sağlanana kadar tekrar tekrar yapmak için yönlendirir._&#8221; diye aktarmış Geleceğin Yazarları.

Bu tarz teknik tanımlarda daha evrensel cümleler kullanmaya özen gösteriyorum ki [Türkçe Yazılım](https://www.mkoseoglu.com/turkce-yazilim/)&#8216;da belirli bir kalıp oluşturalım.

While döngüsü kullanımına dair genel kullanım örneği verelim:

<pre class="lang:default decode:true ">while (x &gt; 0) {
    x--
}</pre>

Burada, x değeri 0&#8217;dan büyük olma koşulunu gerçekleştirmeye devam ettiği sürece döngü çalışacaktır.

<pre class="lang:default decode:true ">var i:Int = 1
  while(i &lt;= 10){
  println(i)
  i++
}</pre>

Burada çıktımızın aşağıdaki gibi olmasını bekleriz:

<pre class="lang:default decode:true ">1
2
3
4
5
6
7
8
9
10</pre>

## DO WHILE

**While** döngüsünde belirlenen koşul döngünün başlangıcında bulunmaktadır. Bunun anlamı, koşulun _false_ dönmesi halinde while bloğu çalışmayacaktır. Fakat, bazı zamanlarda while bloğunu bir kere de olsa çalıştırmamız gereken durumlarla karşılaşacağız. Bu tarz durumlarda ise **Do While** ifadesini kullanacağız.

Genel bir kullanım örneği verelim:

<pre class="lang:default decode:true ">var i:Int = 1
do {
  println(i)
  i++
} while(i &lt;= 10)</pre>

## Kaynak ve İleri Okuma

  * <https://kotlinlang.org/docs/reference/control-flow.html>
  * <https://kotlinlang.org/docs/reference/ranges.html>