---
id: 3686
title: 'Kotlin: Koşul İfadeleri'
date: 2017-06-19T09:19:54+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3686
permalink: /kotlin-kosul-ifadeleri
categories:
  - Kotlin
tags:
  - Kotlin
  - Kotlin Dersleri
  - Kotlin IF Kullanımı
  - Kotlin Koşullar
  - Kotlin WHEN Kullanımı
---
[Kotlin](https://www.mkoseoglu.com/etiket/kotlin-dersleri/)&#8216;de şartlı deyimler ve koşul ifadelerini inceleyelim. Bunun için [IF Koşulu](https://www.mkoseoglu.com/etiket/kotlin-if-kullanimi/) ve [WHEN Koşulu](https://www.mkoseoglu.com/etiket/kotlin-when-kullanimi/) üzerinde sözdizimine göz gezdirelim.

## IF Koşulu

Koşullar, yazılım dillerinde önemli bir yere sahiptir. Kullanılan algoritmalarda şartlı deyimler olarak geçen bu ifadeler sayesinde veri çıktılarımıza ve diyagram akışımıza göre süreci düzenleyebiliriz. Türkçe&#8217;de _eğer_ anlamına gelen **IF**, belirttiğimiz bir koşulun gerçekleşmesi durumunda istenen değerin döndürülmesini sağlar. Bununla ilgili hemen birkaç basit sözdizimi görelim.

### Genel Kullanım

<pre class="lang:default decode:true">var max = a 
if (a &lt; b) max = b</pre>

Yukarıdaki örnekte <span class="lang:default highlight:0 decode:true crayon-inline ">max</span> değişkenine varsayılan olarak a değişkeni atanmış ve hemen altında bir if koşulu yazılmıştır. Eğer, <span class="lang:default highlight:0 decode:true crayon-inline ">a</span> değişkeni <span class="lang:default highlight:0 decode:true crayon-inline ">b</span> değişkeninden küçük ise <span class="lang:default highlight:0 decode:true crayon-inline ">max</span> değişkenine <span class="lang:default highlight:0 decode:true crayon-inline ">b</span> değişkeni atansın.

Bunu <span class="lang:default highlight:0 decode:true crayon-inline ">else</span> kullanarak yapalım.

### Else ile Birlikte Kullanalım:

<pre class="lang:default decode:true ">var max: Int
if (a &gt; b) {
    max = a
} else {
    max = b
}</pre>

IF koşulunda <span class="lang:default highlight:0 decode:true crayon-inline ">else</span> ifadesi, tanımlanan koşula uymayan durumlarda kullanılır. Burada <span class="lang:default highlight:0 decode:true crayon-inline ">a</span> değişkeninin <span class="lang:default highlight:0 decode:true crayon-inline ">b</span> değişkeninden büyük olma koşulu tanımlanmış fakat; belirtilen koşula uymadığı için <span class="lang:default highlight:0 decode:true crayon-inline ">else</span> ifadesi geçerli kılınmış, <span class="lang:default highlight:0 decode:true crayon-inline ">max</span> değişkenine <span class="lang:default highlight:0 decode:true crayon-inline ">b</span> değişkeni atanmış.

İfade Biçiminde Yazalım:

<pre class="lang:default decode:true ">val max = if (a &gt; b) a else b
</pre>

## WHEN Koşulu

When ise C benzeri dillerin geçiş operatörü olarak kullanılmakta.

### Genel Kullanım

<pre class="lang:default decode:true">when (x) {
    1 -&gt; print("x == 1")
    2 -&gt; print("x == 2")
    else -&gt; {
        print("x, 1 ya da 2 değildir.")
    }
}</pre>

### Birden Çok Aralık

<pre class="lang:default decode:true">when (x) {
    0, 1 -&gt; print("x == 0 or x == 1")
    else -&gt; print("x, 0 ve 1 aralığında değildir.")
}</pre>

## Kaynak ve İleri Okuma:

  * <https://kotlinlang.org/docs/reference/control-flow.html>