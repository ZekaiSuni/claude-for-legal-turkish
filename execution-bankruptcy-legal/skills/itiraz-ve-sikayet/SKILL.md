---
name: itiraz-ve-sikayet
description: >
  Ödeme/icra emrine itiraz (Örnek 7, 10, 13, 4-5), İİK m. 16 icra memuru
  işlemini şikâyet, UETS/fiziki usulsüz tebligat (7201 m. 7/a, m. 21/2, m. 32),
  89/1-2-3 haciz ihbarnameleri ve İİK m. 67/68/72 davaları için doğru merci,
  hak düşürücü süre ve savunma/hücum stratejisi üretir.
---

# İtiraz, Şikâyet ve 89/1-2-3 Müdahale Rehberi (`itiraz-ve-sikayet`)

Borçlu savunmasında veya üçüncü kişi `İİK m. 89` ihbarnamesinde yanlış merciye başvurunun takibi kesinleştirmesi riskini, alacaklı tarafında ise itirazın iptali/kaldırılması seçimindeki hataları engeller. `CLAUDE.md` içindeki `## Takip ve Tahsilat Duruşu (Collection & Defense Posture)` ve `## Çekirdek Güvenlik Kuralları (Shared Guardrails)` uygulanır.

## Adım 1 — Tebligat Geçerliliği ve Süre Başlangıcı (`7201 s. TK`)

1. **UETS Elektronik Tebligat (`7201 s. TK m. 7/a`):** Elektronik tebligat, muhatabın elektronik adresine ulaştığı tarihi izleyen **5. günün sonunda** yapılmış sayılır. Muhatabın iletiyi daha erken açması tebliğ tarihini öne çekmez (`[doğrula]`).
2. **Fiziki Tebligat ve MERNİS (`7201 s. TK m. 21/2`):** Muhatabın bilinen son adresi araştırılıp iade dönmeden doğrudan `m. 21/2` şerhli tebligat çıkarılması Yargıtay uygulamasında kural olarak usulsüzdür (`[doğrula]`).
3. **Usulsüz Tebligat (`7201 s. TK m. 32`):** Tebligat usulsüz olsa dahi muhatap öğrenmişse geçerli olur; muhatabın bildirdiği öğrenme tarihi aksi sabit oluncaya kadar esas alınır (**7 gün** içinde İcra Hukuk Mahkemesinde usulsüz tebligat şikâyeti + aynı anda süresinde itiraz stratejisi kontrol edilir).
4. **Süre Hesabı (`İİK m. 19`):** İcra süreleri **Adli Tatilde durmaz**; son gün resmî tatile veya hafta sonuna rastlarsa ilk iş günü mesai bitiminde dolar.

## Adım 2 — Takip Türüne Göre Doğru Merci ve Hak Düşürücü Süre

> **Önem Derecesi Tabanı:** Süre son günü yaklaşan `Örnek 10` (5 gün), `Örnek 7` (7 gün), `89/1-2-3` ve `İİK m. 16` dosyaları her zaman **KRİTİK** sınıflandırılır ve gerekçesiz düşürülemez.

| Konu / Belge | Kanuni Süre | Zorunlu Merci | Kritik Hukuki Uyarı |
|---|---|---|---|
| **Örnek 7 Ödeme Emrine İtiraz** (`İİK m. 62`) | **7 gün** | **İcra Dairesi** | Adi senette imza inkârı **ayrıca ve açıkça** yapılmazsa imza ikrar edilmiş sayılır (`m. 62/5`) |
| **Örnek 10 Kambiyo İtirazı / Şikâyet** (`İİK m. 168–170/a`) | **5 gün** | **İcra Hukuk Mahkemesi** | **İcra Dairesine verilen itiraz geçersizdir!** İtiraz yalnız satışı durdurur; haczi durdurmak için mahkemeden geçici durdurma kararı istenir (`m. 169`) |
| **Örnek 13 Kira İtirazı / Ödeme** (`İİK m. 269`) | **7 gün** itiraz / ödeme: **10 gün** (adi kira), **30 gün** (konut/çatılı işyeri `TBK m. 315`), **60 gün** (hasılat kirası `TBK m. 362`) | **İcra Dairesi** | Kira sözleşmesine ve imzasına açıkça itiraz edilmezse kira akdi ikrar edilmiş sayılır |
| **Örnek 4-5 İlamlı İcranın Geri Bırakılması** (`İİK m. 33`) | **7 gün** | **İcra Hukuk Mahkemesi** | Yalnız itfa/imhal/zamanaşımı ve ancak resmî veya imzası ikrarlı belge ile ileri sürülür; üst mahkeme kararı için `m. 36` tehir-i icra |
| **İcra Memuru İşlemini Şikâyet** (`İİK m. 16`) | **7 gün** (Kamu düzeni/hakkın yerine getirilmemesi **süresiz**) | **İcra Hukuk Mahkemesi** | Süre öğrenmeden başlar; takibin iptali veya işlemin düzeltilmesi talep edilir |

