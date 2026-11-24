# Product Legal - Legal Turkish

Türkiye ürün hukuku, pazarlama ve lansman inceleme eklentisi. Komut adları orijinal repo ile uyum için İngilizce kalır; hukuki çerçeve Türk tüketici hukuku, ticari reklam, e-ticaret, KVKK, ürün güvenliği, erişilebilirlik, sektör regülasyonları ve AI yönetişimi ekseninde uygulanır.

> Bu eklenti hukuki danışmanlık vermez. Her çıktı avukat/hukukçu incelemesine tabi taslak ve karar destek notudur. Kanun, yönetmelik, Kurul/Reklam Kurulu kararı, platform politikası, sektör düzenlemesi, tutar ve tarih bilgileri somut dosyada güncel kaynaktan doğrulanmalıdır.

## Kimler İçin

| Rol | Ana iş akışları |
|---|---|
| Ürün hukukçusu / hukuk müşaviri | Lansman incelemesi, özellik risk analizi, eskalasyon |
| Ürün yöneticisi | Hızlı "bu sorun olur mu?" triyajı |
| Pazarlama / growth | Reklam, iddia, indirim, influencer ve kampanya kontrolü |
| KVKK / uyum / güvenlik | Veri, tedarikçi, güvenlik, sektör regülasyonu kapıları |

## Komutlar

| Komut | Ne yapar |
|---|---|
| `/product-legal:cold-start-interview` | Türk ürün hukuku profilini, risk kalibrasyonunu ve lansman sürecini kurar |
| `/product-legal:customize` | Ürün profili, lansman kapıları ve reklam/KVKK eskalasyon kurallarını günceller |
| `/product-legal:launch-review [PRD/ticket]` | Lansmanı kategori kategori inceler |
| `/product-legal:marketing-claims-review [metin]` | Reklam ve pazarlama iddialarını inceler |
| `/product-legal:is-this-a-problem [soru]` | Hızlı PM/growth sorusuna kalibre triage verir |
| `/product-legal:feature-risk-assessment [özellik]` | Tek bir özellik/riske derin karar notu hazırlar |
| `/product-legal:matter-workspace` | Çok müvekkilli kullanımda matter izolasyonu yönetir |

## Türk Hukuku Kontrol Omurgası

Varsayılan inceleme başlıkları:

1. Sözleşme ve kullanıcı taahhütleri: kullanım şartları, SLA, abonelik, cayma/iptal, garanti, ayıplı hizmet, B2B/B2C ayrımı.
2. KVKK ve veri: yeni veri, yeni amaç, açık rıza, aydınlatma, çerez, İYS, yurt dışına aktarım, tedarikçi/alt işleyen.
3. Reklam ve haksız ticari uygulamalar: doğruluk, dürüstlük, karşılaştırmalı reklam, indirim, örtülü reklam, influencer, sağlık/gıda/finans iddiaları.
4. E-ticaret ve abonelik: 6563, ticari elektronik ileti, sipariş akışı, mesafeli sözleşme, ön bilgilendirme, iade/cayma, elektronik pazar yeri rolleri.
5. Ürün güvenliği, erişilebilirlik ve sektör: güvensiz ürün, teknik mevzuat, BTK, BDDK/TCMB, SPK, TİTCK, EPDK, Rekabet Kurumu, yerel izinler.
6. Fikri haklar ve içerik: lisans, marka/telif, kullanıcı içeriği, veri seti/eğitim verisi, açık kaynak, takedown süreci.
7. Güvenlik ve üçüncü taraflar: yeni vendor, entegrasyon, siber risk, veri akışı, sözleşme ve DPA/veri işleme sözleşmesi.
8. AI / otomasyon: AI kullanım kaydı, otomatik karar, insan denetimi, sentetik içerik, model eğitimi, AI vendor şartı.

## İlk Kurulum

```text
/product-legal:cold-start-interview
```

Kurulum; şirketin ürün yüzeyini, Türkiye ve diğer hedef pazarlarını, regülasyon ayak izini, lansman gate'lerini, reklam iddia politikasını, KVKK/AI eskalasyonlarını ve örnek geçmiş lansman kararlarını profil dosyasına yazar.

## Entegrasyonlar

`.mcp.json` içinde Linear, Asana, Google Drive ve Slack araçları tanımlıdır. Bunlar bağlı değilse eklenti dosya yükleme, ticket metni yapıştırma ve manuel workflow ile çalışır.

## Sürüm ve Kapsam

- **Sürüm:** `1.1.0-tr`
- **Kullanıcı Profili Dizini:** `~/.claude/plugins/config/legal-turkish/product-legal/`
- **Mevzuat Kontrol Listesi:** Güncel parasal sınırlar, idari para cezası eşikleri ve yürürlük tarihleri için `references/currency-watch.md` dosyasını izleyin.
