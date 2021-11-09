---
layout: post
title: Blazor server projesinde Cannot find the fallback endpoint specified by route values hatası
date: 2021-10-06 08:45
comments: true
external-url:
categories: 01&nbsp;Programlama
---

Yeni bir Blazor Server App projesi oluşturdunuz. Mevcut html çalışmanızı dahil ederken varsayılan tüm style dosyalarını wwwroot altından sildiniz. Aktarımı tamamladıktan sonra projeyi çalıştırdınız ve size projenizde hata olmadığı halde hata mesajı oluşturdu. Detaylı bilgi için DevTools'a bakmanızı önerdi ama baktınız ki orada da bir şey yok. Tanıdık geldi mi? Hızlı yanıt için en alttaki çözüm bölümüne, merak ettiyseniz de okumaya devam edin.

Blazor uygulamaları render olurken gerekli görülen alanlardan birisi de _Host.cshtml içerisinde yer alan tüm alanların uygulama tarafından işlenebilir halde olması. Host dosyasını açıp incelediğinizde environment etiketlerini içerisinde barındıran **blazor-error-ui** isimli bir div ile karşılaşacaksınız. 

Bu div uygulamanız hata oluşturduğunda kullanıcıya çıktı üretmesi için eklenen bir alan. Bu alana ait style dosyalarını kodunuzun içinde bulamadığı zaman bu hatayı üretecektir.

Staging veya Production ortamında size döndüreceği hata mesajı:

*An error has occurred. This application may no longer respond until reloaded.*

Development ortamında size döndüreceği hata mesajı:

*An unhandled exception has occurred. See browser dev tools for details.*

## Çözüm

Aşağıdaki style tanımlamalarını projenize dahil etmek.

```
    #blazor-error-ui {
        background: lightyellow;
        bottom: 0;
        box-shadow: 0 -1px 2px rgba(0, 0, 0, 0.2);
        display: none;
        left: 0;
        padding: 0.6rem 1.25rem 0.7rem 1.25rem;
        position: fixed;
        width: 100%;
        z-index: 1000;
    }

        #blazor-error-ui .dismiss {
            cursor: pointer;
            position: absolute;
            right: 0.75rem;
            top: 0.5rem;
        }
```

## Bonus

ASP.NET Core versiyon 6.0.100-rc.1.21458.32 ile bazen RazorSourceGenerator hatası alabiliyoruz. Bunun önüne geçmek için aşağıdaki çözümü uygulayabilirsiniz.

```
<PropertyGroup>
  <UseRazorSourceGenerator>false</UseRazorSourceGenerator>
</PropertyGroup>
```