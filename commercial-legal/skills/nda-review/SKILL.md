---
name: nda-review
description: >
  Gelen Gizlilik Sözleşmelerini (GS / NDA) Türk ticaret hukuku playbook'una göre
  hızla YEŞİL / SARI / KIRMIZI olarak sınıflandırır. /commercial-legal:review
  tarafından bir gizlilik sözleşmesi tespit edildiğinde yüklenir.
user-invocable: false
---

# Gizlilik Sözleşmesi (NDA) İncelemesi

Bu beceri gelen Gizlilik Sözleşmelerini (GS/NDA) hızlıca **YEŞİL / SARI / KIRMIZI** olarak sınıflandırır. Amaç, standart ve avukat onaylı playbook'a uyan belgeleri imza sürecine yaklaştırmak; riskli veya gizlilik kapsamını aşan belgeleri ise hukukçuya yönlendirmektir.

Hukuki değerlendirme Türk borçlar/ticaret hukuku (`6098 s. TBK`, `6102 s. TTK`), `6698 s. KVKK` ve `4054 s. RKHK` ekseninde yapılır.

## Dosya Bağlamı (`Matter Context`)

`~/.claude/plugins/config/legal-turkish/commercial-legal/CLAUDE.md` içindeki `## Matter Workspaces` ayarını kontrol et. Etkinse ve aktif bir dosya seçilmemişse şunu sor:

> Bu inceleme hangi dosya için? `/commercial-legal:matter-workspace switch <kisa_ad>` komutunu çalıştırabilir veya yalnızca genel pratik bağlamında çalışmak istediğinizi belirtebilirsiniz.

Aktif `matter.md` dosyasını yükle. `Cross-matter context` kapalı olduğu sürece ve kullanıcı açıkça istemedikçe başka bir dosyayı okuma.

## Hedef Kitle Kontrolü — Mesleki Sır

Çıktı üretmeden önce hedefin neresi olduğunu kontrol et. Herkese açık kanallar, şirket geneli dağıtım listeleri, karşı taraf veya tedarikçiler gizlilik ve strateji riski doğurabilir (`1136 s. Av.K. m. 36`, `CMK m. 130`, `CMK m. 46`, `HMK m. 249`):

> Bu çıktı dahili hukuki değerlendirme ve müzakere stratejisi içerebilir. Hukuk ekibi dışına gönderilecekse iç strateji notlarından arındırılmış bir sürüm hazırlayayım.

Sunulabilecek seçenekler:
- yalnızca hukuk ekibi için tam sürüm,
- iş birimi/karşı taraf için arındırılmış ticari sürüm,
- her ikisi birlikte.

## Önce Playbook'u Yükle

Şirketin sözleşmedeki taraf konumunu netleştir:
- `sales-side`: Şirket müşteri, iş ortağı veya aday alıcıya bilgi/ürün sunmaktadır.
- `purchasing-side`: Şirket başka bir tarafın ürün veya hizmetini değerlendirmektedir.
- `mutual` (karşılıklı): Sözleşme karşılıklı olsa da metni kimin sunduğunu ve operasyonel olarak hangi tarafın bilgisinin daha hassas olduğunu tespit et.

`~/.claude/plugins/config/legal-turkish/commercial-legal/CLAUDE.md` -> `## Playbook` -> ilgili taraf -> `## NDA Triage Positions` bölümünü ve `## Turkish Contract Concepts` tablosunu oku. İlgili taraf veya NDA pozisyonları eksikse **YEŞİL** verme; eksik pozisyonu sor ve profil dosyasına kaydetmeyi teklif et.

## Kapsam Kontrolü (Gizli Yükümlülük Taraması)

