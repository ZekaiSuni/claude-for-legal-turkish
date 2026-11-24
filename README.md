# Claude Legal Turkish

Claude Legal Turkish, Anthropic'in açık kaynaklı **Claude for Legal** yapısını temel alan Türkiye uyarlamasıdır. Amaç, aynı plugin/skill iskeletini koruyarak hukuki içerikleri Türk hukuku, Türkiye yargı sistemi ve yerel regülasyonlar ekseninde çalışır hale getirmektir.

Bu repo; hukuk departmanları, avukatlar, uyum ekipleri ve hukuk operasyonları için sözleşme inceleme, dava/uyuşmazlık takibi, icra ve iflas takibi, idare ve vergi uyuşmazlıkları, KVKK, iş hukuku, ürün hukuku, şirketler hukuku ve regülasyon izleme iş akışlarına yönelik Claude Code plugin'leri içerir.

> Önemli: Bu proje hukuki danışmanlık vermez. Üretilen her çıktı avukat/hukukçu incelemesine tabi taslak, araştırma notu veya karar destek çıktısıdır. Kanun, içtihat, süre, tebliğ, yetki, imza ve resmi kaynak kontrolleri somut dosya için ayrıca doğrulanmalıdır.

## Tasarım Kararı

Operasyonel adlar orijinal repo ile uyumlu tutulur:

- Plugin klasörleri: `commercial-legal`, `litigation-legal`, `privacy-legal` vb.
- Komutlar: `/commercial-legal:review`, `/regulatory-legal:reg-feed-watcher` vb.
- Dosya adları: `SKILL.md`, `CLAUDE.md`, `.mcp.json`, `.claude-plugin/plugin.json`

Türkçeleştirme; hukuki içerikte, kontrol listelerinde, çıktı şablonlarında, örneklerde ve kaynak/kavram katmanında yapılır. Komut adlarını `/ticari-hukuk:*` gibi Türkçeleştirmek ayrı bir repo-geneli refactor işidir.

## Durum Özeti

| Alan | Durum | Not |
|---|---|---|
| `commercial-legal` | Uyarlandı | Türk ticari sözleşme pratiğine göre uyarlandı. |
| `corporate-legal` | Uyarlandı | Türk şirketler hukuku pratiğine göre uyarlandı. |
| `litigation-legal` | Uyarlandı | Türkiye yargı ve dava pratiğine göre uyarlandı. |
| `privacy-legal` | Uyarlandı | KVKK pratiğine göre uyarlandı. |
| `employment-legal` | Uyarlandı | Türk iş hukuku pratiğine göre uyarlandı. |
| `product-legal` | Uyarlandı | Türk ürün, tüketici, reklam ve e-ticaret pratiğine göre uyarlandı (`1.1.0-tr`). |
| `regulatory-legal` | Uyarlandı | Türkiye düzenleyici kurumları (Resmî Gazete, KVKK, Rekabet, SPK, BDDK, BTK, EPDK, TCMB, MASAK, USOM, TÜRKPATENT, RTÜK, GİB, TİHEK) izleme pratiğine uyarlandı (`1.1.0-tr`). |
| `managed-agent-cookbooks` | Uyarlandı | Türkiye yargı ve düzenleyici kurum kaynakları ile çok katmanlı güvenlik mimarisine göre uyarlandı. |
| `ip-legal` | Uyarlandı | Türk fikri ve sınai mülkiyet (FSEK, SMK, 5651, TRABİS, TÜRKPATENT/WIPO) pratiğine tam Türkçeyle uyarlandı (`1.1.0-tr`). |
| `ai-governance-legal` | Uyarlandı | KVKK, 7545 s. Kanun, FSEK, TİHEK, TKHK, TTK ve sınır ötesi AB AI Act ekseninde 10 skill ile Türkiye hukukuna uyarlandı (`1.1.0-tr`). |
| `execution-bankruptcy-legal` | Yerli Eklenti | Türk İcra ve İflas Hukuku (2004 s. İİK, 7201 m. 7/a UETS, 89/1-2-3, e-satış ve konkordato) için 8 skill + 1 ajanla sıfırdan tasarlandı (`1.1.0-tr`). |
| `administrative-tax-legal` | Yerli Eklenti | Türk İdare ve Vergi Uyuşmazlıkları (2577 İYUK, 213 VUK, 7524 s. K., 6183 AATUHK, 5326 ve 4734 KİK) için 8 skill + 1 ajanla sıfırdan tasarlandı (`1.1.0-tr`). |
| `legal-builder-hub` | Uyarlanmadı | Hukuki içerik modülü değil, teknik/meta araç olduğu için kapsam dışında bırakıldı. |
| `law-student` | Uyarlanmadı | ABD hukuk eğitimi/bar prep modeline dayandığı için kapsam dışında bırakıldı. |
| `legal-clinic` | Uyarlanmadı | US law school clinic modeline dayandığı için kapsam dışında bırakıldı. |
| `cocounsel-legal` | Uyarlanmadı | Üçüncü taraf Westlaw/Practical Law plugin'i olduğu için değiştirilmedi. |

