---
name: launch-review
description: >
  Türk ürün hukuku çerçevesinde PRD, ticket veya lansman dokümanını kategori
  kategori inceler. Kullanıcı "review this launch", "legal review", "can we
  ship", "lansman incelemesi" veya PRD/ticket verdiğinde kullan.
argument-hint: "[PRD file | Drive link | tracker ticket ID]"
---

# /launch-review

## Akış

1. `~/.claude/plugins/config/legal-turkish/product-legal/CLAUDE.md` profilini oku; placeholder varsa cold-start iste.
2. PRD, ticket, tasarım, checkout akışı, reklam/plan, policy ve hedef pazar bilgisini topla.
3. `references/seven-category-framework.md` içindeki Türk product launch framework'ünü veya profilin kendi framework'ünü uygula.
4. Bulguları profil risk kalibrasyonuna göre `Düşük / Orta / Yüksek / Bloke` olarak sınıfla.
5. KVKK varsa `/privacy-legal:use-case-triage`; AI varsa `/ai-governance-legal:use-case-triage`; reklam iddiası varsa `/product-legal:marketing-claims-review` handoff'u yap.
6. İç hukuk notu ve paylaşılabilir ticket yorumu olarak iki ayrı çıktı üret.

## Girdi Kontrolü

- Ürün/özellik ne yapıyor?
- Kim kullanıyor: tüketici, tacir, çalışan, çocuk, hasta, finansal tüketici, kamu?
- Hedef pazar: Türkiye, AB, ABD veya diğer?
- Yeni veri, yeni amaç, yeni vendor, yeni fiyat/abonelik, yeni reklam iddiası, yeni sektör veya yeni AI bileşeni var mı?
- Lansman tarihi ve geri alma imkânı nedir?

## Kategori Çıktısı

Her kategori için şu format kullanılır:

```markdown
### [Kategori]

**Kontrol edilen:** [PRD/ticket/policy/metin/ekran]
**Sonuç:** [Temiz | İş gerekiyor | Yüksek risk | Bloke | Uygulanmaz]
**Neden:** [somut bulgu, genel ders değil]
**Kaynak / doğrulama:** [resmî kaynak / kullanıcı sağladı / doğrula]
**Kalibrasyon:** [profildeki pattern veya "yeni pattern"]
**Aksiyon:** [ne yapılacak, kim, ne zamana kadar]
```

Uygulanmayan kategori tek cümleyle açıklanır; boş kontrol listesi doldurulmaz.

## Varsayılan Kategoriler

1. Sözleşme ve kullanıcı taahhütleri.
2. KVKK ve veri.
3. Reklam ve haksız ticari uygulamalar.
4. E-ticaret, checkout ve abonelik.
5. Ürün güvenliği, erişilebilirlik ve sektör.
6. Fikri haklar ve içerik.
7. Güvenlik ve üçüncü taraflar.
8. AI / otomasyon.

## Sektör Overlay

Şu işaretler varsa kategoriye ek overlay ekle ve güncel resmî kaynak doğrula:

| İşaret | Overlay |
|---|---|
| Çocuk/öğrenci | KVKK çocuk verisi, reklamda çocuk istismarı yasağı, eğitim sektörü, platform yaş derecelendirmesi |
| Sağlık/gıda/kozmetik/takviye | TİTCK, ilgili Bakanlık mevzuatı, sağlık beyanları, Reklam Kurulu |
| Finans/ödeme/kripto/yatırım | BDDK, TCMB, SPK, MASAK, finansal tüketici, yatırım tavsiyesi |
| Telekom/iletişim | BTK, elektronik haberleşme, ticari ileti |
| Oyun/şans/bahis/loot box | Şans/bahis mevzuatı, tüketici, platform yaş sınıfı, ödeme/iade |
| Kamu/ihale | Kamu ihale/sözleşme, veri lokasyonu, güvenlik, sektör izinleri |
| Pazaryeri | ETHS/ETAHS, mesafeli sözleşme rolleri, satıcı bilgisi, ürün güvenliği |

## Çıktı

```markdown
[GİZLİ HUKUKİ / ÜRÜN HUKUKU ÇALIŞMA TASLAĞI - HUKUKÇU İNCELEMESİNE TABİDİR]

Reviewer note
- Kaynaklar:
- Okuma kapsamı:
- Doğrulanması gerekenler:
- Aksiyon öncesi:

# Lansman İncelemesi: [Özellik]

**Tarih:** [YYYY-MM-DD]
**Lansman tarihi:** [varsa]
**PRD/Ticket:** [link/path]

## Kısa sonuç

**Çağrı:** [Ship edilebilir | Şartlı ship | Hukuk/uyum onayı gerekli | Bloke]

[Bir paragraf: ne ship oluyor, ana risk, ship için hangi şartlar gerekir.]

## Bulgular

[Kategori blokları]

## Aksiyonlar

| # | Aksiyon | Sahip | Son tarih | Bloke mi? |
|---|---|---|---|---|

## Eskalasyonlar

[Gerekirse]

## Sonraki kalibrasyon notu

[Bu pattern profil kalibrasyonuna eklenmeli mi?]

---

## SAFE TO POST TO TRACKER

**Launch status:** [green / yellow / red]

**Conditions:**
- [ ] [PM/eng/legal aksiyonu] - Owner: [ ] - Due: [ ]
```

Tracker yorumu hukuki gerekçe, kaynak, gizli analiz veya regülasyon tartışması içermez; sadece yapılacakları söyler.

## Yapmadıkları

- Lansmanı onaylamaz.
- Resmî kaynak kontrolü yapılmadan güncel tutar, ceza, eşik veya platform politikası kesinleştirmez.
- Teknik güvenlik veya ürün performansını belge olmadan doğru varsaymaz.