Tek tek NDA maddelerine geçmeden önce belgenin basit bir gizlilik sözleşmesinin ötesine geçip geçmediğini kontrol et:
- münhasırlık (`exclusivity`),
- fikri mülkiyet devri veya geniş lisans (`FSEK m. 48–52`),
- çalışan veya müşteri ayartmama (`non-solicit`),
- rekabet etmeme (`TBK m. 444–447` / `TTK`),
- önalım veya öncelikli görüşme hakkı,
- NDA dışı uyuşmazlıkları kapsayan geniş tahkim veya yabancı mahkeme yetkisi,
- cezai şart (`TBK m. 179–182`; tacirler için `TTK m. 22`),
- kişisel veri işleme veya yurt dışına veri aktarımı (`KVKK m. 9`).

Belge gizlilik dışı yükümlülükler içeriyorsa doğrudan en az **SARI** sınıfına al ve avukat incelemesine yönlendir.

## Türk Hukuku Kavram Eşleştirmesi

Çıktılarda şu yerleşik karşılıkları kullan:
- **`survival`** -> **bakiye hükümler / sözleşmenin sona ermesinden sonra devam edecek yükümlülükler**.
- **`residuals` (hafızada kalan bilgi istisnası)** -> Zararsız standart ifade gibi geçiştirme. Çalışan sadakat borcu (`TBK m. 394–400`), haksız rekabet ve ticari sır (`TTK m. 54–55`), KVKK ve rekabet hukuku açısından incele.
- **cezai şart (`TBK m. 179–182`)** -> Orantılılık ve fahiş cezanın tenkisi (`TBK m. 182/3`) ile tacirlerdeki sınırlamayı (`TTK m. 22`; `TBK m. 27` istisnası saklı) kontrol et.
- **`damga vergisi (488 s. DVK)`** -> Yüksek tutarlı taahhüt, teminat, kefalet, sulh veya tadil hükümleri varsa vergi tutarı hesaplamadan vergi/mali müşavir incelemesi için işaretle.
- **`arabuluculuk`** -> Uyuşmazlık çözümünde `6325 s. Arabuluculuk Kanunu` ve ticari/iş/kira zorunlu arabuluculuk koşullarını hatırlat.
- Aşırı tek taraflı veya irade/yorum riski taşıyan hükümlerde `TBK m. 19, 27 ve 28` incelemesi öner.

## Triyaj Karar Kuralları

### YEŞİL (`GREEN`) — İmzaya Uygun
Yalnızca şu şartların tamamı sağlanıyorsa verilir:
- Tüm playbook kontrolleri geçer,
- Gizlilik dışı ek yükümlülük gizlenmemiştir,
- Uygulanacak hukuk ve yetkili merci playbook ile uyumludur,
- KVKK ve rekabet hukukuna hassas bilgi sorunu yoktur veya güvenli şerhler eklenmiştir,
- Playbook avukat onaylı YEŞİL ölçütleri içerir.

Kullanıcı hukukçu değilse imza öncesi yetkili hukukçu onay kapısı ekle.

### SARI (`YELLOW`) — Hukukçu İncelemesi Gerekli
Şu hallerde verilir:
- Bir veya daha fazla hüküm playbook'tan sapıyor ama kırmızı çizgiye çarpmıyor,
- İlgili konuda playbook sessiz,
- NDA dışı yan yükümlülük içeriyor,
- KVKK, rekabet hukuku veya yabancı hukuk unsuru değerlendirme gerektiriyor.

### KIRMIZI (`RED`) — Durdurun, Hukuk Birimine Yönlendirin
Şu hallerde verilir:
- Asla kabul edilmeyecek kırmızı çizgilerden biri tetikleniyor,
- Tek taraflı yapı işin doğasıyla bağdaşmıyor,
- Süre veya bakiye hükümler (`survival`) playbook sınırını aşıyor,
- Üst sınırsız veya fahiş cezai şart içeriyor,
- Yasaklı yabancı hukuk/yabancı mahkeme bulunuyor,
- Onaysız yurt dışı veri aktarımı (`KVKK m. 9`) veya model eğitimi izni içeriyor.

## Türk Hukuku Kontrol Listesi

