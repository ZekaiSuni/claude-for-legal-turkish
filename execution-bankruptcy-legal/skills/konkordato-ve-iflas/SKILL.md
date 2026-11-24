---
name: konkordato-ve-iflas
description: >
  İİK m. 285-309 konkordato süreçlerinde geçici/kesin mühlet yasakları,
  m. 299 15 günlük alacak bildirimi, rehinli (m. 295) ve birinci sıra
  alacak (m. 206) istisnaları, alacaklılar toplantısı nisapları (m. 302),
  tasdik ve iflas masasına alacak kaydı (m. 206, 219, 232-235) analizini yapar.
---

# Konkordato ve İflas Masası Yönetimi (`konkordato-ve-iflas`)

Borçlunun konkordato ilan etmesi veya iflasının açılması halinde müvekkilin alacak hakkını, rehin statüsünü, takas/mahsup haklarını ve projeye karşı oy/itiraz imkânlarını korumak için uygulanır. `CLAUDE.md` içindeki `## Konkordato ve İflas İzleme Politikası` ve `### Onay ve Eskalasyon Matrisi` esas alınır.

## Adım 1 — Mühlet Türü ve Süre Denetimi (`İİK m. 287–289`)

1. **Geçici Mühlet (`İİK m. 287`):** Başvuru üzerine **3 ay** verilir; komiserin raporuyla en fazla **2 ay** daha uzatılabilir (toplam azami 5 ay). Kesin mühletin tüm hukuki sonuçlarını doğurur (`m. 288`).
2. **Kesin Mühlet (`İİK m. 289`):** Borçlunun projesinin başarıya ulaşacağının anlaşılması halinde **1 yıl** verilir; güçlük arzeden durumlarda komiser talebiyle en fazla **6 ay** uzatılabilir.
3. **Alacaklılar Kurulu:** Borçlunun durumu gerektiriyorsa Asliye Ticaret Mahkemesince alacaklı sınıflarını temsilen oluşturulur (`m. 289/3`).

## Adım 2 — Takiplere, Faizlere ve Sözleşmelere Etkisi (`İİK m. 294–297`)

| Alacak / İşlem Türü | Konkordato Mühleti İçindeki Rejim | Hukuki Dayanak & Kontrol |
|---|---|---|
| **Adi (Rehinsiz) Alacak Takipleri** | Mevcut takipler **durur**, yeni takip **yapılamaz**, ihtiyati haciz/tedbirler uygulanmaz | `İİK m. 294/1`; mühletten önce hacizli malların satışı da durur |
| **`İİK m. 206` Birinci Sıra Alacaklar** (İşçi alacakları, nafaka) | İstisnaen mühlet içinde **haciz yoluyla takip yapılabilir** | `İİK m. 294/2` — takip yapılabilse bile tahsilat sınırları denetlenir |
| **Rehinli Alacaklar (`m. 295`)** | Rehnin paraya çevrilmesi yoluyla takip **başlatılabilir/devam eder**, ancak **muhafaza tedbiri ve satış yapılamaz** | `İİK m. 295`; rehin kıymetinden fazla kalan rehin açığı adi alacak rejimine girer |
| **Faiz İşlemesi (`m. 294/3`)** | Rehinle karşılanmayan adi alacaklarda **mühlet kararıyla faiz durur** (tasdik şartına göre) | Projedeki tenzilat (indirim) veya vade uzatımı seçenekleriyle birlikte incelenir |
| **Sözleşmelerin Devamı (`m. 296`)** | Karşı taraf sırf konkordato başvurusu nedeniyle sözleşmeyi feshedemez (aksi sözleşme hükümleri geçersiz) | Kritik tedarik/kira sözleşmelerinde önemli sebep dışında fesih riski `[doğrula]` |
| **Takas Hakkı (`m. 294/6`, `m. 200–201`)** | Geçici mühlet ilanından önceki karşılıklı muaccel alacaklarda takas şartları | Kötü niyetle devralınan alacaklarda takas yasağı (`m. 201`) kontrol edilir |

## Adım 3 — `İİK m. 299` Alacak Bildirimi (**15 Gün — KRİTİK**)

- Konkordato komiserinin **Basın İlan Kurumu / Türkiye Ticaret Sicili Gazetesi** ilanından itibaren **15 gün** içinde yazılı ve dayanak belgeli (fatura, sözleşme, çek/senet sureti, kesinleşme şerhi, icra dosya hesabı) **alacak bildirimi** yapılmalıdır.
- **Önem Derecesi Tabanı:** Bildirim yapmayan alacaklılar, borçlunun bilançosunda kayıtlı olmadıkça konkordato projesinin müzakerelerine kabul edilmez; çekişmeli alacakların akıbeti ise projenin tasdiki sonrası genel hükümlere/komiser raporuna göre riske girer (`## Çekirdek Güvenlik Kuralları (Shared Guardrails)`).
- Bildirilen tutarda faizin kesin mühlet/geçici mühlet tarihine kadar hesaplanmış dökümü ayrı gösterilir (`[doğrula]`).

## Adım 4 — Alacaklılar Toplantısı, Nisap (`m. 302`) ve Tasdik İtirazı

- **Kabul Çoğunluğu (`İİK m. 302/3`):** Konkordato projesi,
  1. Kaydedilmiş alacaklıların ve alacakların **yarısını aşan**, **VEYA**
  2. Kaydedilmiş alacaklıların **dörtte birini (1/4)** ve alacakların **üçte ikisini (2/3)** aşan çoğunlukla imza edilirse kabul edilmiş sayılır.
- **Rehinli Alacaklılar Müzakeresi (`m. 308/h`):** Rehinli alacaklılarla borçların yapılandırılması ayrı nisap ve prosedüre tabidir.
- **Proje Oyu ve Kanun Yolu (`### Onay ve Eskalasyon Matrisi`):** Kabul/ret oyu verilmesi veya tasdik kararına itiraz/istinaf (**2 hafta** — `7499 s. K.` uyumu dosya özelinde `[doğrula]`) doğrudan kıdemli avukat/yönetim onayına sunulur.

## Adım 5 — İflas ve Sıra Cetveli (`İİK m. 154–256`, `m. 206`)

- Borçlunun iflası halinde alacakların **iflas idaresine bildirilmesi** (`m. 219–220`: ilan tarihinden itibaren **1 ay**),
- **Sıra Cetveline Başvuru (`İİK m. 232–235`):** Sıraya itiraz için **7 gün** içinde İcra Hukuk Mahkemesine **şikâyet**, alacağın esasına/miktarına itiraz için **15 gün** içinde Ticaret Mahkemesinde **itiraz davası** açılır (`### Onay ve Eskalasyon Matrisi`).
- Tüm kritik mühlet tarihleri, komiser iletişim bilgileri ve bildirim makbuzları `verification-log.md` dosyasına kaydedilir.
