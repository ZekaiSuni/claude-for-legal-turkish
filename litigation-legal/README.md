# Litigation (Dava ve Uyuşmazlık) Eklentisi

Şirket içi dava/uyuşmazlık (litigation) müşavirleri için portföy yönetim desteği. "Cold-start" süreci; risk kalibrasyonunuzu, uyuşmazlık haritanızı ve şirket içi dilinizi (house style) öğrenerek tüm yeni uyuşmazlıkları bu çerçevede değerlendirir. Standart kayıt (intake) süreci, yeni uyuşmazlıkları yapılandırılmış kütüphane kayıtlarına ve dosyaya özel tarihçe dosyalarına dönüştürür. UYAP entegrasyonu veya manuel takiple portföy özetleri ve derinlemesine bilgilendirmeler bu loglardan okunur.

Dosyalarının çoğunu dış hukuk büroları (outside counsel) aracılığıyla yürüten, aynı anda birçok dosyayı yöneten hukuk müşavirleri için tasarlanmıştır. Bu eklenti bir Dava Yönetim Sistemi (örn. UYAP Kurum / LawVu / SimpleLegal) değil, onun yanında çalışan **yapılandırılmış bir akıl yürütme katmanıdır**.

**Üretilen her çıktı, avukat onayı gerektiren, kaynakları belirtilmiş, işaretlenmiş ve güvenlik sınırlarıyla (gate) çevrelenmiş bir taslaktır — kesin bir hukuki sonuç değildir.** Eklenti ön çalışmayı yapar: Belgeleri okur, playbook'unuzu uygular, uyuşmazlık noktalarını bulur ve bilgi notu taslağını hazırlar. Ruhsatlı bir avukat inceler, doğrular ve karar verir. Atıflar kaynağına göre etiketlenir, böylece hangisinin kullanıcı tarafından sağlanan UYAP veya ticari veri tabanı dışa aktarımından geldiğini, hangisinin model bilgisi olup doğrulanması gerektiğini bilirsiniz. Gizlilik işaretleri (`Av.K. m. 36` vb.) ihtiyatlı biçimde uygulanır; dava açma, ihtarname çekme veya sözleşme feshi gibi kritik adımlar açık onay alınmadan gerçekleştirilmez.

## Ön Koşullar

Bazı özellikler Gmail, KEP (Kayıtlı Elektronik Posta) ve zamanlanmış görev (scheduled-tasks) entegrasyonlarına referans verir. Bunlar ortamınızda kurulu MCP sunucuları gerektirir — paketle birlikte gelmez. Bunlar yoksa, çıktılar manuel gönderim için dosyalara yazılır:

- **Email MCP (Gmail vb.)** — `/oc-status`, yetkilendirilmişse taslak e-postalar oluşturur; aksi halde `oc-status/[YYYY-MM-DD]/[kisa_ad].md` dizininde markdown taslaklarına düşer.
- **Zamanlanmış görev MCP'si** — Otomatik zamanlama dâhil değildir. Haftalık komutları çağırmak için tekrarlayan bir takvim hatırlatıcısı ayarlayın.

Eklenti bunların hiçbiri olmadan da uçtan uca çalışır; entegrasyonlar sadece süreci hızlandırır.

## Kimin İçin?

| Rol | Ana Kullanım Alanı |
|---|---|
| **Şirket İçi Dava/Uyuşmazlık Avukatı** | Tümü — kayıt (intake), önceliklendirme (triage), durum raporu, tarihçe, brifing |
| **Müşavir Yrd. (Deputy GC)** | Portföy gözetimi, yönetim kurulu raporlama özetleri |
| **Başhukuk Müşaviri (GC)** | Portföy hakkında hızlı durum raporu, herhangi bir davaya derinlemesine bakış |

## İlk Çalıştırma: Cold-Start

Cold-start (ilk kurulum) mülakatı, her dosyada geçerli kalacak olan *kurumsal* (house) uyuşmazlık profilini oluşturur. Üç ana sacayağı:

