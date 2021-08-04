---
layout: post
title: Commit Hatası - Git'te izlenmek istenmeyen dosyalar nasıl geri çağırılır?
date: 2021-08-04 16:18
comments: true
external-url:
categories: 01&nbsp;Programlama
---

>Yazılımcıların en büyük problemi düşünmeden, hızlı bir şekilde çözüme giderken başına gelen ve onu daha da yavaşlatan hatalara zemin veren hızları. 

Peki bu hızlarından ödün vermek istemeyen ve yanlışlıkla git sistemine takip etmek istemedikleri klasörleri ve dosyaları gönderen, .gitignore dosyasında bu klasörleri ve dosyaları belirtmeyi unutanlar ne yapacak? İşte bu benim diyorsanız, size güzel bir haber: git hap bilgilerde bugün dosyaların untrack operasyonunu ele alacağız.

Sadece hatalı yapılan işlemler için değil, bazen köklü revizyonlarda mevcut dosyaların artık değişikliklerde yer almasını istemeyebilirsiniz. Bu tarz durumlarda git sisteminden bu dosyaları çıkartmanın en kolay yoluna gelin birlikte bakalım.

**Git dosyaları izleme**

Git'in dosyaları izlemeyi bırakması için *git rm* komutunu kullanın.

```
git rm --cached <dosyaadi>
``` 

Eğer birden fazla dosya için tek seferde buna ihtiyacınız olursa;

```
git rm --cached <dosyaadi> <dosyaadi2> <dosyaadi3>
``` 

Her iki komutta da dosyalarınızı silmeden takipten çıkartmış olacaksınız. Bunun sebebi *--cached* opsiyonunu kullanmış olmamız. Eğer bu cache edilen dosyaların diskten silinmesini istiyorsanız;

```
git rm <dosyaadi>
``` 

Bu değişikliği yaptıktan sonra commit atmayı unutmayın. Git güncellemesi sonrası diğer geliştirici cihazlarda da aynı koşullar geçerli olacak.

**Git klasörleri izleme**

Peki klasörler ne olacak? Klasörü ve içeriğini tamamen takipten çıkartmak istersek *--r* (recursive) opsiyonu ile basit bir şekilde yapabiliriz.

```
git rm -r --cached <klasoradi>
``` 

**Gelecekte yeniden problem yaşamamak için**

Dilerseniz kaldırdığınız dosyaları git tarafından görmezden gelinen dosyaların arasına alabilirsiniz. Bunun için .gitignore dosyasına eklemeniz yeterli.

**Niçin 'rm' kullanmak yerine dosyaları kaldırmak için 'git rm' kullanıyoruz?**

Teknik olarak ikisi de aynı. *git rm* dosyanın index'ten çıkarılması ve çıkarılan dosyanın bir sonraki commit için staging komutunu birlikte çalıştırır.

*rm* ise sadece diskten dosyayı kaldırır. Stage ve commit işlemlerini yine de yapmanız gerekir. *git rm* ise tek hamlede ikisini halletmiş olur.