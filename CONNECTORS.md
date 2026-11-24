# Bağlayıcılar ve MCP Mimarisi (Legal Turkish)

Bu eklenti seti; belgeleri doğrudan yerel dosya yollarından okuyabileceği gibi, aşağıdaki opsiyonel operasyonel MCP bağlayıcılarıyla da çalışabilir. Bağlı MCP yoksa tüm skill'ler kullanıcı tarafından paylaşılan dosya/metin girdileriyle kesintisiz çalışır.

## İyi Bir Hukuk MCP Bağlayıcısında Aranan İlkeler

- **HTTPS üzerinden uzak MCP sunucusu** (OAuth veya API anahtarı doğrulamalı; streamable HTTP / SSE).
- **Salt okunur öncelik:** Arama, listeleme ve okuma araçları varsayılandır. Oluşturma, gönderme veya dosyalama yapan yazma araçları kullanıcı tarafında açık onay kapısı gerektirir.
- **Kaynak izlenebilirliği (Provenance):** Sonuçlarda kaynak adı, erişim tarihi ve atfa hazır kayıt/karar numarası döndürülmelidir.
- **Talimat enjeksiyonuna karşı ayrım:** Alınan hukuki metinler ve belgeler **veri** olarak işlenir, asla komut olarak yorumlanmaz.
- **Zaman aşımı ve hata toleransı:** Bağlantı yoksa skill sessizce uydurma yapmaz; `[model bilgisi - doğrula]` uyarısıyla güvenli fallback uygular.

## Varsayılan `.mcp.json` Bağlayıcıları

Haricî hukuk veri tabanları ve üçüncü taraf CLM/VDR sistemleri bu eklenti paketine varsayılan olarak dahil edilmemiştir; kurum içi kullanımda yalnızca aşağıdaki operasyonel bağlayıcılar opsiyonel olarak yer alır:

| Bağlayıcı | Kapsanan Eklentiler | Kullanım Notu |
|---|---|---|
| **Slack** | Tüm uyarlanmış eklentiler | Ekip bildirimleri ve yazışma arama (KVKK ve avukatlık sırrı kurallarına dikkat edilerek) |
| **Google Drive** | Tüm uyarlanmış eklentiler | Sözleşme, VDR klasörü, dava dosyası ve politika belgelerini okuma (özel nitelikli veri aktarımına dikkat) |
| **Linear** | `product-legal` | Ürün yol haritası ve lansman ticket'larını izleme |
| **Asana** | `product-legal` | Lansman ve pazarlama görevlerini izleme |

> Not: Kapsam dışı bırakılan `law-student`, `legal-clinic`, `legal-builder-hub` ve `external_plugins/cocounsel-legal` eklentileri orijinal referans amaçlı korunmuştur.

## Türkiye İçin Geliştirilmesi Değerli Özel Bağlayıcı Adayları

Kurumsal hukuk ekipleri kendi ortamlarına aşağıdaki salt-okunur özel MCP sunucularını ekleyebilir:

- **Resmî Gazete & Mevzuat Bilgi Sistemi (`resmigazete.gov.tr` / `mevzuat.gov.tr`)** — Konsolide kanun/yönetmelik/tebliğ metinlerine ve günlük yayım akışına salt-okunur erişim.
- **Kurumsal UYAP / UETS Dışa Aktarım Köprüsü** — Avukat portalından alınan safahat, duruşma ve tebligat kayıtlarının salt-okunur okunması (otomatik işlem/gönderim yapmaksızın).
- **KEP / E-İmza Arşivi** — İhtarname ve fesih bildirimlerinin teslim/okunma tarihlerinin doğrulanması (`KEP Yönetmeliği m. 15/2`).
- **GİB Dijital Vergi Dairesi / İnteraktif Vergi Dairesi (Salt-Okunur)** — e-Tebligat (`VUK m. 107/A`), borç/tarhiyat ve `6183` ödeme emri kayıtlarının salt-okunur kontrolü.
- **TÜRKPATENT / MERSİS / KAP Salt-Okunur Sorgu** — Marka/patent yenileme takibi, ticaret sicili ve özel durum açıklaması kontrolü.
