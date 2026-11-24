---
name: saas-msa-review
description: >
  Referans: SaaS ve abonelik sözleşmelerini otomatik yenileme, fiyat artışı,
  çıkış/veri taşınabilirliği, SLA, KVKK, alt işleyenler, AI/veri kullanım hakları
  ve renewal-tracker devri açısından Türk hukuku katmanıyla inceler. SaaS veya
  abonelik hükümleri tespit edildiğinde /commercial-legal:review tarafından
  yüklenir.
user-invocable: false
---

# SaaS / Abonelik Sözleşmesi İncelemesi

SaaS ve abonelik sözleşmeleri maliyet, yenileme, veri, çıkış ve hizmet sürekliliği risklerini biriktirir. Bu skill genel commercial playbook'u uygular ve üzerine SaaS'a özgü Türk hukuku ve pratik kontrollerini ekler.

## Matter Bağlamı

Commercial `## Matter Workspaces` kurallarını uygula. Aktif bir matter varsa onu yükle ve çıktıları ilgili matter klasörüne yaz.

## Amaç

SaaS şartlarını ekibin playbook'u ve Türkiye uygulaması çerçevesinde incele. Odak alanları:

- otomatik yenileme ve bildirim süreleri,
- fiyat artışı ve döviz/endeksleme mekanizması,
- veri taşınabilirliği / çıkış (exit),
- SLA / erişilebilirlik (uptime),
- KVKK ve alt işleyenler (subprocessors),
- yapay zekâ (AI) veya makine öğrenmesi veri kullanım hakları,
- sorumluluk sınırı, tazminat, FSEK/fikri mülkiyet, bilgi güvenliği, denetim ve fesih.

## Uygulanacak Hukuk Varsayımı

Profildeki `## Turkish Law Defaults` / uygulanacak hukuk yaklaşımını uygula. Sözleşme yabancı hukuk veya yabancı mahkeme/tahkim seçiyorsa Türk hukuku analizinin doğrudan geçerli olmayabileceğini işaretle; playbook dışındaysa avukat incelemesine eskale et.

## Playbook Yükleme

`commercial-legal/CLAUDE.md` dosyasından şunları oku (`## Playbook`, `## Escalation and Approval Matrix`, `## Outputs`, `## Matter Workspaces`):

- genel satın alma (purchasing-side) veya satış (sales-side) playbook pozisyonları,
- SaaS/abonelik tercihleri,
- KVKK duruşu,
- yenileme ve bildirim tercihleri,
- eskalasyon matrisi.

SaaS pozisyonları profilde eksikse, temiz/onaylı sonuç vermeden önce kullanıcıya sor ve pozisyonu kaydet.

## SaaS'a Özgü İnceleme Katmanı

### 1. Otomatik Yenileme

Şu bilgileri çıkar:

- başlangıç süresi,
- mevcut dönem,
- yenileme mekanizması,
- fesih/yenilememe bildirim süresi,
- bildirim yöntemi (KEP, noter, iadeli taahhütlü — TTK m. 18/3 uyumu kontrolü),
- yenileme fiyatı,
- yenilememenin sonuçları.

Tarih izlenebiliyorsa `renewal-tracker` devri oluştur:

```yaml
renewal_handoff:
  counterparty:
  agreement:
  current_term_end:
  notice_period_days:
  notice_method:
  price_on_renewal:
  annual_value:
  currency: TL
  notes:
```

### 2. Fiyat Artışı

Tek taraflı fiyat değişikliği, "güncel liste fiyatı", TÜFE/ÜFE endekslemesi, döviz/kur artış şartları (Türk Parası Kıymetini Koruma hakkında mevzuat sınırları kontrolü `[doğrula]`), tavan (cap), bildirim süresi ve artış durumunda fesih hakkını kontrol et.

### 3. Veri Taşınabilirliği ve Çıkış (Exit)

Şunları kontrol et:

- veri dışa aktarım formatı,
- çıkış destek süresi,
- verilerin silinmesi / imha tutanağı (KVKK m. 7),
- geçiş (transition) desteği,
- dışa aktarım ücretleri,
- API veya yedek erişimi,
- tedarikçiye bağımlılık (vendor lock-in) riski.

### 4. SLA ve Hizmet Kredileri

Erişilebilirlik (uptime) yüzdesi, istisnalar, planlı bakım saatleri, münhasır çözüm hükmü (remedy exclusivity), hizmet kredileri, tekrarlanan kesintilerde fesih hakkı ve log/denetim erişimini kontrol et.

### 5. KVKK ve Alt İşleyenler

Rolleri belirle:

```yaml
kvkk:
  role: veri_sorumlusu | veri_isleyen | ortak_sorumluluk | belirsiz
  personal_data: true | false | belirsiz
  special_category_data: true | false | belirsiz
  sub_processors: listed | approval_required | notice_only | belirsiz
  cross_border_transfer: true | false | belirsiz
  transfer_mechanism: yeterlilik | uygun_guvence | standart_sozlesme | bcr | taahhutname | arizi_istisna | acik_riza | belirsiz
```

### 6. AI / Makine Öğrenmesi Hakları

Tedarikçinin müşteri verilerini, kullanım verilerini, prompt/girdileri, çıktıları, belgeleri, logları veya üstveriyi (metadata) model eğitimi, analitik, kıyaslama (benchmarking) veya ürün geliştirme amacıyla kullanıp kullanamayacağını işaretle. Belirsizse en az `YELLOW` (Sarı) olarak sınıfla.

### 7. Bilgi Güvenliği ve İhlal Bildirimi

Olay/ihlâl bildirim süresini (KVKK m. 12 ve varsa 7545 s. Kanun uyumu), denetim haklarını, güvenlik standartlarını (ISO 27001 / SOC 2), alt yükleniciyi, loglamayı, erişim kontrollerini, veri barındırma yerini ve sözleşme sonu silmeyi kontrol et.

## Çıktı

`## Outputs` (`### Work Product Header`) uyarınca uygun dahili çalışma başlığını ekle:

```markdown
# SaaS / Abonelik Sözleşmesi İncelemesi: [Karşı Taraf]

## Sonuç
[GREEN / YELLOW / RED veya profildeki playbook statüsü]

## En Önemli Riskler
1. [risk]

## SaaS Kontrol Katmanı
| Konu | Durum | Not |
|---|---|---|
| Yenileme | [uygun/uyarı] | [bildirim tarihi/devir] |
| Fiyat artışı | [uygun/uyarı] | [tavan/sınırsız] |
| KVKK | [uygun/uyarı] | [rol/yurt dışı aktarım] |
| SLA | [uygun/uyarı] | [uptime/tazmin] |
| Çıkış (Exit) | [uygun/uyarı] | [veri iadesi/imha] |

## Önerilen Revizyonlar
[uygulanabilir en sade metin değişiklikleri]

## Yenileme Devri (Renewal Handoff)
[uygulanıyorsa]

## Sonraki Adımlar
[hukuk / iş sahibi / renewal tracker]
```

## Yapmadıkları

- SaaS sistemini fiilen işletmez veya teknik beyanları doğrulamaz.
- Tam kapsamlı siber güvenlik denetiminin yerine geçmez.
- Kişisel veri işlemenin esaslı olduğu durumlarda KVKK veri işleyen (DPA) incelemesinin yerine geçmez.
- Yenileme veya fesih kararını kendisi vermez; tarihleri `renewal-tracker` akışına devreder.
