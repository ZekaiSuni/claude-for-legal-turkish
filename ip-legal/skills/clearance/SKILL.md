---
name: clearance
description: >
  Marka ön araştırması (Clearance) ilk geçiş taraması — mutlak ve nispi ret
  nedenleri (6769 s. SMK m. 5 ve m. 6), Nice sınıfları ve karıştırılma ihtimali
  (iltibas) faktörleriyle risk işaret listesi üretir; nihai tescil mütalaası
  değildir ve asla "marka temiz / engel yok" sonucu vermez.
argument-hint: "[önerilen marka, mal/hizmet sınıfları ve hedef ülkeler]"
---

# /clearance

## ⚠️ BU BİR İLK GEÇİŞ ÖN TARAMASIDIR — MARKA TESCİL MÜTALAASI DEĞİLDİR

Bu skill **asla "marka temizdir / tescil edilir / engel yoktur" sonucuna varmaz**. Ürettiği çıktı; tescil başvurusu ve marka lansmanı öncesinde yetkili avukat veya TÜRKPATENT nezdinde sicile kayıtlı marka vekilinin profesyonel araştırma ile değerlendireceği ön risk ve kontrol listesidir.

## İş Akışı

1. `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` dosyasını (`## Şirket Profili`, `## Kullanıcı Rolü`, `## Entegrasyonlar`, `## Fikri Mülkiyet (IP) Uygulama Profili`, `## Uygulama ve İhtar Duruşu (Enforcement Posture)`, `## Çıktılar`, `## Öznel Hukuki Değerlendirmelerde Karar Duruşu`, `## Matter Workspaces`) oku. Kullanıcı `"provisional"` (geçici) derse profilsiz olarak Türkiye / ölçülü risk duruşuyla ön çalışma yapabilir ve boşlukları bayraklayabilirsin.
2. Eksik bilgileri topla (**Marka ibaresi**, logosu/şekli varsa tanımı, somut mal/hizmetler ve **Nice Sınıfları (1–45)**, hedef ülkeler [Türkiye / WIPO Madrid / EUIPO], planlanan lansman tarihi ve mevcut ticari kullanım olup olmadığı).
3. **Mutlak Ret Nedenleri Kontrolü (6769 s. SMK m. 5):**
   - Ayırt edicilik düzeyi (Fantasie/icadi → keyfî/arbitrary → çağrışımsal → tanımlayıcı m. 5/1-(c) → cins/çeşit/jenerik ad m. 5/1-(d) reddi).
   - **SMK m. 5/1-(ı) ve (i):** Dinî değerler ve semboller ile **kamu düzenine ve genel ahlaka aykırı** işaretler TÜRKPATENT tarafından **mutlak ret nedeni olarak re'sen reddedilir** `[doğrula]`.
   - Coğrafi yer adı/türlü aldatıcı nitelik (m. 5/1-(f)), devlet armaları/kültürel semboller (m. 5/1-(g)-(ğ)).
