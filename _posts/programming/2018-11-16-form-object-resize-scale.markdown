---
layout: post
title: Form ve nesnelerin çalışma anında yeniden ölçeklendirilmesi
date: 2018-11-16 10:30
comments: true
external-url:
categories: 01&nbsp;Programlama
---

>Arkaplanında görsel bulunan ve standart ölçekte oluşturulan bir projemizde daha düşük çözünürlüğe ihtiyaç duyuldu. 

Gerekli çözünürlüğü ve oranlamayı hesaplayan, küçültme ve büyütme işlemlerini yapabileceğiniz bir fonksiyon oluşturdum. Örnek kodları GitHub üzerinde  [paylaştım](https://github.com/theilgazcode/ScaleObjects).
 

**Ekran Görüntüleri**

Orjinal Form

 
![1.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606595134014/57hw7xxVe.png)


Büyütülmüş Form


![2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606595139415/yTAl15tV4.png)


 

```
 ScaleForm(MyForm,TScaleScreen.TLarger);
``` 

Küçültülmüş Form

![3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1606595143902/5sNmhVfWb.png)

```
 ScaleForm(MyForm,TScaleScreen.TSmaller);
```