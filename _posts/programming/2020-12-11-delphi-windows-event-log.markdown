---
layout: post
title: Delphi ile Windows Event Log Kayıtları Oluşturma
date: 2020-12-11 10:30
comments: true
external-url:
categories: 01&nbsp;Programlama
---

>
![2.PNG](https://cdn.hashnode.com/res/hashnode/image/upload/v1607681481808/37Hy7yzR4.png)

**Delphi VCL **projenizde kullanıcıların gerçekleştirdiği hareketleri ve olayları kayıt altına almak, karşılaşılan hatalarda çözüme daha hızlı kavuşmanız için size yol gösterecektir. Kullanıcının sistemin gidişatını bozacak şekilde bir işlem yapması, geriye dönük olarak tüm işlemlerin izlenebilirliği ihtiyacını ortaya çıkartıyor. 

Gelin birlikte **Delphi VCL** projenizdeki tüm olayları nasıl Windows Event Log (EventViewer) sistemine kaydedeceğimizi inceleyelim.

Oluşturduğum örnekte iki farklı yöntem ile log kaydı oluşturulabilir. İlk yöntem SvcMgr.TEventLogger ve ikinci yöntem Windows.ReportEvent fonksiyonunu kullanan Helper sınıfı.

You can add your logs to Windows Event Log with **SvcMgr.TEventLogger** and with **TLogger Helper** using **Windows.ReportEvent**.


```
procedure TForm1.LogWithHelper;
begin
  TLogger.Source := 'MyApplicationName';
  TLogger.Log('This is an information.', lkInfo);
  TLogger.Log('This is an error.', lkError);
  TLogger.Log('This is an warning.', lkWarning);
end;

procedure TForm1.LogWithSvcMgr;
begin
  with TEventLogger.Create('MyApplicationName') do
  begin
    LogMessage('This is an error.', EVENTLOG_SUCCESS, 12345);
    LogMessage('This is another error.', EVENTLOG_ERROR_TYPE, 12345);
    LogMessage('This is information.', EVENTLOG_INFORMATION_TYPE, 12345);
    LogMessage('This is a warning.', EVENTLOG_WARNING_TYPE, 12345);
  end;
end;
``` 

![3.PNG](https://cdn.hashnode.com/res/hashnode/image/upload/v1607681467787/uwCg31FEx.png)
Önemli: WindowsEventLog içerisindeki kayıtlarda Source bilgisinin sistemin(Windows) kayıtlarında tanımlı olması gerekiyor. Bu yüzden uygulamanızı kurarken registry kayıtlarını da oluşturmanız gerekiyor. Bunun için yönetici olarak çalıştırmalısınız.

Important: If you are going to use WindowsEventLog, you should register your application when you are installing. This requires administrative rights.


```
program WindowsEventLogSample;

uses
  Vcl.Forms,
  Unit1 in 'Unit1.pas' {Form1},
  Logger in 'Logger.pas';

{$R *.res}
{$R MessageFile.res}

begin
  Application.Initialize;
  Application.MainFormOnTaskbar := True;
  Application.CreateForm(TForm1, Form1);
  TLogger.AddEventSourceToRegistry('MyApplicationName', ParamStr(0));
  Application.Run;
end.
``` 


![4.PNG](https://cdn.hashnode.com/res/hashnode/image/upload/v1607681489811/i8VbepUsF.png)

Örnek çıktı


![1.PNG](https://cdn.hashnode.com/res/hashnode/image/upload/v1607681499339/cLIrafZQu.png)

 [Kaynak Kod](https://github.com/theilgazcode/windows-event-log-delphi-sample) 