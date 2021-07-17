---
layout: post
title: Delphi projelerinize Font Awesome ikonlarının desteğini ekleyin
date: 2017-09-26 10:30
comments: true
external-url:
categories: 01&nbsp;Programlama
---

>Son yılların yükselen bootstrap altyapısı ve bu altyapıya uygun çatıların geliştirilmesi, ikon fontların kullanımını yaygınlaştırdı. 

Web ile uğraşanların yaygın olarak kullandığı yada bildiği Font Awesome kütüphanesini duymayanınız yoktur. Masaüstü ve mobil uygulamalarınızda bu güzel görselleri kullanmanız için bir imkan var.


![install.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606522512989/RrIPF8WpA.png)

Öncelikle Font Awesome karakter kütüphanesini  [buradan](http://fontawesome.io/#modal-download)  indirin.

Daha sonra indirdiğiniz fontun üzerine sağ tuş yaparak kurulumunu gerçekleştirin.


![cheatsheet.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606522538149/RuWWrM5u0.png)

Font Awesome'un geliştiricilere sağladığı kolaylıklar saymakla bitmez. Kapsamlı bir  [Cheatsheet dokümanı](http://fontawesome.io/cheatsheet/)  olan Font Awesome, ihtiyaç duyduğunuz ikonun kullanım değerlerine hızlıca ulaşmanızı sağlıyor.


![FontAwesome.gif](https://cdn.hashnode.com/res/hashnode/image/upload/v1606522570084/YVKLkWgjE.gif)

- Şimdi yapmanız gereken şey Cheatsheet üzerinden seçtiğiniz FontAwesome ikonlarını belirlemek.
- Daha sonra ikonu kopyalayın. (unicode değerini değil)
- Kullanacağınız komponente gidin.
- Font özelliğinden Font Awesome'u seçin.
- Kopyaladığınız ikonu Caption yada Text değeri olan özelliğe yapıştırın.
- İhtiyacınız doğrultusunda Font Size özelliğini değiştirin.

---

**Örnek**

Font Awesome kullanmadan önce

![before.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606522590511/kbtyxbonH.png)


Font Awesome kullandıktan sonra

![after.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606522582119/HINHxnzAs.png)

Son olarak belirtelim; Font Awesome kütüphanesini sadece VCL projelerinizde değil, aynı zamanda FMX projelerinizde de kullanabilirsiniz.



![firemonkey.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606545958232/gu2ozyo7H.png)
