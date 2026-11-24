# Regulatory Legal - Legal Turkish

Türkiye regülasyon izleme ve politika gap takibi eklentisi. Komut adları orijinal repo ile uyum için İngilizce kalır; hukuki içerik Resmî Gazete, Mevzuat Bilgi Sistemi, KVKK/Kurul, Rekabet Kurumu, SPK, BDDK, BTK, EPDK, TCMB, Ticaret Bakanlığı, USOM, TÜRKPATENT, RTÜK, GİB, TİHEK ve sektör kurum duyuruları ekseninde yürütülür.

> Bu eklenti hukuki danışmanlık vermez. Her çıktı hukukçu incelemesine tabi taslak, izleme notu veya karar destek çıktısıdır. Resmî metin, yürürlük tarihi, görüş son tarihi, idari para cezası, kurum kararı ve sektör yükümlülüğü somut dosyada güncel resmî kaynaktan doğrulanmalıdır.

## Kimler İçin

| Rol | Ana iş akışları |
|---|---|
| Regülasyon / compliance hukukçusu | Watchlist, gap triage, politika güncelleme koordinasyonu |
| KVKK / ürün / finans / telekom ekipleri | Kendi alanlarına dokunan gelişmeleri filtrelenmiş şekilde almak |
| GC / yönetim | Maddi gap, son tarih ve eskalasyon raporu |
| Özel hukuk bürosu | Müvekkil bazlı regülasyon değişikliği ve görüş süreci takibi |

## Komutlar

| Komut | Ne yapar |
|---|---|
| `/regulatory-legal:cold-start-interview` | İzlenecek kurumları, politika kütüphanesini ve önem (materiality) eşiğini kurar |
| `/regulatory-legal:customize` | Mevcut kurumsal izleme profilini, eşikleri ve kurum listesini günceller |
| `/regulatory-legal:reg-feed-watcher` | İzleme listesindeki resmî kaynakları şimdi kontrol eder |
| `/regulatory-legal:policy-diff [düzenleme]` | Düzenleme değişikliğini politika kütüphanesiyle karşılaştırır |
| `/regulatory-legal:gaps` | Açık gap tracker durumunu gösterir |
| `/regulatory-legal:gap-surfacer` | Yeni düzenlemeler ile şirket politikaları arasındaki boşlukları yüzeye çıkarır |
| `/regulatory-legal:comments` | Taslak düzenleme / kamuoyu görüşü / görüş bildirme son tarihlerini takip eder |
| `/regulatory-legal:policy-redraft` | Gap'i kapatacak politika değişikliği taslağı üretir |
| `/regulatory-legal:matter-workspace` | Çok müvekkilli kullanımda matter izolasyonu yönetir |

## Varsayılan Kaynak Omurgası

- Resmî Gazete ve Mevzuat Bilgi Sistemi.
- KVKK/Kurul duyuruları, kararlar, rehberler, standart sözleşmeler.
- Rekabet Kurumu kararları, duyurular, mevzuat çalışmaları.
- SPK bültenleri, duyurular, idari yaptırımlar.
- BDDK mevzuat duyuruları, düzenleme taslakları, kurul kararları.
- BTK duyuruları, kurul kararları ve kamuoyu görüşüne açılan taslaklar.
- EPDK, TCMB, MASAK, Ticaret Bakanlığı, TİTCK, SGK/ÇSGB, Siber Güvenlik Başkanlığı / USOM, TÜRKPATENT, RTÜK, GİB ve TİHEK kaynakları.

## İlk Kurulum

```text
/regulatory-legal:cold-start-interview
```

Kurulum; izlenecek kurumları, sektörleri, kaynak URL'lerini, politika sahiplerini, önem eşiğini, gap kapanış sürecini ve görüş bildirme karar sahiplerini profil dosyasına yazar.

## Sürüm ve Kapsam

- **Sürüm:** `1.1.0-tr`
- **Kullanıcı Profili Dizini:** `~/.claude/plugins/config/legal-turkish/regulatory-legal/`
- **Kaynak Kataloğu ve Güncellik:** Genişletilmiş Türkiye kurum kaynakları (Resmî Gazete, KVKK, Rekabet, SPK, BDDK, BTK, EPDK, TCMB, MASAK, USOM, TÜRKPATENT, RTÜK, GİB, TİHEK) için `skills/reg-feed-watcher/references/source-catalog.md` ve `references/currency-watch.md` dosyalarını inceleyin.
