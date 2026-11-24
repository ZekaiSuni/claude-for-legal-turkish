# `oc-status/` — Haftalık Dış Hukuk Bürosu Durum İsteği Taslakları

`/litigation-legal:oc-status` komutundan üretilen çıktılar tarih bazlı alt klasörlerde toplanır; her çalışma klasöründe dosya bazında taslak e-posta/mesaj dosyaları ile bir `_summary.md` özeti yer alır.

## Klasör Düzeni

```text
oc-status/
├── _README.md                       # bu bilgilendirme dosyası
└── [YYYY-MM-DD]/
    ├── _summary.md                  # hangi dosyaların çalıştırıldığı ve atlandığı
    ├── [dosya-kisa-adi-1].md        # ilgili dosya için durum sorma e-posta taslağı
    ├── [dosya-kisa-adi-2].md
    └── ...
```

Ortamda yetkilendirilmiş bir E-posta MCP sunucusu (ör. Gmail) bulunursa taslaklar doğrudan gelen kutusunda oluşturulabilir; bağlı bir e-posta aracı yoksa buradaki Markdown dosyaları kalıcı çalışma kaydı olarak kullanılır ve gönderim sorumlu avukat tarafından manuel yapılır.

## Periyot ve Kullanım

- Haftalık rutin tarama olarak (varsayılan Pazartesi sabahı) takvimlendirilebilir (`--setup-schedule`).
- İstenildiği zaman manuel çalıştırmak için: `/litigation-legal:oc-status` (varsayılan aktif portföy filtresi) veya tek bir dosya için `/litigation-legal:oc-status --slug=[dosya-kisa-adi]`.

## Arşiv ve Temizlik

Dış hukuk bürosundan yanıt alınıp `matters/[dosya-kisa-adi]/history.md` tarihçesi güncellendikten sonra 30 günden eski tarihli taslak klasörleri arşivlenebilir veya temizlenebilir.
