---
layout: post
title: Blazor Server-Side projesine PWA desteği eklemek
date: 2021-02-17 15:46
comments: true
external-url:
categories: 01&nbsp;Programlama
---

>Blazor Server projenize Progressive Web Application (PWA) desteğini hızlı bir şekilde eklemek ister misiniz?

Aşağıdaki 3 adımı takip ederek hızlı bir şekilde projenize PWA desteğini aktif edebilirsiniz.

**1. Adım: Geçici Blazor WASM Projesi Oluşturma**

Blazor WASM projesinin varsayılan desteklerinden birisi de PWA desteğidir. CLI üzerinden kolay bir şekilde geçici bir Blazor WASM projesi oluşturalım. (**--pwa** argümanını unutmayın.)

```
dotnet new blazorwasm -o {PROJE_ADI} --pwa
``` 


**2. Adım: PWA Dosyalarının Taşınması**

Blazor WASM projesi oluşturduktan sonra {PROJE_ADI}\wwwroot altındaki ilgili dosyaları Blazor Server projemizdeki wwwroot dizinine taşıyoruz.

**Dosyalar**

1. manifest.json
2. service-worker.js
3. service-worker.published.js
4. icon-512.png (opsiyonel)


**3. Adım: Blazor Server Projesinde PWA Aktivasyonu**

Projemizin **_Host.cshtml** dosyasında blazor.server.js referansının hemen altına aşağıdaki serviceWorker kaydını ekliyoruz.

```
    <script>
        navigator.serviceWorker.register('service-worker.js');
    </script> 
``` 


Yine _Host.cshtml dosyasının head bölümüne manifest dosyamızı çağırıyoruz.

    
```
<link rel="manifest" href="manifest.json" />
``` 



Artık Blazor Server projemizin PWA desteği hazır!

