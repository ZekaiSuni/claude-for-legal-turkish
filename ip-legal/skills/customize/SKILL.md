---
name: customize
description: >
  Fikri mülkiyet (IP) uygulama profilinde tek bir bölümü baştan kurulum
  yapmadan günceller: risk/ihtar duruşu, onay matrisi ve eskalasyon kişileri,
  portföy kapsamı, marka izleme stratejisi, ön araştırma eşikleri, OSS lisans
  politikası veya matter workspace ayarları.
argument-hint: "[bölüm adı veya değiştirmek istediğiniz kural]"
---

# /customize

## Ne Zaman Çalışır

Kullanıcı `/ip-legal:customize` yazdığında çalışır; tüm `cold-start-interview` görüşmesini tekrar etmeden profildeki belirli bir kuralı, onay yetkilisini veya izleme ayarını güncellemek içindir.

## İş Akışı

1. **Profili oku:** `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` ve bir üst klasördeki `~/.claude/plugins/config/legal-turkish/company-profile.md` dosyalarını oku. Eklenti profili yoksa veya `[PLACEHOLDER]` içeriyorsa şu yanıtı ver:

   > Henüz kurulum yapılmamış görünüyor. Önce `/ip-legal:cold-start-interview` çalıştırın; `customize` mevcut bir profili güncellemek içindir.

2. **Düzenlenebilir haritayı göster:** Mevcut özetle birlikte bölümleri listele:

   - **Şirket / Profil Bilgileri (`## Şirket Profili` ve ortak `company-profile.md`)** — kurum adı, sektör, yetki alanları, çalışma ortamı *(uyarlanan eklentiler arasında paylaşılır)*.
   - **Kullanıcı Rolü (`## Kullanıcı Rolü`)** — avukat / marka-patent vekili / hukukçu olmayan kullanıcı ve sorumlu hukukçu.
   - **Fikri Mülkiyet Profili (`## Fikri Mülkiyet (IP) Uygulama Profili`)** — hak karması, tescil ülkeleri, FSEK m. 52/48-2 ve SMK m. 113–122 standart devir duruşu, açık kaynak (OSS) lisans politikası.
   - **Uygulama ve İhtar Duruşu (`## Uygulama ve İhtar Duruşu (Enforcement Posture)`)** — agresif / ölçülü / muhafazakâr duruş, otomatik eskalasyonlar, `### Onay Matrisi`.
   - **Marka Koruma ve İzleme (`## Marka Koruma ve İzleme`)** — izlenen markalar, TÜRKPATENT Resmî Marka Bülteni / TRABİS tarama sıklığı ve yenileme bildirim kanalı.
   - **Çıktılar ve İş Akışı (`## Çıktılar`, `## Matter Workspaces`, `## Entegrasyonlar`)** — Slack, Google Drive, `portfolio.yaml` ve matter izolasyon ayarları.

3. **Ne değiştirmek istediğini sor:** Eski değeri göster, yeni değeri al ve alt skill'lere (`cease-desist`, `takedown`, `oss-review`, `ip-clause-review`, `portfolio`) etkisini açıkla.
4. **Ortak şirket profili değişikliği:** Şirket adı, sektör veya yargı alanı değişirse `~/.claude/plugins/config/legal-turkish/company-profile.md` dosyasını da güncelle ve diğer eklentilere yansıyacağını belirt.
5. **Onay alıp yaz ve özetle.**

## Güvenlik Kuralları (Guardrails)

- **Hiçbir bölümü silme:** Kullanılmayacak alanı silmek yerine `[Yapılandırılmadı / Devre Dışı]` yap ve etkisini açıkla.
- **İç tutarsızlık kontrolü:** Örneğin marka izlemesi aktif yazılıp `Yenileme bildirim kanalı` boş bırakılırsa veya `copyleft yasak` iken GPL istisnası açık bırakılırsa çelişkiyi bildir.
- **Koruma katmanlarını zayıflatma:** Av.K. m. 36 gizlilik uyarısı, `[review]` bayrağı, kaynak köken etiketleri (`[TÜRKPATENT]`, `[WIPO]`, `[Mevzuat.gov.tr]`), `[doğrula]` / `[verify]` mevzuat uyarıları ve FSEK Ek m. 4 / 5651 m. 9 AYM iptal kapısı kaldırılamaz.
- **Tek seferde tek değişiklik:** Çoklu talepleri sırayla ve onay alarak uygula.
