---
name: escalation-flagger
description: >
  Ticari pratik profilindeki eskalasyon matrisine göre bir sözleşme riskini veya
  playbook sapmasını Türk hukuku risk kategorileri, TL tutar eşikleri, imza
  yetkisi ve avukat onay kapılarıyla doğru onay makamına yönlendiren talep
  taslağı üretir. Mesajı göndermez veya onaylamaz.
argument-hint: "[konuyu özetleyin veya inceleme notunu referans gösterin]"
---

# Risk Eskalasyon Yönlendiricisi (`/escalation-flagger`)

Sözleşme riskini veya playbook sapmasını doğru onay makamına yönlendirir ve gönderilmeye hazır bir onay talep taslağı hazırlar. Kararı kendisi vermez ve mesajı otomatik göndermez.

## Talimatlar

1. `~/.claude/plugins/config/legal-turkish/commercial-legal/CLAUDE.md` -> `## Escalation and Approval Matrix` bölümünü yükle.
2. Tarafı netleştir (`sales-side` mı `purchasing-side` mı). Bir hüküm bir tarafta kabul edilebilirken diğer tarafta eskalasyon sebebi olabilir.
3. Konuyu kategorize et:
   - TL / döviz işlem tutarı eşiği (`32 s. Karar` döviz kısıtı dahil),
   - Playbook sapması,
   - Otomatik eskalasyon tetikleyicisi,
   - İmza ve temsil yetkisi boşluğu,
   - Hukuki değil ticari/işletmesel risk kararı.
4. Matrisle eşleştir ve onay verecek kişi/kurulu belirle.
5. Konuyu, ilgili maddeyi, playbook pozisyonunu, seçenekleri, öneriyi ve karar son tarihini içeren taslağı oluştur.
6. Otomatik gönderme; kullanıcıya önizleme olarak sun.
7. Aktif bir dosya (`matter`) varsa eskalasyon durumunu dosya kaydına işle.

## Beklenen Matris Şeması (`Expected Matrix`)

```yaml
eskalasyon_matrisi:
  - can_approve: "Sözleşme Hukukçusu"
    threshold: "standart şartlar / < 1.000.000 TL"
    escalates_to: "Kıdemli Hukuk Müşaviri"
    via: "Slack / e-posta"
  - can_approve: "Hukuk Direktörü / Başmüşavir"
    threshold: "standart dışı şartlar / < 10.000.000 TL"
    escalates_to: "CFO / Genel Müdür / Yönetim Kurulu"
    via: "onay bilgi notu"
automatic_triggers:
  - sinirsiz_sorumluluk
  - fahis_cezai_sart_tbk_179_182_ttk_22
  - fsek_ip_devri
  - kvkk_m9_aktarim_riski
```

## Türk Hukuku Otomatik Eskalasyon Tetikleyicileri

- Sınırsız sorumluluk veya ağır kusur dışındaki sınırsız tazminat kalemleri.
- Fahiş veya tek taraflı cezai şart (`TBK m. 179–182`; tacirler arası `TTK m. 22` ve `TBK m. 27` istisnası).
- `FSEK` / sınai mülkiyet devri veya geniş münhasır lisans.
- Onaylı mekanizma olmadan `KVKK m. 9` yurt dışı veri aktarımı veya özel nitelikli veri.
- Rekabet yasağı, münhasırlık, müşteri/çalışan ayartmama (`non-solicit`).
- Playbook dışı yabancı uygulanacak hukuk veya yabancı mahkeme yetkisi.
- Kurumu, tahkim yeri veya dili belirsiz tahkim şartı.
- Kefalet, garanti, ana ortak garantisi veya banka teminat mektubu.
- İmza sirküleri, iç yönerge veya yönetim kurulu/genel kurul onay boşluğu.
- Üst sınırsız fiyat artışı veya `32 s. Karar` dövizle sözleşme yasağı maruziyeti.
- İmza, tadil, teminat, sulh veya devir nedeniyle uzman incelemesi gerektiren `damga vergisi (488 s. DVK)` etkisi.
- Uyuşmazlık çözümünde `6325 s. Arabuluculuk Kanunu` zorunlu dava şartı etkileşimi.

## Talep Taslağı Formatı

```markdown
**Onay Makamı:** [İsim / Unvan]
**Kanal:** [E-posta / Slack / Toplantı / Onay Akışı]
**Aciliyet:** [Son tarih]
**Uygulanan Playbook:** [sales-side / purchasing-side]

---

Sayın [İsim],

[Karşı Taraf] ile akdedilecek [sözleşme türü] kapsamında aşağıdaki konuda onayınıza ihtiyaç vardır.

**Risk / Sapma:** [Sade Türkçe özet]

**Sözleşmedeki Madde:**
> "[kısa birebir alıntı]"

**Playbook Pozisyonumuz:** [`CLAUDE.md` pozisyonu]

**Seçenekler:**
1. **Kabul Et** — [hangi şartla/neden katlanılabilir olduğu]
2. **Revize / Karşı Öneri Sun** — "[daraltılmış revizyon önerisi]"
3. **Durdur / Üst Onaya Taşı** — [reddi veya üst kurul kararı]

**Önerim:** [Gerekçeli tavsiye]

**Karar Beklenen Tarih:** [tarih]

[Tam inceleme notuna bağlantı]
```

## Kalibrasyon

Madde belgelenmiş geri çekilme (`fallback`) sınırı içindeyse eskalasyon açma. Sınır dışındaysa veya otomatik tetikleyiciler listesindeyse mutlaka eskale et; belirsiz ise belirsizliği açıkça yazarak eskale et.

## Bu Beceri Neleri Yapmaz

- Onay vermez veya ticari riski kendi başına üstlenmez.
- İmza yetkisi yaratmaz.
- Mesajı otomatik olarak göndermez.
- Yönetim kurulu, genel kurul veya iç yetki devri prosedürünün yerine geçmez.
