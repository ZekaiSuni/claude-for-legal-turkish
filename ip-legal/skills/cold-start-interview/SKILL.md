---
name: cold-start-interview
description: >
  Fikri ve Sınai Mülkiyet (IP) uygulama profilini öğrenmek ve
  `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` dosyasını yazmak
  için kurulum görüşmesini yürütür. Profil eksikse, `[PLACEHOLDER]` içeriyorsa,
  `--redo` ile yenilenecekse veya `--check-integrations` ile bağlantılar test
  edilecekse çalışır.
argument-hint: "[--redo | --check-integrations | --full]"
---

# /cold-start-interview

1. `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` dosyasını kontrol et — doluysa ve `--redo` yoksa üzerine yazmadan önce teyit al ya da `/ip-legal:customize` öner.
2. Önce ortak şirket profilini (`~/.claude/plugins/config/legal-turkish/company-profile.md`) kontrol et; varsa kurum sorularını tekrar sormadan onayla, yoksa ilk kurulumda onu da yaz.
3. Hızlı Kurulum (2 dk) veya Tam Kurulum (10–15 dk) yolunu sor.
4. Varsa çekirdek dokümanları (marka/portföy listesi, standart ihtarname taslağı, OSS politikası, standart IP sözleşme maddeleri) oku.
5. Eksik alanları sessizce doldurma; özetle, kullanıcıya açık noktaları göster ve `CLAUDE.md` dosyasını (`## Şirket Profili`, `## Kullanıcı Rolü`, `## Entegrasyonlar`, `## Fikri Mülkiyet (IP) Uygulama Profili`, `## Uygulama ve İhtar Duruşu (Enforcement Posture)`, `## Marka Koruma ve İzleme`, `## Çıktılar`, `## Öznel Hukuki Değerlendirmelerde Karar Duruşu`, `## Çekirdek Güvenlik Kuralları (Shared Guardrails)`, `## Matter Workspaces`) yaz.

## `--check-integrations`

Yalnızca `Slack`, `Google Drive`, IP yönetim sistemi veya doküman deposu bağlantılarının gerçekten çalışıp çalışmadığını test eder (`--redo` olmadan profili silmez):
- Bir okuma/arama aracı çağrısı gerçekten yanıt döndürürse `✓` yaz.
- Yapılandırılmış ama test edilemiyorsa `⚪ (tanımlı ancak doğrulanmadı)` yaz.
- Bağlı değilse `✗` yaz ve manuel fallback yöntemini (`portfolio.yaml`, metin yapıştırma) belirt. `.mcp.json` içinde görünmek tek başına `✓` değildir.

## Bekleme, Kurulum Kapsamı ve Soru Temposu

- **Duraklatma/Devam:** Mevcut profilde `<!-- SETUP PAUSED AT: ... -->` varsa kaldığı bölümden devam öner. Kullanıcı görüşme ortasında durursa `[PENDING]` işaretleriyle ilerlemeyi kaydet.
- **Proje kapsamı uyarısı:** Çalışma dizini kullanıcının ana dizini dışında bir proje klasörüyse dosya erişiminin o klasörle sınırlı olabileceğini bir kez hatırlat.
- **Taze profesyonel profil:** Kişisel sohbet geçmişinden izin almadan bilgi çekme; yalnızca kullanıcının verdiği yanıt ve dokümanları esas al.
- **Tempo:** Tek turda alt sorular dahil en fazla 2–3 cevaplanabilir soru sor; belge varsa yazdırmak yerine dosya/link iste.

## Giriş Seçimi (Hızlı mı, Tam mı?)

> **`ip-legal`, marka/patent portföyü, marka ön araştırması (SMK m. 5–6), FTO ve buluş taraması (SMK m. 82 vd.), tecavüz triyajı, noter/KEP ihtarnamesi, FSEK Ek m. 4 uyar-kaldır, sözleşme IP devri ve OSS lisans uyumu içindir.**
>
> - **Hızlı Kurulum (2 dk):** Rolünüzü (avukat / marka-patent vekili / hukukçu olmayan), çalışma ortamınızı (in-house / büro), temel hak karmasını ve varsayılan yetki alanlarını alır; diğer ayarları `[DEFAULT]` ile başlatır.
> - **Tam Kurulum (10–15 dk):** İhtar duruşunuzu (agresif/ölçülü/muhafazakâr), onay matrisinizi, OSS politikanızı, sözleşme FSEK m. 52/48-2 beklentilerinizi ve çekirdek belgelerinizi okuyarak kuruma özel profil çıkarır.
>
> Hızlı mı, Tam mı? *(Sonradan `/ip-legal:cold-start-interview --full` ile tamamlayabilirsiniz.)*

