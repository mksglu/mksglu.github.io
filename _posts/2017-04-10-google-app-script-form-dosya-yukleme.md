---
id: 3409
title: Google App Script Form Oluşturma ve Dosya Yükleme
date: 2017-04-10T01:23:51+00:00
author: Mert Köseoğlu
layout: post
guid: https://www.mkoseoglu.com/?p=3409
permalink: /google-app-script-form-dosya-yukleme
categories:
  - Google Developers
tags:
  - Google App Script Access
  - Google App Script Anyone
  - Google App Script File Upload
  - Google App Script ile Resim Yükleme
  - Google App Script Permisson
  - Google Form Resim Yükleme
---
Merhabalar, **Google Form**&#8216;a dosya yüklemek için gerekli adımları birlikte inceleyelim. Öncelikle **Google App Script** dökümanlarına bir göz atalım.

  * <https://developers.google.com/apps-script/>

## **Google App Script**

GAP ile çevrimiçi hazırladığınız kullanıcı formlarından alınan bilgileri Exel üzerine tutabilir, gruplandırabilir; eklenen fotoğrafları ise ilgili başvuru Id&#8217;si ile Google Driver hesabınızda depolayabilirsiniz.

[<img class="aligncenter size-full wp-image-3413" src="https://www.mkoseoglu.com/wp-content/uploads/google-apps-script.jpg" alt="" width="1280" height="850" srcset="https://www.mkoseoglu.com/wp-content/uploads/google-apps-script.jpg 1280w, https://www.mkoseoglu.com/wp-content/uploads/google-apps-script-300x199.jpg 300w, https://www.mkoseoglu.com/wp-content/uploads/google-apps-script-768x510.jpg 768w, https://www.mkoseoglu.com/wp-content/uploads/google-apps-script-1024x680.jpg 1024w" sizes="(max-width: 1280px) 100vw, 1280px" />](https://www.mkoseoglu.com/wp-content/uploads/google-apps-script.jpg)

## Code.GS

<pre class="lang:default decode:true ">var submissionSSKey = '--ID--';
var folderId        = "--ID--";


function doGet(e) {
  var template    = HtmlService.createTemplateFromFile('form.html');
  template.action = ScriptApp.getService().getUrl();
  return template
  .evaluate()
  .setSandboxMode(HtmlService.SandboxMode.IFRAME)
  .setXFrameOptionsMode(HtmlService.XFrameOptionsMode.ALLOWALL); 
  
}


function processForm(theForm) {

  var img               = theForm.img;
  var folder            = DriveApp.getFolderById(folderId);
  var doc               = folder.createFile(img);
  var template          = HtmlService.createTemplateFromFile('thanks.html');
  var name              = template.name               = theForm.name;
  var file              = template.doc  = doc.getUrl();
  var sheet             = SpreadsheetApp.openById(submissionSSKey).getSheets()[0];
  var lastRow           = sheet.getLastRow();
  var targetRange       = sheet.getRange(lastRow+1, 1, 1, 2).setValues([
    [
      mert,
      file
      
    ]
  ]);

  return template.evaluate().getContent();
}
</pre>

## Form.HTML

<pre class="lang:xhtml decode:true ">&lt;script&gt;
  function bosluk() {
    if ($('#myForm')[0].checkValidity()!= false) {
      var myFormObject = document.getElementById('myForm');
        toggle_visibility('formDiv');
        toggle_visibility('inProgress');
        google.script.run
        .withSuccessHandler(updateOutput)
        .processForm(myFormObject)
    }else{
       $('#myForm').checkValidity();

    }
  }

 function updateOutput(resultHtml) {
     toggle_visibility('inProgress');
     var outputDiv = document.getElementById('output');
     outputDiv.innerHTML = resultHtml;
   }

function toggle_visibility(id) {
     var e = document.getElementById(id);
     if(e.style.display == 'block')
       e.style.display = 'none';
     else
       e.style.display = 'block';
   }

&lt;/script&gt;

&lt;div style="display:block;" id="formDiv"  &gt;
  &lt;form id="myForm"&gt;
    &lt;input type="text" name="name" value=""&gt;
    &lt;input type="file" name="img" value=""&gt;
    &lt;input type="submit" class="btn btn-lg btn-info" value="Gönder!"onclick="bosluk(); return false;" /&gt;
  &lt;/form&gt;
&lt;/div&gt;
&lt;div id="inProgress" style="display: none;"&gt;
  Yükleniyor..
&lt;/div&gt;
&lt;div id="output"&gt;
&lt;/div&gt;

</pre>

## Thanks.HTML

<pre class="lang:default decode:true ">&lt;h1&gt;Sn. &lt;?= name; ?&gt;&lt;/h1&gt;
&lt;p&gt;Başvurun tarafımıza ulaştı, sana en kısa zamanda dönüş yapacağız.&lt;/p&gt;</pre>

## Kaynaklar:

<https://developers.google.com/apps-script/>

## Örnek Çalışma:

  * <https://script.google.com/macros/s/AKfycby6dZ1GgREAuBcQt-oN9gQNVi_YXXM2toFL2AldHUl1/dev>