---
name: marketing-claims-review
description: >
  Reklam, landing page, e-posta, sosyal medya, app store metni, indirim ve
  kampanya iddialarını Türk reklam hukuku ve Reklam Kurulu pratiği açısından
  inceler. "Can we say this", "bu reklam olur mu", "check these claims"
  gibi isteklerde kullan.
argument-hint: "[paste copy, or file path]"
---

# /marketing-claims-review

## Amaç

Pazarlama metnindeki ölçülebilir, karşılaştırmalı, mutlak, ima edilen veya hassas sektör iddialarını bul; kanıt gereksinimini ve düzeltme önerilerini ver. Reklam Kurulu/Ticaret Bakanlığı, 6502 ve ilgili sektör kuralları güncel kaynak kontrolü gerektirebilir.

## Akış

1. Product profile `## Pazarlama İddiaları` bölümünü oku.
2. Materyali oku: metin, görsel ima, fiyat/indirim, influencer/testimonial, mecra ve hedef kitle.
3. Her iddiayı ayıkla; saf subjektif ifade dışında kalanları tabloya al.
4. İddia tipini belirle: olgusal, karşılaştırmalı, ima edilen, mutlak, fiyat/indirim, influencer/testimonial, sektör hassas.
5. Kanıt dosyası, metodoloji, tarih, kapsam ve zorunlu açıklamalar (disclaimers) kontrolü yap.
6. Kısa metinlerde düzeltilmiş metni doğrudan yaz; uzun metinlerde değişiklik listesini ver.

## Türk Reklam Kontrol Kapıları

- Reklam doğru, dürüst, kamu düzeni/genel ahlak ve kişilik haklarına uygun mu?
- Tüketici deneyim/bilgi eksikliği istismar ediliyor mu?
- Örtülü reklam veya ifşasız influencer/testimonial var mı?
- Karşılaştırmalı reklamda rakip marka/logo/unvan kullanılıyor mu; karşılaştırma objektif, ölçülebilir, doğrulanabilir mi?
- İndirimde önceki fiyat, başlangıç/bitiş tarihi ve stok/miktar sınırı açık mı?
- "Ücretsiz", "garantili", "sınırsız", "en iyi", "tek", "%100", "risksiz" gibi mutlak ifadeler kanıtlanabilir mi?
- Sağlık, gıda, takviye edici gıda, kozmetik, finans, çocuk, oyun veya regüle sektör iddiası var mı?
- Platform politikası veya mecra kuralı canlı doğrulama gerektiriyor mu?

## İddia Tablolama

```markdown
**İddia:** "[tam alıntı]"
**Tip:** [Olgusal | Karşılaştırmalı | İma edilen | Mutlak | Fiyat/indirim | Influencer/testimonial | Sektör hassas]
**Kanıt dosyası:** [Var - kaynak | Yok | Bilinmiyor]
**Çağrı:** [Temiz | Kanıt gerekir | Yeniden yaz | Kes]
**Önerilen metin:** "[alternatif]"
**Neden:** [tek cümle]
**Doğrulama:** [Ticaret Bakanlığı/Reklam Kurulu/KVKK/platform/kullanıcı sağladı/doğrula]
```

## Çıktı

```markdown
[GİZLİ HUKUKİ / ÜRÜN HUKUKU ÇALIŞMA TASLAĞI - HUKUKÇU İNCELEMESİNE TABİDİR]

Reviewer note
- Kaynaklar:
- Okuma kapsamı:
- Doğrulanması gerekenler:
- Aksiyon öncesi:

# Reklam İddia İncelemesi: [Materyal]

## Özet

[N] iddia incelendi. [N] temiz, [N] kanıt/düzeltme, [N] kes.

**Yayın durumu:** [Yayınlanabilir | Değişiklikle yayınlanabilir | Yayınlanmamalı]

## İddia Bazlı İnceleme

[Kırmızı önce, sonra sarı, sonra temiz]

## Önerilen Revizyon

[Kısa metinlerde final revize metin; uzun metinlerde değişiklik listesi]

## Yayın Öncesi Gereken Kanıtlar

| İddia | Gereken kanıt | Sahip |
|---|---|---|
```

Non-lawyer kullanıcı için "Yayınlanabilir" ifadesi hukukçu incelemesi sonrası kullanılır; aksi halde "hukukçuya götürülecek taslak çağrı" olarak yaz.

## Handoff

- KVKK/çerez/hedefleme varsa `/privacy-legal:use-case-triage`.
- AI iddiası varsa `/ai-governance-legal:use-case-triage`.
- Sektör iddiası varsa ilgili uzman/hukukçu onayı.