## Görüşme Bölümleri

### Bölüm 0: Kullanıcı Rolü ve Çalışma Ortamı
- **Rol (`## Kullanıcı Rolü`):** Avukat / Hukuk Profesyoneli | Kayıtlı Marka/Patent Vekili (yetki kapsamı 6769 s. SMK / TÜRKPATENT işlemleridir) | Avukat erişimli hukukçu olmayan kullanıcı | Avukat erişimi olmayan hukukçu olmayan kullanıcı.
- **Çalışma ortamı (`Practice setting`):** Kurum içi (In-house) / Tek veya küçük büro / Orta-büyük büro (çok müvekkilli izolasyon için `## Matter Workspaces` açılır) / Klinik veya diğer.

### Bölüm 1: Hak Karması, Yetki Alanları ve Portföy
- Ağırlıklı haklar: Marka, Patent/Faydalı Model, Tasarım, Telif (FSEK), Ticari Sır (TTK m. 54–56), Açık Kaynak (OSS).
- Tescil/uyum coğrafyası: Türkiye (TÜRKPATENT / TRABİS), WIPO (Madrid/Lahey/PCT), EPO, EUIPO.
- Güncel portföy listesi varsa hemen `/ip-legal:portfolio --audit` veya ilk `portfolio.yaml` kaydını oluşturmayı öner.

### Bölüm 2: Sözleşme IP Duruşu ve Açık Kaynak (OSS) Politikası
- Çalışan eser ve buluşlarında FSEK m. 18 ve SMK m. 113–122 prosedürü nasıl işletiliyor? Yüklenici/freelancer sözleşmelerinde FSEK m. 52 yazılı devir + FSEK m. 48/2 teslim anı devri standardı ne?
- OSS politikası: GPL/AGPL gibi güçlü copyleft lisanslar yasak mı, hukuk onayına mı tabi, yoksa yalnızca permissive (MIT/Apache-2.0/BSD) mi kabul ediliyor?

### Bölüm 3: Uygulama ve İhtar Duruşu (`## Uygulama ve İhtar Duruşu (Enforcement Posture)`)
- Varsayılan ihlal yaklaşımı: `aggressive | measured | conservative`.
- Otomatik eskalasyon tetikleyicileri: karşı tarafın müşteri/iş ortağı olması, hükümsüzlük (SMK m. 25–26, m. 138) veya menfi tespit (SMK m. 154) karşı dava riski, haksız rekabet (TTK m. 54–56).
- `### Onay Matrisi`: FSEK Ek m. 4 uyar-kaldır, yumuşak uyarı, noter/KEP ihtarnamesi, TÜRKPATENT itiraz/iptal, FSHHM dava ve ihtiyati tedbir onay mercileri.

### Bölüm 4: Marka İzleme, Yenileme Bildirimi ve Çekirdek Belgeler
- Aktif izlenen markalar, TÜRKPATENT Resmî Marka Bülteni ve TRABİS (`.tr`) izleme sıklığı.
- `**Yenileme bildirim kanalı (Renewal alerts):**` (`ip-renewal-watcher` çıktılarının nereye düşeceği).
- Çekirdek belgeler: standart C&D ihtarnamesi, OSS politikası, standart IP devri maddesi, marka kullanım kılavuzu.

## Kapanış

- Profil yazıldıktan sonra açık/atlanan alanları `[PENDING - kullanıcı atladı]` ile listele; sessiz boşluk bırakma.
- Hemen denenebilecek ilk 2–3 gerçek işi öner (`/ip-legal:portfolio --report`, `/ip-legal:ip-clause-review`, `/ip-legal:clearance`) ve `references/currency-watch.md` güncellik listesini hatırlat.
