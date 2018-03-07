---
id: 3957
title: 'CakePHP Xml: Sitemap Oluşturalım'
date: 2017-11-22T02:12:23+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3957
permalink: /cakephp-xml-sitemap
categories:
  - CakePHP
tags:
  - CakePHP
  - CakePHP 3.x Sitemap Create
  - CakePHP Sitemap
---
Merhaba,

PHP çatıları arasında hangisini tercih etmezsin diye sorulursa bir gün CakePHP diyeceğimden kuşkunuz olmasın.

CakePHP üzerine geniş bir bilgim yok aslında. Bunun nedeni ise yine çatının kendisinde saklı. Çok dar ve kısıtlı bir topluluk desteği var. Bunun yanı sıra güncellemelerde gelen metodların çok sık değişmesi ve kullanıcı kitlesinin az olması gibi birçok olumsuz neden sayabilirim. Ve bugün tüm bu olumsuzluklara rağmen <span class="lang:default highlight:0 decode:true crayon-inline">CakePHP 3.x</span> sürümü ile bir çalışma yapacağız.

Bu çalışma kodlarını açıklamak benim için oldukça zorlu olacak. Çünkü yerel sunucumda çalışan sitemap, sunucuda hata verdi. Bu yüzden nerde ne kullanacağımı ben de kestiremiyorum. Birkaç günlük yoğun bir araştırma ile Xml elde ettim ve gelen verimi ekrana bastırmayı başardım.

## Sitemap Paketi

Öncelikle GitHub&#8217;ta CakePHP için yazılmış bir paket bulunmakta. Ben temiz bir CakePHP sürümünü üzerinde değil de zaten kompleks olan bir betik üzerinde çalıştığım için midir yoksa bilgi eksikliğinden midir bilemiyorum paketi çalıştıramadım. Birçok yere mail attım lakin yine de çözüm bulamadım.

Ben paylaşayım, eğer çalıştırmayı başarırsanız mailinizi bekliyorum.

<https://github.com/loadsys/CakePHP-Sitemap>

## Controller

Her çatıda ve her MVC mimarisinde olduğu gibi CakePHP de sağ olsun bize bu güzelliği sunan teknolojilerden. Bazı çatılarda yönlendirme metodları ile controller ve model akışını ayarlayabiliyoruz. Fakat CakePHP de dosya isimlerine göre belirleniyor. O yüzden buna dikkat edelim.

Ana dizinimde <span class="lang:default highlight:0 decode:true crayon-inline">src/Controller</span> içerisinde SitemapController adında bir dosya oluşturuyorum.

<pre class="line-numbers">namespace App\Controller;<code class="language-php">
use App\Controller\AppController;
use Cake\Event\Event;

    class SitemapController extends FrontController 
    {    

        public function initialize() {

            parent::initialize();
            $this-&gt;loadComponent('RequestHandler');     
                        
        } 
        
        public function index() {

            $this-&gt;loadModel('SitemapModel');
            $data = $this-&gt;Sitemap-&gt;find('all');
            $compact = $this-&gt;set(compact('data'));
            
            }  
        
    }</code></pre>

## Model

Model dosyamı oluşturmamın buradaki tek nedeni ORM kullandığım için.tablomu seçmek.

Ana dizinimde <span class="lang:default highlight:0 decode:true crayon-inline">src/Model/Table</span> içerisinde <span class="lang:default highlight:0 decode:true crayon-inline">SitemapTable.php</span> adında bir dosya oluşturuyorum.

<pre class="line-numbers">namespace App\Model\Table;<code class="language-php">
use Cake\ORM\Table;
class SitemapTable extends Table
{
    public function initialize(array $config)
    {
        $this-&gt;table('pages');
    }
}</code></pre>

Benim <span class="lang:default highlight:0 decode:true crayon-inline">pages</span> ismindeki tablomdaki verileri Controller dosyamdaki find metodu ile çekebilirim artık.

Burada yer alan table metodu CakePHP 2.x sürümlerinde setTable imiş galiba.

## View

Bu katmanların isimlerini yabancı dilde yazmaktan hiç hoşlanmasam da mimariye uysun diye mecbur kalıyorum.

