---
name: renewal-tracker
description: >
  Türk bildirim ve tebligat pratiğine göre uyarlanmış yenileme kayıt defterini
  kullanarak fesih ihbarı veya yenilememe bildirim tarihleri yaklaşan sözleşmeleri
  listeler ve süre penceresi kapanmadan uyarır. Yaklaşan yenilemeler veya
  kaçırılan fesih pencereleri sorulduğunda çalışır.
argument-hint: "[--days N ile gün penceresini değiştir | --missed kaçırılan pencereler için]"
---

# Sözleşme Yenileme ve Fesih İhbar Takibi (`/renewal-tracker`)

Sözleşmelerin otomatik yenileme, dönem sonu ve fesih ihbar tarihlerini izler. Yenilemeye veya feshe karar vermez; karar verilmesi gereken tarihi ve güvenli gönderim penceresini görünür kılar.

## Talimatlar

1. `~/.claude/plugins/config/legal-turkish/commercial-legal/renewal-register.yaml` (veya şablon testinde eklenti altındaki örnek kayıt defterini) oku.
2. Varsayılan mod: `send_by_effective` tarihine göre önümüzdeki **90 günü** aciliyet bantlarına ayırarak göster.
3. `--days N`: pencereyi `N` gün olarak değiştir.
4. `--missed`: fesih/yenilememe kaydı düşülmeden süresi geçmiş sözleşmeleri listele.
5. Kayıt defteri boşsa ve belge deposu/arşiv bağlıysa tarama ve toplu içe aktarım teklif et.
6. Her öneride iş birimi sahibini, varsa hukuk sorumlusunu, bildirim yöntemini ve fiyat artış riskini göster.

## Kayıt Şeması (`Register Schema`)

Kayıtlar Türk hukukunda bildirim şekli ve ulaşma tamponunu yansıtan şu şemada tutulur:

```yaml
- counterparty: "Acme Yazılım A.Ş."
  agreement: "Platform Abonelik Sözleşmesi"
  signed_date: 2025-06-15
  initial_term_end: 2026-06-15
  current_term_end: 2026-06-15
  renewal_mechanism: "otomatik yıllık yenileme"
  notice_period_days: 60
  notice_method: "kep"               # noter | kep | iadeli_taahhutlu_posta | e-posta | portal | sözleşmeye göre
  transit_buffer_days: 0
  cancel_by_calendar: 2026-04-16
  cancel_by_effective: 2026-04-16
  send_by_effective: 2026-04-16
  cancel_by_roll_note: ""
  cancel_by_provenance: "[model hesabı - bildirim maddesinden doğrulayın]"
  price_on_renewal: "TÜFE/ÜFE veya güncel tarife"
  annual_value: 48000
  currency: "TL"
  business_owner: "[sorumlu-birim]"
  clm_id:
  uyap_no: ""                         # yalnızca dava/icra dosyasına bağlıysa
  status: "active"                    # active | cancelled | renewed | lapsed
  notes:
```

## Türk Hukuku Bildirim Yöntemi Kontrolü

Tacirler arasında temerrüt, sözleşmeden dönme ve **fesih ihbarları** `TTK m. 18/3` uyarınca kural olarak **noter, taahhütlü mektup, telgraf veya güvenli elektronik imza ile kayıtlı elektronik posta (KEP)** üzerinden yapılmalıdır (ayrıca sözleşmedeki bildirim maddesi her zaman kontrol edilir).

Sözleşme açıkça imkân tanımıyorsa ve ispat riski göze alınmıyorsa sıradan e-postayı yeterli sayma; e-posta öngörülmüşse ulaşma/ispat riskini ve `KEP Yönetmeliği m. 15/2` 24 saat okundu karinesi tamponunu işaretle.

## Tarih Hesaplama İlkeleri

Üç tarihi ayrı ayrı takip et:
- `cancel_by_calendar`: ham takvim hesabı.
- `cancel_by_effective`: sözleşme lafzı ve iş günü riskine göre bildirimin muhataba varması gereken son tarih.
- `send_by_effective`: tebligat/posta/KEP ulaşma tamponu düşüldükten sonraki **en geç gönderim tarihi**.

