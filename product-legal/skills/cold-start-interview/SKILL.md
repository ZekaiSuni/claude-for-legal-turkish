---
name: cold-start-interview
description: >
  Product-legal profilini Türk ürün hukuku için kurar: lansman gate'leri,
  risk kalibrasyonu, reklam iddia politikası, KVKK/AI/sektör eskalasyonu ve
  entegrasyonları toplar.
argument-hint: "[--redo] [--check-integrations]"
---

# /cold-start-interview

## Amaç

Bu kurulum, product-legal skill'lerinin şirketin gerçek risk kalibrasyonuna göre çalışmasını sağlar. Türkiye ürün hukuku için odak: tüketici/e-ticaret, reklam, KVKK, sektör regülasyonu, ürün güvenliği, AI ve lansman süreci.

## Konum

Profil şu yola yazılır:

```text
~/.claude/plugins/config/legal-turkish/product-legal/CLAUDE.md
```

Var olan profil doluysa yeniden yazma; kullanıcı `--redo` istemediyse mevcut profili özetle ve `customize` öner.

## `--check-integrations`

Yalnızca Linear/Asana, doküman depolama ve Slack gibi bağlantıları test eder. Bir connector sadece `.mcp.json` içinde görünüyor diye çalışır kabul edilmez; küçük bir okuma/arama denemesi başarılı olmadan `bağlı` yazma.

## Hızlı Kurulum Soruları

Kullanıcı hızlı kurulum isterse yalnızca şunları sor ve kalan alanları `[DEFAULT]` olarak işaretle:

1. Rolünüz nedir: hukukçu, PM, pazarlama, kurucu, operasyon?
2. Şirket/ürün modeli nedir: B2C, B2B, pazaryeri, abonelik, fintech, sağlık, oyun, eğitim, diğer?
3. Ana pazarlar neresi: Türkiye, AB, ABD, global?
4. En hassas alanlar: KVKK, reklam, fiyat/abonelik, sektör regülasyonu, AI, güvenlik, fikri haklar?
5. Lansman onayı kimde ve kritik risk kime eskale edilir?

## Tam Kurulum Soruları

### 1. Şirket ve ürün

- Ürün ne satıyor ve kime?
- Tüketiciye mi, tacire mi, ikisine birden mi?
- Pazaryeri, abonelik, finansal hizmet, sağlık, eğitim, oyun, telekom veya kamu ayağı var mı?
- Türkiye dışında hangi pazarlar hedefleniyor?
- Hangi regülatörler veya kurumlar pratikte kritik?

### 2. Lansman süreci

- Lansmanlar nereden gelir: Linear, Asana, Google Drive, Slack, manuel?
- Hukuk hangi aşamada devreye girer?
- Hangi değişiklikler otomatik hukuk review ister?
- Tipik SLA nedir?
- Geçmişte hangi lansmanlar bloklandı veya şartlı ship edildi?

### 3. Risk kalibrasyonu

Aşağıdaki pattern'ler için `FYI / bakmak gerekir / bloke` kararını iste:

- yeni veri/çerez/tracking,
- yeni vendor veya veri aktarımı,
- karşılaştırmalı veya sayısal reklam iddiası,
- fiyat/indirim/abonelik/otomatik yenileme,
- çocuk/sağlık/finans/eğitim/telekom gibi sektör,
- AI, otomatik karar, model eğitimi,
- app store/platform politikası,
- müşteri logosu/testimonial/influencer.

### 4. Pazarlama iddiaları

- Kim inceler?
- Karşılaştırmalı reklam politikası nedir?
- "En iyi / tek / garantili / ücretsiz / sınırsız / %100" gibi ifadeler için ev kuralı nedir?
- İndirim ve fiyat gösteriminde hangi kanıtlar tutulur?
- Influencer/testimonial ve müşteri logosu için izin/ifşa standardı nedir?

### 5. KVKK, AI ve güvenlik

- KVKK sorumlusu ve privacy review süreci kimde?
- Çerez/CMP, İYS, VERBİS, aydınlatma ve yurt dışına aktarım nasıl yönetilir?
- AI use-case registry veya AI politikası var mı?
- Güvenlik review ve vendor review nerede yapılır?

### 6. Çıktı ve eskalasyon

- Dahili not formatı nedir?
- Ticket'a paylaşılabilir kısa yorum nasıl olmalıdır?
- Kim hangi riskte imza verir?
- Hukukçu olmayan kullanıcı için hangi noktada durup avukat onayı istenir?

## Yazılacak Profil

Kök dizindeki `product-legal/CLAUDE.md` şablonunu kullan. `[PLACEHOLDER]` alanlarını kullanıcının yanıtlarıyla doldur. Bilinmeyen alanlara `[PENDING - kullanıcı atladı]` yaz; sessiz boşluk bırakma.

## Doğrulama

Kullanıcı belirli bir kanun, tutar, ceza, tarih, regülatör kararı veya platform politikası söylerse, yazmadan önce doğrulama gerektiğini belirt. Güncel resmî kaynak olmadan profile kesin hukuk kuralı yazma; `[doğrula]` notu koy.

## Kapanış

Kurulum sonunda:

- risk kalibrasyonu tablosunu özetle,
- ilk denenebilecek komutları söyle,
- eksik kalan alanları listele,
- `references/currency-watch.md` dosyasının güncellik kontrol listesi olduğunu belirt.
