# Turkish Product Launch Review Framework

Bu varsayılan çerçeve, ekipte özel bir framework yoksa kullanılır. Kategoriler sabittir; sonuç ve ağırlık şirket profilindeki risk kalibrasyonuna, hedef pazarlara ve sektör düzenlemelerine göre belirlenir.

## 1. Sözleşme ve Kullanıcı Taahhütleri

**Soru:** Lansman mevcut kullanım şartları, SLA, abonelik, garanti, mesafeli satış, iade/cayma veya müşteri sözleşmeleriyle çelişiyor mu?

**Kontrol:** ToS, gizlilik/çerez politikası, SLA, kampanya şartları, abonelik sözleşmesi, mesafeli sözleşme, ön bilgilendirme, kurumsal MSA, kamuya açık dokümanlar.

**Auto-skip:** Kullanıcıya görünmeyen, taahhüt değiştirmeyen saf iç altyapı değişikliği.

## 2. KVKK ve Veri

**Soru:** Yeni veri, yeni amaç, yeni paylaşım, yeni tedarikçi, çerez/profil veya yurt dışına aktarım var mı?

**Kontrol:** Veri kategorileri, ilgili kişi grupları, KVKK m. 5/m. 6 işleme şartı, aydınlatma, açık rıza, saklama, imha, aktarım, VERBİS/envanter, çerez/CMP, İYS.

**Auto-skip:** Gerçekten veri akışı değişmiyor ve yeni logging/analytics yok.

## 3. Reklam ve Haksız Ticari Uygulamalar

**Soru:** Metin, görsel, UX veya kampanya tüketiciyi yanıltabilecek iddia, karşılaştırma, indirim, örtülü reklam veya eksik bilgi içeriyor mu?

**Kontrol:** Ticari Reklam ve Haksız Ticari Uygulamalar Yönetmeliği, Reklam Kurulu duyuruları, fiyat/indirim kılavuzları, sosyal medya etkileyici kılavuzu, sektör reklam yasakları.

**Auto-skip:** Dış pazarlama, ürün içi iddia, fiyat/indirim, influencer veya kampanya yok.

## 4. E-ticaret, Checkout ve Abonelik

**Soru:** Online satış, sipariş, abonelik, otomatik yenileme, ücretsiz deneme, iptal, iade veya ticari elektronik ileti akışı değişiyor mu?

**Kontrol:** 6502, 6563, mesafeli sözleşme, abonelik yönetmeliği, ön bilgilendirme, cayma istisnası, sipariş özeti, ETBİS/İYS, ETHS/ETAHS rolleri.

**Auto-skip:** Para, sipariş, abonelik, ticari ileti veya checkout akışı yok.

## 5. Ürün Güvenliği, Erişilebilirlik ve Sektör

**Soru:** Ürün regüle bir sektör, güvenlik standardı, teknik mevzuat, erişilebilirlik veya kamu/yerel izin etkisi doğuruyor mu?

**Kontrol:** BTK, BDDK/TCMB, SPK, TİTCK, EPDK, Rekabet Kurumu, Ticaret Bakanlığı ürün güvenliği, ilgili teknik düzenlemeler, app store/marketplace kuralları.

**Auto-skip:** Aynı kullanıcı, aynı sektör, aynı pazar ve aynı teknik yüzey.

## 6. Fikri Haklar ve İçerik

**Soru:** Yeni üçüncü taraf içerik, marka, lisans, açık kaynak, veri seti, kullanıcı içeriği veya AI çıktısı var mı?

**Kontrol:** FSEK/SMK etkisi, lisans koşulları, marka kullanımı, müşteri logosu, stok görsel/font, UGC moderasyon, takedown, eğitim verisi hakları.

**Auto-skip:** Yeni içerik, bağımlılık (dependency), logo, veri seti veya çıktı yok.

## 7. Güvenlik ve Üçüncü Taraflar

**Soru:** Yeni vendor, entegrasyon, API, bulut servisi, kimlik doğrulama veya veri erişim paterni var mı?

**Kontrol:** Vendor sözleşmesi, DPA/veri işleme sözleşmesi, alt işleyen, güvenlik review, SLA, olay bildirimi (incident notice), veri lokasyonu, erişim yetkileri.

**Auto-skip:** Yeni üçüncü taraf veya teknik saldırı yüzeyi yok.

## 8. AI / Otomasyon

**Soru:** AI, otomatik karar, skorlama, öneri motoru, üretken içerik, model eğitimi veya AI vendor kullanımı var mı?

**Kontrol:** AI use-case kaydı, insan denetimi, veri hakları, model eğitimi, sentetik içerik ifşası, KVKK profil/otomatik karar etkisi, vendor AI şartları, sektör kuralları.

**Auto-skip:** AI veya otomasyon bileşeni yok.