Ana dizinimde <span class="lang:default highlight:0 decode:true crayon-inline">src/Template/Sitemap/xml/</span> içerisinde <span class="lang:default highlight:0 decode:true crayon-inline">index.ctp</span> adında bir dosya oluşturuyorum.

<pre class="line-numbers">&lt;?php echo '&lt;?xml version="1.0" encoding="UTF-8"?&gt;'; ?&gt;
&lt;urlset xmlns="http://www.sitemaps.org/schemas/sitemap/0.9" 
xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
xsi:schemaLocation="http://www.sitemaps.org/schemas/sitemap/0.9 
http://www.sitemaps.org/schemas/sitemap/0.9/sitemap.xsd"&gt;
&lt;url&gt;
&lt;loc&gt;&lt;?php echo $this-&gt;Url-&gt;build('/', true);?&gt;&lt;/loc&gt;
&lt;changefreq&gt;weekly&lt;/changefreq&gt;
&lt;priority&gt;0.8&lt;/priority&gt;
&lt;/url&gt;
&lt;?php foreach($data as $key): ?&gt;
&lt;url&gt;
&lt;loc&gt;&lt;?php echo $this-&gt;Url-&gt;build(["controller" =&gt; $key['slug'] ], true);?&gt;&lt;/loc&gt;
&lt;lastmod&gt;&lt;?php echo $key['modified']-&gt;i18nFormat('yyyy-MM-dd'); ?&gt;&lt;/lastmod&gt;
&lt;changefreq&gt;weekly&lt;/changefreq&gt;
&lt;priority&gt;0.5&lt;/priority&gt;
&lt;/url&gt;
&lt;?php endforeach; ?&gt;
&lt;/urlset&gt;</pre>

Burada <span class="lang:default highlight:0 decode:true crayon-inline">pages</span> tablomdan gelen <span class="lang:default highlight:0 decode:true crayon-inline">slug</span> ve <span class="lang:default highlight:0 decode:true crayon-inline">modified</span> kolonlarımı kullandım.

## Routes

URL&#8217;de Xml uzantısına izin vermeli ve sitemap yolumu tanımlamalıyım. Ana dizinimde <span class="lang:default highlight:0 decode:true crayon-inline">config/routes.php</span> dosyamı düzenlemem gerek.

Buradaki <span class="lang:default decode:true crayon-inline ">Router::defaultRouteClass(DashedRoute::class);</span> kodundan hemen sonra <span class="lang:default decode:true crayon-inline">Router::extensions([&#8216;json&#8217;, &#8216;xml&#8217;]);</span> kodunu ekliyorum. Ve hemen aşağısına yeni bir yönlendirme bloğu tanımlıyorum.

<pre class="line-numbers"><code class="language-php">Router::scope(
    '/sitemap.xml',
    ['controller' =&gt; 'Sitemap','action' =&gt; 'index'],
    function ($routes) {
        $routes-&gt;connect(
            '/', 
            ['action' =&gt; 'index']
        );              
    }
);</code></pre>

Ve onun da hemen altına hatalarımızı takip edebilmek için hata ayıklama modunu açıyoruz.

<pre class="line-numbers"><code class="language-php">use Cake\Core\Configure; 
Configure::write('debug',2);</code></pre>

## Sonuç

Ben genelde bu tarz düzenlemeler paylaşmasam da bunu gerekli buldum. Çünkü stabil olmayan bir döküman var ve açıklamalar yeterli değil. Sürümler arasında farklar var. Yerel sunucumda çalışan kodların, uzak sunucuda hata vermesi gibi birçok aksilik yaşadım. Hiçbir anlamı olmayan garip hata kodları var. Bu yüzden CakePHP ile Xml çalışmanız gerektiğinde bu yazı size yardımcı olabilir.

Sevgiler.

## Kaynak ve İleri Okuma:

  * https://stackoverflow.com/questions/35102199/cakephp-3-creating-xml-view
  * https://stackoverflow.com/questions/39212157/when-i-create-a-view-using-xml-layout-in-cakephp-a-head-tag-is-showed
  * https://stackoverflow.com/questions/23408838/cakephp-sitemap-error