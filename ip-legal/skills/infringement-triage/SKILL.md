---
name: infringement-triage
description: >
  Marka (SMK m. 7/2, 29, 149–152), telif (FSEK m. 1/B, 8, 14–25, 30–40, 68, 71),
  patent/tasarım (SMK m. 89, 138, 141, 150–151) ve ticari sır/haksız rekabet
  (TTK m. 54–56, TBK m. 396/444, TCK m. 239) kapsamında tecavüz ön incelemesi
  (triyaj) yapar. Kesin ihlal hükmü vermez; leh/aleyh faktörleri, savunmaları,
  HMK delil tespitini ve zorunlu arabuluculuğu (TTK m. 5/A) çıkarır.
argument-hint: "[olguları ve hak türünü açıklayın]"
---

# /infringement-triage

## ⚠️ BU BİR ÖN TRİYAJDIR — KESİN İHLAL TESPİTİ DEĞİLDİR

Olayı iki yönlü değerlendirir (**lehimize olan ve aleyhimize işleyen faktörler**): ister karşı tarafın haklarımıza tecavüzünü, ister bizim ürünümüze yöneltilen tecavüz iddiasını inceliyor olun, strateji/ihtarname/dava öncesinde savunmaları, görevli mahkemeyi (FSHHM), delil tespiti ve zorunlu arabuluculuk koşullarını çıkarır.

## İş Akışı

1. `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` dosyasını (`## Şirket Profili`, `## Kullanıcı Rolü`, `## Fikri Mülkiyet (IP) Uygulama Profili`, `## Uygulama ve İhtar Duruşu (Enforcement Posture)`, `## Çıktılar`, `## Öznel Hukuki Değerlendirmelerde Karar Duruşu`, `## Matter Workspaces`) oku.
2. Hak modunu belirle (**Marka**, **Telif (FSEK)**, **Patent/Tasarım** veya **Ticari Sır / Haksız Rekabet**) ve somut olguları (kim, hangi işaret/eser/ürün/sır, nerede, ne zamandan beri, biliniyor mu) al.

## 4 Hak Modu ve Türk Hukuku Çekirdeği

### Mod 1: Marka Tecavüzü (`6769 s. SMK`)
- **Tecavüz ve İltibas (`SMK m. 7/2-(b)` & `m. 29`):** İşaretlerin aynılığı/benzerliği ve mal/hizmet aynılığı/benzerliği nedeniyle **halk tarafından karıştırılma ihtimali** (tescilde `m. 6/1`). Görsel, işitsel, kavramsal benzerlik ve markanın ayırt edicilik gücü incelenir.
- **Tanınmış Marka Koruması (`SMK m. 7/2-(c)` — tescilde `m. 6/4–5`):** Farklı mal/hizmetlerde dahi haksız yarar, itibar zedelenmesi veya ayırt ediciliği zedeleme riski + paralel **TTK m. 54–56** haksız rekabet / ticari takdim şekli (trade dress) koruması.
- **Temel Savunmalar:** Tescilin üzerinden **5 yıl geçmişse kullanmama def'i (`SMK m. 29/2`, `m. 19/2`)**, **5 yıl sessiz kalma yoluyla hak kaybı (`SMK m. 25/6`)**, **uluslararası tükenme ilkesi (`SMK m. 152` — orijinal ürünün dünyada herhangi bir yerde piyasaya ilk sürülmesi)**, dürüst ticari ad/adres/tanımlayıcı kullanım (`SMK m. 7/5`) `[doğrula]`.

### Mod 2: Telif / Eser Tecavüzü (`5846 s. FSEK` & `5651 s. Kanun`)
- **Korumaya Hak Kazanma:** Türkiye'de telif koruması yaratıldığı anda tescilsiz başlar (**FSEK m. 1/B** hususiyet taşıyan fikir ve sanat ürünü, **m. 8** eser sahibi, **m. 27** yaşam + 70 yıl); Kültür ve Turizm Bakanlığı kayıt-tescil belgesi zorunlu değildir, yalnızca ispat kolaylığı sağlar.
- **Hak İhlali ve Tazminat:** Mali haklara (işleme, çoğaltma, yayma, temsil, umuma iletim `m. 21–25`) veya manevi haklara (`m. 14–17`) tecavüz varsa durdurma/men (`m. 66–69`), rayiç bedelin **üç katına kadar tazminat (`FSEK m. 68`)** ve şikâyete bağlı ceza sorumluluğu (`FSEK m. 71`) doğabilir `[doğrula]`.
- **İstisna Kapısı (`FSEK m. 30–40`):** **Türk hukukunda ABD/Anglosakson tarzı genel bir "fair use" veya geniş "transformativeness (dönüştürücü kullanım)" istisnası yoktur!** Yalnızca kanunda sınırlı sayılan iktibas serbestisi (`m. 35`), eğitim/öğretim (`m. 33–34`), şahsi kullanım (`m. 38`), kamu düzeni vb. dar istisnalar uygulanır `[review]`.
- **Yer Sağlayıcı / Hosting (`5651 s. K. m. 5` & `FSEK Ek m. 4`):** Yer sağlayıcı genel izleme yükümlülüğüne tabi değildir; ancak hukuka aykırı içerik usulünce bildirildiğinde (`FSEK Ek m. 4`: 3 gün) kaldırmakla yükümlüdür `[doğrula]`.

