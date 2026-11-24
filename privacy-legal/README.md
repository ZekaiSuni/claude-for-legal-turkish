# Privacy / KVKK Legal Plugin - Legal Turkish

Bu klasör, kişisel verilerin korunması iş akışlarını Türk hukuku ve uygulamasına göre yürütür. Amaç yabancı privacy şablonunu çevirmek değil; aynı işlevi 6698 sayılı Kişisel Verilerin Korunması Kanunu, Kişisel Verileri Koruma Kurumu/Kurul uygulaması, VERBIS, aydınlatma yükümlülüğü, açık rıza, özel nitelikli veri, yurt dışına aktarım, veri ihlali bildirimi ve Türkiye'deki ticari uygulama içinde yeniden kurmaktır.

Her çıktı avukat/hukukçu incelemesine tabi taslaktır. Kurul bildirimi, ilgili kişi yanıtı, politika yayını, veri işleyen sözleşmesi imzası, yurt dışı aktarım bildirimi veya veri ihlali aksiyonu açık insan onayı olmadan yapılmaz.

## Kimler Kullanır

| Rol | Ana iş akışları |
|---|---|
| KVKK / privacy counsel | VKED/PIA, yurt dışı aktarım, veri işleyen sözleşmesi, Kurul süreci |
| Hukuk operasyonu / uyum | İlgili kişi başvuruları, VERBIS envanteri, politika drift takibi |
| Ürün / IT / güvenlik ekibi | Yeni veri işleme faaliyeti triyajı, ihlal ilk değerlendirmesi |
| Dış hukuk bürosu | Müvekkil bazlı matter workspace, sözleşme ve politika incelemesi |

## İlk Kurulum

```
/privacy-legal:cold-start-interview
```

Hazır olması yararlı bilgiler:

- Aydınlatma metni / gizlilik politikası,
- Kişisel veri işleme envanteri veya VERBIS kaydı,
- Standart veri işleyen / hizmet sağlayıcı sözleşmesi,
- Bir örnek VKED/PIA veya iç privacy review,
- Yurt dışına aktarım ve saklama/imha politikası.

Profil `~/.claude/plugins/config/legal-turkish/privacy-legal/CLAUDE.md` yoluna yazılır ve plugin güncellemelerinden etkilenmez.

## Komutlar

| Komut | İşlev |
|---|---|
| `/privacy-legal:cold-start-interview` | KVKK pratik profilini kurar |
| `/privacy-legal:use-case-triage [faaliyet]` | Yeni veri işleme faaliyeti için ilerleyebilir / VKED gerekli / dur seçeneklerini verir |
| `/privacy-legal:pia-generation [faaliyet]` | VKED / privacy impact assessment taslağı üretir |
| `/privacy-legal:dpa-review [dosya]` | Veri işleyen, veri sorumluları arası aktarım veya yurt dışı aktarım sözleşmesini inceler |
| `/privacy-legal:dsar-response` | İlgili kişi başvurusu için doğrulama, sistem taraması ve yanıt taslağı üretir |
| `/privacy-legal:reg-gap-analysis [mevzuat]` | Yeni KVKK/Kurul/Resmi Gazete düzenlemesine göre gap analizi çıkarır |
| `/privacy-legal:policy-monitor` | Politika, aydınlatma metni, CMP/çerez ve uygulama çıktıları arasında drift arar |
| `/privacy-legal:customize` | Profilde tek alan değişikliği yapar |
| `/privacy-legal:matter-workspace` | Çok müvekkilli kullanımda dosya izolasyonu sağlar |

## Temel Guardrail'ler

- KVKK m.5/m.6 işleme şartı belirlenmeden "uygun" denmez.
- Aydınlatma metni ile açık rıza ayrı değerlendirilir; battaniye rıza kabul edilmez.
- Özel nitelikli veri, çocuk verisi, çalışan verisi, konum/biyometri/sağlık/ceza mahkumiyeti verisi ve büyük ölçekli izleme daima eskalasyon konusudur.
- Yurt dışına aktarımda KVKK m.9 güncel çerçevesi, yeterlilik kararı, uygun güvenceler, standart sözleşme bildirimi ve arızi aktarım istisnaları kontrol edilir.
- Veri ihlali şüphesinde güvenlik ve hukuk birlikte devreye alınır; Kurul/ilgili kişi bildirimi için süreler güncel kaynaktan doğrulanır.
- VERBIS, saklama-imha, çerez/ETK/İYS ve sektör regülatörü etkileri ayrıca işaretlenir.

## Dosya Yapısı

```
privacy-legal/
├── CLAUDE.md
├── README.md
├── references/
│   └── currency-watch.md
├── skills/
│   ├── cold-start-interview/
│   ├── use-case-triage/
│   ├── pia-generation/
│   ├── dpa-review/
│   ├── dsar-response/
│   ├── reg-gap-analysis/
│   ├── policy-monitor/
│   ├── customize/
│   └── matter-workspace/
└── hooks/hooks.json
```
