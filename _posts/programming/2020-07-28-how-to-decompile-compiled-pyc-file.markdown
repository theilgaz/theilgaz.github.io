---
layout: post
title: Derlenmiş .pyc Python dosyaları nasıl kaynak koda geri döndürülür?
date: 2020-07-28 17:00
comments: true
external-url:
categories: 01&nbsp;Programlama
---

Python için geliştirilen çok nitelikli kütüphaneler, yardımcı programlar ve araçlar mevcut. 

Bu makalede **uncompyle6** yardımıyla dizinimizde derlenmiş .pyc dosyalarının kaynak koda nasıl geri döndürüleceğine bakalım.

>**uncompyle6 Kurulumu**

```
pip install uncompyle6
```

[uncompyle6](https://pypi.org/project/uncompyle6/) , Python için geliştirilmiş, native bir sürümler arası kod çözücü ve parça kod çözücüdür. **decompyle**, **uncompyle** ve **uncompyle2**'nin halefidir.

>**Cmd üzerinden uncompyle6'yı çalıştır**

Python dizininin environment variables *(çevre değişkenleri)* içindeki Path'e doğru bir şekilde eklendiğinden emin olun. Örneğin, Anaconda kullanıyorsanız aşağıdaki şekilde eklemelisiniz:

```
C:\Users\KULLANICI_ADI\Anaconda3
C:\Users\KULLANICI_ADI\Anaconda3\Scripts
```

Bu doğrudan uncompyle6'yı Windows command prompt üzerinden çalıştırabilmenizi sağlar. Testini yapmak için uncompyle6 yazın ve çalıştırın. Kullanım örnekleri ve opsiyonları listeleyecektir.

>**Cihazınızdaki .pyc dosyasının kaynak koda döndürülmesi**

Kaynak koda döndürmek istediğiniz .pyc dosyasının yer aldığı dizine gidin.

Windows Explorer içerisinde Ctrl+Shift+Sağ tuş ile "Open PowerShell window here *(PowerShell'i burada aç)*" seçeneğine tıklayın.

Şimdi aşağıdaki komutu yazın.

```
uncompyle6 -o . <dosya-adi.pyc>
```

Bu komut, .pyc dosyasının bulunduğu dizine .py olarak kaynak koda döndürülmüş halini oluşturacaktır.

