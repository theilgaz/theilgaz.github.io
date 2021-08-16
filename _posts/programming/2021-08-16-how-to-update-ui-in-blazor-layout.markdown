---
layout: post
title: Blazor projesinde layout üzerindeki dinamik verilerin sayfa değişiminde güncellenmesi
date: 2021-08-16 10:08
comments: true
external-url:
categories: 01&nbsp;Programlama
---

Layout üzerinde tanımlanan bazı property değerlerinin sayfa özelinde değişiklik gösterdiği durumlarla karşılaşabilirsiniz. WebAssembly projelerinin PWA desteğinin olması ile birlikte mobil arayüzler üreteceğiniz SPA uygulamaları üretmeniz oldukça yaygın bir yaklaşım.

Peki layout üzerinde navigation bilgisinin yer aldığı bir komponent veya property oluşturduysanız, bu değeri açılan sayfaya göre özelleştirmek isterseniz, sayfada state değişimini yakalamanızı engelleyebilecek çeşitli javascript kodlarını projenize bilmeden dahil edebilirsiniz. 

Kullanacağınız hazır template veya tasarımların kendi gereksinimlerinden ötürü ekledikleri özel kodlarla sizin arayüz tazeleme mekaniğinize müdahale edebilecek çeşitli durumlarla karşılaşabilirsiniz.

İşte tam bu noktada Blazor için Uri yönetimini sağlayan ve sizin için iyi bir yardımcı olan **NavigationManager** sınıfının nasıl projenize dahil edeceğine bir örnek oluşturalım.

Layout sayfamızın **MainLayout** olduğunu varsayalım. 

MainLayout içerisinde NavigationManager sınıfını çağırmamız gerekiyor. 

```
@inject NavigationManager UriHelper
```

Şimdi navigasyon yönetimine dair birçok olaya ve metoda erişimimiz oldu. NavigationManager hakkında daha kapsamlı bilgi almak için [burayı](https://docs.microsoft.com/en-us/aspnet/core/blazor/fundamentals/routing?view=aspnetcore-5.0#uri-and-navigation-state-helpers-1) ziyaret edebilirsiniz.

Doğrudan bir komponentin yer aldığı ve tanımlı route üzerine uygulamayı yönlendirmek için NavigateTo metodunu kullanabilirsiniz.


```
@inject NavigationManager UriHelper

@code {
    private void NavigateToMyComponent()
    {
        UriHelper.NavigateTo("component-name");
    }
}
```

Şimdi gelelim sayfa konumunun değiştirilmesi durumunda MainLayout üzerinde yer alan komponent ve arayüz çıktılarının güncellenmesine. Bunu gerçekleştirmek için HandleLocationChanged metodunu kullanacağız. Bu metodu layout yüklendiğinde yardımcı sınıfımızdaki ilgili event üzerine atamasını gerçekleştirerek aktif edebiliriz.

Metodun içerisinde ise çeşitli durumlarda olası komponent değişikliklerinin güncellenmeme problemi ile karşılaşmamak için arayüzü güncellemeye zorlamış olacağız. Bu işlemi StateHasChanged metodunu çağırarak gerçekleştireceğiz.


```
@inject NavigationManager UriHelper

@code {
    protected override void OnInitialized()
    {
        UriHelper.LocationChanged += HandleLocationChanged;
    }

    private void HandleLocationChanged(object sender, LocationChangedEventArgs e)
    {
        StateHasChanged();
    }

    public void Dispose()
    {
        UriHelper.LocationChanged -= HandleLocationChanged;
    }
}
```

Eğer async olarak initialize işlemini gerçekleştiriyorsak ve servis kaynaklı verilerin getirilmesinden oluşan bir sayfadaysak, OnInitializedAsync metodunun içerisinde de atama işlemini gerçekleştirebiliriz.

```
@code {
    protected async override Task OnInitializedAsync()
    {
        // smth...
        UriHelper.LocationChanged += HandleLocactionChanged;
    }
}
```

