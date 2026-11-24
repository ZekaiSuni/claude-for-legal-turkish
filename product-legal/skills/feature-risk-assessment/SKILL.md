---
name: feature-risk-assessment
description: >
  Tek bir özellik veya ürün riski için derin Türk ürün hukuku karar notu.
  Lansman incelemesinde yeni/yüksek risk çıkarsa, GC/yönetim karar istiyorsa
  veya regüle sektör/AI/KVKK/tüketici riski yoğunsa kullan.
---

# Feature Risk Assessment

## Amaç

Lansman incelemesi geniştir; bu skill tek riski derinleştirir. Çıktı, karar verene "ne olabilir, ne kadar ciddi, hangi azaltımla ship edilebilir" sorularını yanıtlayan 2-4 sayfalık karar notudur.

## Tetikleyiciler

- Kalibrasyon tablosunda olmayan yeni pattern.
- `Yüksek` veya `Bloke` bulgu.
- Tüketici checkout/abonelik, çocuk, sağlık, finans, telekom, AI, yurt dışına veri aktarımı, rekabet veya ürün güvenliği riski.
- Reklam Kurulu/KVKK/sektör regülatörü ilgisi olabilecek konu.
- Liderlik "ship edersek ne olur?" diye soruyor.

## Yapı

```markdown
[GİZLİ HUKUKİ / ÜRÜN HUKUKU ÇALIŞMA TASLAĞI - HUKUKÇU İNCELEMESİNE TABİDİR]

Reviewer note
- Kaynaklar:
- Okuma kapsamı:
- Doğrulanması gerekenler:
- Aksiyon öncesi:

# Özellik Risk Değerlendirmesi: [Özellik]

## 1. Ne inceleniyor

[Özellik, kullanıcı, hedef pazar, yenilik ve neden eskale edildi.]

## 2. Riskler

### Risk [N]: [Kısa ad]

**Senaryo:** [Somut kötü senaryo]
**Etkilenenler:** [tüketici/müşteri/çalışan/üçüncü kişi/şirket]
**Olasılık:** [Düşük/Orta/Yüksek + neden]
**Etki:** [Düşük/Orta/Yüksek + neden]
**Mevcut azaltımlar:** [varsa]
**Boşluk:** [eksik kontrol]
**Kalan risk:** [kabul edilebilir mi?]
**Kaynak/doğrulama:** [etiket]

## 3. Regülatör ve mevzuat görünümü

[Yalnızca ilgiliyse; Ticaret Bakanlığı/Reklam Kurulu/KVKK/BTK/BDDK/SPK/TİTCK/Rekabet Kurumu/platform]

## 4. Seçenekler

| Seçenek | Açıklama | Risk azalımı | Maliyet / gecikme |
|---|---|---|---|
| A | Ship as designed | | |
| B | Şartlı ship | | |
| C | Kapsam daralt / ertele | | |

## 5. Öneri

**Önerilen:** [Seçenek]

[Neden, kalan risk, kim kabul etmeli.]
```

## Kalibrasyon

Profildeki risk iştahı, sektör ve geçmiş kararlar okunmadan genel hukuki risk notu yazma. Aynı risk fintech, sağlık, çocuk ürünü veya regüle olmayan B2B araç için farklı ağırlıkta olabilir.

## Handoff

- KVKK/veri varsa `/privacy-legal:pia-generation` veya `/privacy-legal:use-case-triage`.
- AI varsa `/ai-governance-legal:aia-generation`.
- Reklam iddiası varsa `/product-legal:marketing-claims-review`.
- Regüle sektör varsa ilgili uzman/hukukçu ve güncel resmî kaynak kontrolü.
