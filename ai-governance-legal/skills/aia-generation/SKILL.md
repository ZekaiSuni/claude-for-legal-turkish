---
name: aia-generation
description: >
  Yapay Zekâ Etki Değerlendirmesi (YZED / AIA) oluşturur: yapılandırılmış bilgi
  toplama, Türkiye mevzuatı (KVKK, 7545, FSEK, TKHK, TİHEK, sektörel kurallar)
  ve sınır ötesi AB AI Act sınıflandırması, kurum AI politikası gap analizi ve
  koşullu öneri sunar. "impact assessment", "YZED", "AIA üret", "AI risk analizi"
  taleplerinde veya şartlı triyaj sonrasında kullanılır.
argument-hint: "[kullanım senaryosunu veya sistemi tanımlayın ya da triyaj sonucunu verin]"
---

# /aia-generation

## İlk İş Akışı

1. `~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md` dosyasını oku (`## Şirket Profili`, `## Kullanıcı Rolü`, `## Etki Değerlendirmesi (YZED / AIA) Kurum Stili`, `## AI Politika Taahhütleri`, `## Çıktılar`). Eksik/placeholder varsa önce `/ai-governance-legal:cold-start-interview` iste.
2. `## Yapay Zekâ Kullanım Envanteri` ve `### Yönetişim Katmanları` üzerinden risk kulvarını (Hızlı Tarama / Tam Değerlendirme) belirle.
3. Sohbet içinde (form doldurtmadan) teknik ve operasyonel olguları topla.
4. Kurumun düzenleyici ayak izine göre mevzuat sınıflandırmasını yap (Türkiye birincil + `eu_nexus` varsa AB AI Act).
5. `## Etki Değerlendirmesi (YZED / AIA) Kurum Stili` formatında (yoksa aşağıdaki varsayılan şablonda) değerlendirmeyi yaz.
6. `## AI Politika Taahhütleri` ile karşılaştır ve KVKK / tedarikçi sözleşmesi devirlerini (`handoff`) işaretle.

## Matter Bağlamı

`## Matter Workspaces` altında `Enabled` kapalıysa (şirket içi kullanımda varsayılan) practice-level bağlamda çalış. Açıksa aktif matter'ın `matter.md` dosyasını yükle ve çıktıyı `~/.claude/plugins/config/legal-turkish/ai-governance-legal/matters/<slug>/` klasörüne yaz; `Cross-matter context` kapalıyken başka matter dosyalarını okuma.

## Amaç ve KVKK PIA / VERBİS Ayrımı

YZED (AIA), yalnızca kişisel veri hukukunu inceleyen KVKK Veri Koruma Etki Değerlendirmesi / PIA yerine geçmez; sistemin tasarımını, doğruluğunu, yanlılık (bias) riskini, insan gözetimini, siber güvenliğini ve telif/tüketici etkilerini ölçer. Kişisel veri işleniyorsa `/privacy-legal:pia-generation` akışıyla paralel yürütülür.

## Adım 0: Etki Değerlendirmesi Gerekli mi?

`## Etki Değerlendirmesi (YZED / AIA) Kurum Stili` tetikleyicilerini ve şu kriterleri kontrol et:
- Bireyler hakkında karar veriyor veya kararı esaslı şekilde etkiliyor mu (işe alım, terfi, kredi, fiyatlama, hizmete erişim, içerik moderasyonu)?
- Kişisel veri (özellikle KVKK m. 6 özel nitelikli veri veya m. 9 yurt dışı aktarım) işliyor mu?
- Müşteriye/tüketiciye dönük bir AI özelliği mi?
- Üçüncü taraf model mi kullanıyor veya risk katmanı Yükseltilmiş / Yüksek mi?

Hiçbiri geçerli değilse gereksiz bürokrasi yaratma; dosyaya konulmak üzere tek paragraflık "neden tam YZED gerekmedi" kayıt notu yaz.

## Adım 1: Risk Kulvarı ve Doğrulama Hijyeni

Şüphe varsa Tam Değerlendirme çalıştır. Tüm atıflarda `## Çekirdek Güvenlik Kuralları (Shared Guardrails)` kaynağa göre etiketleme sistemini uygula:
- **`[yerleşik]`:** Değişmesi düşük olasılıklı temel normlar (ör. KVKK m. 11/1-(g) — münhasıran otomatik sistemlerle analiz sonucu aleyhe sonuca itiraz hakkı; not: KVKK m. 22 Kurulun görevlerini düzenler; AB bağlamında ise GDPR m. 22 ve (AB) 2024/1689 AI Act geçerlidir).
- **`[doğrula]`:** İkincil yönetmelikler, KVKK Kurul ilke kararları, Reklam Kurulu/TİHEK kararları, 7545 s. Siber Güvenlik Kanunu ikincil düzenlemeleri, AB AI Act uygulama tasarrufları ve yürürlük tarihleri.
- **`[kesin-madde-doğrula]` (`[verify-pinpoint]`):** Spesifik bent, fıkra, Ek (Annex) numaraları mutlaka birincil kaynaktan (`mevzuat.gov.tr`, `resmigazete.gov.tr`, `kvkk.gov.tr`, `EUR-Lex`) teyit edilmelidir.

