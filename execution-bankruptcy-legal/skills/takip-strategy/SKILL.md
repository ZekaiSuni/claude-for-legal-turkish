---
name: takip-strategy
description: >
  Uyuşmazlık ve alacak belgesine göre en uygun Türk icra takip yolunu
  (ilamsız Örnek 7, kambiyo Örnek 10, kira/tahliye Örnek 13, ilamlı,
  rehin İİK m. 45, ihtiyati haciz İİK m. 257), yetkili icra dairesini,
  faiz türünü ve arabuluculuk/döviz kurallarını analiz ederek takip
  stratejisi oluşturur.
---

# İcra Takip Stratejisi ve Başlatma Planı (`takip-strategy`)

Alacaklı veya müvekkil adına takip açılmadan önce yanlış takip yolu, yetkisizlik, rehin bariyeri veya faiz hatası nedeniyle süre ve harç kaybını önlemek için uygulanır. `CLAUDE.md` içindeki `## Takip ve Tahsilat Duruşu (Collection & Defense Posture)`, `### Onay ve Eskalasyon Matrisi` ve `## Öznel Hukuki Değerlendirmelerde Karar Duruşu` kuralları esas alınır.

## Adım 1 — Belge, Teminat ve Rehin Ön Kontrolü

1. **Belge Tespiti (`İİK m. 68` ve `TTK`):** Eldeki belge ilam/ilam niteliğinde belge (`İİK m. 38`: noter onaylı kayıtsız şartsız para borcu ikrarlı düzenleme şeklinde senetler dahil) mi, kambiyo senedi (`çek`, `bono`, `poliçe` — zorunlu şekil unsurları, ciro silsilesi, çekte süresinde ibraz/karşılıksızdır şerhi, bonoda vade) mi, yoksa fatura/sözleşme/cari hesap mutabakatı mı?
2. **Önce Rehne Başvuru Kuralı (`İİK m. 45`):** Alacak ipotek veya ticari işletme/taşınır rehni ile güvence altına alınmışsa kural olarak **önce rehnin paraya çevrilmesi yoluyla takip** yapılmalıdır; kambiyo senedine dayanılması (`m. 45/2` istisnası) veya müteselsil kefillere başvuru durumu ayrıca ayrıştırılır.
3. **Borçlu Durumu ve Konkordato Kontrolü:** Borçlu hakkında geçici/kesin mühlet (`İİK m. 287–294`) veya iflas kararı olup olmadığı kontrol edilir; eksik bilgi varsa `[Kullanıcı Doğrulaması Gerekli]` işaretlenir.

## Adım 2 — Takip Yolu Karşılaştırma ve Seçim Matrisi

| Takip Yolu (Örnek No) | Uygun Dayanak | İtiraz Süresi ve Merci | Güçlü / Zayıf Yön |
|---|---|---|---|
| **İlamlı Takip (Örnek 4-5)** | Mahkeme kararı, arabuluculuk son tutanağı (icra edilebilirlik şerhli), noter düzenleme senedi (`m. 38`) | Takip durmaz (`İİK m. 36` tehir-i icra hariç) | En hızlı icra kabiliyeti; karşı taraf teminat yatırmadan durduramaz |
| **Kambiyo Senetlerine Özgü Haciz (Örnek 10)** | Şekil şartları tam çek, bono, poliçe | **5 gün** — **İcra Hukuk Mahkemesi** | İtiraz satışı durdurur ama **haczi kendiliğinden durdurmaz** (`m. 169`); şekil eksikliği varsa iptal (`m. 170/a`) ve tazminat riski |
| **Genel Haciz Yoluyla İlamsız Takip (Örnek 7)** | Fatura, sözleşme, cari hesap, mutabakat veya belgesiz para alacağı | **7 gün** — **İcra Dairesi** | İtirazla takip kendiliğinden durur; kaldırılması (`m. 68`, 6 ay) veya iptali (`m. 67`, 1 yıl) gerekir |
| **Kira / Tahliye Takibi (Örnek 13)** | Kira sözleşmesi + ödenmeyen kira bedeli | **7 gün** itiraz / ödeme: **10 gün** (adi kira `TBK m. 315`), **30 gün** (konut/çatılı işyeri), **60 gün** (hasılat `TBK m. 362`) | Süresinde ödenmezse İcra Hukuk Mahkemesinden tahliye imkânı |
| **Rehnin Paraya Çevrilmesi (Örnek 6 / 8 / 9)** | İpotek akit tablosu, taşınır rehni | Takip türüne göre ilamlı/ilamsız | Rehinli mal doğrudan satışa konu edilir; rehin açığı belgesi sonrası haciz |

## Adım 3 — Zorunlu Arabuluculuk, Faiz, Harç ve Döviz Kuralları

- **Arabuluculuk (`TTK m. 5/A`, `7036 m. 3`, `7445 s. K.`):** İcra takibi açmak için arabuluculuk ön şartı yoktur; ancak borçlu `Örnek 7` takibine itiraz ederse ve uyuşmazlık **ticari, iş veya kira** niteliğindeyse **`İİK m. 67` itirazın iptali davasından önce zorunlu arabuluculuk** şarttır. (`İİK m. 68` itirazın kaldırılmasında aranmaz — `m. 68` belgesi yoksa `m. 67` arabuluculuk takvimi baştan hesaba katılmalıdır).
- **Yetkili İcra Dairesi (`İİK m. 50`, `HMK m. 6–17`):** Borçlunun yerleşim yeri, sözleşmenin ifa yeri; yetki sözleşmesi yalnızca tacirler ve kamu tüzel kişileri arasında geçerlidir (`HMK m. 17`).
- **Faiz Seçimi (`references/currency-watch.md`):** Adi alacaklarda `3095 s. K.` yasal faiz (%24 `[doğrula]`), ticari işlerde TCMB avans faizi (`[doğrula]`), sözleşme faizinde `TBK m. 120` (adi işlerde yasal faizin %100 fazlası sınırı) ve bileşik faiz yasağı (`TBK m. 388`, `TTK m. 8` istisnası) denetlenir.
- **Yabancı Para Alacakları (`İİK m. 58/3`, `32 s. Karar`):** Alacağın hangi tarihteki TCMB kuru üzerinden TL karşılığının yazılacağı (`takip tarihi` veya `vade/fiili ödeme` seçimi — Yargıtay içtihat sınırları `[doğrula]`) ve `32 s. Karar m. 4/g` istisna uyumu belirtilir.

## Adım 4 — İhtiyati Haciz (`İİK m. 257`) ve Çıktı Güvenliği

- Borçlunun mal kaçırma şüphesi, muayyen yerleşim yerinin bulunmaması veya vadesi gelmiş rehinsiz alacak varlığında **İhtiyati Haciz (`İİK m. 257`)** seçeneği değerlendirilir; mahkemece genellikle talep edilen alacağın **%10–15'i oranında teminat** (`[doğrula]`) istenmesi ve ihtiyati haciz kararından itibaren **10 gün** içinde infaz, hacizden itibaren **7 gün** içinde tamamlayıcı takip açılması (`İİK m. 261`, `m. 264`) zorunluluğu **kıdemli onayına** sunulur (`### Onay ve Eskalasyon Matrisi`).
- Hazırlanacak takip talebi veya ihtarname taslağı dışa gönderilmeden önce `## Çekirdek Güvenlik Kuralları (Shared Guardrails)` kapsamında **hedef kitle kontrolünden** geçirilir ve dahili strateji notları arındırılır.
