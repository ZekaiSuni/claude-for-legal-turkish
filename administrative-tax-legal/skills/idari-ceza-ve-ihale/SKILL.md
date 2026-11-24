---
name: idari-ceza-ve-ihale
description: >
  Düzenleyici kurum (KVKK, Rekabet, SPK, BTK, EPDK, RTÜK, Reklam Kurulu)
  ve genel idari para cezalarında İdare Mahkemesi (60 gün) vs. 5326 s.
  Kabahatler K. Sulh Ceza Hâkimliği (15 gün) görev ayrımını, %25 peşin ödeme
  indirimini (m. 17/6) ve 4734 s. KİK zorunlu şikâyet/itirazen şikâyet +
  İYUK m. 20/A ivedi yargılama sürecini yönetir.
---

# İdari Para Cezaları ve Kamu İhale Uyuşmazlıkları (`idari-ceza-ve-ihale`)

Kuruma kesilen düzenleyici idari para cezalarında ölümcül **Sulh Ceza Hâkimliği (15 gün)** vs. **İdare Mahkemesi (60 gün)** görev/süre hatasını önlemek ve `4734 s. Kamu İhale Kanunu` kapsamındaki zorunlu başvuru zincirini kaçırmamak için uygulanır. `CLAUDE.md` içindeki `## İdare ve Vergi Uyuşmazlık Duruşu` ve `## Çekirdek Güvenlik Kuralları (Shared Guardrails)` esas alınır.

## Adım 1 — İdari Para Cezalarında Görevli Merci ve Süre Tuzakları (`5326` vs. Özel Kanunlar)

> **Önem Derecesi Tabanı:** İdari para cezasının hangi kanuna dayandığı kesinleşmeden **15 günlük** `5326` süresi geçmiş gibi risk taşıyan her karar dosyası **KRİTİK** işlenir; önem seviyesi gerekçesiz düşürülemez.

| Ceza Dayanağı / Kurum | Kanun Yolu Süresi | Görevli Merci | Özel Notlar & Dikkat Edilecek Hususlar |
|---|---|---|---|
| **Genel İdari Para Cezaları (Özel Kanunda Hüküm Yoksa)** | **15 gün** (`5326 s. Kabahatler K. m. 27`) | **Sulh Ceza Hâkimliği** | İdare Mahkemesine dava açılırsa **görevsizlik sonrası süre kaçırma riski!** Aynı karar içinde hem iptale tabi idari yaptırım (mühürleme, ruhsat iptali) hem idari para cezası varsa **`5326 m. 27/8`** uyarınca ikisi birlikte İdare Mahkemesinde görülür (`[doğrula]`) |
| **KVKK İdari Para Cezaları (`6698 m. 18`)** | **60 gün** (`İYUK m. 7` / `7499` sonrası düzenleme) | **İdare Mahkemesi** | `7499 s. K.` (01.06.2024 yürürlük) ile Sulh Ceza'dan **İdare Mahkemesine** geçirildi (`[doğrula]`) |
| **Rekabet Kurulu (`4054 m. 55`)** | **60 gün** | **Ankara İdare Mahkemeleri** | Tüm Rekabet Kurulu kararlarına karşı Ankara İdare Mahkemeleri yetkili ve görevlidir |
| **SPK (`6362`), BDDK (`5411`), BTK (`5809`), EPDK (`4628`), RTÜK (`6112`), TİHEK (`6701`)** | **60 gün** (özel kanun veya `İYUK m. 7` — her kararda metin kontrol edilir) | **İdare Mahkemesi** | Karar tebliğ metninde gösterilen kanun yolu (`Anayasa m. 40/2`) ile özel kanun süresi tek tek `[doğrula]` |
| **Reklam Kurulu ve 6502 İdari Yaptırımları (`6502 s. TKHK m. 77, m. 78/2`)** | **30 gün** (özel kanuni süre — `6502 m. 78/2`) | **İdare Mahkemesi** | 60 günlük genel İYUK süresine güvenilirse dava **süre aşımından reddedilir**; özel 30 günlük süreyi güncel metinden `[doğrula]` |
| **İş Kanunu / İSG / SGK İPC (`4857`, `6331`, `5510 m. 102`)** | Kurum itiraz süreleri (ör. SGK **15 gün** itiraz + ret üzerine **30 gün** İdare Mahkemesi; `4857/6331` **15 gün** Sulh Ceza) | SGK'da İtiraz Komisyonu → İdare; 4857/6331'de **Sulh Ceza Hâkimliği** | SGK vs. İŞKUR/ÇSGB ayrımını güncel madde üzerinden mutlaka `[doğrula]` |

