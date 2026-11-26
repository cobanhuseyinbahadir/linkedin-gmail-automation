# LinkedIn ve Gmail otomasyon tanımları

Gmail temizliği, fatura arşivleme, LinkedIn iş fırsatları taraması ve günlük birleşik özet için görev talimatları.

Bu depo bir **talimat ve yapılandırma şablonu** içerir. Çalıştırılabilir uygulama, GitHub Actions iş akışı veya Gmail/LinkedIn bağlantısı içermez. GitHub'a yüklemek mevcut ChatGPT/Codex zamanlamasını taşımaz ya da başlatmaz.

## Görevler

- 09.00 (Europe/Istanbul): Gmail temizliği ve fatura arşivi.
- 10.00 (Europe/Istanbul): LinkedIn iş fırsatları ve aynı günün Gmail sonucu ile birleşik özet.

## Kullanım

1. `config.example.json` dosyasını `config.local.json` olarak kopyalayın.
2. Kendi e-posta adresinizi ve doğrulanmış aday profilinizi girin. Profil; deneyim, hedef roller, konum ve ulaşım tercihlerini içermelidir.
3. Görev talimatlarındaki `YOUR_EMAIL` ve `CANDIDATE_PROFILE` alanlarını çalıştırıcıda bu yerel ayarlara bağlayın.
4. Görevleri Gmail ve arama araçlarına erişimi olan bir asistan ortamında zamanlayın. Özet görevi, Gmail görevinin güncel raporuna ve önceki gönderim kayıtlarına erişebilmelidir.

Yeni bir çalıştırıcıya geçerken Gmail değişiklikleri ve rapor gönderimi için hesap sahibinin yetkisini ayrıca alın. Şablondaki yetki ifadeleri önceki özel kuruluma aittir; başka hesaplar için yetki oluşturmaz.

## Koruma kuralları

Reklamlar yalnızca geri alınabilir Çöp Kutusu'na taşınır. Kalıcı silme yapılmaz. Gerçek faturalar korunur; belirsiz iletiler, kişisel yazışmalar ve iş başvuruları korunur. İş başvurusu veya üçüncü kişilere mesaj gönderimi yapılmaz. Günlük özet yalnızca yapılandırılan hesap sahibine gider ve aynı gün tekrar gönderilmez.

## Dışa aktarım kapsamı

Yerel iki otomasyon tanımından kişisel ad, e-posta, ayrıntılı aday geçmişi ve eski tarama sayacı ayıklanmıştır. Sohbet geçmişi, e-posta içerikleri, kimlik bilgileri ve erişim anahtarları dahil değildir. Yerel kaynak tanımlar dışa aktarım sırasında PAUSED durumundaydı; bulutta çalışan görevlerin durumu bu paketten anlaşılamaz. Mevcut görevlerde değişiklik yapılmadı.

## Lisans

MIT. Ayrıntı: `LICENSE`.

## ChatGPT üzerinde kullanım ve takip hafızası

Sistem ChatGPT görevleri olarak çalışır; depoda durum dosyası yoktur. 10.00 görevi hafıza olarak Gmail SENT'teki önceki günlük özetlerin **Takip tablosu** bölümünü ve sohbet geçmişini kullanır. Görev şunları yapar:

- **Takip tablosu:** Fırsatlar Yeni / Görüldü / Aday başvurdu / Yanıt bekleniyor / Kapandı durumlarıyla izlenir. "Başvurdu" yalnızca sen bildirirsen yazılır.
- **Hatırlatmalar:** Uzun süre yanıtsız kalanlar, kapanmak üzere olan ilanlar, karar verilmemiş güçlü eşleşmeler.
- **Recruiter gelen kutusu:** Son 2 günün recruiter iletileri salt okunur sınıflandırılır (Acil / Sıcak / Soğuk / Gereksiz); Acil ve Sıcak için yanıt taslağı yalnızca özet e-postasında önerilir. Gmail'de değişiklik, taslak kaydı veya gönderim yapılmaz.

Talimatları güncellediğinde `prompts/` içindeki metni ChatGPT'deki ilgili görevin talimat alanına elle yapıştır.
