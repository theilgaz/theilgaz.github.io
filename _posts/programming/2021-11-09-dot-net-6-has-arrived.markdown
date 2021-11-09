---
layout: post
title: Şimdiye kadarki en hızlı .NET - Karşınızda .NET 6 
date: 2021-11-09 09:00
comments: true
external-url:
categories: 01&nbsp;Programlama
---

Neredeyse 1 yıldan uzun süredir .NET ekibi ve topluluk tarafından yoğun bir çalışma ile sürdürülen .NET 6 nihayet karşımızda. Gelirken de eli dolu gelmiş anlaşılan. C# 10 ve F# 6 sürümleri ile kodunuzu daha basit ve daha iyi hale getirecek güzellikler sunuyor. Oldukça bariz olan ise [büyük bir performans iyileştirmesi](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-6/). 

.NET 6, Apple Silicon (Arm64) işlemcileri native olarak destekleyen ilk .NET sürümü oldu. Windows Arm64 desteğinde de iyileştirmeler söz konusu. 

Linux, macOS ve Windows için [.NET 6'yı buradan indirebilirsiniz](https://dotnet.microsoft.com/download/dotnet/6.0).

## Öne Çıkanlar

.NET 6,

- **Üç yıl desteklenecek** ve en güncel [uzun dönem desteklenecek (LTS) sürüm](https://github.com/dotnet/core/blob/main/releases.md) oldu.
- Tarayıcı, bulut, masaüstü, IoT ve mobil uygulamalarda kullanılan aynı .NET kütüphanelerini ve kod paylaşımının yapılabileceği **birleşik platform**.
- **Performans** açısından [büyük iyileştirmeler](https://devblogs.microsoft.com/dotnet/performance-improvements-in-net-6/), [I/O işlemleri](https://devblogs.microsoft.com/dotnet/file-io-improvements-in-dotnet-6/) için işlem süresi, gecikme süresi ve bellek kullanımında ciddi azalmalar.
- **C# 10** için record struct, implicit using, yeni lambda özellikleri, ve daha fazla [dil geliştirmeleri](https://devblogs.microsoft.com/dotnet/welcome-to-csharp-10/), F# 6 için [Task based async, pipeline debugging ve sayısız performans iyileştirmeleri](https://aka.ms/fsharp-6-release).
- **Visual Basic** [iyileştirmeleri](https://devblogs.microsoft.com/dotnet/whats-new-for-visual-basic-in-visual-studio-2022).
- **Hot Reload** *-uygulamanızın değişikliklerini görmek için uygulamayı yeniden derlemenize ve tekrar başlatmanızı ortadan kaldırır.-*, C# ve Visual Basic için .NET CLI ve Visual Studio 2022 üzerinden kullanılabilir.
- **Bulut teşhis/Cloud diagnostics**, Azure App Service ile kullanılabilen, [OpenTelemetry](https://devblogs.microsoft.com/dotnet/opentelemetry-net-reaches-v1-0/) ve [dotnet monitor](https://devblogs.microsoft.com/dotnet/whats-new-in-dotnet-monitor/) ile production ortamında desteklenen bulut teşhis çözümleri.
- **JSON API** [iyileştirmeleri](https://devblogs.microsoft.com/dotnet/try-the-new-system-text-json-source-generator/).
- **Minimal API** ile [başlangıç deneyimini basitleştir](https://www.hanselman.com/blog/exploring-a-minimal-web-api-with-aspnet-core-6)erek, HTTP servislerinin performansını iyileştirmek için sunulan yeni apiler.
- **Blazor** [komponentleri artık JavaScript'ten oluşabilir](https://docs.microsoft.com/aspnet/core/blazor/components/?view=aspnetcore-6.0#render-razor-components-from-javascript) ve mevcut JavaScript projelerine dahil edilebilir.
- **WebAssembly AOT**, [Blazor WebAssembly (Wasm) uygulamaları için derleme](https://docs.microsoft.com/aspnet/core/blazor/host-and-deploy/webassembly?view=aspnetcore-6.0#ahead-of-time-aot-compilation), ve ayrıca çalışma anında yeniden bağlama ve native bağımlılıkları destekliyor.
- ASP.NET Core ile oluşturulan **Single-page apps**, artık Angular, React ve diğer popüler frontend Javascript frameworkleri ile kullanılabilecek esnek bir kalıp kullanıyor.
- **HTTP/3** ile ASP.NET Core, HttpClient ve gRPC, [HTTP/3 istemcileri ve sunucularıyla etkileşim](https://devblogs.microsoft.com/dotnet/http-3-support-in-dotnet-6/)e girebilecek.
- **File IO**, yeniden yazılan `FileStream` ile sembolik link ve arttırılmış performans deneyimi.
- **Güvenlik**, [OpenSSL 3](https://www.openssl.org/blog/blog/2021/09/07/OpenSSL3.Final/), [ChaCha20Poly1305 encryption scheme](https://cryptopp.com/wiki/ChaCha20Poly1305) ve çalışma anında derinliğine savunma azaltmaları (özellikle [W^X](https://github.com/dotnet/designs/blob/main/accepted/2021/runtime-security-mitigations.md#wx) ve [CET](https://github.com/dotnet/designs/blob/main/accepted/2021/runtime-security-mitigations.md#intel-control-flow-enforcement-technology-cet)), desteği ile iyileştirildi. 
- **Tek dosyalık uygulamalar** artık Linux, macOS ve Windows'a çıktı verebilir. *(Önceki sürümlerde sadece Linux çıktısı mevcuttu.)*
- **IL Trimming**, daha başarılı nihai sonuçlar için yeni kurallar, uyarılar ve analizörlerle, artık daha başarılı.
- **Source generators and analyzers** sayesinde daha iyi, daha güvenli ve daha yüksek performanslı kod üretebilirsiniz.
- **Source build**, kurumsal yapıların, kullanıcılarına özel, kaynaktan .NET oluşturup sunmalarını sağlar.

Konu başlıkları bu şekilde. Bu konularla ilgili daha fazla içeriğe resmi kaynaklardan ulaşabilirsiniz. Her madde içerisinde kendi referanslarını paylaşmaya çalıştım. Şimdi gelelim .NET 6 hayatımızda ne kadar süre yer alacak? sorusunun yanıtına.

## Destek

.NET 6, uzun dönem desteği (LTS, Long-term Support) ile birlikte yayınlandı ve önümüzdeki [üç yıl boyunca destek](https://github.com/dotnet/core/blob/main/releases.md) devam edecek. macOS Apple Silicon ve Windows Arm64 dahil olmak üzere [birden çok işletim sisteminde destekleniyor](https://github.com/dotnet/core/blob/main/release-notes/6.0/supported-os.md).


