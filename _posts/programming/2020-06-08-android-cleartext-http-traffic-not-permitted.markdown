---
layout: post
title: Android Cleartext HTTP traffic not permitted hatasının çözümü
date: 2020-06-08 10:30
comments: true
external-url:
categories: 01&nbsp;Programlama
---

**Delphi 10.3 Rio** ile **Android 64bit** olarak uygulamanızı paketlediğiniz zaman, **HTTPRio** kullandığınız projelerinizde aşağıdaki hatayı alabilirsiniz.

*Cleartext HTTP traffic not permitted*

**Çözümü**

AndroidManifest.template.xml dosyasının içerisine aşağıdaki satırı ekleyin.

    <application android:persistent="%persistent%" 
        android:restoreAnyVersion="%restoreAnyVersion%" 
        android:label="%label%"  
        android:usesCleartextTraffic="true" <<-- bu satırı ekleyin.