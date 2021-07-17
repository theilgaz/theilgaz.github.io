---
layout: post
title: FMX Projelerinize hızlı dil desteği eklemek
date: 2017-08-03 10:30
comments: true
external-url:
categories: 01&nbsp;Programlama
---

>Geçtiğimiz günlerde yaptığım küçük bir projede deneme fırsatı bulduğum **TLang** komponentinin kullanımı ile ilgili çeşitli bilgilendirmelerde bulunmak istiyorum. 

Öncelikle FMX Projelerinize hızlı dil desteği eklemek için başvuracağınız bu yolun, köklü ve devasa bir projede kullanımında size istediğiniz yanıtı vereceğinden emin değilim. Nitekim yaşadığım sıkıntıları da yazının sonuna doğru sizlere ileteceğim.

**Öncelikle nedir bu TLang, ne işimize yarar?**

TLang, FMX projelerimizde yer alan string değerlerin çok pratik bir şekilde değiştirilerek, yerelleştirme (localize) yapmamıza olanak sunan bir komponent.

Nasıl oluşturulur, Dil karşılığı nasıl girilir, Dil nereden eklenir ve komponent nasıl kullanılır?

Herhangi bir komponent yerleştirir gibi Tool Palette'in içerisinden alıp form üzerine bırakabilirsiniz. Bu komponent, diğerlerine nazaran tüm projenin içindeki statik olan string değerleri tarayıp toplama kabiliyetine sahip. (Form1'e yerleştirdiğiniz Lang1, Form2..10, kısaca tüm formları tarar.)

Form üzerine yerleştirdiğiniz TLang komponentinin üstüne çift tıklayarak Language Designer'ı aktif edersiniz. Burada üst kısımdan Add language butonuna basarak TR dilini ekleyin. Tüm projenizde yer alan string değerlerin bir listesini altta göreceksiniz. Karşılarına olduğu gibi değerleri aktarın. Ardından yeni dil ekle diyerek EN olarak İngilizce'yi dahil edin. (Örneklem için)

Yukarıda yer alan ComboBox'tan Dil seçimi yaparak string değerlerin o dilde yer alan karşılığını doldurun. Tüm işlem bittiğinde Save file ile dosyanızı projenin kaynak kodlarının olduğu dizinde Language.lang (yada isim ne verirseniz, uzantı lang olmalı) olarak kaydedin. Kullanıma hazırız.

**Run-time (Çalışma anında) Dil değişimi nasıl yapılır?**

Bu komponentin acemilik döneminde yapılan basit bir yöntem var. Bu yöntem bazı sorunlar oluşturabiliyor. Mesela Android cihazda çok dil desteği hazır bir projenin Combobox nesnelerinde sadece ItemIndex'inde yer alan string değer dil değişimini görüyorken, diğer ön tanımlı değerler ne yazık ki başarısız oluyor. Tüm değerleri mevcut fonksiyon ile aldığınızda bu sorun yaşanmıyor.


```
//Lang1.Lang := 'en'; // bunu kullanmayın!
LoadLangFromStrings(Lang1.LangStr['en']); // bu sağlıklı yöntem
``` 

**Köklü ve devasa bir projede neden tercih edilmez?**

Bir önceki soruda yaşadığımız statik string değerlerin okunmasındaki problem, dinamik değerlerin dil karşılıklarını da okumamıza engel olacaktır. Bunun yerine çok dil desteği olan projelerde genellikle veritabanı yapılarının çoklu dile uyumlu olması sorunumuzu çözecektir. Kelime tablosunda işaretlemeleri yapacak uygun KEY değerlerini oluşturup, dilleri tanıttıktan sonra aktif dilde bu key'in value'su ne ise onu doğrudan kullanabilirsiniz.

**TLang hangi projeler için doğru bir tercih olur?**

Üzerinde veritabanı işlemlerini çok yapmayacağınız, yapacaksanız da ortak değerleri muhafaza edecek şekliyle dinamik verilerin çeviri yönetimini manuel yapacağınız her projede kullanılabilir. Statik string değerlere sahip projeler için müthiş hız kazandıracaktır. Tanıtım projelerinde, ürün projelerinde, basit fonksiyonel işlemlerde ve oyunlarda genellikle sabit menü ve  string kullanımı yaygındır. Bu yüzden saydığım proje türlerinde kullanmanız avantajlı olacaktır.


Dip: örnek bir proje oluşturup ekran görüntüleri almak için yeterli zamanım olmadığı için sizlere hazır bir örnek linki vereceğim. Örnekte ListBox'ta seçilen dil doğrultusunda string değerlerin değişimini ve kelimenin kullanımını gösteriyor.