---
name: gaps
description: >
  Türkiye regülasyon takip akışındaki açık politika/prosedür boşluklarını
  listeler; kapatma veya risk kabul kararlarını kaydeder. Kullanım: "açık
  gapler", "remediation status", "--close GAP-ID", "--accept GAP-ID".
argument-hint: "[opsiyonel: --close GAP-ID | --accept GAP-ID]"
---

# /gaps

1. `~/.claude/plugins/config/legal-turkish/regulatory-legal/gap-tracker.yaml` dosyasını oku.
2. `--close` varsa çözüm notu ve onay bilgisini kaydet.
3. `--accept` varsa risk kabul gerekçesi ve yetkili kişiyi kaydet.
4. Aksi halde açık gap'leri önem, yaş, sahip ve son tarihe göre raporla.

Detaylı şema, bildirim kuralları, doğrulanmamış kaynakların overdue sayılmaması ve hukuki sonuç kapısı `gap-surfacer` referans skill'indedir; substantive çalışma öncesi onu yükle.
