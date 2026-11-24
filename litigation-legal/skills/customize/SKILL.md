---
name: customize
description: >
  Dava/uyuşmazlık uygulama profilinde (litigation-legal) tek bir bölümü baştan
  kurulum yapmadan günceller: pratik rolü, taraf konumu (davacı / davalı / karma),
  risk kalibrasyonu, uyuşmazlık haritası, kurum dili (dilekçe/ihtarname stili),
  eskalasyon kişileri, ciddiyet sözlüğü veya matter workspace ayarları.
argument-hint: "[bölüm adı veya değiştirmek istediğiniz kural]"
---

# /customize

## Ne Zaman Çalışır

Kullanıcı `/litigation-legal:customize` yazdığında çalışır; tüm `cold-start-interview` görüşmesini baştan yürütmeden risk kalibrasyonunu, kurum dilini, eskalasyon kişisini veya mahkeme/dış büro haritasını değiştirmek içindir.

## İş Akışı

1. **Profili oku:** `~/.claude/plugins/config/legal-turkish/litigation-legal/CLAUDE.md` ve bir üst klasördeki `~/.claude/plugins/config/legal-turkish/company-profile.md` dosyalarını oku. Eklenti profili yoksa veya `[PLACEHOLDER]` içeriyorsa şu yanıtı ver:

   > Henüz kurulum yapılmamış görünüyor. Önce `/litigation-legal:cold-start-interview` çalıştırın; `customize` mevcut bir profili güncellemek içindir.

2. **Düzenlenebilir haritayı göster:** Mevcut özetle birlikte değiştirilebilecek bölümleri listele:

   - **Şirket / Profil Bilgileri (`## Şirket profili` ve ortak `company-profile.md`)** — kurum adı, sektör, yargı alanları, çalışma ortamı *(uyarlanan eklentiler arasında paylaşılır)*.
   - **Pratik Rolü (`## Pratik Rolü`)** — kurum içi hukuk müşaviri / dış dava avukatı / tekil avukat / kamu veya klinik.
   - **Taraf Konumu (`## Taraf (Side)`)** — davacı / davalı / karma (ticari alacak, iş davaları, düzenleyici kurum yaptırımı savunması, seri tüketici/topluluk davası vb.).
   - **Risk Kalibrasyonu (`## 1. Risk Kalibrasyonu`)** — gelen ihtarname, müzekkere veya yeni davada yüksek/orta/düşük risk ölçütleri, sulh yetki merdiveni ve yönetim/denetim kurulu eskalasyon eşikleri.
   - **Uyuşmazlık Haritası (`## 2. Harita (Landscape)`)** — sık karşılaşılan karşı taraflar, yetkili/sık görülen mahkemeler (ATM, AHM, İş, Fikri ve Sınai Haklar, İdare), çalışılan dış hukuk büroları.
   - **Kurum Dili (`## 3. Kurum Dili (House style)`)** — dilekçe ve layiha stili, ihtarname şablonu, isticvap/tanık hazırlık çerçevesi, hukuki saklama (legal hold) ve dış büro raporlama formatı.
   - **Ciddiyet Sözlüğü (`## Severity vocabulary map`)** — iç analiz / yönetim / müvekkil çıktılarında önem derecesi etiket eşlemesi.
   - **Kişiler ve Eskalasyon (`## Bunu Kim Kullanıyor`)** — iç paydaşlar, dosya sorumluları, dava türüne göre dış bürolar ve onay zinciri.
   - **İş Akışı ve Entegrasyonlar (`## Matter workspaces`, `## Available integrations`, `## Çıktılar (Outputs)`)** — Google Drive, SharePoint, Slack ve UYAP/UETS/KEP manuel akış sıklığı.

3. **Ne değiştirmek istediğini sor:** Eski değeri göster, yeni değeri al ve alt komutlara etkisini açıkla.

   Örnek etki açıklamaları:
   - *Taraf konumunu karma → yalnızca davalı yapma:* "`/litigation-legal:matter-intake` davacı taraf sorularını atlar; `/litigation-legal:demand-draft` talep/cevap ihtarnamesini savunma perspektifinden kurgular."
   - *Yüksek risk eşiğinin sıkılaştırılması:* "Daha fazla ihtarname ve müzekkere otomatik olarak `/litigation-legal:matter-briefing` ve `/litigation-legal:oc-status` takibine yönlendirilir."
   - *Fikri mülkiyet davaları için yeni dış büro eklenmesi:* "`/litigation-legal:oc-status` haftalık taramalarında IP etiketli dosyalar için bu büroyu esas alır."

4. **Ortak şirket profili değişikliği:** Şirket adı, sektör, yargı alanı veya çalışma ortamı değişirse `~/.claude/plugins/config/legal-turkish/company-profile.md` dosyasını da güncelle ve bunun diğer eklentilere yansıyacağını bildir.

5. **Onay alıp yaz ve özetle.**

## Güvenlik Kuralları (Guardrails)

- **Hiçbir bölümü silme:** Kapsam dışına alınan bir dava türünü silmek yerine `[Şu an takip edilmiyor]` olarak işaretle ve intake yönlendirme etkisini açıkla.
- **İç tutarsızlık kontrolü:** Örneğin "yalnızca davacı tarafı" seçili olup tüm dış büro listesi "savunma odaklı" ise veya yüksek hacimli dava portföyünde `Matter workspaces` kapalıysa kullanıcıyı uyar.
- **Koruma katmanlarını zayıflatma:** `/litigation-legal:demand-draft` üzerindeki gizlilik ve arabuluculuk/uzlaşma beyanı kontrol kapısı, Av.K. m. 36 / gizlilik başlığı, kaynak köken etiketleri, `[review]` bayrakları, `[doğrula]` / `[verify]` atıf uyarıları ve "avukat incelemesi olmadan mahkemeye/icraya sunulmaz" kuralı kaldırılamaz.
- **Tek seferde tek değişiklik:** Çoklu talepleri sırayla ve onay alarak işle.
