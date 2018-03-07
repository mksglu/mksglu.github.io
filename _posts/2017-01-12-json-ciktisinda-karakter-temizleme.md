---
id: 3245
title: JSON Çıktısında Karakter Temizleme
date: 2017-01-12T20:43:01+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=3245
permalink: /json-ciktisinda-karakter-temizleme
categories:
  - PHP
tags:
  - Jquery Json
  - Json
  - PHP
  - PHP JSON \r\n
  - PHP JSON array_map Fonksiyonu
  - PHP JSON Dizi
  - PHP JSON Temizleme
---
Esenlikler, ufak bir çalışma için **JSON** çıktısına ihtiyaç duydum. Bu çıktı sonucunda temizlenmesi gereken karakterler baş gösterdi. Bu konuda birçok forumda çözülemeyen başlıklara rastladım. Blogumda paylaşmanın uygun olacağını düşündüm. Sizlerle birlikte, adım adm **JSON** çıktımızı dizi üzerinde değiştirmemize olanak sağlayacak kodlarımızı yazalım. **JSON** konusuna burada fazla değinmeyeceğim. Eğer ki bu konuda bilgi sahibi olmak isterseniz [**dökümanlardan**](http://www.json.org/json-tr.html) faydanabilirsiniz.

Çıktımızda istenmeyen karakterleri dizi (array) içerisinde **array_map** fonksiyonu içinde **preg_raplace** fonksiyonu ile değiştireceğiz. Öncelikle, **array_map** fonksiyonundan bahsedelim biraz.

## PHP array_map Fonksiyonu:

Bir dizimizde, tüm elemanları istediğimiz koşullarda işlevselleştirerek tekrar bize döndürmesini sağlayan ve birçok işimizde bizlere yardımcı olan fonksiyonumuzdur kendileri.

### Kullanımı:

<pre class="lang:php decode:true ">array_map ($işlev , dizi)</pre>

PHP array_map fonksiyonu, iki parametre almaktadır.

Birinci parametremiz, her dizinin her elemanına uygulanan geri çağırım işlevidir. İkinci parametremiz ise, elemanları **$islev** tarafından işlenecek dizidir. Bizlere dönen değer ise yine dizi olacaktır.

## PHP preg_replace Fonksiyonu:

Kullanılan düzenli ifadeye göre dizgemizde değişiklik yapar.

### Kullanımı:

<pre class="lang:php decode:true ">preg_replace("sablon", "yenisi", "konu");</pre>

**Konu** dizgesini **sablon** ile eşleştirir ve bulduklarını **yenisi** ile değiştirir.

## JSON:

**JSON** kodlarımızın tamamını paylaşıyorum ki mantığında çelişkiye düşmeyin. Yukarıda bahsettiğim fonksiyon ile ilgili farklı kaynaklardan örneklere ulaşabilirsiniz.

### Kodlar:

<pre class="lang:php decode:true ">&lt;?php

header("Content-type: application/json; charset=utf-8");
$db = "Veritabanı"; 
$hatObje = ["hat"=&gt;null];
$hatDizi = [];
try {
	$baglan = new PDO("mysql:host=localhost;dbname=$db;charset=utf8","root","");
} catch ( PDOException $e ){
	die($e-&gt;getMessage());
}
$satirlar = $baglan-&gt;query("SELECT * FROM hatlar", PDO::FETCH_ASSOC);
foreach ($satirlar as $satir) {

  $hatDizi[count($hatDizi)] = $satir;


}
$hatDizi = array_map(
    function($str) {
        return preg_replace("!\r?\n!", " ", $str);
    },
    $hatDizi
);
 $hatObje["hat"] = $hatDizi;

echo $ilk = json_encode($hatObje, JSON_UNESCAPED_UNICODE | JSON_PRETTY_PRINT);
?&gt;
</pre>

JSON çıktımızı yukarıda yer alan kod bloğuna benzer bir mantık çerçevesinde kullanırsak **\r\n** gibi karakterleri temizlemiş oluruz.

&nbsp;

&nbsp;