# Employment Legal Plugin - Legal Turkish

Bu klasör, iş hukuku ve insan kaynakları iş akışlarını Türk hukuku ve uygulamasına göre yürütür. Amaç yabancı employment şablonunu çevirmek değil; işe alım, iş sözleşmesi, ücret/çalışma süresi, izin, fesih, iç soruşturma, işyeri politikaları, SGK/İŞKUR/İSG ve zorunlu arabuluculuk akışlarını Türkiye pratiğinde yeniden kurmaktır.

Her çıktı hukukçu incelemesine tabi taslaktır. Skill'ler belge okur, risk kapılarını uygular, kontrol listesi ve taslak üretir; nihai karar, fesih, imza, resmi bildirim, arabuluculuk/dava stratejisi ve çalışanla paylaşılacak metin insan onayından geçer.

## Kimler İçin

| Rol | Ana iş akışları |
|---|---|
| İş hukuku avukatı / hukuk müşaviri | Fesih incelemesi, işçilik alacağı, politika, iç soruşturma, arabuluculuk hazırlığı |
| İnsan kaynakları | İşe alım kontrolü, izin takibi, disiplin süreci, çalışan talepleri |
| Yönetim / GC | Toplu işten çıkarma, üst düzey fesih, yüksek riskli uyuşmazlık ve regülatör konuları |

## İlk Kurulum

```text
/employment-legal:cold-start-interview
```

Kurulum; işyeri, çalışan grupları, SGK/İŞKUR/İSG kapsamı, sendika/TİS, ücret ve çalışma süresi, izin, fesih, iç soruşturma, KVKK ve eskalasyon kurallarını çıkarır. Yapılandırma şu kalıcı yola yazılır:

```text
~/.claude/plugins/config/legal-turkish/employment-legal/CLAUDE.md
```

## Skill'ler

| Skill | İşlev |
|---|---|
| `/employment-legal:cold-start-interview` | Türk iş hukuku practice profilini kurar |
| `/employment-legal:hiring-review` | İş teklifi, iş sözleşmesi, deneme süresi, SGK ve KVKK kontrolleri |
| `/employment-legal:termination-review` | Fesih, savunma, iş güvencesi, ihbar/kıdem, SGK çıkış kodu ve arabuluculuk kontrolü |
| `/employment-legal:wage-hour-qa` | Ücret, fazla çalışma, UBGT, hafta tatili, prim, bordro ve çalışma süresi soruları |
| `/employment-legal:worker-classification` | İşçi/bağımsız çalışan/alt işveren/geçici iş ilişkisi sınıflandırması |
| `/employment-legal:policy-drafting` | İşyeri politikası ve prosedür taslağı |
| `/employment-legal:handbook-updates` | Personel yönetmeliği ve politika değişikliği fark analizi |
| `/employment-legal:leave-tracker` | Yıllık izin, rapor, doğum, ücretsiz izin ve kritik tarihleri izler |
| `/employment-legal:log-leave` | İzin/rapor kaydı ekler |
| `/employment-legal:investigation-open` | İç soruşturma dosyası açar |
| `/employment-legal:investigation-add` | Soruşturma kaydına belge/görüşme/not ekler |
| `/employment-legal:investigation-query` | Soruşturma kaydı içinde kontrollü soru-cevap yapar |
| `/employment-legal:investigation-memo` | İç soruşturma değerlendirme notu üretir |
| `/employment-legal:investigation-summary` | Yönetim/İK/hukuk hedef kitlesine göre özet üretir |
| `/employment-legal:internal-investigation` | İç soruşturma ana playbook'u |
| `/employment-legal:international-expansion` | Türkiye'de veya Türkiye dışı çalışan istihdamında genişleme planı |
| `/employment-legal:expansion-kickoff` | Yeni ülke/şehir/çalışma modeli genişleme dosyası başlatır |
| `/employment-legal:expansion-update` | Genişleme tracker'ını günceller |
| `/employment-legal:customize` | Profilde tekil iş hukuku ayarı değiştirir |
| `/employment-legal:matter-workspace` | Çok dosyalı/müvekkilli iş hukuku matter ayrımını yönetir |

## Takip Ajanı

| Agent | İzlediği konu | Varsayılan ritim |
|---|---|---|
| `leave-tracker` | Açık izin/rapor dosyaları, dönüş tarihi, rapor/analık/ücretsiz izin, iş göremezlik ve kritik aksiyonlar | Haftalık kontrol |

## Kaynak Disiplini

İş hukuku rakamları ve süreleri değişebilir. Asgari ücret, kıdem tazminatı tavanı, SGK bildirimi, idari para cezaları, arabuluculuk ve İSG yükümlülükleri için güncel resmi kaynak kontrolü gerekir. Kaynak önceliği: Mevzuat.gov.tr, Resmi Gazete, Çalışma ve Sosyal Güvenlik Bakanlığı, SGK, İŞKUR, Arabuluculuk Daire Başkanlığı, Yargıtay/AYM/UYAP, Lexpera/Lextera/Kazancı ve kullanıcı belgeleri.
