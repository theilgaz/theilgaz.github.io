---
layout: post
title: Delphi FireMonkey'de Özel Thread Sınıfı Kullanımı
date: 2020-12-08 10:30
comments: true
external-url:
categories: 01&nbsp;Programlama
---

Merhaba,

Uygulamanın ana thread'i içerisinde arayüz güncelleme ve arayüzde bir bekletme, yüklenme, doldurma vb. işlemlerinizi sorunsuz gerçekleştirmek için yan thread tanımlaması yapmanız ve işlemlerinizi doğru şekilde çağırmanız çok önemli.

Bu bağlamda Delphi'de Thread kullanımına örnek oluşturacak bir çalışma hazırladım.

### Kendi TThread Sınıfımızı Oluşturalım

TThread sınıfından miras alan özel sınıfımızı aşağıdaki gibi oluşturuyoruz.

```
type
  TMyThread = class(TThread)
 private
   FJob: TNotifyEvent;
 public
   procedure Jobs;
 published
   property Job: TNotifyEvent read FJob write FJob;
 protected
   procedure Execute; override;
 end;
``` 

Tanımlanan **Jobs** ve **Execute** prosedürlerinin gövdelerini oluşturalım.

```
procedure TMyThread.Execute;
begin
 inherited;
 Jobs;
 Synchronize(
 
   procedure()
   begin
      // Do something...
   end);
end;
 
procedure TMyThread.Jobs;
begin
 if Assigned(FJob) then
   FJob(Self);
end;
``` 

### TMyThread Sınıfının Kullanımı

```
procedure MyJob(Sender: TObject);
procedure MyJobOnTerminate(Sender: TObject);
``` 

Kullanacağımız sınıf içerisinde thread sınıfımıza ait 2 prosedürü tanımlıyoruz ve gövdelerini oluşturuyoruz. 

MyJob prosedüründe thread içinde yapılacak işi, MyJobOnTerminate prosedürü içerisinde işlem tamamlandığında yapılacak işi tanımlıyoruz.

Daha sonra sınıf içerisinde kullanacağımız değişkenimizi tanımlıyoruz.

```
var AThread: TMyThread;
``` 

Oluşturduğumuz AThread'e yapmak istediğimiz işlemi ve sonrasında yapacağı işlemi atıyoruz. Daha sonra başlatıyoruz.


```
AThread := TMyThread.Create(True);
AThread.Job := MyJob;
AThread.OnTerminate := MyJobOnTerminate;
Sleep(100);
AThread.Start;
``` 

Artık kendimize ait TMyThread sınıfını kullanarak kolaylıkla loader, activity, progress dialog ekranlarını yönetebilir, arkaplanda yaptığımız işlem bitene kadar kullanıcının farklı bir işlem yapmasını engelleyebiliriz.

