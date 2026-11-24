---
name: chronology
description: >
  Beyan edilen kaynaklardan, UYAP evraklarından ve yüklenen belgelerden Türk
  dava ve uyuşmazlık pratiğine uygun tarihli olay kronolojisi oluşturur veya
  günceller. Tarihli olguları çıkarır, mükerrer kayıtları birleştirir, dava
  teorisine göre önem derecesi atar; eksik delilleri, KVKK/gizlilik risklerini
  ve HMK/İİK süre risklerini işaretler.
argument-hint: "[matter slug] [--format=working|facts|witness-[ad]]"
---

# /chronology

Belge ve kaynaklardan tarihli olayları çıkararak dava teorisine bağlı bir kronoloji oluşturur. Çıktı delil sadakati gerektirir; kaynaklanmayan olaylar kesin vakıa gibi yazılmaz (`[DOĞRULA]` veya `[BELİRSİZ]` olarak işaretlenir).

## Talimatlar

1. `~/.claude/plugins/config/legal-turkish/litigation-legal/CLAUDE.md` dosyasını (`## Bunu Kim Kullanıyor`, `## Çıktılar (Outputs)`) oku.
2. `matter slug` verilmişse veya `## Matter workspaces` altında aktif matter varsa `matter.md`, dava teorisi, bilinen dilekçeler ve delil dizinini yükle.
3. Kaynakları şu sırayla tara:
   - kullanıcının doğrudan verdiği dosyalar,
   - aktif matter klasörü,
   - tanımlı belge depoları,
   - ilgili ve kullanıcının sağladığı UYAP/UETS/KEP kayıtları.
4. Tarihli olayları çıkar (kesin tarih yoksa yaklaşık olduğunu belirt).
5. Mükerrer olay kayıtlarını birleştir.
6. Dava teorisi altındaki önem düzeyini işaretle.
7. İstenen formatta (`working`, `facts` veya `witness-[ad]`) çıktı üret.

## Kaynaklar

Tipik kaynaklar:

- dava dilekçesi ve ekleri,
- cevap / cevaba cevap / ikinci cevap dilekçeleri,
- noter veya KEP ihtarnameleri,
- e-posta ve yazışma kayıtları,
- sözleşme ve ek protokoller,
- fatura, irsaliye ve ödeme/dekont kayıtları,
- yönetim kurulu / toplantı tutanakları,
- UYAP evrakları, tensip ve duruşma zabıtları,
- bilirkişi ve uzman mütalaaları,
- tanık bilgi notları,
- ticaret sicili / tapu / noter gibi resmî kayıtlar.

## KVKK ve Gizlilik

Kişisel veri, 6698 s. KVKK m. 6 kapsamındaki özel nitelikli kişisel veri, sağlık verisi, çalışan özlük verisi veya üçüncü kişi bilgisi geçerse işaretle ve veri minimizasyonu uygula. Geniş dağıtımlı çıktılarda gereksiz kimlik bilgilerine (T.C. kimlik no, açık adres vb.) yer verme.

## Olay Kaydı Yapısı

```yaml
event:
  date: ""
  title: ""
  description: ""
  source: ""
  confidence: high | medium | low
  importance: critical | relevant | background
  theory_link: ""
  deadline_effect: ""
```

Tarih yaklaşık veya yalnızca aya/yıla ilişkinse bunu açıkça belirt.

## Çıktı Formatları

### Çalışma Kronolojisi (`working`)

```markdown
# Kronoloji - [Dosya / Matter]

## Zaman Çizelgesi
| Tarih | Olay | Kaynak | Güven | Önem |
|---|---|---|---|---|
| [YYYY-AA-GG] | [olay özeti] | [kaynak/UYAP evrak no] | [high/medium/low] | [critical/relevant/background] |

## Kritik Vakıalar
[Kısa hukuki değerlendirme]

## Eksikler ve Teyit Edilecekler
- [Eksik delil / teyitsiz tarih / vakıa boşluğu]

## Süre Etkileri (Zamanaşımı / Hak Düşürücü Süre / Usul)
- [Zamanaşımı, cevap/itiraz süresi, arabuluculuk son tutanağı, istinaf/temyiz süresi etkisi]
```

### Vakıalar Formatı (`facts`)

Dava veya cevap dilekçesinin "Açıklamalar / Vakıalar" bölümü için yalnızca birebir kaynaklanmış, ispat vasıtası bulunan olayları kronolojik olarak listeler.

### Tanık / İsticvap Formatı (`witness-[ad]`)

Tanık beyanı veya isticvap hazırlığı için kullanılır. Kesinlikle hayali tanık beyanı uydurmaz; tanığa sorulacak konular, gösterilecek belgeler ve teyit edilecek çelişkileri listeler.

## Önem Etiketlemesi

- `critical`: Dava teorisi veya davanın esası açısından belirleyici vakıa.
- `relevant`: Yardımcı ve bağlam kurucu vakıa.
- `background`: Arka plan bilgisi.

Dava teorisi tanımlanmamışsa kullanıcıdan iste ya da tarafsız kronoloji üret.

## Yapmadıkları

- Delilin hukuken caiz veya ispat gücüne yeterli olup olmadığına kesin hüküm vermez (avukat değerlendirir).
- Tanık beyanı veya olgu uydurmaz.
- UYAP üzerinden dilekçe veya delil göndermez.
- Tebliğ/tefhim ve UETS 5. gün başlangıç tarihlerini (7201 s. Tebligat K. m. 7/a) birincil belgeden doğrulamadan kesin hak düşürücü süre veya zamanaşımı son günü ilan etmez.
- `Cross-matter context` açık ve talep edilmiş olmadıkça başka dosya klasörünü okumaz.
