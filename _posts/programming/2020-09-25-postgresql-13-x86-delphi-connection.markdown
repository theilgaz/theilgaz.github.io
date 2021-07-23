---
layout: post
title: Delphi ile PostgreSQL 13 Bağlantısı
date: 2020-09-25 22:40
comments: true
external-url:
categories: 01&nbsp;Programlama
---

Yeni yayınlanan PostgreSQL 13 sürümündeki veritabanlarınıza Delphi IDE güncel sürümlerinden bağlanırken başınıza gelebilecek bir hatadan bahsedeceğim.

>**Hata Özeti**

Delphi 10.2 (ve üzeri) ile sorunsuz bir şekilde çalışan FireDAC x64 desteği, bazı veritabanı sürücülerinde x86 için problem oluşturmaktadır. Uygulamada PostgreSQL'e erişmek istediğiniz zaman mimari uyumsuzluk hatası almak dışında kütüphane hatası almanız pek olası.

**[FireDAC][Phys][PG]-314. Cannot load vendor library [libpg.dll]. Hint: check it is in the PATH or application EXE directories, and has x86 bitness.**

>**Çözüm Yöntemi ve Çözümü**

PostgreSQL Server ve PostgreSQL Advanced Server 7.4 (ve üzeri) sürümlerde PG protocol 3.0 kullanıldığı için FireDAC native driver doğrudan PostgreSQL desteği ile birlikte gelmektedir.

1. x86-32 mimarisine ait binary dosyalarını Postgres resmi sayfasından indirin: [PostgreSQL Binaries](https://www.enterprisedb.com/download-postgresql-binaries)
2. İndirilen dosyayı arşivden çıkartıp pgsql/bin dizininde yer alan aşağıdaki dosyaları uygulama dizinine kopyalayın:

- libpq.dll
- ssleay32.dll
- libeay32.dll
- libintl-8.dll
- libiconv-2.dll

Probleminiz çözülmüş olacaktır. Eğer problem devam ediyorsa, **C:\Users\Public\Documents\Embarcadero\Studio\FireDAC** dizininde yer alan **FDDrivers.ini** dosyasını açın. Şimdi aşağıdaki konfigürasyon tanımını yapın.

```
[PG]
VendorLib=LIBRARY_PATH_BURAYA_GELECEK\libpq.dll
```

FDDrivers tanımını yaptığınız tüm veritabanı sürücülerinin dağıtım kütüphaneleri tasarım zamanında veritabanı işaretleme ve bağlantı probleminiz de ortadan kalkmış olacaktır. 

>**Veritabanı Erişimi**

Eğer veritabanı erişiminizle ilgili hata alırsanız **C:\Program Files\PostgreSQL\13\data** yolundaki **pg_hba.conf** dosyasını düzenleyin ve bağlantıların alt bölümünde tüm bağlantılara izin vermek için şu satırı ekleyin.

```
host    all             all             0.0.0.0/0            md5
```