- **Risk kalibrasyonu** — Risk iştahı, önem (materiality) eşikleri, karşılık (reserve) ayırma ve SPK/KAP bildirim tetikleyicileri, sulh/uzlaşma yetkisi, sigorta profili (D&O vb.), etki-olasılık matrisi.
- **Harita (Landscape)** — Şirket profili, operasyon bölgeleri, sektörel düzenlemeler, uyuşmazlık tipleri, sık karşılaşılan karşı taraflar, çalışılan dış hukuk büroları, iç paydaşlar.
- **Kurum dili (House style)** — Yönetim / denetim kurulu rapor formatı, karşılık (reserve) notu formatı, dış bürolara talimat tarzı, Avukat-Müvekkil Gizliliği uyarıları ve eskalasyon kuralları.

Her adımda mantıklı varsayılanlar (örn. 3x3 etki-olasılık matrisi) sunar ve her şeyi serbestçe düzenlenebilir tutar. Eğer henüz yazılı bir çerçeveniz yoksa, bu süreç sizi bunu formüle etmeye zorlayacaktır.

```
/litigation-legal:cold-start-interview
```

Yapılandırmanız `~/.claude/plugins/config/legal-turkish/litigation-legal/CLAUDE.md` konumunda saklanır ve eklenti güncellemelerinden etkilenmez.

## Komutlar

| Komut | İşlevi |
|---|---|
| `/litigation-legal:cold-start-interview` | Kurulum → Kurumsal profili yazar: `CLAUDE.md` |
| `/litigation-legal:customize` | Mevcut kurumsal profili, eşikleri veya evrak tercihlerini günceller |
| `/litigation-legal:matter-workspace` | Çok müvekkilli veya dosya bazlı çalışmalarda dosya bağlamını yönetir |
| `/litigation-legal:matter-intake` | Standart Kayıt → `matters/[kisa_ad]/` yazar ve `_log.yaml`'a ekler (Arabuluculuk şartı, Dava/Harç Değeri vb. dâhil) |
| `/litigation-legal:portfolio-status` | Portföy Özeti — Risk dağılımı, yaklaşan kesin süreler/duruşmalar, hareketsiz dosyalar |
| `/litigation-legal:matter-briefing [slug]` | Tek dosyaya derin bakış — Başmüşavir veya dış büro toplantısı öncesi okumaya hazır brifing |
| `/litigation-legal:matter-update [slug]` | Dosya tarihçesine tarihli bir olay (Örn. Tensip, Ara Karar) ekler; logdaki `last_updated` bilgisini yeniler |
| `/litigation-legal:matter-close [slug]` | Dosyayı aktif portföyden çıkararak arşivler (silinmez, elde tutulur) |
| `/litigation-legal:brief-section-drafter` | Dava/cevap/istinaf dilekçesi bölümlerini kayıt ve hukuk atfı disipliniyle taslaklar |
| `/litigation-legal:deposition-prep` | HMK isticvap ve tanık/taraf sorgusuna hazırlık soru seti ve çelişki taraması hazırlar |
| `/litigation-legal:privilege-log-review` | `Av.K. m. 36` ve Rekabet Kurumu yerinde inceleme sınırlarına göre gizlilik dökümü inceler |
| `/litigation-legal:demand-intake [başlık]` | İhtarname (Ödeme/Fesih/İhlal vb.) öncesi bağlam toplama aşaması |
| `/litigation-legal:demand-draft [slug]` | İhtarname taslağını oluşturur — Gizlilik filtrelerinden geçer, `.docx` üretir, noter/KEP gönderim kontrol listesi yazar |
| `/litigation-legal:demand-received [yol]` | Gelen ihtarname/icra emri triyajı — Seçenek analizi (Cevap verme/menfi tespit vs.), portföy çapraz kontrolü |
| `/litigation-legal:subpoena-triage [yol]` | Kurum/Mahkeme/Savcılık Müzekkeresi (Subpoena) triyajı — Bilgi/belge talebini sınıflandırır (KVKK m.28 dengesi), itiraz çerçevesi ve yanıt planı üretir |
| `/litigation-legal:legal-hold [slug] [--issue/--refresh/--release/--status]` | Şirket İçi Kayıt/Delil Muhafaza Talimatı — İlgili birimlere (IT, İK) "silmeyin" ihtarı yazar ve Delil Tespiti (HMK m. 400) hazırlığı yapar |
| `/litigation-legal:chronology [slug]` | İddia/Savunmanın genişletilmesi yasağına hazırlık — Sunulan belgelerden veya dosyalardan kronoloji çıkarır, her olayı uyuşmazlık teorisine göre etiketler |
| `/litigation-legal:oc-status` | Dış hukuk bürolarından haftalık UYAP / dava safahat raporu isteyen taslaklar (Email MCP varsa direkt Gmail taslağı) |
| `/litigation-legal:claim-chart` | Unsur Tablosu (Claim Chart) — Fikri Sınai Haklar (Patent/Marka tecavüzü, hükümsüzlük) veya ticari davalar için boşluk tespiti sağlayan iddia-delil eşleştirme şeması |

