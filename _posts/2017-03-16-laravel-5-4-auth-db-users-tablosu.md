---
id: 3326
title: Laravel 5.4 Auth DB Users Tablosu
date: 2017-03-16T21:23:03+00:00
author: Mert Köseoğlu
layout: post
guid: http://www.mkoseoglu.com/?p=3326
permalink: /laravel-5-4-auth-db-users-tablosu
categories:
  - Laravel 5.4
tags:
  - Laravel 5.4 E-Mail Kontrolü
  - Laravel 5.4 Users Tablo Yeniden Adlandırma
  - Laravel 5.4 Yönetim Paneli
---
**Laravel 5.4**&#8216;de yönetim paneli kullanımında **giriş** ve **çıkışlarda** **Auth** mekanizmasını kullanıyoruz. **Migration** ile oluşturduğumuz veritabanı şemasında tablo ismi **users** olarak gelmekte. Biz peki bunu değiştirmek istersek nasıl bir yol izlemeliyiz?

## Model

Öncelikle model dosyamızda aşağıdaki güncellemeyi yapalım ve tablo ismini belirleyelim.

<pre class="lang:php decode:true">/**
     * The database table used by the model.
     *
     * @var string
     */
    protected $table = 'newUsersTable';

</pre>

## Config

Sonraki adımda config içerisinde yer alan auth.php dosyamızı güncelleyelim.

<pre class="lang:php decode:true ">/*
    |--------------------------------------------------------------------------
    | Authentication Table
    |--------------------------------------------------------------------------
    |
    | When using the "Database" authentication driver, we need to know which
    | table should be used to retrieve your users. We have chosen a basic
    | default value but you may easily change it to any table you like.
    |
    */
 
    'table' =&gt; 'newUsersTable',
</pre>

## Validation

En çok yapılan hata da burası. Ben dahil birçok kişinin yapmayı unuttuğu güncelleme. E mail alanında yapılan kontrollerin sağlandığı tablo ismi.

Dizin: app/Http/Controllers/Auth/AuthController.php

<pre class="lang:php decode:true ">protected function validator(array $data)
    {
        return Validator::make($data, [
            'name' =&gt; 'required|max:255',
            'email' =&gt; 'required|email|max:255|unique:newUsersTable',
            'password' =&gt; 'required|confirmed|min:6',
        ]);
    }</pre>

&nbsp;