## Kurulum

Claude Code içinde bu klasörü yerel marketplace olarak ekleyin:

```text
/plugin marketplace add C:\path\to\claude-for-legal-turkish-main
```

Bir plugin kurun:

```text
/plugin install commercial-legal@legal-turkish
```

Claude Code'u yeniden başlatın. Ardından ilgili plugin'in başlangıç mülakatını çalıştırın:

```text
/commercial-legal:cold-start-interview
```

İlk kullanım örneği:

```text
/commercial-legal:review "C:\sozlesmeler\tedarikci-taslak.docx"
```

Diğer örnekler:

```text
/litigation-legal:demand-intake
/privacy-legal:pia-generation
/employment-legal:termination-review
/regulatory-legal:reg-feed-watcher
/execution-bankruptcy-legal:itiraz-ve-sikayet
/administrative-tax-legal:vergi-uyusmazlik
```

Kısa kurulum akışı için: [QUICKSTART.md](QUICKSTART.md)

> **Profil Dizini Ayrımı:** Aynı makinede orijinal `claude-for-legal` eklentisiyle çakışmaması için tüm Türk uyarlaması kullanıcı profilleri ve dosya alanları `~/.claude/plugins/config/legal-turkish/` altında saklanır. Eski `~/.claude/plugins/config/claude-for-legal/` klasöründe profiliniz varsa yeni yola kopyalayabilirsiniz.

## Bağlantılar ve MCP

Eklentilerde Slack, Google Drive, Linear ve Asana gibi operasyonel bağlayıcılar opsiyonel olarak tanımlıdır; ticari CLM/VDR araçları ve ücretli/haricî hukuk veri tabanları bu pakete dahil edilmemiştir. Ayrıntılar için [CONNECTORS.md](CONNECTORS.md) dosyasına bakın.

> Not: Varsayılan kurulumda haricî bir mevzuat veya içtihat MCP sunucusu bulunmaz. Hukuki doğrulama; Resmî Gazete, Mevzuat Bilgi Sistemi (`mevzuat.gov.tr`), ilgili kurum duyuruları, UYAP evrakı ve kullanıcı tarafından sağlanan belgeler üzerinden yapılır. Bağlı bir araştırma aracı yoksa veya ilgili resmî metin oturumda çekilmediyse çıktılardaki kanun/karar atıfları `[model bilgisi - doğrula]` uyarısı taşır.

## Repo Yapısı

```text
claude-for-legal-turkish-main/
├── .claude-plugin/
│   └── marketplace.json
├── commercial-legal/
├── corporate-legal/
├── litigation-legal/
├── privacy-legal/
├── employment-legal/
├── product-legal/
├── regulatory-legal/
├── ip-legal/
├── ai-governance-legal/
├── execution-bankruptcy-legal/
├── administrative-tax-legal/
├── managed-agent-cookbooks/
├── legal-builder-hub/
├── references/
└── scripts/
```

## Doğrulama

Depo genelindeki otomatik yapısal kontroller:

- Marketplace `source` yolları ve plugin manifestleri çözümleniyor.
- Tüm JSON ve YAML dosyaları parse ediliyor.
- Somut plugin komut atıfları, Markdown bağlantıları ve eklenti `README.md` komut listeleri doğrulanıyor.
- Managed-agent `manifest`, `file` ve `from_plugin` referansları ile JSON Schema kuralları çözümleniyor.
- `CLAUDE.md` bölüm sözleşmeleri ve Türk hukuku regresyon kuralları denetleniyor.

Windows ve Linux/macOS ortamlarında tüm yapısal kontrolleri, frontmatter/başlık sözleşmelerini, Türkçe managed-agent şema testlerini ve regresyon taramasını çalıştırmak için:

```bash
python scripts/lint-tool-scope.py
python scripts/audit_repo.py
```

## Yayın Notu

Bu repo bir Türkiye uyarlama çalışmasıdır. Orijinal Claude for Legal projesinin lisans ve katkı koşulları korunur. Uyarlanan içeriklerde Türk hukuku terminolojisi kullanılsa da hiçbir çıktı doğrudan hukuki mütalaa, avukat görüşü veya resmi kaynak doğrulaması yerine geçmez.

## İletişim

Soru, katkı ve bildirimler için: [info@hukukcuapp.com](mailto:info@hukukcuapp.com)

## Lisans

Apache License 2.0. Ayrıntı için [LICENSE](LICENSE).
