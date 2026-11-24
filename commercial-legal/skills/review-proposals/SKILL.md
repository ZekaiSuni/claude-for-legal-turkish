---
name: review-proposals
description: >
  Playbook-monitor ajanının Türk ticari sözleşme pratiği için ürettiği bekleyen
  playbook güncelleme önerilerini inceler, onaylar, düzenler, erteler veya
  reddeder. Onaylanan değişiklikleri yalnızca avukat teyidinden sonra commercial
  uygulama profiline işler.
argument-hint: "[argüman gerekmez - bekleyen öneriler dosyasından çalışır]"
---

# /review-proposals

Playbook-monitor ajanının oluşturduğu bekleyen playbook güncelleme önerilerini tek tek hukukçu onayına sunar. Açık hukukçu onayı olmadan `CLAUDE.md` dosyasını değiştirmez.

## Talimatlar

1. `~/.claude/plugins/config/legal-turkish/commercial-legal/playbook-proposals.md` dosyasını yükle.
2. Dosya yoksa veya boşsa şu yanıtı ver:

   > Bekleyen playbook önerisi yok. Playbook güncel görünüyor.

3. Önerileri tek tek sun.
4. Her öneri için şu seçenekleri sun:
   - Kabul et,
   - Reddet,
   - Düzenle,
   - Ertele.
5. Kabul et / Düzenle seçilirse `~/.claude/plugins/config/legal-turkish/commercial-legal/CLAUDE.md` üzerinde yapılacak tam değişikliği (diff) göster.
6. Yalnızca açık avukat onayından sonra dosyaya uygula.
7. Reddet / Ertele durumunda profili değiştirmeden karar kaydını tut.
8. Tüm öneriler sonuçlandığında özeti göster ve öneriler dosyasını arşivle.

## Öneri İnceleme Çerçevesi

Her öneri için şu şablonu göster:

```markdown
## Öneri [N]

**Madde / konu:** [madde]
**Gözlenen uygulama:** [patern]
**Mevcut playbook:** [mevcut pozisyon]
**Önerilen değişiklik:** [önerilen yeni pozisyon]
**Destekleyen örnekler:** [sapma kayıtları]
**Risk:** [Türk hukuku / ticari / onay riski]

Seçenekler: Kabul et | Reddet | Düzenle | Ertele
```

## Güvenlik Kuralları (Guardrails)

- Riskli sapmaları sessizce normalleştirme.
- Bir öneri KVKK, sorumluluk sınırı, cezai şart (TBK m. 179–182 / TTK m. 22), fikri mülkiyet/FSEK, yabancı hukuk/yetki, zorunlu arabuluculuk/dava şartı kontrolleri, damga vergisi incelemesi veya imza yetkisi kurallarını zayıflatıyorsa bunu `yüksek etkili (high-impact)` olarak işaretle ve mutlaka avukat onayı iste.
- Öneri tek seferlik stratejik istisnalara dayanıyorsa otomatik revizyon yerine `Reddet` veya `Ertele` öner.
- Alınan kararların günlüğünü tut.

## Yapmadıkları

- Playbook politikasını tek başına belirlemez.
- Açık onay olmadan `CLAUDE.md` dosyasını güncellemez.
- Tekrarlanan hatalı uygulamayı otomatik olarak kabul edilebilir saymaz.
