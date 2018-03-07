---
id: 3579
title: Laravel 5.4 Eloquent Sluggable Kullanımı
date: 2017-05-02T03:53:10+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3579
permalink: /laravel-5-4-eloquent-sluggable-kullanimi-seo
categories:
  - Laravel 5.4
tags:
  - Eloquent Sluggable
  - Laravel
  - Laravel 5.4
  - Laravel 5.4 SEO Uyumlu Link
  - Laravel 5.4 Slug Türkçe Karakter
  - Laravel 5.4 Slugify Kullanımı
  - PHP
---
**Laravel 5.4** ile Eloquent Sluggable paketininin kullanımını inceleyeceğiz. **Eloquent Sluggable**, bizlere &#8220;**SEO**&#8221; dostu link yapısı oluşturmaktadır.

Öncelikle **Laravel** kurulumumuzu gerçekleştirelim. &#8220;**_Laravel_**&#8221; yazısını gördükten sonra **Eloquent Sluggable** kullanımına geçebiliriz. Makalede döküman olarak [GitHub](https://github.com/cviebrock/eloquent-sluggable#) adresini kullancağım. Sizler de GitHub adresinden **Eloquent Sluggable** kullanımına dair çok daha fazla bilgiyi edinebilir, projelerinizde kullanabilirsiniz.

