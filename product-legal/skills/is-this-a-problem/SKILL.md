---
name: is-this-a-problem
description: >
  PM, marketing veya founder tarafından gelen hızlı "bu sorun olur mu?"
  sorularına Türk ürün hukuku kalibrasyonuyla cevap verir. Kısa triage:
  temiz / bakmak gerekir / dur.
argument-hint: "[the question]"
---

# /is-this-a-problem

## Amaç

Uzun memo yazmadan riski ayıkla. Soru basitse kısa cevap ver; hukuki/teknik kaynak gerektiren yerde "emin değilim" demekten çekinme ve doğru skill'e yönlendir.

## Akış

1. Product profile `## Risk Kalibrasyonu` bölümünü oku.
2. Soruyu şu tipe ayır: hukuki problem, ticari karar, UX/müşteri deneyimi, policy kararı, teknik güvenlik, marka/pazarlama.
3. Kalibrasyon pattern'leriyle eşleştir.
4. Tuzak sorulardan biri varsa tek yakalayıcı soru sor.
5. Çıktı: `Temiz`, `Bakmak gerekir` veya `Dur`.

## Tuzak Sorular

| Soru gibi görünür | Neden riskli olabilir | Tek soru |
|---|---|---|
| "Bu veriyi yeni özellikte kullanalım mı?" | KVKK'da yeni amaç/aktarım/açık rıza gerekebilir | Veriyi ilk toplarken kullanıcıya hangi amacı söyledik? |
| "A/B testte farklı fiyat gösterelim mi?" | Tüketici, ayrımcılık, haksız ticari uygulama, fiyat şeffaflığı | Segmentler nasıl belirleniyor ve aynı ürüne farklı fiyat mı var? |
| "Ücretsiz deneme bitince otomatik ücret alalım mı?" | Abonelik, ön bilgilendirme, cayma, açık onay | Kullanıcı ödeme öncesi hangi ekranda neyi onaylıyor? |
| "Müşteri logosunu siteye koyalım mı?" | Marka/tanıtım/sözleşme izni ve referans iması | Yazılı logo/referans izni var mı? |
| "Influencer bunu söylesin mi?" | Örtülü reklam ve ifşa | İş birliği açık ve görünür şekilde belirtiliyor mu? |
| "En hızlı/en iyi/tek çözüm diyelim mi?" | Karşılaştırmalı/mutlak iddia kanıt ister | Bu iddiayı destekleyen güncel, objektif kanıt var mı? |
| "Yeni vendor'a veri gönderelim mi?" | KVKK, DPA, yurt dışı aktarım, güvenlik | Hangi veri, hangi ülkeye, hangi sözleşme ile gidiyor? |
| "Sadece dahili (internal) araç" | Çalışan/müşteri verisi yine KVKK kapsamında olabilir | Kimin verisine erişiyor? |
| "AI sadece yardımcı" | AI use-case, otomatik karar, veri eğitimi, vendor şartı | AI ne karar veriyor, girdi/çıktı kimi etkiliyor? |
| "Çerez banner'ına dokunmadan tracking ekleyelim" | Aydınlatma/açık rıza/çerez kategorisi değişebilir | Yeni tracking hangi amaçla ve hangi kategoriyle çalışıyor? |

## Cevap Formatı

```markdown
[Temiz | Bakmak gerekir | Dur]

[Tek cümle karar ve neden.]

[Gerekirse tek sonraki adım: privacy triage / claims review / launch review / sektör uzmanı / hukukçu onayı.]
```

Örnek:

```markdown
Bakmak gerekir - yeni vendor'a müşteri verisi gidiyorsa KVKK, yurt dışına aktarım ve güvenlik review kapısı açılıyor.

Sonraki adım: veri akışına bakıp `/privacy-legal:use-case-triage` çalıştıralım.
```

## Ne zaman kullanma

- PRD veya kapsamlı lansman varsa `launch-review`.
- Reklam metni/claim varsa `marketing-claims-review`.
- Tek risk derin karar gerektiriyorsa `feature-risk-assessment`.
- Güncel mevzuat/tutar/platform kuralına dayalı kesin cevap isteniyorsa önce resmî kaynak doğrula.
