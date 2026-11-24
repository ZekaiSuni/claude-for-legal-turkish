# Commercial Legal - Legal Turkish

Türk hukuku ve Türkiye ticari sözleşme pratiğine uyarlanmış commercial contracts plugin'i.

Bu plugin tedarikçi sözleşmeleri, gizlilik sözleşmeleri, SaaS/abonelik sözleşmeleri, tadil geçmişi, yenileme/fesih ihbar takibi, onay eskalasyonu ve iş birimi özetleri için kullanılır. Komut adları orijinal plugin ile uyumlu kalır; hukuki içerik ve çıktı dili Türk hukukuna göre düzenlenir.

> Her çıktı avukat incelemesine tabi taslaktır. İmza, gönderim, noter/KEP bildirimi, UYAP işlemi veya karşı tarafa metin iletimi açık insan onayı olmadan yapılmaz.

## Kimler İçin

| Rol | Ana iş akışları |
|---|---|
| Hukuk müşaviri / ticari sözleşme avukatı | Sözleşme inceleme, redline, eskalasyon, playbook yönetimi |
| Sözleşme yöneticisi / legal ops | İlk inceleme, yenileme takibi, iş birimi özeti |
| Satın alma | Tedarikçi sözleşmesi, yenileme/fesih penceresi, fiyat artışı riski |
| Satış / iş geliştirme | GS/NDA tasnifi ve hukuk öncesi hazırlık |
| Hukuk bürosu / serbest avukat | Müvekkil bazlı dosya çalışma alanı ve ticari sözleşme incelemesi |

## İlk Kurulum

```text
/commercial-legal:cold-start-interview
```

Kurulum şunları öğrenir:

- kullanıcı rolü ve avukat erişimi,
- satış tarafı / satın alma tarafı playbook ayrımı,
- Türk hukuku varsayımları,
- mahkeme, tahkim, KEP/noter bildirim tercihleri,
- KVKK ve yurt dışına aktarım yaklaşımı,
- TL onay eşikleri ve imza yetkisi,
- NDA GREEN/YELLOW/RED kriterleri,
- yenileme/fesih takip düzeni,
- matter workspace ihtiyacı.

Profil şu yola yazılır:

```text
~/.claude/plugins/config/legal-turkish/commercial-legal/CLAUDE.md
```

## Komutlar

| Komut | İşlev |
|---|---|
| `/commercial-legal:cold-start-interview` | Türk commercial profile kurulumunu yapar veya günceller |
| `/commercial-legal:review [file]` | Sözleşme türünü tanır ve doğru inceleme skill'ine yönlendirir |
| `/commercial-legal:renewal-tracker` | Yenileme ve fesih ihbar pencerelerini gösterir |
| `/commercial-legal:escalation-flagger` | Risk veya playbook sapmasını doğru onay makamına yönlendirir |
| `/commercial-legal:amendment-history [file(s)]` | Ana sözleşme, ek protokol, zeyilname ve tadil geçmişini izler |
| `/commercial-legal:review-proposals` | Playbook güncelleme önerilerini hukukçu onayına sunar |
| `/commercial-legal:matter-workspace` | Çok müvekkilli çalışma için dosya bağlamlarını yönetir |

## Skill'ler

| Skill | Durum | Amaç |
|---|---|---|
| `cold-start-interview` | Türk sürüm | Pratik profilini kurar |
| `review` | Türk sürüm | Router ve birleşik ticari sözleşme incelemesi |
| `vendor-agreement-review` | Türk sürüm | Tedarikçi/hizmet/MSA incelemesi |
| `nda-review` | Türk sürüm | Gizlilik sözleşmesi GREEN/YELLOW/RED tasnifi |
| `saas-msa-review` | Türk sürüm | SaaS, abonelik, KVKK, alt işleyen, yenileme katmanı |
| `renewal-tracker` | Türk sürüm | KEP/noter/ihbar tarihi odaklı yenileme takibi |
| `amendment-history` | Türk sürüm | Ek protokol, zeyilname, tadil, devir/temlik takibi |
| `escalation-flagger` | Türk sürüm | TL eşikler, imza yetkisi, onay yönlendirmesi |
| `stakeholder-summary` | Türk sürüm | İş birimi için arındırılmış özet |
| `matter-workspace` | Türk sürüm | Müvekkil/dosya bağlamı izolasyonu |
| `customize` | Türk sürüm | Profilde tekil ayar değişikliği |
| `review-proposals` | Türk sürüm | Playbook proposal onayı |

## Scheduled Agents

| Agent | Durum | İşlev |
|---|---|---|
| `renewal-watcher` | gözden geçirilecek | Yenileme kayıt defterinden haftalık rapor üretir |
| `deal-debrief` | gözden geçirilecek | İmzalanan sözleşmelerde playbook sapmalarını loglar |
| `playbook-monitor` | gözden geçirilecek | Sapma logundan playbook güncelleme önerisi üretir |

## Türk Hukuku Guardrail'leri

- UYAP sadece dava/icra bağlantısı varsa kullanılır.
- KEP/noter/iadeli taahhütlü posta ve sözleşmesel bildirim maddesi ayrıca kontrol edilir.
- KVKK, veri sorumlusu/veri işleyen, yurt dışına aktarım ve alt işleyenler işaretlenir.
- Arabuluculuk dava şartı otomatik varsayılmaz; uyuşmazlık türüne göre kontrol edilir.
- İmza ve temsil yetkisi sözleşme temiz olsa bile ayrı kontrol edilir.
- Karşı tarafa gönderilecek metin veya redline avukat onayı olmadan nihai kabul edilmez.

## Dosya Yapısı

```text
commercial-legal/
├── CLAUDE.md
├── README.md
├── agents/
├── hooks/
├── logs/
├── references/
└── skills/
```

## Not

Bu eklenti Türk ticaret ve borçlar hukuku sözleşme pratiği için yapılandırılmıştır (`1.1.0-tr`). Güncel oran ve mevzuat eşikleri için `references/currency-watch.md` dosyasını kontrol edin.

