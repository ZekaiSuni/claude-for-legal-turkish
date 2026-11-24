# Google Sheets Çıktı Şartnamesi

Google Workspace kullanan ekipler için Excel şartnamesiyle aynı mantıksal yapıda çıktı kurallarıdır. Hem Excel hem Google Sheets kullanılabilirse tahmin etme; kullanıcıya tercihini sor.

## Yazma Yolları (Öncelik Sırasıyla)

1. **Google Sheets MCP** (yazma/oluşturma yetkili bir Sheets veya Drive bağlantısı mevcutsa API üzerinden e-tabloyu ve sayfaları oluştur).
2. **Google Sheets API (ADC)** (`google-api-python-client` ve yetkili Google hesabı hazırsa `sheets.spreadsheets().create()` ve `batchUpdate` ile biçimlendir).
3. **Fallback: CSV + manuel içe aktarım:** `.csv` dosyalarını ve `format-instructions.md` yönergesini üret.

Doğrulamadığın yazma yetkisini var sayma; erişimi önce kontrol et, yoksa temiz biçimde fallback'e geç.

## Çalışma Kitabı Yapısı

Excel şartnamesindeki dört sayfa düzeni korunur:
- **`Review`:** Satır 1'de `CLAUDE.md` `## Çıktı kuralları` gizli çalışma taslağı başlığı; Satır 2'de başlıklar; Kolon A'da belge adı (Drive'da ise dosyaya köprü/hyperlink); her veri kolonunda birebir alıntı ve konum **hücre notu (`note`)** olarak eklenir (Sheets yorumları sohbet dizisidir, notlar kalıcıdır ve `.xlsx` dışa aktarımında yoruma dönüşür); durum renkleri ve `✓ | ✗ | ?` veri doğrulamalı `Verified` kolonu eklenir.
- **`Flags`:** `unclear` / `needs_review` hücrelerinin kuyruğu.
- **`_schema`:** `.review-schema.yaml` tanımları.
- **`_summary`:** Sayımlar, işaretli kolonlar ve doğrulama hatırlatması.

## Google Sheets'e Özgü Avantajlar ve Dikkat Noktaları

- **Kaynak belgelere doğrudan bağlantı:** Belgeler Google Drive'daysa satır başlıklarına Drive linki ver.
- **Paylaşım varsayılanı (Gizlilik Kuralı):** Bu çıktı gizli hukuki çalışma taslağıdır. Tabloyu yalnızca oluşturan kişiye açık (restricted) şekilde üret; asla `"bağlantıya sahip herkes"` olarak açma ve paylaşım uyarısı ver.
- **Yazdırma notu:** Hücre notları kâğıt/PDF çıktısında görünmez; toplantı çıktısı alınacaksa alıntıları `Flags` sayfasında da tut.
- **10 milyon hücre sınırı:** Çok büyük arşivlerde (>20.000 belge × 30 kolon) önceden uyar ve böl.

## Yapılmayacaklar ve Formül Enjeksiyonu Savunması

- Güven yüzdesi ekleme, alıntı kesme, veri alanında hücre birleştirme yapma; `_schema` ve `_summary` sayfalarını mutlaka ekle.
- Karşı taraf/belge kaynaklı `=`, `+`, `-`, `@`, `\t`, `\r` veya `\n` ile başlayan her hücreyi tek tırnak (`'`) ile kaçışla (ör. sözleşmedeki `- Taraflar anlaşmıştır...` alıntısının formül hatası vermemesi için zorunludur); CSV aktarımlarında RFC 4180 kurallarını uygula.