4. **Nispi Ret Nedenleri ve Benzer Marka Taraması (6769 s. SMK m. 6):**
   - **Bağlı veri tabanı uyarısı:** Bu eklentide TÜRKPATENT EPATS, WIPO Global Brand Database veya TMview'a canlı bağlı bir MCP yoktur. Kullanıcı sicil dışa aktarımını (`[kullanıcı sağladı]`) paylaştıysa doğrudan onu analiz et; paylaşmadıysa bilinen tescilleri uydurma — web araması (`[web search - verify]`) ya da tescilsiz durum için **"resmî sicil araması yapılmadı"** uyarısıyla ilerle (sessiz tamamlama yok!).
   - **SMK m. 6/1 İltibas (Karıştırılma İhtimali):** Aynı veya benzer mal/hizmet sınıflarında (Nice sınıfı + bağlantılı yan sınıflar, ör. 9 ile 42, 25 ile 35) **Yargıtay 11. Hukuk Dairesi ve TÜRKPATENT YİDK Marka İnceleme Kılavuzu** ölçütleriyle görsel, işitsel (fonetik) ve kavramsal benzerlik + ortalama tüketici algısı üzerinden bütüncül izlenim değerlendirmesi yapılır `[model bilgisi - doğrula]`.
   - **SMK m. 6/4–6/5 Tanınmış Markalar:** Farklı mal/hizmetlerde dahi haksız yarar, itibar zedelenmesi veya ayırt edicilik zayıflaması doğuran tanınmış markalar.
   - **SMK m. 6/6 Ticaret Unvanı, Kişi Adı, Telif & Tasarım:** Kullanıcının kendi veya üçüncü kişilerin ticaret unvanları (`MERSİS`), alan adları (`TRABİS .tr`), sosyal medya kullanıcı adları.
   - *(Yalnızca sınır ötesi ABD başvurusu varsa ilgili yargı alanı farklılığı ayrıca not edilir.)*

## Çıktı Formatı

```markdown
[GİZLİ ÇALIŞMA ÜRÜNÜ - bkz. CLAUDE.md ## Çıktılar ve ## Kullanıcı Rolü]

> **⚠️ Reviewer note**
> - **Kaynaklar:** [Kullanıcı sağladı / Web araması / Resmî sicil bağlı değil `[doğrula]`]
> - **Okuma kapsamı:** [Sunulan marka ve mal/hizmet listesi]
> - **Hukukçu kararı gerektirenler:** [`[review]` iltibas ve tanımlayıcılık noktaları]
> - **Güncellik:** [`references/currency-watch.md` kontrolü]
> - **İşlem öncesi:** TÜRKPATENT EPATS ve WIPO/TMview üzerinden tam profesyonel araştırma yapılmalıdır

# Marka Ön Araştırması (İlk Geçiş): [Önerilen Marka]

**Nice Sınıfları:** [örn. 9, 35, 42] | **Hedef Ülke:** [Türkiye / WIPO Madrid]
**İlk Geçiş Özeti:** [🔴 Yüksek Engel Sinyali | 🟡 Dikkat / Sınırda | 🟢 İlk Geçişte Açık Mutlak Engel Görünmedi — Ancak Profesyonel Araştırma Zorunlu]

## 1. Mutlak Ret Değerlendirmesi (SMK m. 5)
- Ayırt edicilik derecesi (Tanımlayıcı / Çağrışımsal / Keyfî) ve m. 5/1-(ı)-(i) kamu düzeni kontrolü.

## 2. Benzer Marka ve İltibas Faktörleri (SMK m. 6/1 & m. 6/5)
*(Her şüpheli iltibas satırı `## Öznel Hukuki Değerlendirmelerde Karar Duruşu` gereği `[review]` ile işaretlenir.)*
- Görsel / İşitsel / Kavramsal benzerlik ve ilişkili mal/hizmet bağlantısı.
- Tanınmış marka (SMK m. 6/5), ticaret unvanı (`MERSİS`), alan adı (`TRABİS`) sinyalleri.

## 3. Önerilen Sonraki Adımlar
1. TÜRKPATENT EPATS, WIPO Global Brand Database ve TMview'da birebir/benzer + yan sınıf profesyonel araştırması yaptırmak.
2. İlk marka başvurusunda mal/hizmet listesi ve sınıf stratejisini netleştirmek (vekil/avukat onayıyla).
3. Onay sonrası `/ip-legal:portfolio --add` ile kayda almak.
```

**Non-lawyer kapısı:** `## Kullanıcı Rolü` avukat veya kayıtlı marka vekili değilse lansman, tabela/ambalaj baskısı veya başvuru öncesi sorumlu avukat/marka vekili incelemesi için 1 sayfalık brifing ver. Analizi Sonraki Adımlar Karar Ağacı ile bitir.
