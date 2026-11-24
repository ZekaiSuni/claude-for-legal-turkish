---
name: vendor-ai-review
description: >
  Tedarikçi sözleşmelerindeki Yapay Zeka (AI / Copilot) kullanım şartlarını,
  model eğitimi izinlerini, KVKK m. 9 yurt dışı aktarımını, 7545 s. Kanun
  olay/zafiyet bildirimini, FSEK hak sahipliğini ve TTK ticari sır risklerini
  inceler; kırmızı çizgileri ve redline önerilerini çıkarır.
argument-hint: "[sözleşme metnini yapıştırın veya dosya yolu verin]"
---

# /vendor-ai-review (Tedarikçi AI / Copilot Sözleşme İncelemesi)

## Amaç

SaaS ve yapay zekâ tedarikçilerinin kullanım koşullarında (ToS), veri işleme eklerinde (DPA) veya AI ek protokollerinde (AI Addendum) yer alan hükümleri kurum standartlarına göre incelemek. Temel soru: **"Müşteri (şirketimiz) verileriyle tedarikçinin veya üçüncü tarafların modelini eğitiyor muyuz; veri yurt dışına nasıl çıkıyor ve sorumluluk kimde?"**

## İş Akışı

1. `~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md` dosyasından `## Tedarikçi AI Yönetişimi` (`### AI Tedarikçilerinden İstenen Standartlar`, `### Tek Kırmızı Çizgi (Otomatik Ret)`), `## Kullanıcı Rolü` ve `## Yönetişim Ekibi ve Eskalasyon` bölümlerini oku. (`## Matter Workspaces` aktifse `matter.md` sapmalarını ekle.)
2. Sözleşmede **"Artificial Intelligence", "Machine Learning", "Model Training", "Input/Output", "Feedback", "Usage Data", "Telemetry", "Sub-processor"** ve **"Copilot"** hükümlerini tara.
3. Aşağıdaki Türkiye ve Kurum Standardı AI Kontrol Listesini uygula.
4. `### Tek Kırmızı Çizgi (Otomatik Ret)` veya esaslı sapmaları işaretle; somut redline taslaklarını yaz.
5. Kişisel veri aktarımı için `/privacy-legal:dpa-review` / KVKK birimine devri ve `## Yönetişim Ekibi ve Eskalasyon` yönlendirmesini ekle.

## Türkiye ve Kurum Odaklı AI Kontrol Listesi

### 1. Model Eğitimi ve Çıktı İyileştirme (`Data Use`)
- Sözleşme; Müşteri Verisi, prompt (girdi), çıktı veya analitik/telemetri verilerinin tedarikçi ya da alt işleyen temel modellerini (LLM/ML) eğitmek veya iyileştirmek için kullanılmasına izin veriyor mu?
- **Kurum Standardı:** Sıfır eğitim yetkisi (Zero Training / Zero Data Retention) veya varsayılan kapalı (Opt-in zorunlu) yapı; yalnızca "Opt-out" yetmezse yazılı sözleşme ekine dönüştür.

### 2. Girdi/Çıktı Hak Sahipliği ve FSEK (Telif)
- Prompt ve Output mülkiyeti kimde? Çıktılar üzerindeki FSEK m. 48–52 kapsamında devredilebilen mali haklar (işleme, çoğaltma, yayma, umuma iletim) müşteriye devrediliyor veya münhasır geniş kullanım hakkı sağlanıyor mu? Tedarikçi aynı/benzer çıktıyı başka müşterilere sunma veya saklama hakkı tutuyor mu?

### 3. KVKK m. 9 Yurt Dışına Aktarım ve Alt İşleyenler
- Veriler tedarikçinin kullandığı üçüncü taraf temel model API'lerine aktarılıyor mu?
- Alt-veri işleyen (Sub-processor) listesi şeffaf mı ve değişiklikte önceden bildirim + itiraz hakkı var mı?
- Sunucular Türkiye dışında (ABD/AB vb.) ise KVKK m. 9 kapsamında yeterlilik kararı veya Kurul onaylı Standart Sözleşme (+ 5 iş günü Kuruma bildirim `[doğrula]`) mekanizması kurulmuş mu? Özel nitelikli kişisel veri kısıtı mevcut mu?