### Mod 3: Patent / Faydalı Model / Tasarım (`6769 s. SMK`)
- **İhlal Testi:** Bağımsız istemin tüm unsurları (birebir veya **SMK m. 89 Eşdeğerler Doktrini** ile) mevcut mu? Tasarımda bilgilenmiş kullanıcı üzerinde bırakılan genel izlenim farklılığı (`SMK m. 56 vd.`).
- **Savunma ve Karşı Dava:** Önceki kullanım hakkı (**SMK m. 87**), **SMK m. 138 Hükümsüzlük** (yenilik/buluş basamağı eksikliği), lisans sözleşmesi kapsamı.
- **Tazminat (`SMK m. 150–151/2`):** Fiilî zarar + yoksun kalınan kazanç (hak sahibinin muhtemel geliri, mütecavizin net kazancı veya varsayımsal lisans bedeli seçenekleri). **Uyarı:** İhtarnamenin veya bu triyajın okunup ihlale devam edilmesi kasıt/ağır kusur tartışmasını ağırlaştırabilir `[doğrula]`.

### Mod 4: Ticari Sır & Haksız Rekabet (`TTK m. 54–56`, `TBK`, `TCK m. 239`)
- **Koruma Ölçütü:** Bilginin gizli olması, ticari değer taşıması ve gizli kalması için **makul tedbirlerin alınmış olması** (NDA, erişim yetkisi, şifreleme).
- **Fiiller:** **TTK m. 55/1-(b)** (çalışanları/vekilleri sır ifşasına yöneltme), **TTK m. 55/1-(d)** (üretim ve iş sırlarını hukuka aykırı ele geçirme/yararlanma), iş sözleşmesi süresince **TBK m. 396** sadakat borcu ve sonrası **TBK m. 444–447** rekabet yasağı sınırları, kasıtlı ifşada **TCK m. 239** ceza boyutu `[doğrula]`.

## Usul, Görevli Mahkeme ve Zorunlu Arabuluculuk (Tüm Modlar)

- **Görevli Mahkeme:** Kurulmuş yerlerde **Fikri ve Sınai Haklar Hukuk Mahkemesi (FSHHM)** (bulunmayan yerlerde Asliye Hukuk; ticari sır/TTK haksız rekabet eksenli davalarda Asliye Ticaret Mahkemesi ayrımı kontrol edilir `[doğrula]`).
- **Ön Tedbir ve Delil:** Dava öncesi noter/mahkeme eliyle **Delil Tespiti (`HMK m. 400`)** ve **İhtiyati Tedbir (`SMK m. 159`, `FSEK m. 77`)**.
- **Zorunlu Dava Şartı Arabuluculuk (`TTK m. 5/A` & `6325 s. Kanun`):** Konusu bir miktar paranın ödenmesi olan alacak ve tazminat taleplerinde (maddi/manevi/yoksun kalınan kazanç tazminatı) **dava açılmadan önce zorunlu ticari arabuluculuk** dava şartıdır `[doğrula]`.

## Çıktı Formatı ve Devirler

- Üste `## Çıktılar` çalışma başlığı ve `Reviewer note` koy (tüm mevzuat atıflarına `[model bilgisi - doğrula]` veya oturumda açıldıysa `[Mevzuat.gov.tr]` / `[TÜRKPATENT]` / `[UYAP]` resmî kaynak etiketi ekle; yabancı veri tabanı adı kullanma).
- Çıktıda: **Kısa Sonuç** (`Güçlü / Orta / Zayıf / İhlal Riski Yüksek` — asla tek yönlü kesin hüküm yok) · **Leh ve Aleyh Faktör Tablosu** · **Karşı Savunma ve Hükümsüzlük Riskleri** · **Görevli Mahkeme / HMK m. 400 / Arabuluculuk (TTK m. 5/A) Kontrolü** · **Sonraki Adımlar** (`/ip-legal:cease-desist` veya `/ip-legal:takedown` devri).
- **Non-lawyer kapısı:** Resmî ihtarname, delil tespiti, savcılık şikâyeti veya dava adımı öncesinde yetkili avukat incelemesi için 1 sayfalık brifing sun; Sonraki Adımlar Karar Ağacı ile kapat.
