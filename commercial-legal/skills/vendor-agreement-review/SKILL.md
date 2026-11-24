---
name: vendor-agreement-review
description: >
  Gelen tedarikçi, hizmet, MSA veya ticari sözleşmeleri Türk ticaret hukuku
  playbook'una göre inceler; sapmaları işaretler, cerrahi redline önerir ve
  onayları yönlendirir. /commercial-legal:review tarafından tedarikçi
  sözleşmesi algılandığında yüklenir.
user-invocable: false
---

# Tedarikçi Sözleşmesi İncelemesi

Bu beceri bir tedarikçi, hizmet, ana hizmet sözleşmesi (MSA) veya benzeri ticari sözleşmeyi `CLAUDE.md` içindeki playbook'a göre inceler. Çıktı, avukat incelemesine tabi çalışma taslağıdır.

## Dosya Bağlamı ve Hedef Kitle Kontrolü

`## Matter Workspaces` kurallarını uygula. Çıktı üretmeden önce hedefin neresi olduğunu kontrol et; hukuk ekibi / gizlilik çemberi dışına paylaşılacaksa dahili strateji notlarından arındırılmış ticari sürüm öner (`## Outputs` -> `### Destination Rule`).

## Amaç

Sözleşmeyi baştan sona oku, her esaslı hükmü ekibin playbook'u ile karşılaştır, sapmaları tespit et, cerrahi redline önerileri hazırla ve `## Escalation and Approval Matrix` uyarınca onay akışına yönlendir.

## Playbook'u Yükle

`~/.claude/plugins/config/legal-turkish/commercial-legal/CLAUDE.md` dosyasından şunları oku:
- `## Playbook` -> şirketin tarafına (`purchasing-side` / `sales-side`) özel pozisyonlar,
- `## Escalation and Approval Matrix`,
- `## Turkish Contract Concepts`,
- `## Outputs`,
- aktif dosya varsa dosya bazlı istisnalar.

Playbook yapılandırılmamışsa yalnızca varsayılan Türk hukuku kontrol listesiyle geçici modda çalış ve şu uyarıyı ekle:

> Playbook eksik. Varsayılan Türk hukuku kontrol listesine göre ön bulgu çıkarabilirim; ancak imza/YEŞİL onayı öneremem.

## İş Akışı

### Adım 1 — Genel Çerçeve ve Yönelim (`Orientation`)
Sözleşmeden şunları çıkar:
- taraflar ve rolleri,
- sözleşme türü,
- toplam bedel, ödeme vadeleri ve döviz varsa `32 s. Karar` / TL karşılığı kontrolü,
- süre, otomatik yenileme ve bildirim şekli (`TTK m. 18/3`),
- uygulanacak hukuk, yetkili mahkeme/icra veya tahkim,
- imza yetkisi ve temsil durumu,
- kişisel veri / KVKK teması,
- bağlı bir dosya veya gerçek bir UYAP kaydı varsa künyesi.

### Adım 2 — Kırmızı Çizgi Kontrolü (`Deal-Breaker Check`)
Türk ticaret hukuku pratiğinde kritik riskleri tara:
- üst sınırsız sorumluluk veya ağır kusur dışındaki sınırsız tazminat halleri,
- tek taraflı veya fahiş cezai şart (`TBK m. 179–182`; tacirler için `TTK m. 22` ve `TBK m. 27`),
- geniş kapsamlı rücu/tazminat (`indemnity`) veya garanti taahhütleri,
- FSEK / sınai mülkiyet hakkı devri veya aşırı geniş lisans,
- onaylı mekanizma olmadan yurt dışına KVKK veri aktarımı (`KVKK m. 9`),
- geniş denetim veya müşterek müşteri verisine erişim yükümlülükleri,
- playbook dışı yabancı uygulanacak hukuk veya yabancı mahkeme,
- tahkim kurumu, yeri veya dili belirsiz uyuşmazlık maddesi,
- münhasırlık, rekabet etmeme, çalışan/müşteri ayartmama (`TBK m. 444–447` / `TTK m. 54–55`),
- üst sınırsız tek taraflı fiyat artışı,
- uygulamada takip edilemeyecek dar fesih/yenilememe ihbar süresi,
- kefalet (`TBK m. 583` eş rızası / şekil şartı!), ana şirket garantisi, teminat mektubu,
- kamu ihalesi (`4734`) veya sektörel düzenleme (BDDK/TCMB dış hizmet, BTK, SPK, EPDK) etkisi,
- `damga vergisi (488 s. DVK)` veya mali inceleme gerektiren taahhüt, teminat, tadil, sulh ya da devir yapısı.

### Adım 3 — Madde Madde İnceleme
Her önemli bulgu için:
- ilgili sözleşme hükmünden kısa birebir alıntı yap,
- playbook pozisyonunu belirt,
- Türk hukuku ve uygulama riskini sade dille açıkla,
- daraltıcı revizyon (redline) öner veya eskalasyona taşı,
- gerekiyorsa onay makamını adlandır.

### Adım 4 — Onay Yönlendirmesi (`Approval Routing`)
Yetki sınırını aşan konularda eskalasyon bloğunu doldur:

```yaml
escalation:
  issue:
  approver:
  reason:
  deadline:
```

### Adım 5 — Yenileme Takibine Aktarım
Otomatik yenileme veya fesih ihbar süresi saptanırsa `/commercial-legal:renewal-tracker` (Mod 1) kaydı öner.

## Çıktı Şablonu

`CLAUDE.md` içindeki `## Outputs` → `### Work Product Header` başlığını ve `Reviewer note` bloğunu ekleyerek sun:

```markdown
# Tedarikçi Sözleşmesi İncelemesi: [Karşı Taraf] - [Sözleşme Türü]

## Yönetici Özeti
[Net sonuç: İmzaya Uygun / Müzakere Edilmeli / Durdurulmalı / Eksik Bilgi]

## Kırmızı Çizgi Kontrolü
| Konu | Durum | Özet |
|---|---|---|
| Sorumluluk Sınırı | [uygun / riskli] | [kısa özet] |

## Önem Derecesine Göre Bulgular

### [Önem] - [Konu] - Madde [X]
> "[kısa alıntı]"

**Risk:** [sade Türkçe risk açıklaması]
**Playbook:** [ilgili playbook pozisyonu]
**Önerilen Revizyon:** "[cerrahi değişiklik metni]"
**Onay:** [yok / onay makamı]

## Lehe Maddeler ve Eksik Koruma Hükümleri
[lehe hükümler ile sözleşmede eksik bırakılmış koruyucu maddeler]

## KVKK / Rekabet / Yenileme Notları
[ilgili oldukları ölçüde]

## Sonraki Adımlar
[aksiyon listesi]
```

## Redline Kuralları

Küçük ve hedefli değişiklikleri tercih et; sözleşmenin tamamını yeniden kaleme alma. Bir maddenin tamamen sıfırdan yazılması gerekiyorsa hukukçunun taslak hazırlaması gerektiğini açıkça belirt.

## Bu Beceri Neleri Yapmaz

- İmza onayı vermez.
- Karşı tarafa redline göndermez.
- Onay makamının yetkisindeki ticari risk kararını üstlenmez.
- Yabancı hukukta kesin hukuki mütalaa sunmaz.
- Uzman DPA/KVKK, vergi, finans veya siber güvenlik incelemesinin yerine geçmez.
