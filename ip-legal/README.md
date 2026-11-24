# Legal Turkish - Fikri Mülkiyet (IP) Eklentisi (`1.1.0-tr`)

Fikri ve Sınai Mülkiyet Hukuku pratiği: Marka, patent/faydalı model, tasarım, telif hakkı (FSEK), ticari sır (TTK m. 54–56) ve açık kaynak (OSS). FSEK Ek Madde 4 uyarınca uyar-kaldır bildirimleri ve noter/KEP üzerinden tecavüzün men'i ihtarnameleri (gönderme ve yanıtlama) hazırlar veya inceler; marka ön araştırması (clearance) ve faaliyet serbestisi (FTO) triyajı yürütür; sözleşmelerdeki fikri hak devri (FSEK m. 48/2, m. 52, SMK m. 113–122, m. 148) maddelerini denetler; TÜRKPATENT/WIPO/EPO/TRABİS tescil ve yenileme sürelerini izler ve açık kaynak lisans uyumluluğunu kontrol eder.

Sistem bir cold-start mülakatı ile sizin veya kurumunuzun uygulama duruşu, portföyü ve onay matrisi etrafında şekillenir — genel geçer değil, kuruma özel bir uygulama profili öğrenir.

> **Her çıktı avukat/vekil incelemesi için hazırlanmış bir taslaktır — kaynaklı, etiketli ve onaya tabidir — nihai hukuki mütalaa veya resmî işlem yerine geçmez.** Eklenti belgeleri okur, profilinizi uygular, sorunları ve risk faktörlerini yüzeye çıkarır; doğrulama ve karar yetkisi sorumlu avukat veya marka/patent vekilindedir. İhtarname gönderimi, uyar-kaldır başvurusu, TÜRKPATENT başvurusu veya dava açılışı öncesinde yetkili onayı zorunludur.

## Kimler İçin Uygun?

| Rol | Temel İş Akışları |
|---|---|
| **Kurum İçi IP Müşaviri** | İhlal/tecavüz kararları, FSEK/SMK sözleşme maddesi incelemesi, portföy gözetimi, FTO triyajı |
| **Marka / Patent Vekili** | Portföy ve yenileme/itiraz süresi takibi (SMK m. 23, 26, 69, 101), marka ön araştırması |
| **Marka Koruma Yöneticisi** | İhtarnameler, FSEK Ek m. 4 uyar-kaldır ve TRABİS süreçleri, bülten izleme takibi |
| **IP / Fikri Mülkiyet Avukatı** | Müvekkil bazlı çalışma alanları (`matters/`), ihtarname, ihlal değerlemesi, portföy muhafazası *(İstem yazımı HARİÇ)* |
| **Hukuk Operasyonları (Legal Ops)** | Tescil izleme, marka/patent/tasarım yenileme ve yıllık sicil ücreti takibi, OSS sözleşme/SBOM taraması |

Bu eklenti **kesinlikle patent istemi (claim) veya tam patent tarifnamesi yazmaz**. Patent yazımı sınai mülkiyet vekilliği uzmanlığı gerektiren bir alandır ve genel amaçlı araca bırakılmaz. Buradaki patent çalışması; FTO triyajı, buluş bildirimi ön değerlendirmesi (SMK m. 82–84, m. 113–122), sözleşmelerdeki patent maddelerinin incelenmesi ve yenileme/sicil ücreti takibi ile sınırlıdır.

## İlk Çalıştırma: Cold-Start Mülakatı

Profiliniz ilk kurulumda şu dizinde oluşturulur ve eklenti güncellemelerinden korunur:

```text
~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md
```

Başlatmak için: `/ip-legal:cold-start-interview`

## Komutlar

| Komut | İşlev |
|---|---|
| `/ip-legal:cold-start-interview` | Başlangıç mülakatını çalıştırır ve `CLAUDE.md` profilini yazar |
| `/ip-legal:customize` | Görüşmeyi baştan almadan profilin tek bir bölümünü günceller |
| `/ip-legal:cease-desist [bağlam]` | Tecavüzün Men'i İhtarnamesi hazırlar veya gelen ihtarnameyi inceler |
| `/ip-legal:takedown [bağlam]` | FSEK Ek Madde 4 Uyar-Kaldır bildirimi (veya ABD platformları için sınır ötesi bildirim) hazırlar/yanıtlar |
| `/ip-legal:clearance [marka]` | Marka Ön Araştırması — tescil edilebilirlik ve iltibas riskleri (SMK m. 5–6 / TÜRKPATENT) |
| `/ip-legal:fto-triage [ürün/kapsam]` | Faaliyet Serbestisi (FTO) ve bağımsız istem unsur-unsur ön incelemesi (SMK m. 82–145) |
| `/ip-legal:invention-intake [buluş]` | Buluş bildirimi ilk aşama kontrolü (SMK m. 82–84, hizmet/serbest buluş m. 113–122) |
| `/ip-legal:infringement-triage [bağlam]` | Marka, telif, patent ve ticari sır/haksız rekabet tecavüzü ön değerlendirmesi |
| `/ip-legal:ip-clause-review [dosya]` | Sözleşmelerdeki IP maddelerinin (FSEK m. 18, 48/2, 52; SMK m. 113–122, 148) incelenmesi |
| `/ip-legal:oss-review [repo/dosya]` | Açık kaynak (OSS) lisans uyumluluk ve copyleft kontrolü |
| `/ip-legal:portfolio` | TÜRKPATENT/WIPO/EPO/TRABİS tescil, yıllık ücret (SMK m. 101) ve yenileme takibi (`portfolio.yaml`) |
| `/ip-legal:matter-workspace` | Çok müvekkilli bürolarda dosya bazlı bağlam izolasyonu yönetimi (`matters/`) |

## Bağlantılar (Connectors) ve Doğrulama

`.mcp.json` içinde Slack ve Google Drive tanımlıdır. TÜRKPATENT, WIPO, EPO, UYAP veya ticari veri tabanlarına (Lexpera, Kazancı vb.) bağlı bir MCP bulunmadığından resmî sicil/mevzuat kontrolleri kullanıcının sağladığı kayıtlarla veya manuel doğrulama uyarılarıyla (`[doğrula]`) yürütülür. Güncel harç ve mevzuat takibi için `references/currency-watch.md` dosyasına bakın.