Her NDA için şu kalemleri denetle:
- taraflar ve temsil/imza ehliyeti,
- karşılıklılık (`mutuality`),
- gizli bilginin tanımı ve sözlü ifşaların yazılı teyit koşulu,
- izin verilen amaç (`permitted purpose`),
- zorunlu istisnalar (kamuya açık bilgi, bağımsız geliştirme, üçüncü kişiden hukuka uygun elde etme),
- mahkeme / savcılık / düzenleyici kurum talebiyle mecburi açıklama ve bildirim istisnası,
- iade/imha ve otomatik yedekleme (`backup/archive`) istisnası,
- gizlilik süresi ve bakiye hükümler,
- ticari sır (`TTK m. 54–55`) ve hafızada kalan bilgi (`residuals`),
- FSEK/IP devri veya lisans kısıtları,
- cezai şart (`TBK m. 179–182`, `TTK m. 22`),
- uygulanacak hukuk, yetkili mahkeme/icra veya tahkim,
- KVKK kişisel veri aktarımı ve varsa rakipler arası rekabet hassasiyeti (`4054 s. K.`).

## KVKK Kontrol Bloğu

```yaml
kvkk:
  kisisel_veri_paylasimi: true | false | belirsiz
  ozel_nitelikli_veri: true | false | belirsiz
  rol: veri_sorumlusu | veri_isleyen | ortak_sorumluluk | belirsiz
  veri_isleme_sozlesmesi_gerekli: true | false | belirsiz
  yurt_disina_aktarim: true | false | belirsiz
  not: "KVKK m. 9 ve ikincil mevzuat uyarınca standart sözleşme (5 iş günü Kurum bildirimi) kontrol edilmeli."
```

## Rekabet Hukuku Kontrol Bloğu

Taraflar rakip veya potansiyel rakipse ekle:

```yaml
rekabet_hukuku:
  rakipler_arasi_paylasim: true | false | belirsiz
  hassas_bilgi: fiyat | musteri | maliyet | strateji | kapasite | none | belirsiz
  not: "Rekabete hassas bilgi paylaşımı varsa 4054 s. Kanun açısından hukukçu incelemesine yönlendir."
```

## Çıktı Formatı

`CLAUDE.md` içindeki `## Outputs` → `### Work Product Header` başlığını ve `Reviewer note` bloğunu ekleyerek sun:

```markdown
## NDA Triyajı: [Karşı Taraf]

**Durum:** YEŞİL | SARI | KIRMIZI
**Taraf:** sales-side | purchasing-side | mutual
**Uygulanan playbook:** [`CLAUDE.md` referansı]

### Yönetici Özeti
[Temiz YEŞİL NDA ise tek cümle. Risk varsa aksiyon odaklı kısa maddeler.]

### Kontroller
| Kontrol | Durum | Dayanak |
|---|---|---|
| [Kontrol kalemi] | uygun / sapma / belirsiz | [Playbook / TBK / TTK / KVKK] |

### İşaretlenen Maddeler
**1. [Konu] — Madde [X]**
- Alıntı: "[kısa birebir alıntı]"
- Neden sorun: [sade Türkçe gerekçe]
- Öneri: [kabul et / daraltarak revize et / eskale et / bizim taslağı öner]

### Sonraki Adım
[İmza sürecine yönlendir / hukuka sor / durdur]
```

Temiz bir YEŞİL NDA için uzun bilgi notu yazma; yalnızca triyaj sonucunu, kontrol tablosunu ve sonraki adımı ver.

## Redline Hassasiyeti

En küçük işe yarar düzeltmeyi seç:
- sözcük değişikliği ifade değişikliğinden,
- ifade değişikliği cümleden,
- cümle değişikliği tüm madde değişiminden önce gelir;
- tam madde yenilemesi yalnızca cerrahi düzeltme okunaksız olacaksa yapılır ve gerekçesi yazılır.

## Bu Beceri Neleri Yapmaz

- Karşı tarafla doğrudan müzakere etmez.
- Sıfırdan yeni NDA yazmaz.
- SARI veya KIRMIZI maddelerde kesin onay kararı vermez.
- İmza yetkilendirmesi yapmaz veya imza sirküleri doğrulaması yerine geçmez.
- Yabancı hukukta kesin hukuki görüş vermez.
