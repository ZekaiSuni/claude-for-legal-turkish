---
name: tabular-review
description: >
  Tablolu toplu sözleşme/belge incelemesi (Tabular Review): her belge için bir
  satır, her veri noktası için bir kolon ve her hücrede doğrudan kaynak alıntısı
  üretir. M&A veri odası incelemeleri (örn. "200 hedef şirket sözleşmesini
  kontrol değişikliği, devir yasağı ve MAC açısından tara") ve yapılandırılmış
  elektronik tablo çıktısı gerektiren tüm toplu taramalar için kullanılır.
---

# /tabular-review

1. `~/.claude/plugins/config/legal-turkish/corporate-legal/CLAUDE.md` dosyasından due diligence yapısını, önemlilik eşiklerini, `## Yapısal veri standardı` kuralını ve `## Çıktı kuralları` başlığını yükle.
2. Hangi belgelerin, hangi kolonların ve hangi çıktı hedefinin seçileceğini teyit et.
3. Tiplendirilmiş şemayı kur ve `.review-schema.yaml` olarak yaz; kullanıcı onayını al.
4. Örnek çalıştırma (3–5 belge) yap, şemayı ayarla ve onayla.
5. Belge başına paralel inceleme yürüt: her hücre `{value, state, quote, location}` döndürür.
6. Kolon bazlı tutarlılık ve normalleştirme taraması yap; aykırılıkları işaretle.
7. Çıktıyı üret: `.xlsx` veya Google Sheets (tercihi sor) + her zaman `.csv`, `_sources.csv` ve Markdown; üstte `## Çıktı kuralları` uyarınca gizli çalışma taslağı başlığını ekle.
8. Özet sun: her kolon için `not_present` / `unclear` / `needs_review` sayıları, dosya yolları ve her hücrenin "nihai hukuki sonuç değil, doğrulama adayı" olduğu uyarısı.

```text
/corporate-legal:tabular-review
/corporate-legal:tabular-review --schema .review-schema.yaml --docs ./vdr/02-Sozlesmeler/
/corporate-legal:tabular-review --template ma-diligence
```

- **`--schema <yol>`:** Yeni şema kurmak yerine mevcut `.review-schema.yaml` dosyasını kullanır.
- **`--template <ad>`:** Şablon dosya seçer (ör. `references/ma-diligence-columns.md` üzerinden `ma-diligence`).
- **`--docs <yol>`:** Yerel klasör, Google Drive klasör ID'si veya SharePoint/VDR klasör yolu.
- **`--output <xlsx|gsheets|csv>`:** Çıktı formatı.
- **`--sample <n>`:** Şema testi için örnek belge sayısı (varsayılan 5).

---

## Matter Bağlamı

Pratik düzeyindeki `CLAUDE.md` → `## Matter workspaces` bölümünü kontrol et. `Enabled` kapalıysa (`✗`, kurum içi tek şirket kullanımında varsayılan) practice-level bağlamda çalış. Açıksa ve aktif matter yoksa kullanıcıya sor (`/corporate-legal:matter-workspace switch <slug>` veya `practice-level`); aktif `matter.md` dosyasını yükle ve çıktıları `~/.claude/plugins/config/legal-turkish/corporate-legal/matters/<matter-slug>/` klasörüne yaz. `Cross-matter context` kapalıyken başka matter dosyası okuma.

---

## Amaç

Elinizde yüzlerce sözleşme ve her biri hakkında tutarlı biçimde yanıtlanması gereken sabit bir soru listesi varsa (M&A talep listesi, tedarikçi sözleşmesi denetimi, kira portföyü incelemesi) bu skill satırlarda belgeleri, kolonlarda veri noktalarını ve her hücrede doğrudan kaynak alıntısını tutan denetlenebilir bir tablo üretir.

- `diligence-issue-extraction` belgelerdeki hukuki sorunları yakalar; `tabular-review` ise tüm belgelerden aynı veri alanlarını çıkarır.
- Üretilen hiçbir hücre insan okuması yerine geçmez: her hücre **birincil metinden doğrulanacak izleme ipucudur (`lead`)**.

## Bağlam Yükleme

- `~/.claude/plugins/config/legal-turkish/corporate-legal/CLAUDE.md` (`## M&A ve işlem yönetimi`, `## Yapısal veri standardı`, `## Çıktı kuralları`).
- İlgili işlem dosyası (`deal-context.md`) ve varsa mevcut `.review-schema.yaml`.

## Kolon Tip Sistemi

`## Yapısal veri standardı` uyarınca makine-tarafı kolon ID'leri ve durum etiketleri canonical `english_snake_case`, kullanıcıya gösterilen tablo/rapor başlıkları Türkçedir:

| Tip (`type`) | Ne Döndürür | Kullanım Alanı |
|---|---|---|
| `verbatim` | Belgeden birebir karakteri karakterine alıntı | Tanımlar, kilit hüküm metinleri, kelime farkının önemli olduğu maddeler |
| `classify` | Tanımlı seçenek listesinden tek değer | Evet/Hayır, var/yok, standart hüküm varyantları |
| `date` | ISO tarih (`YYYY-AA-GG`) | Yürürlük, bitiş, fesih ihbar son tarihi |
| `duration` | Süre + birim | Sözleşme süresi, ihbar öneli, bakiye gizlilik süresi |
| `currency` | Tutar + para birimi kodu (`TRY`, `USD`, `EUR` vb.) | Sorumluluk tavanı, eşik değer, cezai şart |
| `number` | Yalın sayı | Adet, yüzde, sayfa/madde sayısı |
| `free` | Kısa serbest özet | Sadece diğer tipler uymadığında ölçülü kullanılır |

**Birebir alıntı kuralı (`verbatim rule`):** `verbatim` dışındaki tüm kolonlar da cevabı destekleyen **birebir kaynak cümlesini (`quote`) ve yerini (`location`)** yanında taşır.

## Bulunamayan Değerlerin Üç Açık Durumu

Boş hücre bilgi saklar; pozitif değer çıkmadığında şu üç durumdan biri zorunludur:

| Durum (`state`) | Anlamı | Ne Zaman Kullanılır |
|---|---|---|
| `not_present` | Belge okundu ve ilgili hüküm yok | Konu sözleşmede hiç düzenlenmemişse |
| `unclear` | Hüküm var ama net sınıflandırılamıyor | Muğlak ifade, eksik madde veya çelişen hükümler |
| `needs_review` | Madde bulundu ama hukukçu yorumu gerekiyor | İstisna/sınır vaka, karmaşık atıf veya alıntı doğrulanamıyorsa |

## İş Akışı

### Adım 0: Ne ve Nerede
1. **Belgeler:** Google Drive klasörü, SharePoint/VDR klasörü, yerel klasör veya dosya listesi nerede? Sayı >200 ise önemlilik eşiğiyle alt kümeden başlamayı öner.
2. **Şema:** Kullanıcı `references/ma-diligence-columns.md` (`--template ma-diligence`) şablonundan mı başlayacak yoksa doğal dilde kolon mu tanımlayacak?
3. **Çıktı:** Excel (`.xlsx`) mı, Google Sheets mi? (`.csv` ve Markdown her zaman ek olarak yazılır.)

### Adım 1: Şema Oluşturma ve Onay
Kullanıcının kolonlarını `.review-schema.yaml` içine sabit `id`, Türkçe `label`, `type`, `prompt` ve varsa `options` listesiyle yaz; kullanıcıya gösterip onay al:

```yaml
schema:
  name: "M&A Due Diligence — Proje [Kodu]"
  created: 2026-11-24
  columns:
    - id: counterparty
      label: "Karşı Taraf"
      type: verbatim
      prompt: "Hedef şirket dışındaki sözleşme tarafı (tam ticaret unvanı) kimdir?"
    - id: effective_date
      label: "Yürürlük Tarihi"
      type: date
      prompt: "Sözleşme ne zaman yürürlüğe girmiştir?"
    - id: change_of_control
      label: "Kontrol Değişikliği (CoC)"
      type: classify
      options: [silent, consent_required, consent_not_unreasonably_withheld, automatic_termination, notice_only]
      prompt: "Sözleşmede kontrol değişikliği veya hisse devri düzenleniyor mu; onay/bildirim şartı nedir?"
    - id: assignment
      label: "Devir ve Temlik Yasağı"
      type: classify
      options: [silent, consent_required, consent_not_unreasonably_withheld, freely_assignable, assignable_to_affiliates]
      prompt: "Hedef şirket sözleşmeyi üçüncü kişilere veya grup şirketlerine devredebilir mi?"
```

### Adım 2: Örnek Çalıştırma (3–5 Belge)
200 belgeye dağılmadan önce 3–5 belgede test et; çok `unclear` dönen soruları daralt, `classify` seçeneklerini düzelt ve onay al.

### Adım 3: Paralel İnceleme ve Zorunlu Alıntı Kuralı
Her belge baştan sona okunur (salt RAG parçası değil) ve her kolon `{value, state, quote, location}` döndürür:
- **`quote` mutlaka kaynak metinden harfi harfine kopyalanmış kesintisiz metin olmalıdır.** Başlıktan cümle uydurma, özetleme (paraphrase), hafızadan tamamlama veya kopuk cümleleri `...` ile birleştirme **yasaktır**.
- **`location`** normalleştirme kontrolünde geri açılabilecek kadar net olmalıdır (madde numarası, başlık, sayfa).
- Metin kesikse, OCR bozuksa veya ifade sadece ima ediliyorsa `state: needs_review`, `value: null`, `notes: quote_unavailable: <neden>` verilir; asla uydurulmuş alıntıyla `state: answered` yazılmaz.

### Adım 4: Kolon Bazlı Normalleştirme ve Spot-Check
1. Tüm `classify` değerlerinin `options` listesinde olduğunu ve aykırı kümelenmeleri kontrol et.
2. Tarih, süre ve para birimi (`TRY`/`USD`/`EUR`) tutarlılığını kontrol et; olağandışı değerleri (99 yıl süre, 1 TL sorumluluk sınırı) `needs_review` işaretle.
3. Her `verbatim` kolonunda ve diğer kolonların eşlikçi alıntılarında en az 3–5 satır (veya satırların %10'u) kaynakta yeniden açılıp birebir karşılaştırılır; tek bir uyuşmazlık (`quote_mismatch`) çıkarsa o kolonun tamamı geniş spot-check'e alınır.

### Adım 5: Çıktı Biçimleri
1. **Markdown** (oturum içi kontrol tablosu)
2. **CSV** (`.csv` değerler + `_sources.csv` alıntı ve konumlar)
3. **Excel (`.xlsx`)** veya **Google Sheets** (`references/excel-output.md` ve `references/gsheets-output.md` şartnamesine uygun: gizli `_source` kolonu, hücre not/yorumunda alıntı, durum renkleri, `Verified` kolonu, `_schema` ve `_summary` sayfaları + formül enjeksiyonu koruması).

En üste `## Çıktı kuralları` başlığını ve dağıtım uyarısını ekle:

```text
GİZLİ HUKUKİ ÇALIŞMA TASLAĞI - AVUKAT/HUKUKÇU İNCELEMESİNE TABİDİR
Bu çıktı hukuki görüş, imza onayı, tescil talimatı veya resmi başvuru yerine geçmez.
```

> Bu tablo VDR, sözleşme ve işlem belgelerinden türetilmiş gizli hukuki çalışma taslağıdır. Hukuk ekibi ve yetkili işlem ekibi dışına gönderilecekse gizli hukuki değerlendirme, strateji notu ve kaynak alıntıları arındırılmalıdır.

### Adım 6: Özet ve Kapanış
Belge/kolon sayısını, kolon bazında `not_present` / `unclear` / `needs_review` sayısını (doğrulama iş yükünü), %10 üstü uyarı alan kolonları ve çıktı dosyalarını göster; **her hücrenin hukuki inceleme için başlangıç izi olduğunu** vurgula. Ardından `## Çıktı kuralları` uyarınca Sonraki Adımlar Karar Ağacı ile kapat (material contract schedule üretme, diligence issue extraction çalıştırma, eksik belge talebi, closing checklist'e aktarma veya dış danışmana eskalasyon).

## Yapmadıkları ve Diğer Skill İlişkileri
- Belgeleri okuma yükümlülüğünü ortadan kaldırmaz; doğrulama kolonunu (`Verified`) avukat işaretlemelidir.
- Güven skoru (%73 vb.) uydurmaz; gerçek güven sinyali `unclear`/`needs_review` ve birebir alıntıdır.
- Çıkan kritik maddeler `/corporate-legal:diligence-issue-extraction`, beyan cetveli `/corporate-legal:material-contract-schedule`, çok yüksek hacimli kurumsal lisanslı araç devirleri ise `/corporate-legal:ai-tool-handoff` ile bağlanır.
