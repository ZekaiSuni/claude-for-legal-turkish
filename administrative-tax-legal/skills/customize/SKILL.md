---
name: customize
description: >
  Mevcut `administrative-tax-legal` kurulumundaki uzlaşma/dava onay sınırlarını,
  YMM koordinasyon kurallarını, e-tebligat uyarı pencerelerini veya özel
  şablon yollarını `CLAUDE.md` üzerinde günceller.
---

# İdare & Vergi Profili Özelleştirme (`customize`)

Kurulmuş `administrative-tax-legal` ortamında değişen iç politika, onay eşiği veya sektörel düzenleyici önceliklerini güncellemek için kullanılır. İlk kurulum için `/administrative-tax-legal:cold-start-interview` tercih edilir.

## Güncellenebilir Alanlar

1. **`## Kurum / Büro Profili` ve `## Kullanıcı Rolü`:** Yeni ekip üyesi, YMM koordinasyonu veya imza yetkilendirme değişikliği.
2. **`## İdare ve Vergi Uyuşmazlık Duruşu` & `### Onay ve Eskalasyon Matrisi`:**
   - `7524 s. K.` sonrasında vergi cezaları için `VUK m. 376` peşin indirim vs. `Ek m. 1` uzlaşma vs. dava eşik tutarlarının ayarlanması.
   - İdari para cezalarında `5326 m. 17/6` (%25 peşin ödeme indirimi) için iç finans onay süresi.
   - `6183 m. 48` tecil ve teminat mektubu onay sınırları.
3. **`## Dava, Başvuru ve Tebligat Süre Kuralları` ve `## Vergi İnceleme, Uzlaşma ve Tahsilat Politikası`:** Kuruma özel ön uyarı eşikleri (ör. GİB e-tebligat düşer düşmez ilk 24 saatte YMM+Hukuk toplantısı) ve `references/currency-watch.md` notları.
4. **Özel Şablonlar (`~/.claude/plugins/config/legal-turkish/administrative-tax-legal/`):** Kuruma özel YD talepli dava dilekçesi, `VUK m. 376` veya `6183 m. 58` ödeme emri itiraz şablonlarının bağlanması.

## İş Akışı ve Koruma Kuralları

- Önce mevcut `CLAUDE.md` metnini oku ve yalnızca istenen değişiklikleri uygula.
- `## Çekirdek Güvenlik Kuralları (Shared Guardrails)` altındaki tabanları (**önem derecesi tabanı gerekçesiz düşürülemez**, **sessiz tamamlama yok**, **hedef kitle kontrolü**) asla gevşetme.
- Yapılan güncellemeleri net bir fark özetiyle kullanıcıya sun.
