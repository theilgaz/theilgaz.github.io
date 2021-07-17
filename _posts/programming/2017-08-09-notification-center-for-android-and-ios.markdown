---
layout: post
title: FMX Uygulamasından Android & iOS için bildirim çubuğuna bildirim gönderme 
date: 2017-08-09 10:30
comments: true
external-url:
categories: 01&nbsp;Programlama
---

>FMX projelerinizde uyarı, bilgi ve hatırlatmalar göndermenizi kolaylaştıran pratik bir komponent (TNotificationCenter) bulunuyor. 

Bu komponent, bildirimlerinizi oluşturmanızı, planlamanızı yapmanızı, gönderimlerini sağlamanızı ve kullanıcının bildirime tıkladığı an yanıtı dinlemenizi sağlıyor.

**Kullanımı**
   
Tool Palette'ten;
System > TNotificationCenter (bildirimi yönetmek için) 
Standard > TButton (işlemi tetiklemek için)
Standard > TLabel (bildirime tıklandığını bildirmek için)
komponentlerini formunuza ekleyin.


Eklenen butonunuza çift tıklayın ve OnClick metodunun içine aşağıdaki kodları ekleyin.


```
``` 

 
Kullanıcının bildirime karşı yapacağı etkileşimleri dinlemek için NotificationCenter1'in OnReceiveLocalNotification (tek) event'ını oluşturun ve aşağıdaki kodları ekleyin.
 

```
``` 
