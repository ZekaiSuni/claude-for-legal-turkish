---
name: cold-start-interview
description: >
  Yapay zekâ yönetişimi kurulum görüşmesini yürütür — kurum AI politikası,
  referans etki değerlendirmesi (YZED/AIA) ve tedarikçi AI sözleşmelerinden
  öğrenerek `~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md`
  dosyasını yazar. Kurulum yapılmadığında veya `--redo` / `--check-integrations`
  istendiğinde çalışır.
argument-hint: "[--redo | --check-integrations | --full]"
---

# /cold-start-interview

1. `~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md` dosyasını kontrol et — doluysa ve `--redo` yoksa üzerine yazmadan önce teyit al veya `customize` öner.
2. Eski önbellek yolu `~/.claude/plugins/cache/legal-turkish/ai-governance-legal/*/CLAUDE.md` altında dolu profil olup hedef yolda yoksa, devam etmeden önce yeni config yoluna taşı ve kullanıcıyı bilgilendir.
3. Önce ortak şirket profilini (`~/.claude/plugins/config/legal-turkish/company-profile.md`) kontrol et; varsa şirket sorularını tekrar sormadan onayla, yoksa ilk kurulumda onu da yaz.
4. Hızlı Başlangıç (2 dk) veya Tam Kurulum (10–15 dk) yolunu sor.
5. Varsa çekirdek dokümanları (AI kullanım politikası, örnek YZED, tedarikçi AI eki, model envanteri) oku; kırmızı çizgileri, tedarikçi standartlarını ve onay zincirini çıkar.
6. Eksikleri sessiz geçmeden kullanıcıya göster, ardından `CLAUDE.md` profilini yaz ve ilk görevi öner.

## Bayraklar (`Flags`)

- `--redo` — Tüm görüşmeyi baştan yürütür ve profili günceller (`--redo <bölüm>` tek bölümü yeniler).
- `--full` — Hızlı kurulumdan tam kuruluma geçiş yapar.
- `--check-integrations` — `.mcp.json` içindeki `Slack` ve `Google Drive` bağlantılarını fiilen test eder. Sadece `.mcp.json` içinde tanımlı diye `✓` yazma; test edilemeyen konnektörü `⚪` ("tanımlı ama test edilmedi") olarak işaretle.

## Kurulum Öncesi Kontroller

- **Bekleme/Duraklatma Kontrolü:** Mevcut `CLAUDE.md` içinde `<!-- SETUP PAUSED AT: ... -->` varsa kaldığı bölümden devam etmeyi teklif et. Kullanıcı görüşme sırasında "dur/ara ver" derse ilerlemeyi `[PENDING]` işaretleriyle ve `<!-- SETUP PAUSED AT: [bölüm] -->` yorumuyla kaydet.
- **Proje Kapsamı Kontrolü:** Çalışma dizini kullanıcı ana dizini dışında bir proje klasörüyse (dosya erişimi proje diziniyle sınırlı kalabilir uyarısı için) bunu bir kez belirt.
- **Taze Profesyonel Profil:** Kişisel geçmişten izin almadan veri çekme; yalnızca kullanıcının verdiği yanıt ve dokümanları kullan.
- **Soru Temposu:** Tek seferde alt soruları da sayarak en fazla 2–3 cevaplanabilir soru sor; uzun metin yerine önce doküman/link yapıştırmayı teklif et. Kullanıcının belirttiği kanun/tarih/eşik yanlışsa (ör. KVKK m. 11/1-(g) yerine m. 22 denmesi gibi) kaydetmeden önce nazikçe işaretle (`[beyan işaretlendi — doğrula]`).

## Giriş Seçimi (Hızlı mı, Tam mı?)

> **`ai-governance-legal`, yapay zekâ kullanım senaryosu triyajı, etki değerlendirmesi (YZED), tedarikçi AI sözleşmesi incelemesi ve politika sapma takibi içindir.**
>
> - **Hızlı Kurulum (2 dakika):** Rolünüzü, çalışma ortamınızı, aktif mevzuat kapsamınızı (Türkiye: KVKK, 7545, FSEK, TİHEK + varsa AB AI Act) ve temel kırmızı çizgileri alır; diğer pozisyonları `[DEFAULT]` ile başlatır.
> - **Tam Kurulum (10–15 dakika):** AI kullanım envanterinizi, kırmızı çizgilerinizi, tedarikçi AI kırmızı çizgilerinizi, eskalasyon matrisinizi ve mevcut politika/YZED dokümanlarınızı okuyarak kuruma özel profil çıkarır.
>
> Hızlı mı, Tam mı? *(Sonradan `/ai-governance-legal:cold-start-interview --full` ile yükseltebilirsiniz.)*

## Görüşme Bölümleri

### Bölüm 0: Kullanıcı Rolü, Çalışma Ortamı ve Entegrasyonlar

1. **Günlük kullanıcı kim (`## Kullanıcı Rolü`):**
   - **Avukat / hukuk müşaviri:** Dahili `GİZLİ HUKUKİ ÇALIŞMA TASLAĞI` başlığı kullanılır.
   - **Avukat erişimli non-lawyer** (İK, ürün, satın alma, uyum) veya **Avukat erişimi olmayan non-lawyer:** Çıktılar `"ARAŞTIRMA VE DEĞERLENDİRME NOTU"` çerçevesinde verilir; kullanım onayı, sözleşme imzası ve YZED teyidi öncesinde avukat kontrolü + 1 sayfalık brifing sunulur (avukat erişimi yoksa ilgili Baro danışma/rehber kanalları hatırlatılır).
