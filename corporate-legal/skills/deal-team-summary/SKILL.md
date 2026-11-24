---
name: deal-team-summary
description: >
  Due diligence bulgularını okuyucunun ihtiyacına uygun seviyede işlem ekibi
  özetine sıkıştırır — üst yönetim/kurul için yönetici özeti, işlem ekibi için
  çalışma özeti. "brief the deal team", "diligence özeti çıkar", "işlem durumu
  nedir", "yönetime özet hazırla" denince kullanılır.
---

# İşlem Ekibi Özet Raporu (Deal Team Summary)

## Matter Bağlamı

`CLAUDE.md` → `## Matter workspaces` bölümünü kontrol et. `Enabled` kapalıysa (`✗`, kurum içi tek şirket kullanımı için varsayılan) practice-level bağlamda çalış. Açıksa ve aktif matter yoksa kullanıcıya sor (`/corporate-legal:matter-workspace switch <slug>` veya `practice-level`); aktif `matter.md` dosyasını yükle ve çıktıları `~/.claude/plugins/config/legal-turkish/corporate-legal/matters/<matter-slug>/` klasörüne yaz. `Cross-matter context` kapalıyken başka matter dosyası okuma.

---

## Amaç

İşlem lideri 200 bulgu satırını tek tek okumaz; şunu görmek ister: **esasa etkili (material) ne var, son brifingden bu yana ne değişti, kimden hangi karar bekleniyor?** Bu skill diligence çıktısını hedef kitleye uygun yüksekliğe sıkıştırır.

## Bağlam Yükleme

- `~/.claude/plugins/config/legal-turkish/corporate-legal/CLAUDE.md` (`## M&A ve işlem yönetimi`, `## Kullanıcı rolü`, `## Çıktı kuralları`).
- Aktif işlem klasörü veya matter içindeki `diligence-issue-extraction` / `tabular-review` bulguları.

## Okuyucu Katmanları (Audience Tiers)

Net değilse kullanıcıya hangi katmana yazılacağını sor:

| Okuyucu Katmanı | Alacağı İçerik | Hariç Tutulacaklar |
|---|---|---|
| **Yönetim Kurulu / Üst Sponsor** | En kritik 3–5 esasa etkili bulgu (TTK, Rekabet Kurumu, SPK, KVKK, vergi/sözleşme), fiyat/yapı etkisi, karar gerektiren maddeler | Alt kategori detayı, yeşil (`🟢`) bulgular, süreç detayı |
| **İşlem Lideri (Deal Lead)** | Tüm kırmızı (`🔴`) ve sarı (`🟡`) bulgular, inceleme ilerleme oranı, karar maddeleri, sonraki adımlar | Yeşil (`🟢`) bulgu detayları |
| **Çalışma Ekibi** | Eksiksiz tüm bulgular, kategori bazlı durum ve eksik belge boşlukları | Hiçbiri gizlenmez |

## Rapor Şablonları

### Üst Yönetim Katmanı (`Exec Tier`)

```markdown
GİZLİ HUKUKİ ÇALIŞMA TASLAĞI - AVUKAT/HUKUKÇU İNCELEMESİNE TABİDİR
Bu çıktı hukuki görüş, imza onayı, tescil talimatı veya resmi başvuru yerine geçmez.

Reviewer note
- Kaynaklar: [diligence bulguları / VDR / kullanıcı sağladı]
- Dağıtım: Bu özet gizli hukuki çalışma ve işlem stratejisi içerebilir. Hukuk ekibi ve yetkili işlem ekibi dışına gönderilecekse arındırılmış versiyon hazırlanmalı.

# [İşlem Kodu] — Due Diligence Özeti — [YYYY-AA-GG]

**Durum:** [Takvime uygun | Konular tespit edildi | Esasa etkili (Material) bulgular var]
**İnceleme Kapsamı:** VDR'ın %[X]'i incelendi

## Esasa Etkili Bulgular
[En fazla 3–5 madde; her biri 1 kısa paragraf: bulgunun ne olduğu, bedel/kapanış/izin riski ve önerilen aksiyon (bedel indirimi, özel tazminat, ön koşul).]

## Beklenen Kararlar
- [ ] [Somut karar — örn. Hisse alım sözleşmesinde (SPA) özel tazminat veya Rekabet Kurumu izninin ön koşul (CP) sayılması] — [Karar Mercii] — [Tarih]

## Son Özettenden Bu Yana Değişenler
[Yeni tespit edilenler, kapanan rıza/izinler, kapsam ilerlemesi.]
```

### İşlem Lideri Katmanı (`Deal Lead Tier`)

Yukarıdaki başlıklarla birlikte şunları ekle:

```markdown
## Kategori Bazlı Açık Konular

### 🔴 Kritik (Red)
[Bulgu başlığı + tek satır özet]

### 🟡 Dikkat (Yellow)
[Bulgu başlığı + tek satır özet]

## İlerleme Tablosu
| Kategori | İncelenen Belge | Kapsam % | Kırmızı | Sarı | Durum |
|---|---|---|---|---|---|

## Eksikler ve Yönetimden İstenecek Ek Belgeler
- [Tamamlayıcı VDR talepleri / Q&A soruları]

## Önümüzdeki 72 Saat
[İncelenecek öncelikli klasörler ve planlanan toplantılar]
```

### Çalışma Ekibi Katmanı
Tüm bulgular profildeki tam kurum formatıyla eksiksiz yer alır.

## Değişim Odaklı Güncelleme (Deltas)

Periyodik bir özet üretiliyorsa ("hâlâ 12 sarı var" yerine) mutlaka hareketi öne çıkar: yeni çıkan bulgular, şiddeti düşen/yükselen kalemler, karşı taraf rızasıyla kapanan maddeler.

## Devirler ve Kapanış

- `diligence-issue-extraction` ve `tabular-review` çıktılarını tüketir.
- "Beklenen Kararlar" içinde kapanış ön koşuluna (Condition Precedent) dönüşen her maddeyi `/corporate-legal:closing-checklist` listesine aktar.
- `## Çıktı kuralları` uyarınca Sonraki Adımlar Karar Ağacı ile bitir.

## Yapmadıkları

- Önemlilik (`materiality`) kararını baştan icat etmez; çıkarım aşamasında verilen dereceleri özetler.
- İşlem adına ticari karar vermez, raporu haricî taraflara kendisi göndermez.