Aciliyet uyarılarında **`send_by_effective`** esas alınır. Resmî tatil veya hafta sonu sarkması belirsizse hesabı `[geçici — doğrulayın]` olarak işaretle.

> **Hukuki İncelik (`TBK m. 93`):** Resmî tatil veya hafta sonu son günün ilk iş gününe uzaması ihtimali olsa bile bu takip aracı risk azaltıcı yaklaşım izler; son tarihe güvenmek yerine daha erken uyarır. Kesin hukuki son gün sözleşmedeki bildirim maddesi incelenerek netleştirilmelidir.

## Çalışma Modları

### Mod 1 — Yeni Yenileme Kaydı Ekleme
Bir sözleşme inceleme becerisi yenileme/fesih maddesi yakaladığında kayıt defterine ekle veya güncelle; aynı karşı tarafta mevcut kayıt varsa ikame, ek protokol mü yoksa ayrı sözleşme mi olduğunu sor.

### Mod 2 — Yaklaşan Yenilemeler
`send_by_effective` gün sayısına göre her sözleşme tek bir aciliyet bandına girer:
- **KIRMIZI:** `0–13` gün
- **TURUNCU:** `14–44` gün
- **SARI:** `45–89` gün

```markdown
## Yenileme ve Fesih İhbar Takvimi - Önümüzdeki [N] Gün

### KIRMIZI - 0–13 Gün
| Karşı Taraf | En Geç Gönderim | Dönem Sonu | Yıllık Değer | Sahibi | Bildirim | Not |
|---|---|---|---|---|---|---|
| [Ad] | **[tarih]** | [tarih] | [Tutar] | [Sahip] | [KEP/Noter] | [Notlar] |

### TURUNCU - 14–44 Gün
[aynı tablo]

### SARI - 45–89 Gün
[aynı tablo]

## Önerilen Aksiyonlar
- [ ] [Karşı Taraf] — [İş birimi sahibine] sor: sözleşmeye devam etmek istiyor muyuz?
- [ ] [Karşı Taraf] — yenileme fiyat artışı sınırsız; ihbar penceresi kapanmadan alternatif teklif alınmalı.
```

### Mod 3 — Sözleşme Arşivini Tarama
Belge deposu/Google Drive bağlıysa aktif sözleşmelerde `yenileme`, `otomatik yenileme`, `fesih`, `ihbar`, `süreli`, `müddetli`, `renewal`, `auto-renew`, `termination`, `notice` terimlerini ara; taslak kayıt çıkar ve belirsiz olanları manuel inceleme için işaretle.

### Mod 4 — Kaçırılan Fesih Pencereleri
`send_by_effective` veya `cancel_by_effective` tarihi geçtiği halde iptal kaydı bulunmayan sözleşmeleri ve kurtarma seçeneklerini (karşılıklı ikale/sonlandırma pazarlığı, sonraki dönem şimdiden takvimleme, haklı/olağanüstü fesih incelemesi) raporla.

## Yenileme / Fesih Kapısı

Takip yapmak yalnızca hazırlıktır. Yenilememe ihtarı çekmek, sözleşmeyi sonlandırmak veya yenilemeye izin vermek hukuki sonuç doğurur (`TTK m. 18/3`). Kullanıcı hukukçu değilse şu kapıyı uygula:

> Bu işlem sözleşmeyi sona erdirebilir veya şirketi yeni bir dönem için borç altına sokabilir. Şirket avukatı veya yetkili hukukçu ile teyitleştiniz mi?

Açık yetkilendirme olmadan ihtarname gönderildiğini varsayma. Veri yoğun (`>10` satır) listelerde `CLAUDE.md` içindeki `## Outputs` uyarınca XSS ve CSV formül korumalı HTML pano üretmeyi teklif et.

## Bu Beceri Neleri Yapmaz

- Sözleşmeleri kendiliğinden feshetmez.
- Yenileme veya fesih kararını işletme yerine vermez.
- Noter veya KEP üzerinden otomatik ihtar göndermez.
- Bildirim maddesini okumadan kesin hukuki son gün ilan etmez.
- Vergi, muhasebe veya bütçe hesabını teknik mali inceleme yerine koymaz.
