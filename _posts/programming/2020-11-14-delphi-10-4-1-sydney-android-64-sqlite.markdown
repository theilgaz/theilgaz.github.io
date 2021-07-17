---
layout: post
title: Delphi 10.4.1 Sydney ile Android 64-Bit uygulamada SQLite Hatası ve Çözümü
date: 2020-11-14 10:30
comments: true
external-url:
categories: 01&nbsp;Programlama
---

SQLite kullandığınız projelerinizi IDE güncel sürümlerinde kullanırken başınıza gelebilecek bir hatadan bahsedeceğim.

>**Hata Özeti**

Delphi 10.3.3 ile sorunsuz bir şekilde çalışan SQLite x64 desteği, Delphi 10.4 (ve 10.4.1) ile birlikte problem oluşturmaktadır. Uygulamada SQLite'a erişmek istediğiniz bir form açıldığı anda sizi aşağıdaki hata karşılayacaktır.

**[FireDAC][Phys][SQLite]-314. Cannot load vendor library [libsqlite.so or libdb_sql.so]. Hint: check it is in the PATH or application EXE directories, and has x86 bitness.**

>**Çözüm Yöntemi ve Çözümü**

Uygulamanın SQLite kütüphanelerini sorunsuz şekilde görmesi sayesinde başarılı bir derleme alabiliyorsanız, hatanızın tek kaynağı FireDAC'in SQLite için oluşturduğu Wrapper sınıfından kaynaklı olmasıdır. 

Çözümü oldukça basit. **FireDAC.Phys.SQLiteWrapper.Stat** sınıfını ilgili formunuzun **uses** bölümüne ekleyin. 

Uygulamanızı derlediğiniz zaman **Android x64** için sorunsuz bir şekilde derlendiğini göreceksiniz.