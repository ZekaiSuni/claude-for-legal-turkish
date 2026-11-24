---
name: matter-update
description: >
  Bir dava veya uyuşmazlık dosyasının `history.md` günlüğüne tarihli yeni
  gelişme ekler ve `matters/_log.yaml` satırını günceller — UYAP safahat
  değişiklikleri, duruşma/bilirkişi sonuçları, süre kaymaları, risk yeniden
  değerlendirmesi, önemlilik (karşılık/açıklama) ve sulh yetkisi güncellemeleri
  için kullanılır.
argument-hint: "[slug] [kısa olay açıklaması]"
---

# /matter-update

1. `matters/[slug]/` ve `matters/_log.yaml` içinde dosyanın varlığını kontrol et.
2. Olay türünü, tarihi (varsayılan bugün), 1 paragraflık özeti ve etkilenen log alanlarını (`uyap_no`, `arabuluculuk`, `status`, `stage`, `risk`, `materiality`, `exposure_range`, `next_deadline`, `outside_counsel`, `internal_owners`, `legal_hold`) topla.
3. Gerekli önemlilik ve sulh kabul kapılarını kontrol et.
4. `history.md` ve `_log.yaml` değişikliğini (diff) kullanıcıya gösterip onay aldıktan sonra yaz.

---

## Çıkar Çatışması Kapısı (Atlanamaz Kural)

Güncellemeden önce `matters/_log.yaml` içinde `[slug]` kaydını doğrula; yoksa reddet ve `/litigation-legal:matter-intake` öner.

## Güncelleme Adımları

### 1. Olay Türü
- **Usuli (Procedural):** Dilekçe sunuldu/tebliğ edildi, tensip kuruldu, UETS e-tebligat açıldı, duruşma yapıldı, kesin süre verildi, kanun yoluna başvuruldu.
- **Delil / Tahkikat (Discovery/Evidence):** Belge ibrazı, müzekkere cevabı, tanık dinlenmesi, keşif veya bilirkişi raporu tebliği.
- **Esasa İlişkin (Substantive):** Kilit belge ortaya çıktı, ara karar veya esasa dair hüküm verildi.
- **Strateji / Sulh (Strategy):** Strateji değişikliği, arabuluculuk görüşmesi, sulh teklifi yapıldı veya alındı, sulh yetkisi güncellendi.
- **Risk Yeniden Değerlendirmesi:** Etki veya olasılık değişti.
- **Paydaş / Vekil:** Yeni sorumlu, dış hukuk bürosu değişikliği.
- **İdari:** Vekâletname/masraf avansı, bütçe veya hukuki saklama (legal hold) yenilemesi.

### 2. Tarih ve Özet
Varsayılan tarih bugündür; geçmiş tarihli bir tebligat/karar işleniyorsa gerçek tarihi al. 1 paragrafta ne olduğunu ve hemen doğan hukuki etkiyi yaz.

### 3. Etkilenen Log Alanları
Yalnızca olay türüne göre anlamlı alanları sor (ör. usuli güncellemede `stage` ve `next_deadline`; sulh teklifinde `materiality`, `exposure_range`, `status`, `arabuluculuk`). Tüm dosya alanlarını (`uyap_no`, `arabuluculuk` dahil) koru.

### 4. Sulh Kabul Kapısı (Settlement-Acceptance Gate)
Strateji güncellemesi bir **sulh veya arabuluculuk anlaşmasını kabul etme / imzalama** aşamasındaysa (`~/.claude/plugins/config/legal-turkish/litigation-legal/CLAUDE.md` → `## Bunu Kim Kullanıyor`), kullanıcı **Non-lawyer** ise dur:

> Bir sulh veya arabuluculuk anlaşmasını kabul etmek hukuki sonuç doğurur — haklardan feragat/ibra içerir ve HMK / 6325 s. Arabuluculuk Kanunu uyarınca ilam niteliğinde belgeye dönüşebilir; sigorta ve vergi doğurabilir. Bunu avukatınızla gözden geçirdiniz mi? Hayırsa avukatınıza sunmanız için (`CLAUDE.md` sulh yetki merdiveniyle birlikte) 1 sayfalık özet hazırlıyorum; gerekirse bağlı olduğunuz Barodan destek alabilirsiniz.

Açık onay gelmeden sulh kabulünü loglama.

### 5. Zorunlu Önemlilik (`Materiality`) Kontrolü
Aşağıdaki olay türlerinde kullanıcı `"değişiklik yok"` veya yeni değeri açıkça söyleyene kadar sessiz geçme:
- Esasa ilişkin gelişme (`Substantive`)
- Strateji / sulh teklifi (`Strategy`)
- Risk yeniden değerlendirmesi (`Risk re-assessment`)
- Düzenleyici kurum işlemi (`Rekabet / KVKK / SPK / BDDK / idari yaptırım`)

Karşılık (`reserved`) veya kamu/kurul bildirimi (`disclosed`) seviyesine geçildiyse, `CLAUDE.md` → `## 1. Risk Kalibrasyonu` eşikleri uyarınca finans/denetim birimi bildirimi gerektiğini işaretle.

## Yazma Formatı (Onay Sonrası)

`matters/[slug]/history.md` en üstüne ekle:
```markdown
## [YYYY-MM-DD] — [Olay Türü]: [Kısa Başlık]

[1 paragraf özet.]

**Önemlilik Kontrolü:** [değişiklik yok / X -> Y]
**Gerekçe:** [tek cümle]
**Değişen alanlar:**
- [alan]: [eski -> yeni]
**İlgili belge:** [dosya yolu, varsa]
```

`_log.yaml` içinde ilgili alanları ve `last_updated:` tarihini güncelle.

## Yapmadıkları

- Geçmiş tarihçe kayıtlarını silmez veya değiştirmez; düzeltmeler eski kayda atıf yapan yeni kayıtla yapılır.
- Onay almadan `_log.yaml` üzerinde değişiklik yazmaz.
- Karşılık veya kamuyu aydınlatma kararını tek başına vermez; yalnızca eşik sorusunu yüzeye çıkarır.
