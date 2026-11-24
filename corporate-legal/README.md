# Corporate Legal - Türk Şirketler Hukuku

Bu plugin şirketler hukuku, M&A, kurumsal yönetim, yönetim kurulu/genel kurul işleri, sermaye piyasası uyumu ve tüzel kişi kayıt takibi için Türk hukuku ve Türkiye uygulamasına uyarlanmış çalışma akışları sağlar.

Amaç, ABD şirketler hukuku şablonunu çevirmek değil; aynı işlevi TTK, ticaret sicili/MERSİS, karar defterleri, imza ve temsil yetkisi, SPK/KAP/MKK, Rekabet Kurumu, KVKK ve Türkiye M&A kapanış pratiği içinde yeniden kurmaktır.

Her çıktı avukat veya yetkili hukukçu incelemesine tabi taslaktır. Plugin belge okur, riskleri sınıflandırır, karar taslakları ve takip tabloları hazırlar; imza, tescil, bildirim, dosyalama veya hukuki görüş verme kararını kullanıcının yetkili hukukçusu verir.

## Kimler için

| Rol | Aktif modüller |
|---|---|
| Şirket içi hukuk / genel hukuk müşaviri | M&A, Kurumsal Yönetim, Entity Management |
| M&A avukatı | M&A, due diligence, kapanış listesi, disclosure schedule |
| Yönetim kurulu / genel kurul sekreterliği yapan hukukçu | Kurumsal Yönetim, karar ve tutanak taslakları |
| Halka açık şirket hukuk ekibi | SPK/KAP/MKK, özel durum, kurumsal yönetim, M&A |
| Çok şirketli grup hukuk operasyonu | Entity Management, sicil ve uyum takibi |

## İlk çalıştırma

```text
/corporate-legal:cold-start-interview
```

Bu komut hangi modüllerin gerekli olduğunu sorar ve `~/.claude/plugins/config/legal-turkish/corporate-legal/CLAUDE.md` dosyasına Türk şirketler hukuku pratiğine uygun profil yazar.

Yeni bir işlem veya M&A dosyası için:

```text
/corporate-legal:cold-start-interview --new-deal
```

## Komutlar

| Komut | İşlev |
|---|---|
| `/corporate-legal:cold-start-interview` | Türk şirketler hukuku profilini kurar veya günceller |
| `/corporate-legal:customize` | Şirket profili, temsil sınırları veya kapanış tercihlerini günceller |
| `/corporate-legal:diligence-issue-extraction [folder]` | VDR / belge klasöründen Türkiye M&A risklerini çıkarır |
| `/corporate-legal:tabular-review` | Belge setini kolon bazlı, kaynaklı tabloya dönüştürür |
| `/corporate-legal:deal-team-summary` | İşlem ekibine veya yönetime yönelik M&A durum ve risk özeti üretir |
| `/corporate-legal:ai-tool-handoff` | Toplu inceleme / tablo özetlerini uyumlu araç akışına devretmek üzere yapılandırır |
| `/corporate-legal:material-contract-schedule` | Önemli sözleşmeler listesi ve disclosure schedule taslağı üretir |
| `/corporate-legal:closing-checklist` | İmza/kapanış koşulları, izinler, tesciller ve açık işleri izler |
| `/corporate-legal:board-minutes` | Yönetim kurulu, müdürler kurulu, genel kurul veya komite tutanağı/karar taslağı hazırlar |
| `/corporate-legal:written-consent` | Yönetim kurulu, müdürler kurulu, genel kurul veya toplantısız karar taslağı hazırlar |
| `/corporate-legal:entity-compliance` | Tüzel kişi, sicil, karar defteri, temsil ve uyum takip tablosunu yönetir |
| `/corporate-legal:integration-management` | Kapanış sonrası entegrasyon, bildirim, sözleşme devri ve aksiyon planı üretir |
| `/corporate-legal:matter-workspace` | Çok müvekkilli/dosyalı çalışmada dosya bağlamını ayırır |

Komut adları orijinal yapıyla uyumluluk için İngilizce bırakılmıştır. İçerik ve output dili Türk hukuku ve uygulamasına göre çalışır.

## Modüller

| Modül | Kapsam |
|---|---|
| M&A / İşlem Yönetimi | Hisse/pay devri, malvarlığı devri, birleşme, bölünme, tür değiştirme, yatırım, ortak girişim, kapanış koşulları |
| Kurumsal Yönetim | Yönetim kurulu, müdürler kurulu, genel kurul, karar/tutanak taslağı, karar defteri ve imza süreci |
| Sermaye Piyasası | Halka açık şirketlerde SPK, Borsa İstanbul, KAP, MKK ve özel durum süreçleri |
| Entity Management | MERSİS, ticaret sicili, faaliyet belgesi, imza sirküleri, karar defterleri, VERBİS, vergi/SGK takipleri |

## Entegrasyonlar

Plugin yerel dosyalarla çalışabilir. Google Drive, SharePoint, Slack veya VDR/belge klasörü bağlantıları varsa belge arama ve izleme otomatikleşir; yoksa çıktı yerel dosya ve markdown/CSV olarak üretilir.

Türkiye uygulamasında aşağıdaki kaynaklar özellikle önemlidir:

- MERSİS ve ticaret sicili kayıtları
- Türkiye Ticaret Sicili Gazetesi kayıtları
- KAP ve MKK kayıtları
- KEP, e-imza ve noter kayıtları
- Şirket karar defterleri, pay defteri, genel kurul ve yönetim kurulu tutanakları
- VERBİS, KVKK envanteri ve veri işleme belgeleri
- Rekabet Kurumu, SPK, BDDK, BTK, EPDK gibi sektörel izin veya bildirim kaynakları

Bu kaynaklara doğrudan bağlı connector yoksa skill'ler kullanıcıdan belge, ekran çıktısı veya kayıt bilgisi ister ve doğrulanmamış alanları açıkça işaretler.

## Kapsam sınırı

- İmza, tescil, KAP bildirimi, Rekabet Kurumu başvurusu, ticaret sicili işlemi veya resmi dosyalama otomatik yapılmaz.
- Bir karar taslağının geçerliliği; TTK, esas sözleşme, iç yönerge, temsil yetkisi, toplantı/karar nisabı ve somut belgeye göre hukukçu tarafından kontrol edilir.
- Halka açık şirketlerde SPK/KAP yükümlülükleri güncel mevzuat ve özel olay bazında ayrıca doğrulanır.
- Vergi, muhasebe, damga vergisi, SGK veya sektör lisansı etkileri ilgili uzmanla teyit edilmeden kesin sonuç gibi sunulmaz.

## Kapsam ve Sürüm

Bu eklenti (`1.1.0-tr`), TTK organ kararları, M&A incelemesi (`due diligence`), kapanış kontrol listesi, MERSİS/ETDS/sermaye uyumu ve şirketler hukuku portföy yönetimi süreçlerini kapsar. Güncel eşikler için `references/currency-watch.md` dosyasına bakın.