2. **Çalışma ortamı (`Practice setting`):** Kurum içi (In-house) / Tek veya küçük büro (onay zinciri yerine "ne zaman meslektaşa veya dış uzmana danışılır?" sorulur) / Orta-büyük büro (Matter workspaces açılır) / Kamu veya hukuk kliniği.
3. **Bağlı araçlar (`## Entegrasyonlar`):** `Slack`, `Google Drive` test edilir; bulunmayanlar için manuel metin yapıştırma/yerel dosya fallback'i kaydedilir.

### Bölüm 1: Geliştirici (Provider), Kullanıcı (Deployer) veya Her İkisi?

- Şirket ne yapıyor, kime hizmet veriyor? (Mümkünse kurumsal sayfa/link iste.)
- AI rolü her sistem için ayrı belirlenir (`## AI Sistem Envanteri`); istenirse şimdi 1–3 sistem `/ai-governance-legal:ai-inventory add` ile kaydedilir veya sonraya bırakılır.
- **Gölge AI (Shadow AI) Taraması:** Onaylı araçlar dışında çalışanların kullandığı gömülü AI özellikleri (Slack AI, Copilot, CRM puanlama vb.) veya kurumsal onaylı olmayan ücretsiz LLM kullanımları sorulur ve `[BELGELENMEMİŞ - TRİYAJ GEREKLİ]` olarak envantere işlenir.

### Bölüm 2: Düzenleyici Ayak İzi

- **Türkiye birincil mevzuatı:** 6698 s. KVKK (m. 6, m. 9, m. 11/1-(g)), 7545 s. Siber Güvenlik Kanunu / USOM kritik altyapı veya zafiyet kapsamı, 5846 FSEK, 6701 TİHEK / 4857 İş Kanunu, 6502 TKHK / Reklam Kurulu.
- **Sektörel düzenlemeler:** BDDK/TCMB, SPK, BTK, TİTCK/Sağlık Bakanlığı, EPDK, Rekabet Kurumu.
- **Sınır ötesi:** AB/AEA'ya ürün/hizmet sunumu veya AB bireylerini etkileyen çıktı varsa **AB AI Act ((AB) 2024/1689)** ve GDPR; kurumsal B2B sözleşme talepleri.
- Açık bir Kurul/kurum incelemesi veya gönüllü AI ilkesi taahhüdü var mı?

### Bölüm 3: Kullanım Envanteri ve Kırmızı Çizgiler

Mevcut AI envanteri/politikası yoksa kısa senaryolarla sözlü pozisyon çıkar:
- *Kullanıcı senaryoları:* İK CV ön elemesi, performans özeti, müşteri destek yanıt taslağı, finans harcama anomali tespiti, hukuk ekibinin NDA ilk taslağı.
- *Ürün/geliştirici senaryoları:* Kullanıcı davranışına göre kişiselleştirme, otomatik kredi/risk/lead skorlama, insan onaysız otomatik kararlar.
- **Otomatik Ret (`### Kırmızı Çizgiler`):** Örn. ücretsiz LLM'e kaynak kod/müvekkil/özel nitelikli veri yükleme, tam otonom ret kararı, biyometrik duygu analizi.
- **Yönetişim katmanları:** Standart / Yükseltilmiş / Yüksek onay yolları.

### Bölüm 4: Yönetişim Ekibi ve Eskalasyon

- AI yönetişimi hangi birimde (Hukuk, KVKK, CISO, ortak komite)?
- Tedarikçi AI sözleşme sahibi ve AI risk sorumlusu kim?
- Standart / Yükseltilmiş / Yüksek / Olay-ihlal / Kurum incelemesi durumlarında eskalasyon kime gider?

### Bölüm 5: Çekirdek Dokümanlar (Seed Documents)

Varsa alınır (yoksa "belgesiz başlangıç" ile devam edilip beyana dayalı alanlar açıkça işaretlenir):
1. AI / Kabul Edilebilir Kullanım Politikası → `## AI Politika Taahhütleri` doldurulur.
2. Örnek YZED / AI Risk Değerlendirmesi → `## Etki Değerlendirmesi (YZED / AIA) Kurum Stili` şablonu çıkarılır.
3. Ana Tedarikçi AI Sözleşmesi / Eki → `## Tedarikçi AI Yönetişimi` pozisyonları hizalanır.
4. Sistem envanteri / izinli-yasaklı araç listesi.

### Bölüm 6: Çıktılar ve Politika Konumu

- Tamamlanan YZED/triyaj/tedarikçi raporlarının kaydedileceği klasör (`policy-monitor` taraması için).
- Güncel AI politika belgesinin yolu.
- Dosya adlandırma kuralı (`YZED_Sistem_YYYY-AA-GG` vb.).

## Profilin Yazılması ve Kapanış

- Profili `~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md` dosyasının tam başlık yapısına (`## Şirket Profili`, `## Kullanıcı Rolü`, `## Entegrasyonlar`, `## Yapay Zekâ Kullanım Envanteri`, `## AI Sistem Envanteri`, `## Etki Değerlendirmesi (YZED / AIA) Kurum Stili`, `## Tedarikçi AI Yönetişimi`, `## AI Politika Taahhütleri`, `## Yönetişim Ekibi ve Eskalasyon`, `## Çekirdek Dokümanlar (Seed Documents)`, `## Çıktılar`, `## Matter Workspaces`) göre yaz.
- Atlanan alanlara `[PENDING - kullanıcı atladı]` koy; sessiz boşluk bırakma.
- Kapanışta: (1) yakalanan kırmızı çizgileri teyit et, (2) eksik doküman risklerini açıkça söyle (ör. envanter veya AI sözleşme eki yokluğu), (3) `privacy-legal` bağlantısını ve ilk denenebilecek gerçek görevleri (`/ai-governance-legal:use-case-triage`, `/ai-governance-legal:vendor-ai-review`) öner, (4) `references/currency-watch.md` güncellik uyarısını hatırlat.
