---
name: portfolio
description: >
  Fikri ve sınai mülkiyet portföyünü izler — marka/tasarım yenilemeleri
  (SMK m. 23, m. 69), patent/faydalı model Yıllık Sicil Ücretleri (SMK m. 101),
  5 yıllık kullanmama iptal riski (SMK m. 9 ve m. 26) ve TRABİS/WIPO/EPO
  vadelerini yönetir (`--report`, `--add`, `--update`, `--audit`).
argument-hint: "[--report [--days N] | --add | --update | --audit]"
---

# /portfolio

Yaklaşan IP vadelerini raporlar, yeni hak kaydı ekler, yapılan harç/yenileme ödemelerini işler ve portföyü denetler (`~/.claude/plugins/config/legal-turkish/ip-legal/portfolio.yaml`).

## Kullanım Komutları

- `/ip-legal:portfolio` (veya `--report [--days 30|60|90|180]`) — Varsayılan 90 günlük penceredeki vadeleri aciliyet sırasıyla raporlar.
- `/ip-legal:portfolio --add` — Etkileşimli olarak yeni marka, patent/faydalı model, tasarım, telif kaydı veya alan adı ekler.
- `/ip-legal:portfolio --update` — Yenileme veya yıllık sicil ücreti ödemesini (`filed`) ya da statü değişikliğini işler.
- `/ip-legal:portfolio --audit` — Portföy sağlığı denetimi: ek süreli/düşmüş kayıtlar, uzun süredir sonuçlanmamış başvurular, **SMK m. 9/26 5 yıllık kullanmama riski**, sahip tutarsızlıkları ve izlenmeyen markalar.

## Hukuki Çerçeve ve Süre Varsayımları

Hesaplanan tarihler yalnızca referanstır; **hak düşürücü sonuç doğurmaması için işlem öncesi TÜRKPATENT EPATS/sicil, WIPO Madrid Monitor, EPO Register veya yetkili marka/patent vekilinden canlı teyit alınmalıdır (`references/currency-watch.md`).**

- **Türkiye Markaları (TÜRKPATENT — SMK m. 23):** Koruma süresi başvuru tarihinden itibaren **10 yıl**dır ve 10'ar yıllık dönemlerle yenilenebilir. Olağan yenileme koruma bitiş tarihinden önceki 6 ay içinde; **ek ücretli (cezalı) yenileme** koruma bitiş tarihinden sonraki **6 ay içinde** yapılabilir `[doğrula]`. Türk hukukunda ABD §8/§9 ara kullanım beyanı yoktur; ancak **SMK m. 9 ve m. 26** uyarınca tescilden itibaren 5 yıl içinde ciddi kullanım yoksa TÜRKPATENT nezdinde idari iptal riski doğar `[doğrula]`.
- **Türkiye Patent ve Faydalı Modelleri (TÜRKPATENT — SMK m. 101):** Yıllık sicil ücretleri başvuru tarihinden itibaren **2. yılın sona ermesiyle (3. yıldan başlayarak)** koruma süresi boyunca (patent 20 yıl, faydalı model 10 yıl) her yıl vadesinde ödenir. Vade kaçırılırsa takip eden **6 ay içinde ek ücretle** ödenebilir `[doğrula]`.
- **Türkiye Tasarımları (TÜRKPATENT — SMK m. 69):** Başvuru tarihinden itibaren 5 yıl; 5'er yıllık yenilemelerle toplam 25 yıl; 6 ay ek ücretli yenileme süresi vardır `[doğrula]`.
- **Türkiye Telif Hakları (5846 s. FSEK):** Tescile bağlı değildir; koruma kural olarak eser sahibinin yaşamı + 70 yıldır (m. 27), yenileme takibi gerekmez.
- **Alan Adları (TRABİS `.tr` / `.com`):** Yıllık veya çok yıllık yenileme ve kısa ek/kurtarma pencereleri.
- **Uluslararası (WIPO Madrid / Lahey / EPO / EUIPO):** Ülke ve bölge kuralları (`custom_rules:` altında veya `agent_managed: true` yerel vekil takibinde).

## Kayıt Şeması (`portfolio.yaml`)

Yol: `~/.claude/plugins/config/legal-turkish/ip-legal/portfolio.yaml` (makine alanları canonical `english_snake_case`, açıklamalar ve değerler Türkçe):

