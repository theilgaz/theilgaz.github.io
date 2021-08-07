---
layout: post
title: Blazor projesinde sayfadaki veriler layout tarafına nasıl aktarılır?
date: 2021-08-07 10:08
comments: true
external-url:
categories: 01&nbsp;Programlama
---

Bu işlemi gerçekleştirmenin en basit yöntemi Layout sayfasında ilgili değeri karşılayacak property tanımlamak. Bunu bir örnek üzerinden gerçekleştirelim.

Projemizde bazı sayfalarda başlık değerini duruma göre güncelleme yapmamız gerektiğini, bazı sayfalarda da footer (alt menü) görünümünün gizlenmesi gerektiğini kabul edelim.

Yapmamız gereken şey oldukça basit.

1. Property tanımlamak
2. CascadingValue özelliğini tanımlamak
3. Sayfa içerisinden değer göndermek

**Property tanımlamak**

MainLayout.razor *(Özel bir isim verdiyseniz kendi layout çalışmanız)* dosyasını açın ve ilgili property tanımlarını gerçekleştirin. Varsayılan atamalar, özel atama yapılmayan sayfalarda görünüm için varsayılan şeklini belirler. *Atama yapılmazsa veri tipi varsayılan değerini alır.*

```
public string HeaderText {get; set;} = "My Application";

public bool ShowFooter {get; set;} = true;

``` 

**CascadingValue özelliğini tanımlamak**

MainLayout içerisinde tanımladığımız tüm komponentleri **CascadingValue** etiketlerinin içerisine dahil ediyoruz.

```
@inherits LayoutComponentBase


<CascadingValue Value="this">
    <div>
        ...
        <span>@HeaderText</span>
        ...
    </div>
    ...
     <div class="sidebar">
        <NavMenu />
    </div>
    <div class="main">
         <div class="content px-4">
            @Body
        </div>
    </div>
    ...
    <div>
        ...
    </div>
</CascadingValue>
@code
{
    public string HeaderText {get; set;} = "My Application";

    public bool ShowFooter {get; set;} = true;

    protected override void OnInitialized()
    {
        // Burada property değerlerini kontrol edip istenilen işlemleri yaptırabiliriz.
    }
}
``` 

**Sayfa içerisinden değer göndermek**

Index.razor sayfasından değer gönderelim.

```
@code{
    [CascadingParameter]
    public MainLayout Layout { get; set; } 

    protected override void OnInitialized()
    {
        Layout.ShowFooter = true;
        Layout.HeaderText = "Blazor bir harika!";
    }
}
``` 
