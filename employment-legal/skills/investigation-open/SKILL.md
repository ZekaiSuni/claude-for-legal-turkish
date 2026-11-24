---
name: investigation-open
description: >
  Türk iş hukuku iç soruşturma dosyası açar. Taciz, mobbing, disiplin, veri
  ihlali, İSG, hırsızlık, çıkar çatışması veya çalışan şikayetinde slug, kapsam,
  gizlilik seviyesi, ilk kronoloji ve delil logu oluşturur.
argument-hint: "[soruşturma konusu]"
---

# /investigation-open

`internal-investigation` playbook'unu kullanarak yeni soruşturma dosyası aç.

Gerekli intake:

- konu ve iddia,
- olay/öğrenme tarihi,
- ilgili kişiler,
- acil tedbir,
- delil kaynakları,
- KVKK hassas veri,
- olası disiplin/fesih etkisi,
- dosya slug'ı.

Çıktı: `investigation.md`, `evidence-log.md`, `interview-notes.md`, `timeline.md` için başlangıç taslağı.
