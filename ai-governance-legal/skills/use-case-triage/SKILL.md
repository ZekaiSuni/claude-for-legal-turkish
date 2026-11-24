---
name: use-case-triage
description: >
  Önerilen bir Yapay Zeka (AI) kullanım senaryosunu kurum politikasına, kırmızı
  çizgilere ve envantere göre inceler — Onaylı, Şartlı Onaylı veya Onaylanmadı
  olarak sınıflandırır. KVKK, 7545 s. Siber Güvenlik Kanunu, FSEK, TİHEK ve
  TTK risklerini saptayarak gerekli koşulları belirler.
argument-hint: "[kullanım senaryosunu açıklayın]"
---

# /use-case-triage (Yapay Zeka Kullanım Senaryosu Triyajı)

## Amaç

Bu skill, iş birimlerinden gelen "Şu amaçla X yapay zeka aracını kullanabilir miyiz?" veya "Verileri falanca LLM'e yükleyebilir miyiz?" sorularını; kurumun AI politikası, kırmızı çizgileri ve Türkiye mevzuatı (KVKK, 7545 s. Kanun, FSEK, TİHEK, TTK) ekseninde triyajlar.

Çıktı nihai hukuki mütalaa değil; sorumlu avukata/uyum birimine sunulmadan önceki **ilk risk değerlendirmesi ve zorunlu koşullar** taslağıdır.

## İş Akışı

1. `~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md` dosyasını oku. (`## Matter Workspaces` aktifse ilgili `matter.md` dosyasını yükle; yoksa veya `[PLACEHOLDER]` içeriyorsa `/ai-governance-legal:cold-start-interview` yönlendirmesi yap.)
2. `## Yapay Zekâ Kullanım Envanteri` (`### Kırmızı Çizgiler`, `### Yönetişim Katmanları`) ve `## AI Politika Taahhütleri` bölümlerini kontrol et; `## Kullanıcı Rolü` ile çıktı çerçevesini ayarla.
3. Senaryo belirsizse (hangi veri, hangi araç/sunucu konumu, etkilenen kişi, insan onayı var mı) netleştirici kısa sorular sor.
4. Envanter ve kırmızı çizgi kontrolü → Türkiye mevzuat katmanı kontrolü → `🔴 / 🟡 / 🟢` sınıflandırması yap.
5. Çıktı üstüne çalışma başlığı ve `Reviewer note` koy (`## Çıktılar`); gerekirse `/privacy-legal:use-case-triage`, `/ai-governance-legal:aia-generation` veya `/ai-governance-legal:vendor-ai-review` devri ekle.

## Türkiye Uyarlama Katmanı

