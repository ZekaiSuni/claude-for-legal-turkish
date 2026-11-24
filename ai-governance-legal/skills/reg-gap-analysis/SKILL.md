---
name: reg-gap-analysis
description: >
  Yeni bir Türkiye yapay zekâ/veri/siber güvenlik düzenlemesini veya rehberini
  (KVKK duyurusu, 7545 s. Kanun tebliği, TİHEK/Rekabet Kurumu/Reklam Kurulu
  kararı, sektör tebliği ya da sınır ötesi AB AI Act tasarrufu) kurumun mevcut
  yönetişim duruşuyla karşılaştırır; boşlukları, öncelikleri ve iyileştirme
  (remediation) planını çıkarır.
argument-hint: "[düzenleme adı, mevzuat metni yapıştırın veya dosya verin]"
---

# /reg-gap-analysis

## İş Akışı

1. `~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md` dosyasını (`## Şirket Profili`, `## Yapay Zekâ Kullanım Envanteri`, `## AI Politika Taahhütleri`, `## Tedarikçi AI Yönetişimi`, `## Etki Değerlendirmesi (YZED / AIA) Kurum Stili`, `## Çıktılar`) oku.
2. **Önce kapsam kontrolü yap:** Düzenleme kuruma gerçekten uygulanıyor mu? (Yargı alanı, eşik değer, geliştirici/kullanıcı rolü, sektör muafiyeti.) Açıkça kapsam dışıysa tek cümleyle açıkla (`"Uygulanmaz. Gerekçe: [...]. Aksiyon gerekmez."`) ve gereksiz analiz üretme.
3. Yürürlükteki metinden (birincil kaynaktan araştırarak veya kullanıcının verdiği metinden) somut yükümlülükleri ayrıştır.
4. Mevcut duruşla kıyasla (`Gap: Yok / Kısmi / Tam`).
5. Önceliklendir ve tarihli İyileştirme Planı (`Remediation Plan`) oluştur.

## Mevcut Durum ve Araştırma Kuralları

Sabit eski tablolara yaslanma; her kapsam içi rejim için şu başlıkları kontrol et:
- **Kapsam & Rol:** Geliştirici (Provider) mi, Kullanıcı (Deployer) mı, yoksa sektör kurumuna tabi kuruluş mu?
- **Eşik ve Sektör İstisnaları:** Ciro, kullanıcı sayısı, kritik altyapı statüsü (7545 s. K.), kamu hizmeti vs.
- **Yürürlük ve Geçiş Takvimi:** Resmî Gazete yayım tarihi ile fiilî yürürlük/uygulama tarihi farkı; AB AI Act aşamalı takvimi.
- **Neyin Yeni Olduğu:** Mevcut KVKK / TKHK / TİHEK / TTK yükümlülüklerinin tekrarı mı, yoksa yeni bildirim, kayıt veya denetim mecburiyeti mi?

