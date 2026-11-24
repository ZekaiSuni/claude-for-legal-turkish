---
name: customize
description: >
  Yapay zekâ yönetişimi uygulama profilinde tek bir bölümü baştan kurulum
  yapmadan günceller: risk duruşu, eskalasyon kişileri, kullanım senaryosu
  envanteri, tedarikçi AI pozisyonları, politika taahhütleri, YZED kurum stili
  veya matter workspace ayarları.
argument-hint: "[bölüm adı veya değiştirmek istediğiniz kural]"
---

# /customize

## Ne Zaman Çalışır

Kullanıcı tüm `/ai-governance-legal:cold-start-interview` akışını baştan çalıştırmadan mevcut `ai-governance-legal` profilinde belirli bir pozisyonu, eskalasyon kişisini, düzenleyici ayak izini veya entegrasyonu güncellemek istediğinde çalışır.

## İş Akışı

1. **Profili oku:** `~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md` ve bir üst klasördeki `~/.claude/plugins/config/legal-turkish/company-profile.md` dosyalarını oku. Eklenti profili yoksa veya `[PLACEHOLDER]` içeriyorsa önce `/ai-governance-legal:cold-start-interview` öner.
2. **Düzenlenebilir haritayı göster:** Mevcut özetle birlikte bölümleri listele:
   - **Şirket Profili (`## Şirket Profili` ve ortak `company-profile.md`)** — kurum adı, sektör, yargı alanları, çalışma ortamı (in-house / büro).
   - **Düzenleyici ayak izi** — KVKK, 7545 s. Siber Güvenlik Kanunu, FSEK, TİHEK, sektörel kurumlar (BDDK/SPK/BTK/TİTCK), AB AI Act bağı.
   - **Yapay Zeka Kullanım Envanteri (`## Yapay Zekâ Kullanım Envanteri`)** — Onaylı / Şartlı / Yasak kayıtları, `### Kırmızı Çizgiler` ve `### Yönetişim Katmanları`.
   - **AI Sistem Envanteri (`## AI Sistem Envanteri`)** — Sistem bazlı kayıtlar için `/ai-governance-legal:ai-inventory`.
   - **Tedarikçi AI Yönetişimi (`## Tedarikçi AI Yönetişimi`)** — Model eğitimi yasağı, KVKK m. 9 aktarım, FSEK tazminatı, olay bildirimi, tek kırmızı çizgi.
   - **AI Politika Taahhütleri (`## AI Politika Taahhütleri`)** — Yayındaki şirket AI politikası pozisyonları.
   - **Etki Değerlendirmesi Kurum Stili (`## Etki Değerlendirmesi (YZED / AIA) Kurum Stili`)** — Tetikleyiciler, başlık şablonu, onay makamı.
   - **Yönetişim ve Çıktı Ayarları (`## Yönetişim Ekibi ve Eskalasyon`, `## Çıktılar`, `## Entegrasyonlar`, `## Matter Workspaces`)**.
3. **Ne değişeceğini sor:** Eski değeri göster, yeni değeri al ve alt akışlara (triyaj, tedarikçi incelemesi, YZED, gap analizi) etkisini açıkla.
4. **Ortak şirket profili değişikliği:** Şirket adı, sektör, yargı alanı veya çalışma ortamı değişiyorsa `~/.claude/plugins/config/legal-turkish/company-profile.md` dosyasını da güncelle ve bunun diğer uyarlanmış eklentileri de etkileyeceğini belirt.
5. **Onay alıp yaz ve özetle.**

## Guardrails

- **Hiçbir bölümü silme:** Kullanılmayacak bir alanı silmek yerine `[Yapılandırılmadı / Devre Dışı]` olarak işaretle ve etkisini açıkla.
- **İç tutarsızlık kontrolü:** Örneğin "düzenleyici ayak izinde AB AI Act var" deyip `ai-systems.yaml` içinde tüm sistemleri muaf tutan çelişki varsa uyar.
- **Güvenlik kurallarını gevşetme:** `[review]` bayrakları, kaynak köken etiketleri ve `[doğrula]` / `[verify]` madde kontrolleri kaldırılamaz; talep gelirse riskini açıklayıp koru.
- **Tek seferde tek değişiklik:** Birden fazla değişiklik varsa sırayla ve onay alarak uygula.
