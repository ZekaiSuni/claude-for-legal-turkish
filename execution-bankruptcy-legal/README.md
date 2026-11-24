# Execution & Bankruptcy Legal (İcra ve İflas Hukuku Eklentisi)

Türk İcra ve İflas Hukuku süreçleri (2004 s. İİK, 7201 s. Tebligat Kanunu, 6100 s. HMK, 6102 s. TTK, 6325 s. Arabuluculuk Kanunu) için sıfırdan tasarlanmış yerli Claude Code hukuk eklentisi.

## Öne Çıkan Yetenekler

- **UETS & Tebligat Süre Hesabı:** `7201 s. TK m. 7/a` uyarınca UETS elektronik tebligatta 5. gün sonu kuralı ve fiziki tebligatta `m. 21/2` / `m. 32` usulsüz tebligat denetimi.
- **Takip Stratejisi Seçimi:** İlamsız (`Örnek 7`), kambiyo (`Örnek 10`), kira/tahliye (`Örnek 13`), ilamlı (`Örnek 4-5`), rehin (`İİK m. 45`), ihtiyati haciz (`İİK m. 257`) ve ticari/iş uyuşmazlıklarında zorunlu arabuluculuk (`TTK m. 5/A`, `7036 m. 3`) etkileşimi.
- **İtiraz, Şikâyet ve 89/1-2-3 Triyajı:** Doğru merci (`İcra Dairesi` vs. `İcra Hukuk Mahkemesi` vs. `Genel Mahkeme`) ve hak düşürücü süre ayrımı; `7499 s. Kanun` sonrası 2 haftalık İİK kanun yolu süreleri.
- **Haciz, Maaş/Banka Haczi ve E-Satış (`İİK m. 106–111/b`):** Taşınır/taşınmaz hacizlerinde **1 yıllık** tek tip satış isteme süresi, `esatis.uyap.gov.tr` ihale hazırlığı, kıymet takdiri itirazı (`m. 128/a`) ve haczedilmezlik (`m. 82–83`).
- **Konkordato ve İflas Masası (`İİK m. 285–309`):** Geçici/kesin mühlet yasakları, `m. 299` 15 günlük alacak bildirimi, rehinli alacak istisnası (`m. 295`), `m. 206` sıra cetveli ve `m. 302` nisap kontrolü.

## Komutlar (Skills)

| Komut | Açıklama |
|---|---|
| `/execution-bankruptcy-legal:cold-start-interview` | Kurum/büro icra profilini ve onay eşiklerini yapılandırır |
| `/execution-bankruptcy-legal:customize` | Taraf duruşunu, faiz/para birimi ve eskalasyon kurallarını günceller |
| `/execution-bankruptcy-legal:matter-workspace` | Yeni icra/konkordato dosyası için standart çalışma klasörü oluşturur |
| `/execution-bankruptcy-legal:takip-portfolio` | `takip-register.yaml` portföyünü analiz eder, süre ve değer özeti/HTML pano üretir |
| `/execution-bankruptcy-legal:takip-strategy` | Uyuşmazlık için en uygun icra takip yolunu, faiz ve harç stratejisini belirler |
| `/execution-bankruptcy-legal:itiraz-ve-sikayet` | Ödeme emri itirazı, icra şikâyeti, 89/1-2-3 ve İİK m. 67/68/72 stratejisini kurar |
| `/execution-bankruptcy-legal:haciz-ve-satis` | Haciz kapsamı, maaş/banka haczi, 1 yıllık satış isteme ve e-satış sürecini yönetir |
| `/execution-bankruptcy-legal:konkordato-ve-iflas` | Konkordato mühlet etkileri, m. 299 alacak kaydı, sıra cetveli ve iflas tasfiyesini inceler |

## Arka Plan Ajanı (Agent)

- `execution-deadline-watcher`: Takip portföyünü tarayarak yaklaşan UETS/itiraz/şikâyet, 89/1-2-3, haciz düşme (`m. 106–110`) ve konkordato alacak kaydı sürelerini öncelik sırasıyla raporlar.

## Sürüm ve Bakım

- **Sürüm:** `1.1.0-tr`
- **Mevzuat Takibi:** Güncel parasal sınırlar, faiz oranları ve kanun değişiklikleri için [currency-watch.md](references/currency-watch.md) dosyasına bakın.
- **Konfigürasyon Yolu:** Kullanıcı özel şablonları `~/.claude/plugins/config/legal-turkish/execution-bankruptcy-legal/` altında tutulur.
