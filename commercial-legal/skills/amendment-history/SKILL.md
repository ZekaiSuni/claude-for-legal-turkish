---
name: amendment-history
description: >
  Bir sözleşmenin ana sözleşme, ek protokoller, zeyilnameler, tadil
  sözleşmeleri ve yan yazılar boyunca nasıl değiştiğini izler; kronolojik tüm
  değişiklik özetini veya tek bir maddenin değişiklik zincirini üretir.
argument-hint: "[dosya(lar) | arşiv linki | matter slug] [--provision <madde adı>]"
---

# Sözleşme Tadil ve Ek Protokol Geçmişi (`/amendment-history`)

Ana sözleşme ile ek protokol, zeyilname, tadil sözleşmesi, devir/temlik metni ve yan yazılar arasındaki değişiklik zincirini çıkarır. Nihai hukuki yorum vermez; hangi metnin hangi hükmü nasıl değiştirdiğini gösterir ve çelişkileri hukukçu incelemesine taşır.

## Talimatlar

1. **Belgeleri Al:** Doğrudan yükleme, yerel/Google Drive klasörü, KEP/e-imza paketi veya matter klasörü üzerinden belgeleri al. UYAP atfı yalnızca sözleşme tarihi gerçek bir dava veya icra dosyasına bağlıysa kullanılır.
2. **Modu Belirle:**
   - Mod 1: Belirli bir madde adı verilmemişse tüm tadillerin kronolojik özeti.
   - Mod 2: Kullanıcı belirli bir madde veya konu belirttiyse o hükmün takip zinciri (`--provision`).
3. **Önce Kronolojiyi Kur:** Sıralamada şu önceliği izle:
   - imza tarihi,
   - yürürlük tarihi,
   - geriye yürür (`as of`) tarih ifadesi,
   - KEP veya e-imza zaman damgası,
   - dosya adı veya arşiv tarihi.
4. **Her Belgeyi İndeksle:** Belge türü, taraflar, imza tarihi, yürürlük tarihi, değiştirilen/eklenen/silinen hükümler, imzalar ve kaynak güvenini çıkar.
5. **Belirsiz Sıralamayı İşaretle:** Tarihsel sıra varsayıma dayanıyorsa nihai çıktı öncesi kullanıcıdan teyit iste.

## Dosya Bağlamı (`Matter Context`)

`## Matter Workspaces` etkinse aktif dosyayı yükle ve çıktıları oraya yaz; `Cross-matter context` kapalıyken diğer dosyaları okuma.

## Türk Uygulamasında Belge Türleri

Belgeleri kendi başlıkları ve operatif hükümlerine göre sınıflandır:
- Ana Sözleşme,
- Ek Protokol,
- Zeyilname,
- Tadil Sözleşmesi,
- Devir / Temlik Sözleşmesi (`TBK m. 183–206`),
- Fesih / İkale Protokolü,
- Mutabakat Tutanağı,
- Yan Yazı / Ek Anlaşma.

Başlık belirsizse `muhtemel belge türü` olarak işaretle.

## Adım 1 — Belgeleri Yükle ve Sırala

Her belge için şu yapıyı çıkar; ünvan değişikliği, taraf eklenmesi, devir veya imza yetkisi farkı olup olmadığını denetle:

```yaml
belge:
  tur:
  imza_tarihi:
  yururluk_tarihi:
  kaynak:
  siralama_guveni: yuksek | orta | dusuk
  taraflar:
  degistirilen_maddeler:
```

## Mod 1 — Tüm Değişikliklerin Kronolojik Özeti

Her bulgu madde ve kaynak belge atfı taşımalıdır:

