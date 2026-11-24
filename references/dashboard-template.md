# Pano (Dashboard) Çıktı Şablonu

*Veri yoğun çıktılarda (`>10` satır) sunulan pano teklifi için standart şablon. Amaç görsel gösteriş değil, hızlı taranabilirliktir.*

## Yukarıdan Aşağıya Standart Yapı

1. **Başlık ve üst bilgi:** Konu, üretim tarihi ve kapsam (tek satır).
2. **Özet istatistikler:** Önem derecesine göre sayımlar — ör. `"40 bulgu: 🔴 3 bloke · 🟠 8 yüksek · 🟡 15 orta · 🟢 14 düşük — 6 tanesi bu hafta vadeli."`
3. **İnceleyici notu (Reviewer note):** Standart tek blok formatı (kaynaklar, okuma kapsamı, doğrulama bayrakları, aksiyon öncesi kontroller). Panoda da güvenlik üst verisi asla atlanmaz.
4. **Grafik(ler) — en fazla 1 veya 2:**
   - **Risk dağılımı** (çubuk grafik): önem derecesine göre sayılar.
   - **Kategori dağılımı** (yatay/yığılmış çubuk): sözleşme türü, açık kaynak lisansı veya dava türü dağılımı.
   - **Zaman çizelgesi** (sıralı tablo / basit Gantt): yenileme son tarihleri, kesin süreler veya kapanış adımları.
5. **Tablo:** Sıralanabilir, filtrelenebilir ve önem/durum renk kodlu tablo. Ekrana sığan temel sütunlar önde, `"Notlar / Ayrıntı"` sütunu en sonda yer alır.
6. **Karar ağacı ("Sıradaki Adım Ne?"):** Metin çıktısındaki karar seçeneklerinin aynısı.

## Yüzeye Göre Üretim

- **Cowork / Claude Desktop:** Tek dosya, kendi kendine yeten HTML çıktısı (satır içi CSS; haricî CDN, font veya npm bağımlılığı yok; yalnızca hafif satır içi sıralama/filtreleme JS'i).
- **Claude Code:** Aynı HTML dosyasını `~/.claude/plugins/config/legal-turkish/<eklenti>/outputs/dashboard-<konu>-<tarih>.html` yoluna yaz ve kullanıcıya tarayıcıda açmasını bildir. Terminalde hızlı görünüm için Unicode blok çubuklu kısa Markdown özetini de göster (ör. `🔴 ███ 3  🟠 ████████ 8  🟡 ██████████ 10`).
- **Excel / CSV (uygun yerlerde):** `tabular-review`, `renewal-tracker`, `entity-compliance` gibi toplantıya götürülecek çıktılarda mevcut Excel/CSV dışa aktarım kuralını ve formül enjeksiyonu savunmasını (`=`, `+`, `-`, `@`, `\t`, `\r` önek kaçışı) uygula.

## Güvenilmez Girdi Kaçışı (Zorunlu Güvenlik Kuralı)

Bu oturum dışından gelen her veri (karşı taraf sözleşme metni, OSS paket/lisans alanı, VDR belgesi, karşı taraf/tedarikçi adı, dosya açıklaması) HTML belgesine yazılmadan önce **mutlaka kaçırılmalıdır (HTML-escape)**:

- Hücrelerde, özet satırlarında, grafik etiketlerinde ve ipuçlarında `&`, `<`, `>`, `"`, `'` karakterlerini HTML entity'lerine dönüştür.
- Satır içi JS sıralama/filtreleme kodunda hücre metnini **asla `innerHTML` ile değil, yalnızca `textContent` ile** yaz.
- Güvenilmez string'leri `<script>` blokları içine doğrudan gömme.
- `href` veya `src` niteliklerine yazılan URL'lerde şema kontrolü yap (yalnızca `http:`, `https:`, `mailto:`).

## Sade ve Tutarlı Tasarım

- **Renk paleti:** Önem için kırmızı / turuncu / sarı / yeşil; nötr için gri; durum için mavi.
- **Animasyon, haricî kütüphane veya haricî font kullanma:** Çevrimdışı ortamda da eksiksiz açılmalıdır.