## Adım 3 — Üçüncü Kişi `İİK m. 89/1-2-3` Haciz İhbarnameleri

- **`89/1` İhbarnamesi:** Tebliğden itibaren **7 gün** içinde İcra Dairesine "borçlunun şirket/banka nezdinde doğmuş veya doğacak (müstakbel) alacağı yoktur" (veya varsa güncel tutar + önceki hacizler) yazılı olarak bildirilmelidir. İtiraz edilmezse borç üçüncü kişinin zimmetinde sayılır!
- **`89/2` İhbarnamesi:** Tebliğden itibaren **7 gün** içinde İcra Dairesine tekrar itiraz edilir (son şans ikazıdır).
- **`89/3` Bildirimi (KRİTİK ESKALASYON):** `89/1` ve `89/2`'ye süresinde itiraz edilmediyse `89/3` tebliğinden itibaren **15 gün** içinde yetkili genel mahkemede **Menfi Tespit Davası** açılması ve aynı `89/3` tebliğ tarihinden itibaren **20 gün** içinde dava açıldığına dair belgenin İcra Dairesine ibraz edilmesi zorunludur; aksi halde üçüncü kişi borçtan şahsen sorumlu hale gelir (`### Onay ve Eskalasyon Matrisi`).

## Adım 4 — Alacaklı İtirazı Aşma Yolları (`m. 68` vs. `m. 67`) ve `m. 72` Menfi Tespit

- **İtirazın Kaldırılması (`İİK m. 68`):** İtirazın tebliğinden itibaren **6 ay** (hak düşürücü); İcra Hukuk Mahkemesinde görülür, arabuluculuğa tabi değildir; ancak yalnızca `m. 68/1` belgesi (kayıtsız şartsız borç ikrarı, noter onaylı senet, imzası ikrarlı adi senet) varsa mümkündür.
- **İtirazın İptali Davası (`İİK m. 67`):** İtirazın tebliğinden itibaren **1 yıl** (hak düşürücü); Genel Mahkemede görülür, her türlü delil (ticari defter, e-posta, tanık vb.) incelenebilir; haksız itirazda asgari **%20 icra inkâr tazminatına** hükmedilir. Ticari, iş ve kira alacaklarında dava öncesi **zorunlu arabuluculuk** (`TTK m. 5/A`, `7036 m. 3`, `7445 s. K.`) şarttır!
- **Menfi Tespit ve İstirdat (`İİK m. 72`):** Borçlu takipten önce açarsa %15 teminattan az olmamak üzere ihtiyati tedbir ile takibin durdurulması istenebilir; takipten sonra açılan menfi tespitte takip kendiliğinden durmaz, yalnızca icra veznesindeki paranın alacaklıya ödenmemesi yönünde tedbir alınabilir (%15 teminat). **Zorunlu Arabuluculuk Uyarısı (`7445 s. K.`):** Ticari (`TTK m. 5/A`), iş (`7036 m. 3`) ve kira (`6325 m. 18/B`) uyuşmazlıklarından kaynaklanan **menfi tespit ve istirdat davaları** da dava şartı zorunlu arabuluculuğa tabidir (`[doğrula]` — ihtiyati tedbir aşaması etkileşimi ayrıca kontrol edilir).
- **Kanun Yolu (`7499 s. K.`, `İİK m. 363–364`):** İcra Hukuk Mahkemesi kararlarına karşı istinaf ve BAM kararlarına karşı temyiz süreleri tefhim/tebliğden itibaren **2 haftadır** (parasal sınırları `references/currency-watch.md` üzerinden `[doğrula]`).

## Adım 5 — Hedef Kitle Kontrolü ve Çıktı

Dilekçe taslakları mahkemeye/icra dairesine sunulmadan önce `1136 s. Av.K. m. 36`, `CMK m. 130`, `CMK m. 46` ve `HMK m. 249` kapsamında dahili strateji ve zayıf yön notlarından arındırılır; eksik tebligat tarihleri `[Kullanıcı Doğrulaması Gerekli]` ile işaretlenir.
