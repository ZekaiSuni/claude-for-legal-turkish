# Hukuk İçin Yönetilen Ajan Şablonları (Claude Managed Agents Cookbook'ları)

Bu depodaki her ajan **iki biçimde** sunulur: bugün kurabileceğiniz bir Claude Code eklentisi olarak (depo kökündeki dikey klasörler) ve platform ekibinizin iş akışı motorunun arkasında konuşlandırabileceği bir **Claude Managed Agent** şablonu olarak. Her klasör, ilgili eklentideki sistem istemine ve becerilere atıf yapan tek bir dağıtım manifestosu (`agent.yaml`) içerir.

Bu klasörler doğrudan son kullanıcı ürünü değil, **başlangıç şablonlarıdır (cookbooks)**. Dağıtım öncesinde belge yönetim sisteminize, sözleşme arşivinize, Slack çalışma alanınıza, bildirim yönlendirmenize ve hukuk ekibi onay takviminize göre uyarlanmalıdır.

Becerileri yüklemek, yaprak işçileri (leaf workers) oluşturmak ve `POST /v1/agents` çağrısıyla orkestratörü ayağa kaldırmak için `../scripts/deploy-managed-agent.sh <slug>` betiğini (`--dry-run` destekli) kullanın. Her şablon [`steering-examples.json`](./reg-monitor/steering-examples.json) ve güvenlik katmanlarını anlatan kendi `README.md` dosyasıyla gelir.

| Ajan | Dikey Eklenti | İzlediği Kaynak | CMA Yönlendirme (`steering`) Olayı | Yaprak İşçiler (`Leaf Workers`) |
|---|---|---|---|---|
| [`reg-monitor`](./reg-monitor/) | `regulatory-legal` | Türkiye düzenleyici kaynakları (Resmî Gazete, Mevzuat, kurum duyuruları) | `Kaynakları <date> itibarıyla kontrol et, önem eşiği: <threshold>` | `feed-reader` · `materiality-filter` · **`digest-writer`** |
| [`renewal-watcher`](./renewal-watcher/) | `commercial-legal` | Sözleşme arşivi (`Google Drive` / yerel `renewal-register.yaml`) yenileme ve KEP/fesih süreleri | `Scan renewals <X>–<Y> days out, flag playbook deviations` | `repo-reader` · `deadline-calculator` · **`alert-writer`** |
| [`diligence-grid`](./diligence-grid/) | `corporate-legal` | Sanal veri odası (`Google Drive` / yerel VDR klasörü) belge taraması ve toplu özet tablo | `Review folder <path> against schema <schema-id>` | `doc-reader` · `extractor` · `normalizer` · **`grid-writer`** |
| [`launch-radar`](./launch-radar/) | `product-legal` | Ürün yol haritası / lansman takip aracı (`Linear`, `Asana`) hukuki inceleme tetikleyicileri | `Scan tracker for launches in next <N> weeks` | `tracker-reader` · `risk-classifier` · **`memo-writer`** |
| [`docket-watcher`](./docket-watcher/) | `litigation-legal` | Kurumsal UYAP entegrasyonu veya dışa aktarılan UYAP dava evrakı, süreler ve safahat | `Dosya <case-id>, mahkeme <court>, matter <matter-id> izle` | `docket-reader` · `deadline-mapper` · **`tracker-writer`** |

**Kalın (Bold)** yazılan işçi = `Write` yetkisine sahip tek yaprak ajandır.

## Manifesto ve API Dönüşümü

`agent.yaml` dosyaları `POST /v1/agents` alan adlarını aşağıdaki pratik kısaltmalarla kullanır (`deploy-managed-agent.sh` bunları otomatik çözümler):