```yaml
# IP Portfolio Register
# Disclaimer: computed deadlines are reference only — confirm with TURKPATENT/WIPO/EPO before acting.

metadata:
  company: "[Kurum Adı]"
  generated: "[YYYY-MM-DD]"
  last_updated: "[YYYY-MM-DD]"
  last_audit: "[YYYY-MM-DD or null]"
  source_system: "[manual / vekil_export / yok]"

custom_rules: []

assets:
  - id: "MRK-TR-001"
    type: "trademark"                          # trademark | patent | design | copyright | domain
    jurisdiction: "TR"
    mark_or_title: "[Marka Örneği]"
    owner: "[Hak Sahibi A.Ş.]"
    status: "registered"                       # pending | registered | lapsed | abandoned | cancelled
    application_number: "2021/12345"
    registration_number: "2022 12345"
    classes: ["9", "42"]
    filing_date: "2021-06-15"
    registration_date: "2022-03-10"
    priority_date: null
    grant_date: null
    next_deadlines:
      - type: "Marka Yenileme (10 Yıl — SMK m. 23)"
        due_date: "2031-06-15"
        grace_end: "2031-12-15"                # +6 ay ek ücretli süre [doğrula]
        basis: "Başvuru tarihinden itibaren 10. yıl"
        action: "TÜRKPATENT nezdinde yenileme talebi ve harç ödemesi"
        status: "upcoming"                     # upcoming | due_soon | overdue | grace | lapsed | filed
    use_in_commerce: true                      # SMK m. 9/26 5 yıllık kullanım riski kontrolü
    agent_managed: false
    local_agent: null
    docket_id: null
    outside_counsel: null
    business_owner: "[ürün-ekibi]"
    notes: ""

  - id: "PAT-TR-001"
    type: "patent"
    jurisdiction: "TR"
    mark_or_title: "[Buluş Başlığı]"
    owner: "[Hak Sahibi A.Ş.]"
    status: "granted"
    application_number: "2024/00123"
    registration_number: "TR 2024 00123 B"
    filing_date: "2024-02-01"
    grant_date: "2025-11-15"
    priority_date: null
    expiration_date: "2044-02-01"
    next_deadlines:
      - type: "Yıllık Sicil Ücreti (SMK m. 101 - 3. yıl)"
        due_date: "2026-02-01"
        grace_end: "2026-08-01"                # +6 ay ek ücretli süre (SMK m. 101/2) [doğrula]
        basis: "Başvuru tarihinden itibaren 2. yılın sonundan başlayarak her yıl"
        action: "TÜRKPATENT üzerinden yıllık sicil ücreti ödemesi"
        status: "due_soon"
    claims_count: 15
    docket_id: null
    outside_counsel: "[Vekil Bürosu]"
    business_owner: "[Ar-Ge]"
    notes: ""
```

## Modlara Göre İş Akışı

### Mod 1 (`--init` / İlk Kurulum)
Dosya yoksa kullanıcının dışa aktardığı Excel/CSV veya etkileşimli girişiyle `portfolio.yaml` oluştur; tarihi eksik varlıkları `unknown` işaretle.

### Mod 2 (`--report`)
Çalıştırmadan önce tüm vadeleri bugünkü tarihe göre yeniden hesapla. Üste `## Çıktılar` çalışma başlığını koy ve şu gruplamayı kullan:
- 🔴 `EK ÜCRETLİ SÜREDE (GRACE) / DÜŞMÜŞ`
- ⏰ `PENCERE İÇİNDE VADESİ DOLANLAR`
- 🟡 `YAKLAŞANLAR`
- 🌐 `VEKİL TAKİBİNDEKİLER (Yurt Dışı)`
- ❓ `EKSİK VERİ (HESAPLANAMADI)`

10'dan fazla varlık varsa `` `## Çıktılar → Veri Yoğun Çıktılarda Pano Teklifi` `` uyarınca filtrelenebilir pano teklif et.

### Mod 3 (`--add`)
Varlık türü, ülke, ad/marka, sicil maliki, temel tarihler, numara, Nice sınıfları/istem sayısı, dış vekil ve iş sahibini alıp ekle; bilinmeyen ülke kuralları için `custom_rules:` sorularını sor.

### Mod 4 (`--update`) — Hukuki Sonuç Kapısı
`status: filed` olarak işaretlemeden önce `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` → `## Kullanıcı Rolü` kontrol et. Kullanıcı **Non-lawyer** ise:
> Bir yenileme veya yıllık sicil ücretini `"ödendi/yapıldı (filed)"` olarak işaretlemek takip alarmını kapatır; yanlış tarih, yanlış tutar veya reddedilen işlem hak kaybına yol açar. İşlemin fiilen yapıldığını yetkili avukat/vekil veya TÜRKPATENT EPATS / WIPO alındı belgesinden doğruladınız mı?

Açık teyit olmadan `filed` yazma (gerekirse bağlı Baro/TÜRKPATENT vekil siciline yönlendir).

### Mod 5 (`--audit`)
- `grace` ve `lapsed` durumundaki kalemler, vadesi hesaplanamayanlar.
- 18 aydan uzun süredir `pending` marka başvuruları ve 4 yıldan uzun süredir `pending` patent başvuruları.
- **SMK m. 9 / m. 26 Kullanmama Riski:** Tescilinin 5. yılına yaklaşan ve `use_in_commerce: false` olan markalar.
- Hak sahibi (unvan/birleşme sonrası intikal sicil kaydı SMK m. 148) tutarsızlıkları, 24 ay içinde süresi dolacak patentler ve `## Marka Koruma ve İzleme` listesinde eksik markalar.

## `ip-renewal-watcher` Entegrasyonu ve Yapmadıkları

- Eklentideki `ip-renewal-watcher` ajanı bu skill'in Mod 2 raporunu haftalık çalıştırıp `## Marka Koruma ve İzleme` → `Yenileme bildirim kanalı` hedefine bildirir.
- **TÜRKPATENT / WIPO / EPO nezdinde başvuru veya ödeme yapmaz;** yalnızca hesaplanan referans vadeleri gösterir ve kullanıcının resmî sicilden doğrulamasını zorunlu kılar.
