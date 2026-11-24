---
name: takedown
description: >
  Türkiye'de 5846 s. FSEK Ek Madde 4 uyarınca Uyar-Kaldır bildirimi hazırlar
  (--send), gelen bildirimi inceler (--respond) ya da yalnızca ABD hukukuna
  tabi uluslararası platformlarda geçerli DMCA §512 karşı bildirimi (--counter)
  düzenler. FSEK m. 30–40 dar istisnalarını, TCK m. 267 (İftira) / TTK m. 54–55
  sorumluluğunu ve 5651 s. K. m. 9 AYM iptal uyarısını (E.2020/76, K.2023/172)
  uygular.
argument-hint: "<--send | --respond | --counter> [bağlam veya gelen bildirim metni/yolu]"
---

# /takedown (Uyar-Kaldır Bildirimi ve Savunması)

## ⚠️ YARGI ALANI AYRIMI VE `5651 s. K. m. 9` AYM İPTAL UYARISI

Bu alanda Türkiye hukuku ile yabancı platform (ABD DMCA) mekanizmalarını birbirine karıştırmak ağır hak kaybına ve ceza/tazminat sorumluluğuna yol açar:

1. **Türkiye Telif Uyar-Kaldır Sistemi (`5846 s. FSEK Ek Madde 4`):** Telif haklarının internette ihlali halinde önce **içerik/yer sağlayıcıya başvurularak 3 gün içinde ihlalin durdurulması (yayından kaldırılması)** istenir; ihlale devam edilirse **Cumhuriyet Savcılığı'na** başvurularak 3 gün içinde erişimin/hizmetin durdurulması talep edilebilir `[doğrula]`.
2. **5651 s. Kanun m. 9 AYM İptal Uyarısı:** Kişilik hakları nedeniyle içerik çıkarma / erişimin engellenmesi dayanağı olan **5651 sayılı Kanun m. 9, Anayasa Mahkemesi'nin E.2020/76, K.2023/172 sayılı kararıyla iptal edilmiş olup iptal hükmü 10 Ekim 2024 tarihinde yürürlüğe girmiştir** `[doğrula]`. Güncel yürürlük ve yerine getirilen yeni düzenleme için mutlaka `Resmî Gazete` ve `references/currency-watch.md` kontrol edilmelidir. Kişilik hakkı iddialarını FSEK Ek m. 4 telif prosedürüymüş gibi sunma; FSEK Ek m. 4 yalnızca korunan eser/bağlantılı hak ihlalleri içindir.
3. **E-Ticaret Pazaryeri & Sınai Haklar (`6563 s. E-Ticaret K.` & `SMK m. 159`):** Marka/tasarım taklidi ürün listelemelerinde pazaryeri bildirim kuralları (elektronik ticaret aracı hizmet sağlayıcı yükümlülükleri `[doğrula]`) ve mahkemeden **FSHHM İhtiyati Tedbir (SMK m. 159)** yolu ayrı işler.
4. **Sınır Ötesi ABD Platform İstisnası (`17 U.S.C. §512`):** Yalnızca YouTube, GitHub, Meta, Apple App Store gibi ABD hukukuna tabi platformların kendi resmî DMCA formlarında geçerlidir; **Türkiye mevzuatı yerine geçmez ve Türk uyar-kaldır sisteminde `--counter` (karşı bildirim) mekanizmasının birebir karşılığı yoktur.**

## İş Akışı

1. `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` dosyasını (`## Kullanıcı Rolü`, `## Fikri Mülkiyet (IP) Uygulama Profili`, `## Uygulama ve İhtar Duruşu (Enforcement Posture)`, `## Çıktılar`, `## Öznel Hukuki Değerlendirmelerde Karar Duruşu`, `## Matter Workspaces`) oku.
2. Bayrağı belirle (`--send` | `--respond` | `--counter`); verilmemişse kullanıcıya sor.

## Mod 1: `--send` (FSEK Ek m. 4 Uyar-Kaldır Taslağı)

### Adım 1–2: Hak Sahipliği, Yetki ve Tam Konum Tespiti
- Eser türü, eser sahibi / devralan sıfatı (çalışan eseri FSEK m. 18 veya yükleniciden FSEK m. 52 yazılı devir + varsa Kültür ve Turizm Bakanlığı isteğe bağlı kayıt-tescil no) netleştirilir.
- İhlal edilen URL'ler, ekran görüntüleri ve tarih/saat tespit edilir.