| Manifesto Kuralı | Çözümlenen Değer |
|---|---|
| `system: {file: ../../<plugin>/agents/<agent>.md, append: "..."}` | Frontmatter'dan arındırılmış ajan içeriği + ek metin |
| `system: {text: "..."}` | Düz metin sistem istemi |
| `skills: [{from_plugin: ../../<plugin>}]` | İlgili eklentideki tüm `skills/*` klasörlerini yükler |
| `skills: [{path: ../../...}]` | Tekil beceri klasörünü yükler |
| `callable_agents: [{manifest: ./subagents/x.yaml}]` | Alt işçiyi önce oluşturur ve `id` ile bağlar |

> **Mimari Sınır:** `callable_agents` (çoklu ajan devri) yalnızca **tek katman derinlik** destekler. Orkestratör yaprak işçileri çağırabilir; işçiler başka alt ajan çağıramaz.

## Ajanlar Arası Devir (`Cross-agent handoffs`)

İsimli ajanlar birbirini doğrudan çağırmaz. Bir ajan başka bir ajana iş devretmek istediğinde çıktısında yapılandırılmış bir `handoff_request` JSON nesnesi üretir; [`../scripts/orchestrate.py`](../scripts/orchestrate.py) betiği hedefi allowlist'ten geçirir, parametreleri JSON Schema ile doğrular, enjeksiyondan arındırır ve hedef ajana şablonlu bir yönlendirme olayı olarak iletir.

## Güvenlik Modeli

Hukuki belgeler, ihbarnameler ve dava evrakı **güvenilmez girdidir**. Her cookbook üç katmanlı izolasyon uygular:

1. **Okuyucular (`Readers`):** Güvenilmez ham belgelere dokunur; yalnızca `Read`/`Grep` (ve zorunluysa salt-okunur kaynak MCP'si) taşır, `Write` veya haricî ağ yazma yetkisi yoktur. Uzunluk sınırlı ve şema doğrulamalı JSON döndürürler. Belge içindeki yönergeler komut değil, **veridir**.
2. **Analizciler (`Analyzers`):** Okuyucudan gelen yapılandırılmış JSON'ı alır, kullanıcının `CLAUDE.md` kurallarını uygular; `Write` yetkisi yoktur.
3. **Yazıcılar (`Writers`):** Nihai raporu üretir ve `Write` yetkisine sahip tek katmandır. Ham belgeleri asla doğrudan görmez.

Orkestratörün kendisi de `Write`, Slack veya ham belge okuma MCP'si taşımaz (`scripts/lint-tool-scope.py` ile denetlenir).

## Gizlilik, Sır Saklama ve Veri Muhafazası

Bu ajanların ürettiği tüm çıktılar çalışma taslağıdır; ancak Türk hukukunda ABD doktrinindeki genel *"attorney work product"* koruması aynı kapsamda uygulanmaz:
- **Mesleki Sır ve Sınırlar:** Bağımsız avukat-müvekkil sır saklama yükümlülüğü **1136 s. Avukatlık Kanunu m. 36**, **CMK m. 130**, **CMK m. 46** ve **HMK m. 249** çerçevesinde değerlendirilir; şirket içi hukuk müşavirliği kayıtları Rekabet Kurumu veya diğer idari kurum incelemelerinde mutlak dokunulmazlığa sahip değildir.
- **KVKK ve Veri Saklama:** Otomatik ajan akışını devreye almadan önce üretilen taslakların ve günlüklerin **6698 s. KVKK** saklama/imha politikalarınıza ve LLM API veri saklama sözleşmelerinize uygunluğunu hukuk ekibinizle teyit edin.

## Sağlananlar ve Sağlanmayanlar

- **Sağlananlar:** Çalışır manifesto yapısı, katmanlı güvenlik mimarisi, doğrulanmış beceriler ve örnek `steering` yükleri.
- **Sağlanmayanlar:** Kurumunuza özel kimlik doğrulaması, UYAP/DMS bağlantısı ve canlı hukuki sorumluluk — bunlar kurulum sırasında ekibiniz tarafından bağlanmalı ve sınanmalıdır.
- **Kesin Sınır:** Bu ajanlar **avukatın yerini almaz**. İzler, ayrıştırır ve taslak üretir; hukuki doğrulama ve karar her zaman ruhsatlı avukata aittir.