> Süreli fesih (m. 12.3; 2 No'lu Ek Protokol m. 4 ile değişik): 90 gün önceden KEP/noter bildirimiyle fesih hakkı eklendi.

### Çıktı Şablonu

```markdown
# Sözleşme Tadil Geçmişi: [Karşı Taraf] - [Sözleşme Türü]

**Ana Sözleşme:** [tarih]
**Tadil Belgeleri:** [N adet] ([ilk tarih] -> [son tarih])
**Son Değişiklik:** [tarih]
**Sıralama Güveni:** [yüksek / orta / düşük]

## Değişiklik Kronolojisi

### [Belge Türü] [N] - [tarih]
**Amaç:** [gerekçe/amaç veya bilinmiyorsa atla]

**Esaslı Değişiklikler:**
- [Hüküm] (m. [X]): [eski -> yeni sade Türkçe özet]
- [Eklenen Hüküm] (m. [X]): [pratik etkisi]
- [Silinen Hüküm] (m. [X]): [neden önemli olduğu]

## Güncel Net Durum

| Hüküm | Güncel Pozisyon | Dayanak | Son Değişiklik |
|---|---|---|---|
| [madde] | [sade Türkçe özet] | m. [X] | [belge/tarih] |

## Dikkat Edilecek Hususlar
[çelişkiler, madde numarası kaymaları, devir/imza yetkisi boşlukları]
```

## Mod 2 — Tekil Madde Takibi (`--provision`)

Yalnızca ilgili hükme dokunan belgeleri göster; dokunmayan ek protokolleri atla:

```markdown
# Madde Takibi: [Madde / Konu]
## [Karşı Taraf] - [Sözleşme Türü]

### Orijinal Metin - [Ana sözleşme tarihi], m. [X]
> "[kısa birebir alıntı]"

**Özet:** [tek cümle]

### [Belge Türü] [N] - [tarih], m. [X]
**Eski Hali:** "[alıntı]"
**Yeni Hali:** "[alıntı]"
**Ne Değişti:** [pratik etkisi]

## Güncel ve Geçerli Görünen Hüküm
**m. [X] - [kaynak belge, tarih]**
> "[alıntı]"

## İzleme Notları
[çelişkiler, eksik imzalar, sorumluluk sınırı etkileşimi, numara kaymaları]
```

Hüküm hiç tadil edilmemişse:

> Bu hüküm tadil belgeleriyle değiştirilmemiş görünüyor. Ana sözleşmedeki metin yürürlükte görünmektedir; yine de çelişkili genel hükümler ve öncelik sırası maddesi ayrıca incelenmelidir.

## Çelişki Kuralı

Belgeler arasında çelişki varsa hangi hükmün hukuken üstün geleceğine tek başına karar verme:
- her iki hükmü birebir alıntıla,
- öncelik sırası (`order of precedence`) maddesi olup olmadığını kontrol et,
- belirsizliği açıkla ve hukukçu incelemesine yönlendir.

## Türk Hukuku İzleme Kalemleri

- cezai şart (`TBK m. 179–182`, `TTK m. 22`),
- temerrüt faizi (`3095 s. K.`, `TTK m. 1530`),
- ödeme vadesi, döviz (`32 s. Karar`), fiyat eskalasyonu,
- damga vergisi (`488 s. DVK` — matrah artışı veya yeni taahhüt vergisi kontrolü),
- süre uzatımı ve otomatik yenileme,
- fesih hakları ve bildirim usulü (`TTK m. 18/3`),
- yetkili mahkeme, icra dairesi, tahkim ve arabuluculuk,
- KVKK ve veri işleme ekleri,
- FSEK/IP devir veya lisans sınırları,
- münhasırlık / rekabet yasağı / ayartmama,
- kefalet, garanti, ana ortak garantisi veya teminat mektubu.

## Bu Beceri Neleri Yapmaz

- Çelişki halinde hangi maddenin hukuken üstün olduğuna kesin karar vermez.
- Yeni ek protokol veya zeyilname kaleme almaz.
- Tadil edilmiş sözleşmenin sıfırdan tam risk incelemesini yapmaz (`/commercial-legal:review` gerekir).
- Damga vergisi veya muhasebe tutarı hesaplamaz.
- İmzasız/eksik belgelerden kesinleştirilmiş konsolide metin icat etmez.