## Ajanlar (Agents) - Zamanlanmış Görevler

| Ajan | Neyi İzler | Varsayılan Periyot |
|---|---|---|
| **docket-watcher** | Aktif portföydeki dosyalar için UYAP evrak/duruşma takibi — Yeni tebligatları çeker, itiraz/cevap sürelerini hesaplar, dosya tarihçesiyle eşleştirir | Haftalık |

## Veri Nasıl Organize Edilir?

```
litigation-legal/
├── CLAUDE.md                          # KURUMSAL profil — risk, harita, dil
├── matters/
│   ├── _log.yaml                      # portföy defteri (her dosya için bir satır)
│   └── [dosya-kisa-adi]/
│       ├── matter.md                  # dosyaya özel intake + teori + usul (HMK/Yetki/Görev)
│       ├── history.md                 # ekleme-yapılabilir olay günlüğü (safahat)
│       ├── chronology.md              # savunmaya yönelik zaman çizelgesi
│       └── legal-hold-v[N].docx       # şirket içi delil muhafaza bildirimleri
├── demand-letters/                    # giden ihtarnameler
│   └── [slug]/
│       ├── intake.md
│       ├── draft-v1.docx
│       └── checklist.md
├── inbound/                           # gelen ihtarnameler, icra emirleri, müzekkereler
│   └── [slug]/
│       ├── incoming.[ext]
│       ├── triage.md
│       └── response-v1.docx           # eğer yanıt veriyorsak
└── oc-status/                         # haftalık dış büro safahat durumu taslakları
    └── [YYYY-MM-DD]/
        ├── _summary.md
        └── [slug].md                  # her dosya için bir email
```

## Bağlantılar (Connectors) ve Atıf Doğrulama

**Hukuk araştırma veya UYAP aracınız varsa bağlayın — atıf güvenlik sınırları buna dayanır.** Bağlı bir araç yoksa, her hukuki atıf `[verify/doğrula]` olarak etiketlenir. Eklenti her iki durumda da çalışır; ancak bir araştırma aracı bağlıysa, doğrulama yükünün çoğunu kendisi üstlenir.

## Öğrenme ve Notlar

Kurumsal profil statik değildir; siz kullandıkça gelişir. `_log.yaml` portföy durumunun tek gerçeğidir (source of truth).
- Açılan davalar veya ihtilaflar için Avukat-Müvekkil Gizliliği notlarına her zaman sadık kalınır. (Avukatlık Kanunu m. 36)
- **Delil Tespiti ve Muhafaza:** Türk hukukunda spoliation (delil karartma) sonucu davayı baştan kaybetme (US usulü) kuralı olmasa da; HMK gereği ibrazdan kaçınma (m. 220) ve TCK m. 281 delil karartma risklerine karşı `legal-hold` mekanizması "Şirket İçi Saklama Talimatı" olarak kurgulanmıştır.

## Çıktı Üzerindeki İşaretler (Markers)

- `[CITE: ilgili madde/karar]`: Hukuki otorite boşluğu. Avukat doldurur veya onaylar.
- `[VERIFY: spesifik olgu]`: Kaynağı doğrulanmamış olgusal beyan.
- `[SME VERIFY: uzman görüşü]`: Uzman (avukat) kararı gerektiren subjektif yorum (örn. itiraz gücü, kazanma şansı, gizlilik statüsü).

