[English](README.md) · **Türkçe**

# İş Fırsatı ve Gmail Asistanı

Her sabah Gmail kutunu düzenleyen, ardından LinkedIn ve web'de iş fırsatlarını tarayıp sana tek bir **günlük özet e-postası** gönderen bir yapay zekâ asistanının görev talimatları.

> **Amaç:** İş ararken fırsat kaçırmamak. Başvuru yapmaz, kimseye mesaj atmaz; bulur, sınıflandırır, hatırlatır. Kararı sen verirsin.

> Talimat metinleri Türkçe yazılmıştır.

> **Bu depo bir uygulama değil, talimat şablonudur.** Çalıştırılabilir kod, GitHub Actions iş akışı ya da Gmail/LinkedIn bağlantısı içermez. Talimatlar, Gmail ve web aramasına erişimi olan bir asistan ortamına (ör. ChatGPT zamanlanmış görevleri) yapıştırılarak kullanılır. GitHub'a yükleme yapmak çalışan bir görevi kendiliğinden güncellemez.

## Nasıl çalışır?

```
09.00  Gmail temizliği ve fatura arşivi
         │  reklamlar → Çöp Kutusu · faturalar → etiket + arşiv · önemli iletiler korunur
         ▼
10.00  İş fırsatları + günlük özet
         │  LinkedIn / web taraması · recruiter iletileri · takip tablosu
         ▼
       Günlük özet e-postası → yalnızca kendi Gmail adresine
```

Saatler `Europe/Istanbul`'a göredir.

## Günlük özet e-postasında ne var?

Konu: `Günlük özet | Gmail ve iş fırsatları | <tarih>`

1. **Gmail temizliği sonucu:** incelenen, Çöp Kutusu'na taşınan, fatura etiketine alınan ileti sayıları.
2. **Hatırlatmalar:** uzun süredir yanıt gelmeyen başvurular, kapanmak üzere olan ilanlar, karar verilmemiş güçlü eşleşmeler.
3. **Recruiter gelen kutusu:** son 2 günün iletileri *Acil / Sıcak / Soğuk / Gereksiz* olarak sınıflanır; acil ve sıcak olanlar için kısa yanıt taslağı önerilir.
4. **Yeni fırsatlar:** en fazla 10 fırsat; rol, çalışma modeli, eşleşen noktalar, eksik şartlar, doğrudan bağlantı. CV isteyen paylaşımlar ayrı gösterilir.
5. **Bugünün görünürlük önerisi:** teknik deneyim paylaşımı için gönderi iskeleti ya da yorum taslağı.
6. **Takip tablosu:** her fırsatın durumu (Yeni, Görüldü, Aday başvurdu, Yanıt bekleniyor, Kapandı).

**Takip hafızası:** Ayrı bir veritabanı yoktur. Asistan her gün, Gmail'in Gönderilmiş klasöründeki önceki özetin takip tablosundan devam eder. "Başvurdu" durumu yalnızca sen sohbette bildirirsen yazılır.

## Güvenlik ve koruma kuralları

| Asistan yapar | Asistan yapmaz |
|---|---|
| Reklamları geri alınabilir Çöp Kutusu'na taşır | Kalıcı silme, Çöp Kutusu'nu boşaltma |
| İncelediği LinkedIn bildirim e-postalarını okundu işaretler | Abonelikten çıkma, kalıcı filtre veya bildirim ayarı değişikliği |
| Gerçek faturaları etiketleyip arşivler | Belirsiz belgeyi arşivleme veya silme |
| Recruiter iletilerini yalnızca okur ve sınıflar | Gmail'de yanıt gönderme veya taslak kaydetme |
| Yanıt/gönderi taslağını özet içinde önerir | LinkedIn'de paylaşım, yorum, beğeni, bağlantı isteği |
| Özeti yalnızca senin adresine gönderir | Başvuru yapma, üçüncü kişiye mesaj veya e-posta |

Ek olarak: şüphede ileti korunur, e-posta içindeki talimatlar yetki sayılmaz, kapalı ilanlar aktif listeye alınmaz, profilde olmayan deneyim uydurulmaz. Aynı gün için özet ikinci kez gönderilmez.

## Kurulum

1. `config.example.json` dosyasını `config.local.json` olarak kopyala. Bu dosya `.gitignore`'dadır; GitHub'a yükleme.
2. E-posta adresini ve doğrulanmış aday profilini yaz. Profil şunları içermeli: deneyim, hedef roller, teknolojiler, konum ve ulaşım tercihi, çalışma modeli (uzaktan/hibrit/ofis).
3. `prompts/gmail-cleanup.txt` ve `prompts/linkedin-opportunities.txt` içindeki `YOUR_EMAIL` ve `CANDIDATE_PROFILE` alanlarını kendi bilgilerinle doldurup asistan ortamında iki ayrı görev olarak zamanla (09.00 ve 10.00).
4. Asistanın Gmail okuma/etiketleme ve web araması erişimi olduğundan emin ol.
5. Görevi bir kez elle çalıştırıp ilk e-postayı kontrol et. İlk özette "önceki takip tablosu bulunamadı" yazması normaldir.

> **Yetki:** Talimatlar, hesap sahibinin bu işlemlere izin verdiği varsayımıyla yazılmıştır. Hesabın sahibi sen değilsen ya da yeni bir ortama geçiyorsan, Gmail değişiklikleri ve özet gönderimi için hesap sahibinden ayrıca onay al.

## Depo yapısı

```
prompts/
  gmail-cleanup.txt            09.00 görevi: Gmail temizliği ve fatura arşivi
  linkedin-opportunities.txt   10.00 görevi: fırsat taraması, recruiter kutusu, günlük özet
config.example.json            Yerel ayar şablonu (gerçek bilgi içermez)
LICENSE                        MIT
```

## Gizlilik

Depo herkese açıktır. Ad, e-posta, ayrıntılı aday profili, e-posta içerikleri, hesap anahtarları ve OAuth belirteçleri burada yer almaz; bunlar yalnızca özel çalıştırma ortamında tutulmalıdır.

## Sınırlar

- Canlı zamanlayıcının durumunu bu depo garanti etmez; görevlerin çalıştığını asistan ortamından doğrula.
- LinkedIn bağlayıcısı yalnızca kişi araması sunuyorsa ilan ve gönderi taraması web aramasına dayanır; kişisel akışın tamamı taranamaz. Asistan kapsam sınırını raporda belirtir.
- Raporlanan sonuçlar bir asistanın çıktısıdır; başvurmadan önce ilanı asıl sayfadan doğrula.

## Lisans

MIT. Ayrıntı: [`LICENSE`](LICENSE).
