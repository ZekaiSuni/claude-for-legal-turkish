# AI Governance Legal - Legal Turkish

Türkiye hukuku ve sınır ötesi AB AI Act uyumu için kurum içi ve danışmanlık odaklı Yapay Zekâ Yönetişimi eklentisi: kullanım senaryosu triyajı, yapay zekâ etki değerlendirmesi (YZED / AIA), tedarikçi AI sözleşme incelemesi, AI sistem envanteri, politika taslağı oluşturma, politika sapma takibi ve mevzuat gap analizi.

> **Her çıktı hukukçu incelemesine tabi taslaktır — nihai hukuki mütalaa veya resmî uyum sertifikasyonu değildir.** Eklenti belgeleri okur, iç politikanızı ve Türkiye mevzuat çerçevesini uygular, riskleri ve kırmızı çizgileri yüzeye çıkarır; doğrulama ve karar yetkisi sorumlu avukattadır. Tüm mevzuat atıfları, yürürlük tarihleri, idari para cezaları ve Kurul kararları güncel resmî kaynaklardan doğrulanmalıdır.

## Kimler İçin

| Rol | Ana İş Akışları |
|---|---|
| **KVKK / AI Yönetişimi Hukukçusu** | YZED/AIA incelemeleri, KVKK m. 9/11 uyumu, mevzuat gap analizi, AI envanteri |
| **Ürün Hukukçusu (Product Counsel)** | Yeni AI özellikleri için ön triyaj, şeffaflık ve Reklam Kurulu riskleri |
| **Hukuk Başmüşaviri (GC) / Uyum** | AI politikası yönetişimi, politika sapma (drift) taraması, yönetim eskalasyonu |
| **Satın Alma / Sözleşme Hukukçusu** | AI/Copilot tedarikçi sözleşmelerinde model eğitimi, FSEK ve gizlilik incelemesi |

## İlk Kurulum: Cold-Start Görüşmesi

Eklenti; kurumunuzun AI geliştirici mi, kullanıcı (deployer) mı, yoksa her ikisi mi olduğunu; Türkiye içi ve sınır ötesi düzenleyici ayak izinizi; kırmızı çizgilerinizi ve kurum etki değerlendirmesi (YZED) stilinizi öğrenir. Varsa mevcut AI politikanızı ve sözleşme şablonlarınızı okuyarak profilinizi oluşturur.

```text
/ai-governance-legal:cold-start-interview
```

## Komutlar

| Komut | Ne Yapar |
|---|---|
| `/ai-governance-legal:cold-start-interview` | Kurulum görüşmesi — uygulama profilini `CLAUDE.md` yoluna yazar |
| `/ai-governance-legal:customize` | Tüm görüşmeyi baştan almadan profilin tek bir bölümünü günceller |
| `/ai-governance-legal:use-case-triage [senaryo]` | Önerilen AI kullanımını kayıt/kırmızı çizgiler ve KVKK/FSEK/TTK açısından sınıflar |
| `/ai-governance-legal:aia-generation [kullanım]` | Kurum formatında Yapay Zekâ Etki Değerlendirmesi (YZED / AIA) üretir |
| `/ai-governance-legal:vendor-ai-review [dosya/metin]` | Tedarikçi AI şartlarını model eğitimi, KVKK m. 9, FSEK ve sorumluluk açısından inceler |
| `/ai-governance-legal:ai-inventory` | Sistem bazında AI rolü ve risk katmanı envanterini (`ai-systems.yaml`) yönetir |
| `/ai-governance-legal:reg-gap-analysis [düzenleme]` | Yeni AI düzenlemesini veya KVKK/USOM/AB rehberini mevcut duruma göre diff'ler |
| `/ai-governance-legal:policy-monitor` | Kayıtlı çıktılarda politika sapması (drift) tarar veya yeni uygulama sorusunu kontrol eder |
| `/ai-governance-legal:policy-starter` | Referans politikalardan uyarlanan hukukçu incelemelik ilk AI kullanım politikası taslağı üretir |
| `/ai-governance-legal:matter-workspace` | Çok müvekkilli büro kullanımında dosya bazlı bağlam izolasyonu yönetir |

