# Administrative & Tax Legal (İdare ve Vergi Uyuşmazlıkları Eklentisi)

Türk İdare ve Vergi Hukuku uyuşmazlıkları (2577 s. İYUK, 213 s. VUK, 6183 s. AATUHK, 5326 s. Kabahatler Kanunu, 4734 s. Kamu İhale Kanunu, 7201 s. Tebligat Kanunu) için sıfırdan tasarlanmış yerli Claude Code hukuk eklentisi.

## Öne Çıkan Yetenekler

- **UETS & GİB e-Tebligat Süre Hesabı:** `7201 m. 7/a` ve `VUK m. 107/A` 5. gün sonu kuralı, `7331 s. K.` 30 günlük zımni ret ve `İYUK m. 61` 20 Temmuz–31 Ağustos çalışmaya ara verme (7 Eylül uzaması) hesabı.
- **İptal/Tam Yargı ve Yürütmenin Durdurulması (`İYUK`):** 60/30 gün dava süresi, `m. 20/A` ivedi yargılama, `m. 27` YD (ve 7 gün itiraz) ile `m. 27/4` vergi davasında otomatik durma vs. ihtirazi kayıt/ödeme emri istisnası.
- **Vergi İncelemesi ve `7524 s. K.` Sonrası Karar Matrisi:** Tarhiyat sonrası uzlaşmada vergi aslının çıkarılması sonrası güncel `Dava` vs. `Uzlaşma (Salt Ceza)` vs. `VUK m. 376 %50 İndirim` vs. `İzaha Davet / Pişmanlık` analizi.
- **`6183 s. AATUHK` Tahsilat Savunması:** Ödeme emrine 15 günlük itiraz (`m. 58`), AYM `2021/119 E.` %10 haksız çıkma zammı iptali notu, e-haciz kaldırma, `m. 48` tecil ve `m. 35` / `Mük. m. 35` ortak/kanuni temsilci sorumluluğu.
- **İdari Para Cezaları & Kamu İhalesi (`5326` & `4734`):** İdare Mahkemesi (60 gün) vs. Sulh Ceza Hâkimliği (15 gün) görev ayrımı, %25 peşin ödeme indirimi ve `4734 m. 55–56` zorunlu şikâyet/itirazen şikâyet zinciri.

## Komutlar (Skills)

| Komut | Açıklama |
|---|---|
| `/administrative-tax-legal:cold-start-interview` | Mükellef/kurum/büro idari ve vergi profilini yapılandırır |
| `/administrative-tax-legal:customize` | Taraf duruşu, uzlaşma eşikleri ve güncel oran tercihlerini günceller |
| `/administrative-tax-legal:matter-workspace` | Yeni vergi/idari dava dosyası için çalışma klasörü ve doğrulama günlüğü kurar |
| `/administrative-tax-legal:uyusmazlik-portfolio` | `idari-vergi-register.yaml` portföyünü tarar, süre/risk özeti ve HTML pano üretir |
| `/administrative-tax-legal:idari-dava-ve-yd` | 2577 s. İYUK iptal/tam yargı, zımni ret (30 gün), `m. 20/A` ve YD stratejisini kurar |
| `/administrative-tax-legal:vergi-uyusmazlik` | VUK inceleme, ihbarname 30 gün matrisi (dava/uzlaşma/376) ve `m. 359` riskini inceler |
| `/administrative-tax-legal:kamu-alacagi-6183` | 6183 ödeme emri (15 gün), ihtiyati haciz, e-haciz, tecil ve kanuni temsilci takibini yönetir |
| `/administrative-tax-legal:idari-ceza-ve-ihale` | İdari para cezası merci ayrımı (İdare vs. Sulh Ceza) ve 4734 KİK şikâyet zincirini kurar |

## Arka Plan Ajanı (Agent)

- `admin-tax-deadline-watcher`: `idari-vergi-register.yaml` portföyünü tarayarak GİB `m. 107/A` / UETS 5. gün, 7 gün YD itiraz, 15 gün `6183 m. 58` / Sulh Ceza / `m. 20/A` temyiz, 10/5 gün KİK ve 30/60 gün İYUK dava sürelerini raporlar.

## Sürüm ve Bakım

- **Sürüm:** `1.1.0-tr`
- **Mevzuat Takibi:** Güncel parasal sınırlar, gecikme zammı/tecil faizi ve kanun değişiklikleri için [currency-watch.md](references/currency-watch.md) dosyasına bakın.
- **Konfigürasyon Yolu:** Kullanıcı özel şablonları `~/.claude/plugins/config/legal-turkish/administrative-tax-legal/` altında tutulur.
