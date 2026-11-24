---
name: customize
description: >
  Kurumsal uygulama profilinde (corporate-legal) tek bir bölümü baştan kurulum
  yapmadan günceller: risk duruşu, eskalasyon kişileri, aktif modüller (M&A /
  Kurumsal Yönetim / Sermaye Piyasası / Entity Management), önemlilik eşikleri,
  beyan listesi formatı, karar şablonları veya matter workspace ayarları.
argument-hint: "[bölüm adı veya değiştirmek istediğiniz kural]"
---

# /customize

## Ne Zaman Çalışır

Kullanıcı `/corporate-legal:customize` yazdığında çalışır; tüm `cold-start-interview` görüşmesini baştan almadan mevcut profildeki bir ayarı, modülü, eskalasyon kişisini veya önemlilik eşiğini güncellemek içindir.

## İş Akışı

1. **Profili oku:** `~/.claude/plugins/config/legal-turkish/corporate-legal/CLAUDE.md` ve bir üst klasördeki `~/.claude/plugins/config/legal-turkish/company-profile.md` dosyalarını oku. Eklenti profili yoksa veya `[PLACEHOLDER]` içeriyorsa şu yanıtı ver:

   > Henüz kurulum yapılmamış görünüyor. Önce `/corporate-legal:cold-start-interview` çalıştırın; `customize` mevcut bir profili güncellemek içindir.

2. **Düzenlenebilir haritayı göster:** Mevcut özetle birlikte bölümleri listele:

   - **Şirket / Profil Bilgileri (`## Şirket profili` ve ortak `company-profile.md`)** — kurum adı, sektör, yargı alanları, halka açık/kapalı durumu, çalışma ortamı *(uyarlanan eklentiler arasında paylaşılır)*.
   - **Aktif modüller (`## Aktif modüller`)** — M&A ve işlem yönetimi, Kurumsal yönetim, Sermaye piyasası / SPK, Entity management modüllerinin açık/kapalı durumu.
   - **Risk duruşu ve önemlilik eşikleri (`## M&A ve işlem yönetimi`)** — muhafazakâr / dengeli / ticari esnek yaklaşım; sözleşme bedeli, çalışan sayısı veya ciro eşikleri.
   - **Sorumlu kişiler ve eskalasyon (`## Kullanıcı rolü`)** — işlem ekibi, yönetim kurulu sekreteryası, MERSİS/sicil sorumlusu, eskalasyon zinciri.
   - **M&A modülü** — işlem eşiği (TL/döviz bedeli), güvenilen veri odası klasörü, toplu AI inceleme güven düzeyi (`Spot-check %X` vb.), işlem ekibi brifing sıklığı.
   - **Kurumsal yönetim modülü (`## Kurumsal yönetim`)** — TTK yönetim kurulu / genel kurul tutanak ve karar formatı, imza sirküleri tercihleri, komite yapısı.
   - **Sermaye piyasası modülü (`## Sermaye piyasası ve halka açık şirket`)** — KAP özel durum açıklamaları, SPK finansal raporlama takvimi, içsel bilgi uyumu.
   - **Entity management modülü (`## Entity management`)** — bağlı ortaklık/tüzel kişi tablosu, MERSİS/Ticaret Sicili takipleri, faaliyet belgesi ve genel kurul takvimi.
   - **İş akışı (`## Matter workspaces`, `## Çıktı kuralları`, `## Entegrasyonlar`)** — Google Drive, SharePoint, Slack ve VDR izleme sıklığı (haricî veri odası/sicil manuel fallback'leri dahil).

3. **Ne değiştirmek istediğini sor:** Eski değeri göster, yeni değeri al ve alt skill'lere etkisini açıkla.

   Örnek etki açıklamaları:
   - *Önemlilik eşiği 10 milyon TL → 25 milyon TL:* "`/corporate-legal:diligence-issue-extraction` ve `/corporate-legal:material-contract-schedule` bundan sonra 25 milyon TL altını eşik altı görür; mevcut kayıtlar değişmez."
   - *Sermaye piyasası modülünü açma:* "Bir sonraki SPK/KAP ilişkili görevde özel durum ve raporlama takvimi soruları devreye alınır."
   - *Toplu inceleme güveni "tüm satırları kontrol et" → "%10 örnekleme":* "`/corporate-legal:ai-tool-handoff` çıkarımların tamamını değil %10 örneklemini QA'den geçirir."

4. **Ortak şirket profili değişikliği:** Şirket adı, sektör, yargı alanı veya çalışma ortamı değişirse `~/.claude/plugins/config/legal-turkish/company-profile.md` dosyasını da güncelle ve bunun diğer uyarlanmış eklentilere yansıyacağını belirt.

5. **Onay alıp yaz ve özetle.**

## Güvenlik Kuralları (Guardrails)

- **Hiçbir bölümü silme:** Devre dışı bırakılmak istenen bölümü silmek yerine `[Yapılandırılmadı / Devre Dışı]` olarak işaretle ve etkisini açıkla.
- **İç tutarsızlık kontrolü:** Örneğin "Sermaye piyasası modülü kapalı" iken eskalasyon zincirinde "SPK uyum danışmanı" bırakılırsa çelişkiyi bildir.
- **Koruma katmanlarını zayıflatma:** `[review]`, kaynak köken etiketleri ve `[doğrula]` / `[verify]` mevzuat kontrolleri yapısaldır; kaldırılmak istenirse riski açıkla ve uyarıyı koru.
- **Tek seferde tek değişiklik:** Çoklu talepleri sırayla ve onay alarak işle.