## Adım 2 — `5326 m. 17/6` %25 Peşin Ödeme İndirimi ve YD

- **%25 Peşin İndirim (`5326 m. 17/6`):** Kabahat nedeniyle verilen idari para cezasını kanun yoluna başvurmadan önce (tebliğden itibaren **15 gün** içinde) ödeyen kişiden cezaların **dörtte üçü (`%25 indirim`)** tahsil edilir.
- **Dava/Başvuru Hakkı Koruması:** Peşin ödeme yapılması kişinin **kanun yoluna başvurma hakkını etkilemez**; dava kazanılırsa ödenen tutar iade edilir (`[doğrula]` — vergi dairesi/tahsil dairesi iade ve faiz prosedürü `references/currency-watch.md` ile kontrol edilir).
- **Tahsilat ve YD:** Özel kanunlarda aksi yoksa idari para cezasına dava açmak tahsilatı durdurmaz; itiraz/dava dilekçesinde **yürütmenin durdurulması** (veya Sulh Ceza'da infazın durdurulması) ayrıca talep edilir.

## Adım 3 — `4734 s. Kamu İhale Kanunu (KİK)` Zorunlu Başvuru Zinciri (**5–10 Gün — KRİTİK**)

İhale işlemlerine karşı doğrudan İdare Mahkemesinde dava **AÇILAMAZ**; aşağıdaki **üç aşamalı zorunlu sıra** tüketilmeden açılan dava **idari merci tecavüzü / ret** riski doğurur:

1. **1. Aşama — İhaleyi Yapan İdareye Şikâyet (`4734 m. 55`):** İhale sürecindeki hukuka aykırı işlem veya eylemlerin farkına varıldığı veya varılması gereken tarihi izleyen günden itibaren genel kural olarak **10 gün** içinde (pazarlık `m. 21/b-c` ve istisnai/ivedi hallerde **5 gün** — ilan ve zeyilname süre kısıtları dahil `[doğrula]`) yazılı **Şikâyet** başvurusu yapılır.
2. **2. Aşama — Kamu İhale Kurumu'na (KİK) İtirazen Şikâyet (`4734 m. 56`):** İdare şikâyeti reddederse veya başvuru tarihinden itibaren **10 gün** içinde karar vermezse (zımni ret), karar tebliğini veya 10 günlük sürenin bitimini izleyen **10 gün** içinde başvuru bedeli yatırılarak **KİK'e İtirazen Şikâyet** yapılır. *(İdare şikâyeti süresi geçirilmişse doğrudan KİK'e gidilemez!)*
3. **3. Aşama — Ankara İdare Mahkemelerinde `İYUK m. 20/A` İvedi Dava:** KİK nihai kararının tebliğinden itibaren **30 gün** içinde yetkili **Ankara İdare Mahkemelerinde** `m. 20/A` ivedi yargılama usulüyle dava açılır (`İYUK m. 11` süre kesmez; karara karşı **istinaf yoktur**, tebliğden itibaren **15 gün** içinde Danıştay'a **temyiz** edilir).

## Adım 4 — Hedef Kitle Kontrolü ve Kayıt

Karşı idareye, KİK'e veya mahkemeye sunulacak şikâyet/dava taslakları `1136 s. Av.K. m. 36`, `CMK m. 130`, `CMK m. 46` ve `HMK m. 249` uyarınca iç değerlendirme notlarından arındırılır; ihale başvuru bedeli ve tebliğ tarihleri `verification-log.md` içine kaydedilir.
