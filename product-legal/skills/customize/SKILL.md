---
name: customize
description: >
  Product-legal profilinde tek bir bölümü değiştirir: risk kalibrasyonu,
  lansman framework'ü, reklam iddia politikası, eskalasyon, entegrasyon veya
  matter workspace ayarları.
argument-hint: "[section name, or describe what you want to change]"
---

# /customize

## Ne zaman kullanılır

Kullanıcı tüm cold-start görüşmesini yeniden yapmak istemeden product-legal profilini ayarlamak ister.

## Akış

1. `~/.claude/plugins/config/legal-turkish/product-legal/CLAUDE.md` dosyasını oku. Yoksa veya placeholder doluysa önce `/product-legal:cold-start-interview` iste.
2. Değiştirilebilir haritayı göster:
   - Şirket/ürün modeli ve hedef pazarlar,
   - lansman süreci ve SLA,
   - Türk launch review kategorileri,
   - risk kalibrasyonu,
   - pazarlama iddiaları ve kanıt standardı,
   - KVKK/AI/güvenlik eskalasyonları,
   - entegrasyonlar,
   - matter workspace.
3. Kullanıcı hangi bölümü değiştirmek istediğini söyledikten sonra mevcut değeri göster.
4. Yeni değeri al; downstream etkisini açıkla.
5. Kullanıcı onaylayınca profilde yalnızca ilgili satır/bölümü değiştir.

## Guardrail

- `[doğrula]`, kaynak etiketi, reviewer note ve hukukçu incelemesi guardrail'leri kaldırılamaz.
- Risk kalibrasyonu gevşetiliyorsa etkisini açıkça yaz: hangi komutlar artık daha az flag atacak?
- Yeni sektör veya pazar eklenirse `references/currency-watch.md` uyarısı ve ilgili resmî kaynak ihtiyacı eklenir.
- Ortadan kaldırılmak istenen kategori silinmez; `out of scope / route to [plugin/team]` olarak işaretlenir.

## Kapanış

Değişiklikten sonra kısa özet ver:

```text
Güncellendi: [bölüm]
Etkisi: [launch-review / is-this-a-problem / marketing-claims-review üzerindeki etki]
Eksik doğrulama: [varsa]
```
