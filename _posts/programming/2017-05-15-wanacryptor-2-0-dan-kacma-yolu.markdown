---
layout: post
title: Wanacrypt0r 2.0'dan Kaçma Yolu 
date: 2017-04-30 15:46
comments: true
external-url:
categories: 01&nbsp;Programlama
---

> saldırıları engellemek için bir takım çözümleri mevcuttur. windows ms17-010 güncellemesi ile engellenebilir. <a target="_blank" href="https://technet.microsoft.com/en-us/library/security/ms17-010.aspx">indirmek için</a>

aşağıdaki kod bloğunu windows command'i yönetici olarak açarak çalıştırın ve saldırı portlarını kapatın.

---
```
netsh advfirewall set allprofiles state on

netsh advfirewall firewall add rule name="block outbound port wana crypt0r 2.0" dir=out localport=137,138,139,445 protocol=tcp action=block

netsh advfirewall firewall add rule name="block outbound port wana crypt0r 2.0" dir=out remoteport=137,138,139,445 protocol=tcp action=block

netsh advfirewall firewall add rule name="block outbound port wana crypt0r 2.0" dir=out localport=137,138,139,445 remoteport=137,138,139,445 protocol=tcp action=block

netsh advfirewall firewall add rule name="block inbound port wana crypt0r 2.0" dir=in localport=137,138,139,445 protocol=tcp action=block

netsh advfirewall firewall add rule name="block inbound port wana crypt0r 2.0" dir=in remoteport=137,138,139,445 protocol=tcp action=block

netsh advfirewall firewall add rule name="block inbound port wana crypt0r 2.0" dir=in localport=137,138,139,445 remoteport=137,138,139,445 protocol=tcp action=block

```
---

vaziyetin detaylı duyurusu aşağıdaki gibidir.
 
merhaba,

geçtiğimiz gün dünyanın her yerinden pek çok müşterimiz ve kullanmakta oldukları kritik sistemler “wannacrypt” isimli zararlı yazılımdan etkilendi. microsoft olarak hızla bu saldırıyı inceleyerek müşterilerimizi korumak üzere mümkün olan tüm önlemleri aldık. son kullanıcı ve kurumların bu saldırıdan korunmak için yapması gerekenleri paylaşıyoruz:

ayrıca tüm müşterilerimizi korumak için beklenenin ötesinde bir adım atarak, özel destek politikasına tabi olan windows xp, windows 8 ve windows server 2003 platformları için de bir güvenlik güncellemesi yayınlıyoruz.

mart 2017’de, bu saldırıların faydalandığı zafiyeti adresleyen bir güvenlik güncellemesi yayınladık. böylece, windows update güncellemesi aktif olan tüm kullanıcılarımız bu zafiyeti kullanan saldırılara karşı koruma altına alındılar. bu güvenlik güncellemesini henüz uygulamamış olan kurumların hemen microsoft security bulletin ms17-010 güncellemesini dağıtmalarını öneriyoruz.
windows defender kullanmakta olan müşterilerimiz için bu tehdidi ransom:win32/wannacrypt olarak tespit eden bir güncelleme yayınladık. etkili koruma için ekstra bir önlem olarak, bilgisayarlarınızda kurulu olan antivirüs yazılımlarını güncellemenizi öneriyoruz. farklı bir güvenlik sağlayıcısının antivirüs çözümünü kullanmakta olan müşterilerimiz koruma altında olduklarını bu sağlayıcılarla teyit edebilirler.
bu saldırı zaman içinde gelişebileceği için, daha fazla koruma için kurumlara detaylı savunma stratejileri oluşturmalarını öneriyoruz. (örneğin, smbv1 attacks saldırılarından daha iyi korunmak için müşterilerimiz ağlarındaki eski protokolleri engellemeyi değerlendirebilirler).

bazı müşterilerimizin artık microsoft tarafından desteklenmeyen windows sürümlerini kullanmakta olduğunu biliyoruz. bu müşterilerimiz mart ayında yayınladığımız güvenlik güncellemesi'ni alamadılar. ancak, saldırıların potansiyel etkisini değerlendirerek windows xp, windows 8 ve windows server 2003 gibi sadece özel destek politikasına tabi olan platformlarımız için de güvenlik güncellemesi'ni yayınladık (indirmek için aşağıdaki linklere göz atın). bu karar, detaylı bir durum değerlendirmesinin ardından tüm müşteri ekosistemimizi koruma altına alma prensibiyle alındı.

windows işletim sisteminin desteklenen versiyonlarını kullanan müşterilerimiz (windows vista, windows server 2008, windows 7, windows server 2008 r2, windows 8.1, windows server 2012, windows 10, windows server 2012 r2, windows server 2016) için ms17-010 güvenlik güncellemesi mart ayında yayınlandı. bu versiyonlarda otomatik güncellemeleri aktif hale getirmiş olan veya güncellemeyi manuel olarak yükleyen müşterilerimiz koruma altındalar. diğer müşterilerimizin mümkün olan en kısa süre içinde güncellemeyi yüklemelerini tavsiye ederiz.

saldırıların bazıları yaygın olarak görülen zararlı dosya ekleri gibi oltalama (phishing) taktiklerini kullanmaktalar. bu nedenle, tüm müşteri ve son kullanıcılarımız güvenilmeyen veya bilinmeyen kaynaklardan gelen e-posta ve dokümanlara karşı dikkatli olmalılar. office 365 müşterilerimiz için sürekli olarak ransom:win32/wannacrypt gibi tehditleri monitör ediyor ve koruma servislerimizi güncelliyoruz.

bu zararlı yazılım hakkında daha detaylı bilgi windows güvenlik bloğu'ndaki microsoft zararlı yazılım koruma merkezi’nde bulunuyor. microsoft zararlı yazılım koruma merkezi’ne yeni olanlar için, bu platform bt güvenlik uzmanlarının sistemlerini daha iyi koruyabilmelerine yönelik bilgiler sunma odaklı teknik tartışma platformumuzdur.

gelişmeler oldukça, müşterilerimizle birlikte çalışarak daha fazla destek sağlamak üzere bu forum yazısını güncelleyeceğiz.