> **Sessiz tamamlama yok & 3 kademeli kaynak etiketi:**
> - **`[yerleşik]`:** Değişmesi düşük olasılıklı temel normlar (ör. KVKK m. 11/1-(g) — otomatik sistemlerle analiz sonucu itiraz hakkı; not: KVKK m. 22 Kurulun görevlerini düzenler, AB'de ise GDPR m. 22 ve (AB) 2024/1689 AI Act geçerlidir).
> - **`[doğrula]`:** İkincil yönetmelikler, KVKK/Rekabet/TİHEK rehberleri, 7545 s. Kanun ikincil düzenlemeleri, parasal ceza tutarları, AB AI Act uygulama tasarrufları ve yürürlük tarihleri.
> - **`[kesin-madde-doğrula]` (`[verify-pinpoint]`):** Spesifik fıkra, bent ve Ek numaraları mutlaka `mevzuat.gov.tr`, `resmigazete.gov.tr`, `kvkk.gov.tr` veya `EUR-Lex` üzerinden kontrol edilmelidir.
>
> **Non-lawyer kullanıcı kuralı:** `## Kullanıcı Rolü` non-lawyer ise belirsiz yürürlük/eşik tarihlerini `"yürürlük tarihi: avukatla teyit edilmeli"` diye işaretle ve tüm belirsiz maddeleri belgenin en sonunda **"Emin Olmadığım Noktalar — Onay Öncesinde Avukatınıza Sorun"** başlığı altında topla.

## Adım 2: Yükümlülük Kategorileri

| # | Yükümlülük | Madde / Atıf | Kategori |
|---|---|---|---|

Kategoriler: **Şeffaflık ve Aydınlatma** · **Etki Değerlendirmesi (YZED/PIA)** · **İnsan Gözetimi & İtiraz (KVKK m. 11/1-(g))** · **Doğruluk / Yanlılık Testi (TİHEK/4857)** · **Yönetişim / Kayıt / 7545 Bildirim** · **Tedarikçi Sözleşmesine Yansıtma (Flow-down)** · **Yasaklı Uygulamalar** · **İlgili Kişi Hakları**.

## Adım 3: Mevcut Durumla Kıyas (`Diff`)

Her yükümlülük için:
- **Düzenleme diyor ki:** [somut gereklilik]
- **Mevcut durumumuz:** [`CLAUDE.md` / politika / envanter / YZED pratiği]
- **Gap:** `Yok` | `Kısmi` | `Tam`
- **Eksik olan somut unsur:** [örn. "İK CV eleme aracında aday itiraz kanalı ve yanlılık testi belgelenmemiş"]
- **Kapatma çabası:** `Yalnızca politika güncellemesi` | `Süreç değişikliği` | `Ürün/sistem değişikliği` | `Yeni YZED` | `Tedarikçi sözleşmesi ek protokolü` | `Kurum bildirimi`
- **Uyumsuzluk riski:** [idari para cezası / faaliyet durdurma / itibar riski `[doğrula]`]

## Adım 4: Önceliklendirme Sırası

1. **Kesin yürürlük/ceza tarihi yaklaşan zorunluluklar**
2. **Yasaklı uygulamalar (Prohibited practices)** — yürürlük tarihinden bağımsız ilk sıradadır
3. **Etki/çaba oranı**
4. **Envanterde birden çok sistemi etkileyen ortak boşluklar**

## Adım 5: İyileştirme Planı (Remediation Plan)

```markdown
[GİZLİ HUKUKİ ÇALIŞMA TASLAĞI - bkz. CLAUDE.md ## Çıktılar]

> **⚠️ Reviewer note**
> - **Kaynaklar:** [Resmî Gazete / Mevzuat.gov.tr / KVKK / USOM / EUR-Lex / kullanıcı metni | model bilgisi kullanıldı — doğrulayın]
> - **Okuma kapsamı:** [Tam metin / özet / seçili maddeler]
> - **Hukukçu kararı gerektirenler:** [`[review]` ve belirsiz yorumlar]
> - **Güncellik:** [`references/currency-watch.md` kontrolü]
> - **Güvenmeden önce:** Madde numaraları ve yürürlük tarihleri birincil kaynaktan teyit edilmelidir

## İyileştirme Planı: [Düzenleme Adı]

**Yürürlük Tarihi:** [tarih] | **Uygulama / Ceza Başlangıcı:** [tarih] | **Rolümüz:** [Geliştirici / Kullanıcı / Her İkisi]

### Yürürlük Öncesi Zorunlu (Must-Do)
| Boşluk | Yapılacak Somut Düzeltme | Sahip | Son Tarih | Durum |
|---|---|---|---|---|

### Önemli Ama Engelleyici Olmayan (Should-Do)
[Aynı tablo]

### Halihazırda Uyumlu Olanlar (`Gap: Yok`)
[Kayıt ve yönetim özeti için]

### Kabul Edilen Riskler (Accepted Gaps)
[Risk kabul edildiyse gerekçesi ve kabul eden yönetici]

## Madde Doğrulama Uyarısı (Cite Check)
Tüm mevzuat atıfları `mevzuat.gov.tr`, `resmigazete.gov.tr`, `kvkk.gov.tr` veya `EUR-Lex` üzerinden doğrulanmadan resmî işlemde kullanılmamalıdır.
```

## Entegrasyon ve Yapmadıkları

- `aia-generation` veya `use-case-triage` yeni bir düzenleme tetiklediğinde bu skill elle diff çalıştırır; proaktif izleme için `regulatory-legal` eklentisiyle eşleşir.
- Analizi Sonraki Adımlar Karar Ağacı ile bitir (büyük gap listelerinde `references/dashboard-template.md` pano önerisini sun).
- **Yoruma açık kanun hükümlerinde tek doğru ilan etmez;** muhafazakâr yorumu belirtip dış hukuk/sektör uzmanı değerlendirmesi önerir. Teknik düzeltmeleri bizzat kodlamaz, gereksinimi planlar.