**Non-lawyer kullanıcı kuralı:** `## Kullanıcı Rolü` non-lawyer ise, tarih/tutar/yürürlük belirsizliklerini satır içinde kesinmiş gibi yazma; `"yürürlük/eşik: avukatla teyit edilmeli"` yazıp hepsini raporun en sonunda **"Emin Olmadığım Noktalar — Onay Öncesinde Avukatınıza Sorun"** bölümünde topla.

**Sessiz tamamlama yok:** Mevzuat/kurum bilgisinde boşluk varsa (a) durup kullanıcıdan metni iste, veya (b) açıkça `[web araması — doğrula]` / `[model bilgisi — doğrula]` etiketiyle ilerle.

## Adım 2: Olgusal Bilgi Toplama

1. **Sistem:** Gerçekte ne yapıyor, hangi model/tedarikçi, yardımcı (assistive) / yarı-otomatik / tam otomatik mi, çıktısı ne?
2. **Etkilenenler:** Çalışanlar, adaylar, tüketiciler, hastalar, çocuklar, finansal tüketiciler? Hata olursa en gerçekçi zarar nedir?
3. **Veri girdileri:** Hangi veri kategorileri, özel nitelikli veri, şirket verisiyle model eğitimi var mı, veri Türkiye dışına çıkıyor mu (KVKK m. 9)?
4. **Karar alma ve insan gözetimi:** İnsan incelemesi gerçekçi mi yoksa kağıt üstü onay ("rubber-stamping") riski mi var? Etkilenen kişi için itiraz yolu (KVKK m. 11/1-(g)) var mı?
5. **Doğruluk, yanlılık ve siber güvenlik:** Bilinen hata oranı, yanlılık (TİHEK / 4857 m. 5) testi yapıldı mı? 7545 s. Kanun kapsamında zafiyet/olay günlüğü ve kritik altyapı teması var mı?
6. **Aşama ve ölçek:** Tasarım / pilot / canlı / yaygın ölçek.

## Adım 3: Düzenleyici Sınıflandırma

**Ayak izi güncelliği kontrolü:** Senaryo, `## Şirket Profili` altındaki `**Düzenleyici ayak izi:**` dışında yeni bir etkilenen grup (ör. çocuklar, çalışanlar, AB vatandaşları) veya yeni bir karar türü (kredi skorlama, işe alım, tıbbi teşhis, kritik altyapı) ekliyorsa eski listeyi körü körüne uygulama; yeni kapsama giren Türkiye ve sınır ötesi rejimleri baştan türet ve profilin güncellenmesini öner.

**Kontrol edilecek ana rejimler:**
- **6698 s. KVKK:** Aydınlatma (m. 10), hukuki sebep (m. 5–6), yurt dışı aktarım & 5 iş günü standart sözleşme bildirimi (m. 9), otomatik karara itiraz (m. 11/1-(g)), veri güvenliği (m. 12).
- **7545 s. Siber Güvenlik Kanunu / USOM:** Kritik altyapı AI kullanımı veya siber olay bildirimi kapsamı.
- **6701 s. TİHEK & 4857 s. İş Kanunu m. 5:** İstihdamda ve mal/hizmet erişiminde ayrımcılık yasağı.
- **5846 s. FSEK & 6769 s. SMK:** Eğitim verisi izinleri ve sentetik çıktılarda telif/marka ihlali.
- **6502 s. TKHK & Ticari Reklam Yönetmeliği:** Tüketiciye yapay zekâ/chatbot şeffaflığı ve aldatıcı arayüz (dark pattern) yasağı.
- **Sınır Ötesi AB AI Act ((AB) 2024/1689):** Yalnızca AB bağı varsa risk katmanı + Geliştirici vs. Kullanıcı ayrımı. Eğer şirket hem geliştirici hem kullanıcıysa (`AI rolü: Her İkisi`), Bölüm 6'da mutlaka `| Yükümlülük | Geliştirici (Provider) Olarak | Kullanıcı (Deployer) Olarak |` ayrım tablosu kur. Ayrıca AB AI Act m. 27 Temel Haklar Etki Değerlendirmesi (**FRIA**) gerekiyorsa (kamu hizmeti sunan özel kuruluşlar, bireysel kredi/hayat-sağlık sigortası skorlaması vb.) bunun bu YZED'den **ayrı** bir belge olduğunu işaretle `[doğrula]`.

## Adım 4: Varsayılan YZED / AIA Şablonu

*(Profilde `## Etki Değerlendirmesi (YZED / AIA) Kurum Stili` şablonu tanımlıysa önce onu kullan.)*

