---
layout: post
title: FMX Uygulaması Google Play'e nasıl yüklenir?
date: 2017-10-02 10:30
comments: true
external-url:
categories: 01&nbsp;Programlama
---

>Bu makale, **FireMonkey** Framework ile oluşturduğunuz **Delphi** projelerinizin Google Play'e nasıl yükleneceğini açıklamaktadır.

**Gereksinimler**

Google Play'e uygulamanızı yüklemeden önce yapmanız gereken bazı şeyler bulunuyor.

- Öncelikle **Google Play Geliştirici Hesabı** edinmeniz gerekmektedir. Tek sefere mahsus 25$'lık ücreti olan geliştirici hesabını edinmek için  [buraya](http://developer.android.com/distribute/googleplay/start.html)  tıklayın.

- Uygulamamızın **Deployment*** ayarlarını yapalım. (Project > Options > **Application / VersionInfo / Uses Permissions / Provisioning**)
*(bu ayarlarınızı doğru şekilde muhafaza etmeniz gerekir)

- Application: Bu sayfada uygulamanın görselleri ve ikonlar* ayarlanır.
*(market içinde ve android cihazlarda bu görseller görüntülenir)

- Version Info: Uygulamanın versiyon kodu* buradan ayarlanır.
*(uygulamanıza atacağınız yeni versiyonda buradaki kodu arttırmanız gerekir. market aynı kod ile 2 versiyonu muhafaza etmez)

- Uses Permissions: Uygulamanın çalışması için ihtiyaç duyduğunuz izinler/yetkiler* buradan ayarlanır.
*(Eğer telefon modülünü kullanmıyorsanız ve uygulamanızın tabletlerde çalışmasını istiyorsanız telefona has izinleri istememelisiniz. Markette cihazınıza uyumlu değildir hatası alınır)

- Provisioning: Markete yükleyeceğiniz uygulama için burada Target kısmını Release olarak belirleyin.
*(KeyStore dosyası oluşturarak buradan ayarlarını yapın. Bu dosyayı ASLA kaybetmeyin. Şifresini ASLA unutmayın! Geliştirici cihazınız değişse bile aynı keystore ile yükleme yapmak zorundasınız. Aksi halde başka bir ID ile uygulamayı paketleyip yeniden yüklemeniz gerekir.)

**Uygulamayı Google Play'e Yükleme**

Şimdi uygulamayı Google Play'in kabul etmesi için imzalamamız gerekiyor. 

- Oluşturduğumuz KeyStore dosyası ile imzalanmaya hazır hale gelen uygulamamız imzalamak için:

1. **Project Manager**'dan **Build Configurations**'a çift tıklayın. **Release** olarak belirleyin.
2. **Target Platforms** kısmından **Android**'i seçin. Seçili olanlar kalın yazılır.
3. **Android**'e çift tıklayın ve **Configuration** kısmından **Application Store**'u seçin.
4. Project > **Build** <Proje Adı> ile uygulamayı derleyin.
5. Project > **Deployment** kısmından **Deploy**'a basın ve uygulamayı hazır hale getirin.

- Şimdi  [Google Play Geliştirici Konsolu](https://play.google.com/apps/publish/) na giriş yapın.

- **Add new application** butonuna basın.

- Uygulamanızın varsayılan dilini, başlığını, kısa açıklamasını ve uzun açıklamasını girin.

- Daha sonra **Store Listing** kısmından markette görünecek bilgileri ayarlayın.

- Manage releases kısmından uygulamanızın markette yayınlanacak ilk versiyonunu yükleyin.

- Pricing & Distribution ve Rating işlemlerini de tamamladıktan sonra Publish this app'e basarak uygulamayı yayınlanmak üzere gönderin. 

Google Play tarafından yapılacak incelemelerle birlikte ilk yükleme ise 3-8 saat, aynı uygulamaya yeni versiyon ise 1-4 saat içinde yayına alınır.
