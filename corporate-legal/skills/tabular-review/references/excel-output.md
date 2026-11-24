# Excel Çıktı Şartnamesi (`.xlsx`)

İşlem ekiplerinin ve avukatların fiilen açacağı ana teslimat Excel dosyasıdır; düzen, izlenebilirlik ve güvenlik kuralları eksiksiz uygulanmalıdır.

## Üretim Yöntemi

1. Excel / Office ajanı kullanılabilirse çalışma kitabını doğrudan oluştur.
2. Kullanılamıyorsa Python `openpyxl` kontrolü yap (`python -c "import openpyxl"`); yoksa kurmayı öner veya `.csv` fallback üret.

## Çalışma Kitabı Yapısı

**Sayfa 1: `Review` (Ana İnceleme Tablosu)**
- Satır 1: `CLAUDE.md` `## Çıktı kuralları` başlığından gizli çalışma taslağı uyarısı (birleştirilmiş üst satır: `GİZLİ HUKUKİ ÇALIŞMA TASLAĞI - AVUKAT/HUKUKÇU İNCELEMESİNE TABİDİR`).
- Satır 2: Kolon başlıkları.
- Satır 3+: Belge başına bir satır.
- Kolon A: Belge adı / dosya yolu.
- Kolon B ve sonrası: Şema sırasıyla veri kolonları.
- Her veri kolonunun hemen ardından gizli `_source` kolonu (`[birebir_alıntı] | [konum]`).
- Veri hücresine yorum (`comment`) olarak alıntı ve konum eklenir (gizli kolon açılmadan üzerine gelince görünsün diye).
- Durum renklendirmesi (`state`): dolgusuz = `answered`, `#FFF2CC` (açık sarı) = `unclear` veya `needs_review`, `#EFEFEF` (açık gri) = `not_present`.
- Her `[veri + _source]` grubunun ardından boş bırakılan `Verified` kolonu; veri doğrulama açılır listesi (`✓`, `✗`, `?`) ile avukat teyidi izlenir.

**Sayfa 2: `Flags` (Doğrulama İş Kuyruğu)**
- `unclear` veya `needs_review` işaretli her hücre için bir satır: Belge, Kolon, Durum (`State`), Değer, Alıntı (`Quote`), Konum (`Location`), Not. Kolona göre sıralanır.

**Sayfa 3: `_schema`**
- `.review-schema.yaml` içindeki kolon tanımları (`id`, `label`, `type`, `options`, `prompt`) — çalışma kitabını kendi kendine belgeler.

**Sayfa 4: `_summary`**
- Belge sayısı, kolon sayısı, çalıştırma tarihi, kolon başına `answered` / `not_present` / `unclear` / `needs_review` sayıları, normalleştirme taramasında işaretlenen kolonlar ve doğrulama hatırlatması.

## Yapılmayacaklar

- Yüzdelik güven skoru kolonu ekleme; gerçek sinyal durum ve birebir alıntıdır.
- Hücreye sığsın diye alıntıyı kesme/kırpma (metni kaydır ve tam metni yoruma/gizli kolona yaz).
- Veri bölgesinde hücre birleştirme (`merge`) yapma (sıralama ve filtrelemeyi bozar).
- `_schema` ve `_summary` sayfaları olmadan dosya üretme.

## Formül Enjeksiyonu Savunması (Formula Injection Defense)

Excel, Google Sheets veya CSV çıktısına yazılan **karşı taraf veya dış kaynaklı her metin** (sözleşme alıntısı, taraf unvanı, dosya adı, kullanıcı yapıştırması) potansiyel olarak güvenilmez girdi sayılır. Hücre değeri `=`, `+`, `-`, `@`, `\t`, `\r` veya `\n` ile başlıyorsa formül olarak yorumlanabilir veya satır yapısını bozabilir:

- **Başına tek tırnak (`'`) ekle:** `'=SUM(A1:A10)` (metin olarak görüntülenir, çalıştırılmaz).
- **Kapsam:** Belgelerden, araç çıktılarından veya kullanıcı yapıştırmasından gelen tüm hücrelere zorunlu uygula (yalnızca kendi ürettiğin sabit kolon başlıkları ve hesaplanmış özet sayılar hariçtir).
- **CSV:** Virgül, çift tırnak ve satır sonlarını RFC 4180 kurallarına göre kaçışla.