### Adım 3: Kanuni İstisna Kontrolü (`FSEK m. 30–40` Kapısı)
- **Türkiye hukukunda genel "fair use" doktrini yoktur.** İçeriğin **FSEK m. 30–40** kapsamındaki dar kanuni istisnalara (ör. iktibas serbestisi `m. 35`, şahsi kullanım `m. 38`, eğitim/haber) veya açık/örtülü lisansa girip girmediğini kontrol et `[review]`. *(Yalnızca ABD platformlarına DMCA §512 bildirimi gönderiliyorsa Lenz emsali gereği fair use değerlendirmesi ayrı eklenir.)*

### Adım 4: Cezai ve Hukuki Sorumluluk Kontrolü (`TCK m. 267` & `TTK m. 54–55`)
- Yetki veya telif sahipliği olmadan ya da kanuni istisna/lisans görmezden gelinerek gönderilen kötü niyetli veya haksız bildirimler **TCK m. 267 (İftira)** ve **TTK m. 54–55 (Haksız Rekabet / tazminat)** sorumluluğu doğurur.

```text
┌────────────────────────────────────────────────────────────────┐
│  DUR — GÖNDERMEDEN ÖNCE KONTROL                                │
│  Bu taslak FSEK Ek m. 4 / TTK / TCK kapsamında hukuki ve       │
│  cezai sonuç doğuran resmî bir bildirimdir.                    │
│  [ ] Eser sahipliği veya FSEK m. 52 yazılı devir doğrulandı   │
│  [ ] Tam URL ve ihlal kapsamı birebir tespit edildi           │
│  [ ] FSEK m. 30–40 dar istisnaları / lisans durumu elendi     │
│  [ ] Sorumlu avukat incelemesi tamamlandı                     │
└────────────────────────────────────────────────────────────────┘
```

*(Non-lawyer kullanıcı ise avukat/yetkili onayı olmadan göndermez ve 1 sayfalık brifing alır.)*
Taslakta alıcıya karşı gönderilecek metinden `## Çıktılar` çalışma başlığını mutlaka çıkar.

## Mod 2: `--respond` (Gelen İhlal / Uyar-Kaldır Bildirimini İnceleme)

Bize gönderilen FSEK Ek m. 4 ihtarı, pazaryeri şikâyeti veya DMCA bildirimi için kontrol listesi:
- Bildirim usulüne uygun mu (eser, hak sahipliği belgesi, somut URL var mı)?
- Mevcut lisansımız veya **FSEK m. 30–40** istisnamız var mı?
- Seçenekler: (A) İçeriği kaldırma / uyma, (B) Platform/hukuki itiraz (ABD DMCA ise `§512(g)(3)` karşı bildirimi; Türkiye ise yer/içerik sağlayıcıya yazılı haklılık beyanı + Savcılık/Mahkeme aşamasında itiraz), (C) Hak sahibiyle sulh/lisans (`6325 s. K. m. 4–5` ve `HMK m. 313–315` müzakere hijyeni), (D) Kötü niyetli/haksız bildirime karşı `TCK m. 267` / `TTK m. 54–56` / `SMK m. 154` karşı adımları değerlendirme.

## Mod 3: `--counter` (Yalnızca ABD Platformları İçin `17 U.S.C. §512(g)` Karşı Bildirimi vs. Türk Hukuku Yolları)

> **Türk Hukuku Kapısı:** İçerik Türkiye **FSEK Ek m. 4** veya **5651 s. Kanun** / Türk mahkeme kararıyla kaldırılmışsa **ABD DMCA counter-notice (`§512(g)(3)`) UYGULANMAZ!** Türkiye'de karşı bildirim (otomatik 10–14 gün geri yükleme) mekanizması yoktur; yol Türk içerik/yer sağlayıcıya haklılık ispatı, Cumhuriyet Savcılığı/Sulh Ceza Hâkimliği veya FSHHM nezdinde itirazdır.

Yalnızca karşı bildirim sunulan **ABD hukukuna tabi bir platform (`YouTube`, `GitHub` vb.) ve ABD DMCA §512 bildirimi** söz konusuysa ABD federal yargı yetkisi kabulü ve `17 U.S.C. §512(f)/(g)` yalan beyan sorumluluğu (`perjury`) uyarısıyla taslağı hazırla ve öncesinde avukat onayı al.

## Yapmadıkları

- Savcılığa, mahkemeye, BTK/pazaryerine veya platform formlarına kendiliğinden başvuru yapmaz.
- Yürürlükteki erişim engeli mevzuatını (`references/currency-watch.md`) canlı doğrulamadan kesin sonuç ilan etmez.