### 4. Üçüncü Taraf FSEK / IP Tazminatı ve Sorumluluk
- AI aracının ürettiği kod/metin/görsel üçüncü bir kişinin FSEK/SMK hakkını ihlal ederse tedarikçi hukuki sorumluluk ve tazminat (`IP Indemnity`) üstleniyor mu, yoksa AI çıktılarını sorumluluk sınırlaması/garanti reddi (AS IS) dışında bırakıp riski müşteriye mi yıkıyor?

### 5. Siber Güvenlik, 7545 s. Kanun Olay Bildirimi ve Model Değişikliği
- Veri sızıntısı, prompt enjeksiyonu veya AI model zafiyetlerinde bildirim süresi (örn. 24–48/72 saat — 7545 s. Siber Güvenlik Kanunu / KVKK m. 12 ile uyumlu) yazılı mı?
- Tedarikçi alt modeli veya sürümü değiştirdiğinde müşteriye bildirim (örn. 30 gün önceden) yapıyor mu; denetim hakkı tanınıyor mu?

## Çıktı Formatı

```markdown
[GİZLİ HUKUKİ ÇALIŞMA TASLAĞI - bkz. CLAUDE.md ## Çıktılar]

> **⚠️ Reviewer note**
> - **Kaynaklar:** [Tedarikçi sözleşmesi / DPA / AI Eki + profil standartları]
> - **Okuma kapsamı:** [Okunan bölümler / sayfa aralığı]
> - **Hukukçu kararı gerektirenler:** [satır içi N adet `[review]`]
> - **Güncellik:** [KVKK m. 9 / 7545 s. Kanun ikincil kuralları `[doğrula]`]
> - **Güvenmeden önce:** [Sorumlu avukat ve bilgi güvenliği kontrolü]

# Tedarikçi AI Sözleşmesi İncelemesi: [Tedarikçi / Araç Adı]

## Genel Değerlendirme: 🔴 (Kritik Risk / Kırmızı Çizgi) | 🟡 (Şartlı / Redline Gerekli) | 🟢 (Kurum Standardına Uygun)

## En Büyük AI Riskleri
1. [Örn. Müşteri girdi/çıktılarıyla model eğitimi açık — KVKK ve TTK m. 54–55 ticari sır riski]
2. [Örn. Çıktı hakları ve FSEK tazminatı belirsiz]

## Madde Bazlı İnceleme ve Redline Önerileri

| Konu | Sözleşmedeki Durum | Profil Standardı | Durum |
|---|---|---|---|
| Model eğitimi | | | 🔴 / 🟡 / 🟢 |
| KVKK m. 9 & Alt İşleyen | | | |
| FSEK / Çıktı Mülkiyeti | | | |
| IP Tazminatı & Sorumluluk | | | |
| 7545 / İhlal Bildirimi & Model Değişikliği | | | |

### Önerilen Madde Revizyonları (Redline)
- **Mevcut Metin (Özet/Alıntı):** [...]
- **Risk (`[KVKK / FSEK / TTK / 7545]`):** [...]
- **Önerilen Türkçe/İngilizce Redline:**
  *"Tedarikçi; Müşteri Verilerini, Girdileri (Inputs) ve Çıktıları (Outputs) doğrudan veya dolaylı olarak herhangi bir yapay zekâ veya makine öğrenmesi modelini eğitmek, ince ayar yapmak (fine-tune) ya da başka müşterilere sunulacak sistemleri geliştirmek amacıyla kullanamaz ve üçüncü taraflara aktaramaz."*

## Devir ve Sonraki Adımlar
- KVKK / Yurt dışı aktarım doğrulaması: `/privacy-legal:dpa-review` veya KVKK sorumlusu onayı.
- İmza öncesi eskalasyon (`## Yönetişim Ekibi ve Eskalasyon`).
```

Non-lawyer kullanıcı ise sözleşme onayı/imzası öncesinde durup sorumlu avukata götürülecek 1 sayfalık kısa özet üretir. Analizi Sonraki Adımlar Karar Ağacı ile bitir.