## Türkiye Hukuku Odak Çerçevesi

- **6698 s. KVKK:** Aydınlatma (m. 10), açık rıza/işleme şartları (m. 5), özel nitelikli/biyometrik veriler (m. 6), yurt dışına veri aktarımı ve standart sözleşme / 5 iş günü Kurum bildirimi (m. 9), otomatik kararlara itiraz hakkı (**m. 11/1-(g)**), veri güvenliği ve ihlal bildirimi (m. 12).
- **7545 s. Siber Güvenlik Kanunu (2025) & Siber Güvenlik Başkanlığı / USOM:** Kritik altyapı AI kullanımı, tedarikçi zafiyet ve olay bildirimi uyumu.
- **5846 s. FSEK & 6769 s. SMK:** Eğitim verisinde telif ihlali riski, AI çıktılarının eser niteliği/hak sahipliği ve tedarikçi FSEK tazminatı.
- **6701 s. TİHEK Kanunu & 4857 s. İş Kanunu (m. 5):** İşe alım, değerlendirme, kredi/sigorta skorlama gibi alanlarda algoritmik ayrımcılık riskleri.
- **6102 s. TTK (m. 54–55) & 1136 s. Avukatlık Kanunu (m. 36):** Ticari sır ve avukat-müvekkil sır saklama yükümlülüğü.
- **6502 s. TKHK / 6563 s. E-Ticaret K. / Reklam Kurulu:** Sentetik içerik ve AI iddialarında tüketiciyi aldatma ve örtülü reklam yasağı.
- **Sınır Ötesi AB AI Act ((AB) 2024/1689):** Yalnızca AB/AEA'ya sunulan veya AB'deki bireyleri etkileyen çıktılar üreten sistemlerde zorunlu kapsam; şirket içi Türkiye projelerinde isteğe bağlı referans standardı.

## Eklenti Üçgeni: `ai-governance-legal` ↔ `product-legal` ↔ `privacy-legal`

- **`product-legal`**, ürün lansmanında AI bileşeni tespit ettiğinde `/ai-governance-legal:use-case-triage` ve `/ai-governance-legal:aia-generation` komutlarına devreder.
- **`privacy-legal`**, kişisel veri işleme odaklı etki değerlendirmesi (PIA/VERBİS/KVKK m. 9) gerektiğinde paralel çalışır.
- **`ai-governance-legal`**, YZED/triage aşamasında kişisel veri akışı gördüğünde `/privacy-legal:pia-generation` çalıştırılmasını işaretler; canlı mevzuat akışı takibi için `regulatory-legal` ile eşleşir.

## Yapılandırma ve Konum

Kullanıcı profili eklenti güncellemelerinden korunacak şekilde şu dizinde saklanır:

```text
~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md
```

Ortak şirket profili bir üst dizinde yer alır (`~/.claude/plugins/config/legal-turkish/company-profile.md`).
`.mcp.json` içinde Slack ve Google Drive tanımlıdır; harici mevzuat MCP'si bulunmadığından resmî atıflar kullanıcı girdisi veya web doğrulamasıyla `[doğrula]` / `[Resmî Gazete]` etiketleriyle izlenir.

## Dosya Yapısı

```text
ai-governance-legal/
├── .claude-plugin/plugin.json
├── .mcp.json
├── CLAUDE.md
├── README.md
├── hooks/
├── references/
│   └── currency-watch.md
└── skills/
    ├── ai-inventory/
    ├── aia-generation/
    ├── cold-start-interview/
    ├── customize/
    ├── matter-workspace/
    ├── policy-monitor/
    ├── policy-starter/
    ├── reg-gap-analysis/
    ├── use-case-triage/
    └── vendor-ai-review/
```