```markdown
[GİZLİ HUKUKİ ÇALIŞMA TASLAĞI - bkz. CLAUDE.md ## Çıktılar]

> **⚠️ Reviewer note**
> - **Kaynaklar:** [Resmî Gazete / Mevzuat.gov.tr / KVKK / EUR-Lex / kullanıcı sağladı | model bilgisi kullanıldı — doğrulayın]
> - **Okuma kapsamı:** [okunan belgeler]
> - **Hukukçu kararı gerektirenler:** [satır içi N adet `[review]`]
> - **Güncellik:** [`references/currency-watch.md` kontrolü]
> - **Güvenmeden önce:** [avukatın kontrol etmesi gerekenler]

# Yapay Zekâ Etki Değerlendirmesi (YZED / AIA): [Sistem / Özellik Adı]

**Hazırlayan:** [Ad] | **Tarih:** [YYYY-AA-GG] | **Durum:** TASLAK / ONAYLANDI
**Sistem Sahibi:** [Ad] | **Hukuk İnceleyicisi:** [Ad]
**Yönetişim Katmanı:** [Standart / Yükseltilmiş / Yüksek] | **Kulvar:** [Hızlı Tarama / Tam Değerlendirme]

## Yönetici Özeti
[2 cümle: sistem ne yapar, hangi koşullarla canlıya çıkabilir.]
**Genel Risk:** 🟢 Düşük / 🟡 Orta / 🟠 Yüksek / 🔴 Çok Yüksek

## 1. Sistem Tanımı
**İşlev / Model-Tedarikçi / Otomasyon Modu (Yardımcı/Yarı-otomatik/Otonom) / Çıktı Türü / Aşama**

## 2. Etkilenen Kişiler ve Ölçek
**Muhatap grup / Aylık etkilenecek kişi sayısı / Hata halinde en somut zarar / Kırılgan gruplar**

## 3. Veri Girdileri ve KVKK m. 9
**Veri kategorileri / Özel nitelikli veri / Yurt dışına çıkış / Model eğitimi durumu**

## 4. Karar Alma ve İnsan Gözetimi
**Döngüde insan var mı / Müdahale mekanizması / İtiraz yolu (KVKK m. 11/1-(g)) / Sorumlu sahip**

## 5. Doğruluk, Yanlılık ve Siber Güvenlik
**Hata oranı / Yanlılık ve ayrımcılık testi (TİHEK/4857) / Hata günlüğü ve 7545 s. K. zafiyet uyumu**

## 6. Düzenleyici Sınıflandırma (Türkiye + Varsa Sınır Ötesi)
[Her yürürlükteki rejim için ayrı alt başlık: Katman/Madde, Yasaklı uygulama teması, Yükümlülükler, Ayrı FRIA/DPIA gerekip gerekmediği, Geliştirici/Kullanıcı tablosu]

## 7. AI Politika Uyumu
| Politika Taahhüdü (`## AI Politika Taahhütleri`) | Uyumlu mu? | Not |
|---|---|---|

## 8. Tasarıma Özgü Riskler ve Azaltımlar
*(Genel "AI halüsinasyonu" yazma; "Destek ekibi LLM cevabını kaynak kontrolü olmadan müşteriye gönderirse ayıplı bilgilendirme doğar" gibi somut yaz. 2–5 gerçek risk hedeflenir.)*

| # | Somut Risk | Olasılık | Etki | Azaltım Kontrolü | Durum | Sahip |
|---|---|---|---|---|---|---|

## 9. Öneri ve Koşullar
**[ONAYLI | KOŞULLU ONAYLI | DEĞİŞİKLİK GEREKLİ | ONAYLANMADI]**
- [ ] [Canlıya geçiş öncesi aksiyon — sahip, tarih]
**KVKK Etki Değerlendirmesi / PIA gerekli mi?** [Evet -> `/privacy-legal:pia-generation` | Hayır]

## Madde Doğrulama Uyarısı (Cite Check)
Mevzuat ve ek atıfları onay öncesi `mevzuat.gov.tr`, `resmigazete.gov.tr`, `kvkk.gov.tr` ve ilgiliyse `EUR-Lex` üzerinden doğrulanmalıdır.
```

**Onay Kapısı (`Durum: ONAYLANDI` öncesi):** `## Kullanıcı Rolü` non-lawyer ise sorumlu avukat incelemesi olmadan onay işaretine geçme; tek sayfalık avukat brifingi üret ve baro/avukat onayı iste.

## Devirler ve Kapanış

- KVKK varsa → `/privacy-legal:pia-generation`
- Tedarikçi ek sözleşmesi yoksa → `/ai-governance-legal:vendor-ai-review`
- Yeni mevzuat yükümlülüğü çıktıysa → `/ai-governance-legal:reg-gap-analysis`
- Analizi `## Çıktılar` altındaki Sonraki Adımlar Karar Ağacı ile bitir.
- **Bu skill canlıya onay vermez, uyumluluk beyanı/sertifikasyon veya resmî AB uygunluk değerlendirmesi yerine geçmez.**