1. **6698 s. KVKK Riskleri:**
   - **Veri Tipi:** Anonimleştirilmiş veri mi, genel kişisel veri mi, yoksa m. 6 kapsamındaki Özel Nitelikli Kişisel Veri (özellikle biyometrik/sağlık) mi?
   - **Yurt Dışına Veri Aktarımı (KVKK m. 9):** Bulut tabanlı (OpenAI, Anthropic vb.) modeller veriyi Türkiye dışına aktarır. Sunucu Türkiye içi/kurum içi (On-Prem) değilse, KVKK m. 9 aktarım şartları (yeterlilik kararı, standart sözleşme + Kuruma 5 iş günü bildirim `[doğrula]` veya arızi istisna) açıkça koşul olarak yazılır.
   - **Otomatik Karar Alma (KVKK m. 11/1-(g)):** Münhasıran otomatik sistemlerle analiz sonucu kişi aleyhine bir sonuç doğuyorsa ilgili kişinin itiraz hakkı, aydınlatma (m. 10) ve anlamlı insan denetimi gereklidir. *(Not: KVKK m. 22 Kurulun görevlerini düzenler; otomatik karara itiraz m. 11/1-(g)'dir.)*
2. **Ticari Sır (TTK m. 54–55) & Avukatlık Sırrı (Av.K. m. 36):**
   - Kaynak kodu, finansal tablolar, müvekkil dosyaları eğitimden çıkış (opt-out / Zero Data Retention) garantili kurumsal sözleşme olmadan kamuya açık/ücretsiz LLM'lere girilemez.
3. **7545 s. Siber Güvenlik Kanunu & Bilgi Güvenliği:**
   - Kritik altyapı bileşenleri, kurumsal API anahtarı/erişim güvenliği, tedarikçi zafiyet ve olay bildirimi (USOM uyumu `[doğrula]`) açısından bilgi güvenliği incelemesi gerekip gerekmediği işaretlenir.
4. **FSEK (Telif) & Reklam/Tüketici (6502):**
   - Üretilen içerik/kodda FSEK ihlali ve üçüncü taraf hak sahipliği uyarısı; tüketiciye dönük sentetik içeriklerde aldatıcı uygulama/ifşa kontrolü eklenir.
5. **Ayrımcılık Yasağı (6701 s. TİHEK & 4857 s. İş Kanunu m. 5):**
   - İşe alım, performans, kredi veya hizmete erişim skorlamasında yanlılık ve insan gözetimi kontrolü zorunludur.
6. **Sınır Ötesi AB AI Act (`eu_nexus` varsa):** Yasaklı/yüksek risk sinyali varsa `/ai-governance-legal:ai-inventory` ve `/ai-governance-legal:aia-generation` tetiklenir.

## Sınıflandırma Mantığı

### 🔴 ONAYLANMADI (`NOT APPROVED`)
- Kırmızı çizgiler (`### Kırmızı Çizgiler`) ile doğrudan çatışma.
- Kişisel veri, özel nitelikli veri, müvekkil sırrı veya kaynak kodunun eğitimden çıkış garantisi olmayan ücretsiz/public AI aracına girilmesi.
- Yasaklı biyometrik kategorizasyon / işyerinde duygu analizi (AB AI Act m. 5 / KVKK m. 6).
- Yüksek riskli veya hukuken kritik kararlarda insan denetimi ve itiraz mekanizması olmaksızın %100 otonom uygulama.

### 🟡 ŞARTLI ONAYLI (`CONDITIONAL`)
- Kurumsal anlaşmalı ve sıfır veri saklama/model eğitimi yasağı (opt-out) içeren LLM.
- Yalnızca anonimleştirilmiş veri ile kullanım.
- Çıktıda gerçek anlamlı insan denetimi (human-in-the-loop) ve KVKK aydınlatması/m. 9 güvencesi.

### 🟢 ONAYLI (`APPROVED`)
- Yalnızca kamuya açık verilerin onaylı/sıfır veri eğitimli araçlarla özetlenmesi veya çevirisi.
- Kurum envanterinde onaylı kabul edilmiş şirket içi izole uygulamalar.

## Çıktı Formatı

```markdown
[GİZLİ HUKUKİ ÇALIŞMA TASLAĞI - bkz. CLAUDE.md ## Çıktılar]

> **⚠️ Reviewer note**
> - **Kaynaklar:** [Profil envanteri / politika / kullanıcı senaryosu]
> - **Okuma kapsamı:** [Tam senaryo]
> - **Hukukçu kararı gerektirenler:** [varsa `[review]` satırları]
> - **Güncellik:** [KVKK m. 9 / 7545 s. K. ikincil düzenlemeleri `[doğrula]`]
> - **Güvenmeden önce:** [Hukuk / KVKK / CISO kontrol adımları]

# Yapay Zeka Kullanım Senaryosu Triyajı

**Senaryo:** [Kısa tanım] | **Araç:** [Adı / Sürümü] | **Katman:** [Standart / Yükseltilmiş / Yüksek]

## Sonuç: 🔴 Onaylanmadı | 🟡 Şartlı Onaylı | 🟢 Onaylı

[Gerekçe]

## Zorunlu Şartlar (Şartlı İse)
- **Veri ve KVKK Kısıtı:** [Anonimleştirme / m. 9 güvencesi / m. 10 aydınlatma]
- **Sözleşme ve Güvenlik Şartı:** [Kurumsal sürüm, Zero Data Retention, 7545/CISO onayı]
- **İnsan Denetimi:** [Son karar ve itiraz yolu]

## Risk Analizi ve Eskalasyon
- **KVKK / FSEK / TTK / TİHEK / 7545:** [Somut noktalar]
- **Devir (Handoff):** [`/ai-governance-legal:aia-generation` | `/privacy-legal:use-case-triage` | `/ai-governance-legal:vendor-ai-review`]
```

Non-lawyer kullanıcı ise onay adımına geçmeden önce sorumlu avukat incelemesi için 1 sayfalık kısa brifing sunar (`## Kullanıcı Rolü` kuralı).