[<img class="aligncenter size-full wp-image-3474" src="https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4.png" alt="" width="2220" height="1125" srcset="https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4.png 2220w, https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4-300x152.png 300w, https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4-768x389.png 768w, https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4-1024x519.png 1024w" sizes="(max-width: 2220px) 100vw, 2220px" />](https://www.mkoseoglu.com/wp-content/uploads/laravel-5.4.png)

## Eloquent Sluggable

**Laravel**&#8216;in kurulu olduğu dizine eriştikten sonra uçbirimde

<pre class="lang:default decode:true ">composer require cviebrock/eloquent-sluggable</pre>

komutunu çalıştıralım. Ve hemen ardından <span class="lang:default highlight:0 decode:true crayon-inline ">config/app.php</span> dosyamızı güncelleyelim.

<pre class="lang:default decode:true ">'providers' =&gt; [
    // ...
    Cviebrock\EloquentSluggable\ServiceProvider::class,
];</pre>

Son olarak; tekrar uçbirimde **Laravel&#8217;**in kurulu olduğu dizinde aşağıda yer alan komutu çalıştıralım.

<pre class="lang:default decode:true ">php artisan vendor:publish --provider="Cviebrock\EloquentSluggable\ServiceProvider"</pre>

Buna benzer bir çıktı aldıysanız kurulumu başarıyla tamamlamışsınız demektir.

<pre class="lang:default decode:true ">Copied File [/vendor/cviebrock/eloquent-sluggable/resources/config/sluggable.php] To [/config/sluggable.php]
Publishing complete.
</pre>

## Modelimizi Güncelleyelim

Modelimizi güncellememiz gerekmektedir. Tabii bunun için öncelikle bir **model** dosyasına ihtiyacımız var. Uçbirimde, **Laravel**&#8216;in kurulu olduğu dizinde aşağıdaki komutu çalıştıralım.

<pre class="lang:default decode:true ">php artisan make:model Article -m</pre>

Sonundaki **-m** parametresi aynı zamanda ismini Article olarak tanımladığımız **model** dosyasına ait bir &#8220;**_Migrate_**&#8221; dosyası da oluşturmaktadır.

<pre class="lang:default decode:true ">Model created successfully.
Created Migration: 2017_05_01_224056_create_articles_table
</pre>

Buna benzer bi çıktı aldıysak başarılı bir şekilde **model** ve **migrate** dosyalarımız oluşmuş demektir.

**Laravel** dizinimizde bulunan **App** klasöründe &#8220;_**Article**_&#8221; isminde **model** dosyamızın başarılı bir şekilde oluşturulduğunu görüyoruz ve dosyanın en üstüne; <span class="lang:default highlight:0 decode:true crayon-inline ">namespace App;</span>  satırının hemen altına şu kodu ekliyoruz:

<pre class="lang:default decode:true ">use Cviebrock\EloquentSluggable\Sluggable;</pre>

**Model** dosyamızın devamını ise aşağıda gösterildiği şekilde güncelliyoruz.

<pre class="lang:default decode:true ">class Article extends Model
{
    use Sluggable;

    protected $table = "articles";

    protected $fillable = [
      'title' , 'body'
    ];

    public function sluggable()
   {
       return [
           'slug' =&gt; [
               'source' =&gt; 'title'
           ]
       ];
   }

 
}</pre>

Buradaki değerlerin anlamlarını irdelemek ve konfigüre etmek için yukarıda paylaştığım pakete ait **GitHub** bağlantısını inceleyebilirsiniz. Burada <span class="lang:default highlight:0 decode:true crayon-inline ">title</span>  alanını döndürmesini sağladık.

## Migrate

**Model** dosyamızı oluşturken aynı zamanda **migrate** dosyamızı da oluşturmuştuk. Şimdi içerisinde ufak bir güncelleme yapalım.

<pre class="lang:default decode:true ">public function up()
    {
        Schema::create('articles', function (Blueprint $table) {
            $table-&gt;increments('id');
            $table-&gt;string('title');
            $table-&gt;string('slug');
            $table-&gt;text('body');
            $table-&gt;timestamps();
        });
    }</pre>

Burada <span class="lang:default highlight:0 decode:true crayon-inline ">slug</span>  olarak tanımladığım alanıma kullanacağımız bağlantı adresimiz eklenecektir. Tabii ki <span class="lang:default highlight:0 decode:true crayon-inline ">title</span>  alanını referans almak şartı ile.

Tablomuzu veritabanına tanımlamadan önce pek tabii bir veritbanımızın olması gerekmekte ve bunu **Laravel**&#8216;e bildirmek durumundayız.

Laravel ana diziminizde bulunan **.env** dosyasını açalım ve ilgili kısımları aşağıdaki gibi düzenleyelim. Ben <span class="lang:default highlight:0 decode:true crayon-inline ">slug</span>  isminde bir veritabanı oluşturdum.

Benim kullanıcı ismim **root** ve **parolam bulunmamakta**. Siz kendinize göre düzenlemeyi unutmayın!

<pre class="lang:default decode:true">DB_CONNECTION=mysql
DB_HOST=127.0.0.1
DB_PORT=3306
DB_DATABASE=slug
DB_USERNAME=root
DB_PASSWORD=</pre>

Bu ayarlarımı kaydettikten sonra **Laravel** dizinimizde açtığımız uçbirimde aşağıdaki komutu çalıştırarak <span class="lang:default highlight:0 decode:true crayon-inline ">config</span>  ayarlarımızı güncelleyelim.

<pre class="lang:default decode:true ">php artisan config:cache
php artisan config:clear</pre>

Şimdi veritabanımıza tablolarımızı ekleyebiliriz.

<pre class="lang:default decode:true ">php artisan migrate
</pre>

Ben bu komutu çalıştırdığımda **Laravel 5.4** ile bir hata aldım. Siz almadı iseniz devam edin. Benim aldığım hata şu şekilde:

<pre class="lang:default decode:true ">[Illuminate\Database\QueryException]                                                                                 
  SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key was too long; max key length is 767 bytes (SQ  
  L: alter table `users` add unique `users_email_unique`(`email`))  

  [PDOException]                                                                                                   
  SQLSTATE[42000]: Syntax error or access violation: 1071 Specified key was too long; max key length is 767 bytes</pre>

Çözüm olarak, **AppServiceProvider.php** dosyamızın en üstüne aşağıdaki kodu ekleyelim.

<pre class="lang:default decode:true ">use Illuminate\Support\Facades\Schema;</pre>

Ve devamında;

<pre class="lang:default decode:true ">public function boot()
     {
         Schema::defaultStringLength(191);
     }</pre>

Dosyamızda bulunan <span class="lang:default highlight:0 decode:true crayon-inline ">boot</span>  fonksiyonunu güncelleyelim. **Tekrar deniyorum.**

<pre class="lang:default decode:true ">php artisan migrate</pre>

Eğer aşağıdakine benzer bir çıktı aldıysanız tablolarınız başarılı bir şekilde eklenmiş demektir.

<pre class="lang:default decode:true">Migration table created successfully.
Migrating: 2014_10_12_000000_create_users_table
Migrated:  2014_10_12_000000_create_users_table
Migrating: 2014_10_12_100000_create_password_resets_table
Migrated:  2014_10_12_100000_create_password_resets_table
Migrating: 2017_05_01_224056_create_articles_table
Migrated:  2017_05_01_224056_create_articles_table
</pre>

<img class="aligncenter size-full wp-image-3582" src="https://www.mkoseoglu.com/wp-content/uploads/tablo1.png" alt="" width="851" height="169" srcset="https://www.mkoseoglu.com/wp-content/uploads/tablo1.png 851w, https://www.mkoseoglu.com/wp-content/uploads/tablo1-300x60.png 300w, https://www.mkoseoglu.com/wp-content/uploads/tablo1-768x153.png 768w" sizes="(max-width: 851px) 100vw, 851px" />
  
<img class="aligncenter size-full wp-image-3581" src="https://www.mkoseoglu.com/wp-content/uploads/tablo.png" alt="" width="1080" height="213" srcset="https://www.mkoseoglu.com/wp-content/uploads/tablo.png 1080w, https://www.mkoseoglu.com/wp-content/uploads/tablo-300x59.png 300w, https://www.mkoseoglu.com/wp-content/uploads/tablo-768x151.png 768w, https://www.mkoseoglu.com/wp-content/uploads/tablo-1024x202.png 1024w" sizes="(max-width: 1080px) 100vw, 1080px" />

## Laravel 5.4 Türkçe Karakter Sorunu

### 1. Yöntem:

 **Laravel 5.4** sürümünde <span class="lang:default highlight:0 decode:true crayon-inline ">str_slug</span> &#8216;ta karakter hatası mevcut. Şöyle ki;

&#8216;ö&#8217; harfimiz &#8216;oe&#8217;, &#8216;ü&#8217; harfimiz ise &#8216;ue&#8217; şeklinde çıkmaktadır. Bunu düzeltmek için <span class="lang:default highlight:0 decode:true crayon-inline ">sluggable.php</span> dosyamızda kırk yedinci satırda güncelleme yapalım.

<pre class="lang:default decode:true ">'method' =&gt; function( $string, $sep  ) {
  return strtolower(str_replace(['ü', 'Ü', 'ö', 'Ö',' '], ['u', 'u', 'o', 'o','-'], $string));
},</pre>

### 2. Yöntem:

**Laravel**&#8216;de karakter setleri üzerine **Slugify** paketini kullanabiliriz.

<pre class="lang:default decode:true ">composer require cocur/slugify</pre>

**Model** dosyamızı açalım.

<pre class="lang:default decode:true ">use Cocur\Slugify\Slugify;</pre>

Yukarıdaki satırı tanımladıktan sonra **model** dosyamıza aşağıdaki satırları ekleyelim.

<pre class="lang:default decode:true ">public function customizeSlugEngine(Slugify $engine, $attribute) {
 return $engine-&gt;activateRuleset('turkish');
}</pre>

Hangi yöntemi kullanacağınız size kalmış.

[Slugify GitHub](https://github.com/cocur/slugify) ve bu sorun üzerine gelişmeleri [buradan](https://github.com/cviebrock/eloquent-sluggable/issues/359) takip edebilirsiniz.

## Test Edelim

**Laravel** dizinimizde açtığımız uçbirimde <span class="lang:default highlight:0 decode:true crayon-inline ">php artisan tinker </span> komutunu çalıştıralım ve sırası ile aşağıdaki komutları takip edelim.

<pre class="lang:default decode:true">namespace App;
$article = new Article
$article-&gt;title ="Merhaba Selam naber?"
$article-&gt;body = "Sana da selam Body"
$article-&gt;save()
Article::all()</pre>

<span class="lang:default highlight:0 decode:true crayon-inline">Article::all()</span> komutumuzun çıktısı aşağıdakine benzer olacaktır.

<pre class="lang:default decode:true ">Illuminate\Database\Eloquent\Collection {#661
     all: [
       App\Article {#665
         id: 1,
         title: "Merhaba Selam naber?",
         slug: "merhaba-selam-naber",
         body: "Sana da selam Body",
         created_at: "2017-05-01 23:58:59",
         updated_at: "2017-05-01 23:58:59",
       },
     ],
   }
</pre>

Görüldüğü üzere; <span class="lang:default highlight:0 decode:true crayon-inline ">slug</span>  alanımız <span class="lang:default highlight:0 decode:true crayon-inline ">title</span>  alanını referans alarak bizlere **SEO** dostu bir link oluşturdu.

&nbsp;

Herkese iyi çalışmalar.

&nbsp;