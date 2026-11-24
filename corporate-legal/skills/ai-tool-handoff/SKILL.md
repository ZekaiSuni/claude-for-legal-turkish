---
name: ai-tool-handoff
description: >
  Luminance, Kira veya benzeri toplu sözleşme tarama (bulk-review) aracının
  kullanıldığı durumları tespit eder, yüksek hacimli madde çıkarımını bu araca
  devreder ve dönen çıktıyı `~/.claude/plugins/config/legal-turkish/corporate-legal/CLAUDE.md`
  içindeki güven düzeyine göre QA'den geçirir. "bulk review", "toplu inceleme",
  "Luminance'a gönder" veya diligence-issue-extraction yüksek hacme ulaştığında
  kullanılır.
---

# Yapay Zekâ Toplu İnceleme Devri (AI Tool Handoff)

## Matter Bağlamı

Pratik düzeyindeki `CLAUDE.md` → `## Matter workspaces` bölümünü kontrol et. `Enabled` kapalıysa (`✗`, kurum içi tek şirket kullanımı için varsayılan) practice-level bağlamda çalış. Açıksa ve aktif matter yoksa kullanıcıya sor (`/corporate-legal:matter-workspace switch <slug>` veya `practice-level`); aktif matter'ın `matter.md` dosyasını yükle ve çıktıları `~/.claude/plugins/config/legal-turkish/corporate-legal/matters/<matter-slug>/` klasörüne yaz. `Cross-matter context` kapalıyken başka matter dosyası okuma.

---

## Amaç

Toplu tarama araçları (Luminance, Kira vb.) 500 sözleşmeyi okuyup tüm kontrol değişikliği (Change of Control - CoC) veya devir yasağı maddelerini listelemekte hızlıdır; ancak söz konusu CoC hükmünün mevcut pay devri, malvarlığı devri veya TTK birleşme/bölünme yapısıyla **hukuken tetiklenip tetiklenmediğine** karar veremezler.

**Devirden önce kontrol et:** Önce `/corporate-legal:tabular-review` kullanmayı değerlendir. Birkaç yüz sözleşmeye ve net kolon şemasına sahip dosyalarda yerel tablolu inceleme daha hızlıdır, ek belge başı maliyet doğurmaz ve veriyi içeride tutar. Yalnızca veri seti gerçekten çok büyükse, ekibin aktif lisansı varsa veya denetlenmiş bir aktarım zinciri gerekiyorsa haricî toplu tarama aracına devret.

## Bağlam Yükleme

`~/.claude/plugins/config/legal-turkish/corporate-legal/CLAUDE.md` içinde AI destekli inceleme tercihlerini oku (kullanılan araç, hedef madde türleri, güven düzeyi: `olduğu gibi kullan` / `örnekleme %X` / `işaretlilerin tam insan incelemesi`, yükleyen ve QA sorumlusu). Profilde haricî AI aracı yoksa bu skill devreye girmez; tüm inceleme doğrudan `diligence-issue-extraction` ve `tabular-review` üzerinden yürür.

## Ne Zaman Devredilir

Tüm koşullar sağlanıyorsa devret:
- Kategoride >50 belge varsa (altında doğrudan okumak daha hızlıdır),
- Hedef madde mekanik çıkarıma uygunsa (kontrol değişikliği, devir/temlik yasağı, münhasırlık, MFN, fesih, otomatik yenileme),
- Belgeler biçimce benzer ve tek tipse (ör. standart müşteri veya tedarikçi sözleşmeleri).

Şunları devretme: özel pazarlıklı ana sözleşmeler, ek protokoller/yan mektuplar (`side letter`), yorumsal deal etkisi gerektiren metinler.

## Devir Süreci

### Adım 1 ve 2: Parti Hazırlığı ve Yükleme Talebi
- VDR envanterinden parti listesini ve önemli eşiği (`## M&A ve işlem yönetimi`) belirle.
- Başka biri yükleyecekse şu özeti üret:

```markdown
## [Araç Adı] Yükleme Talebi — [İşlem Kodu] — [Kategori]
**Belgeler:** VDR klasörü [yol] içinde [N] adet dosya
**Hedef çalışma alanı:** [Workspace/Matter]
**Çıkarılacak maddeler:** Kontrol değişikliği / Devir yasağı / Münhasırlık / [diğer]
**Filtre:** Yalnızca hükmün bulunduğu sözleşmeleri işaretle (her temiz dosya için kayıt üretme).
**Hedef teslim tarihi:** [tarih]
```

### Adım 3: Çıktı Kalite Kontrolü (QA)
Araç sonuçları döndüğünde profildeki güven düzeyini uygula:
- **"Olduğu gibi kullan" (Nadir):** Doğrudan diligence bulgularına aktar.
- **"%X Örnekleme (Spot-check)":** İşaretlenenlerden rastgele %X oku ve araç çıkarımını gerçek metinle kıyasla; hata oranı yüksekse örneklemi genişlet.
- **"İşaretlilerin Tam İnsan İncelemesi":** Araç 500 dosyadan madde içeren 80 dosyayı ayıklar; avukat bu 80 dosyayı birebir okur.

### Adım 4: Hukuki Yargı Katmanı (Türk Hukuku)
Araç maddeyi buldu; şimdi işlem yapısına göre değerlendir:
- Pay devri vs. malvarlığı/işletme devri (TBK m. 202 / TTK) vs. birleşme/bölünme (TTK m. 134 vd.) ayrımında madde gerçekten tetikleniyor mu?
- Sözleşmedeki "kontrol değişikliği" tanımı (%50+ oy hakkı, yönetim kurulu kontrolü, grup içi devir istisnası) olaya uyuyor mu?

## Çıktı

> Aşağıdaki QA özeti gizli VDR belgelerinden türetilmiştir; kaynak belgelerin gizlilik ve sır statüsünü taşır. Yetkili hukuk ve işlem ekibi dışında dağıtılmamalıdır.

```markdown
## Toplu İnceleme QA Özeti — [Kategori]

**Araç:** [Luminance / Kira] | **İşlenen Belge:** [N] | **Hedef Maddeler:** [liste]

### QA Sonucu
**Güven Düzeyi:** [profil pozisyonu] | **Örneklenen:** [N] dosya | **Hata Oranı:** %[X] — [Kabul / Örneklem Genişletildi / Yeniden Tam İnceleme]

### Sonuç Tablosu
| Madde Türü | İşaretlenen Belge | Hukuki Değerlendirme Sonrası Tetiklenen | Önem Eşiği Üstü |
|---|---|---|---|
| Kontrol değişikliği (CoC) | [N] | [N] | [N] |
| Devir / Temlik yasağı | [N] | [N] | [N] |

**→ [N] bulgu diligence listesine eklendi**
**→ [N] onay/bildirim koşulu kapanış kontrol listesine eklendi**
```

## Kapanış

`## Çıktı kuralları` uyarınca Sonraki Adımlar Karar Ağacı ile bitir (diligence bulgusuna aktarma, kapanış kontrol listesine ekleme, örneklem genişletme, dış danışmana eskalasyon veya izlemede tutma).

## Yapmadıkları

- Luminance veya Kira'yı kendisi çalıştırmaz; hazırlık ve QA katmanını yönetir.
- Profil `%10` örnekleme diyorsa sessizce kapsamı değiştirmez; güven düzeyini kullanıcı belirler.
