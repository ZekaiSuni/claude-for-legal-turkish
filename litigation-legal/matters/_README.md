# matters/ — Dava/Dosya Portföyü Verisi

Bu klasör aktif ve kapalı tüm dava portföyünü barındırır. İki katmanlıdır:

- **`_log.yaml`** — Kütük (ledger). Her dosya için bir satır. Beceriler (skills) tarafından makine okumasına uygundur. Özet raporlar (rollups) için yegane gerçeklik kaynağıdır.
- **`[kisa-ad]/`** — Dosya detayları. Hikaye, strateji ve safahat (history). İnsanların (avukatların) okuyup düzenlediği yer.

## Düzen (Layout)

```
matters/
├── _log.yaml                  # kütük (kapanmış dosyalar dahil hepsi)
├── _README.md                 # bu dosya
└── [dosya-kisa-adi]/
    ├── matter.md              # giriş/intake hikayesi + dava teorisi + hukuki durum (posture)
    └── history.md             # yalnızca ekleme yapılabilen (append-only) olay günlüğü / safahat
```

## İsimlendirme Kuralları (Slug conventions)

Küçük harfler, tire işaretleri ve sonda yıl. Örnekler:
- `acme-v-us-2026`
- `rekabet-kurumu-sorusturma-2026`
- `is-davasi-calisan-2026`

Yıl, ileride benzer bir dava ortaya çıksa bile dosya adını (slug) kalıcı/benzersiz yapar. Klasör adı, bu dosya adıyla tam olarak eşleşir.

## Kim Neyi Yazar?

| Dosya | Yazan/Oluşturan | Doğrudan Elle Düzenlenebilir mi? |
|---|---|---|
| `_log.yaml` | `/matter-intake`, `/matter-update`, `/matter-close` | Evet, ancak değişikliği dosyanın `history.md` günlüğüne de not edin. |
| `matter.md` | Açılışta `/matter-intake`; kapanışta `/matter-close` ek yapar. | Evet, değişen teori / strateji / hukuki durum notları için. |
| `history.md` | `/matter-intake` başlatır; `/matter-update` ve `/matter-close` ekler. | Pratikte yalnızca ekleme yapılır (append-only) — geçmiş kayıtları "resmi evrak" gibi kabul edin. |

## Kapalı (Sonuçlanmış) Davalar

Burada kalır. Silmeyin. `/portfolio-status` varsayılan olarak bunları aktif raporlardan filtreler; `/portfolio-status --all` kapalı dosyaları da dahil eder. Kapalı davalar, portföy içtihadı ve stratejik öngörü (training set) için birikim oluşturur.

## Düzeltmeler

Eğer geçmiş bir safahat (history) kaydı yanlış girilmişse, silip düzenlemeyin (edit). Hatalı kayda atıf yapan ve doğrusunu belirten yeni bir kayıt (append) ekleyin. Düzeltmenin kaydı, düzeltmenin kendisi kadar hukuki önem taşır.
