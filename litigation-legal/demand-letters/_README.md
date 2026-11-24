# demand-letters/ — Dava Öncesi İhtarnameler ve İhbarnameler

Bu klasör, şirket avukatının/hukuk müşavirliğinin gönderdiği her türlü ihtarname (demand letter) için üretilen iş-ürünlerini barındırır: Alacak ihtarnameleri, sözleşmeye aykırılık/fesih ihtarları, haksız rekabet/durdurma ihtarları, işe iade/işçilik alacakları arabuluculuk davetleri, delil muhafaza ihtarları (noter kanalıyla veya KEP ile gönderilenler dahil).

`matters/` (Dava Portföyü) klasöründen ayrı tutulmuştur çünkü:

- Çekilen her ihtarname takip edilecek bir davaya (matter) dönüşmez. Düşük meblağlı alacak ihtarnameleri veya rutin tahsilat yazıları için `_log.yaml` dosyasında ayrı bir satır açılmasına gerek yoktur.
- İleride davaya dönüşüp dönüşmeyeceğine bakılmaksızın, her ihtarnamenin iş akışı şablonu aynıdır (Talep alımı → Taslak hazırlama → Gönderme → Kontrol listesi).
- Bir ihtarname fiilen davaya dönüştüğünde, davanın `matter.md` dosyası geriye dönük olarak buraya link verir — ihtarnamenin taslak geçmişi kendi klasöründe kalır.

## Düzen (Layout)

```
demand-letters/
├── _README.md                     # bu dosya
└── [kisa-ad]/
    ├── intake.md                  # bağlam toplama, strateji, pazarlık gücü (leverage), gizlilik (privilege) filtreleri
    ├── draft-v1.docx              # ihtarname taslağı (v2, v3)
    └── checklist.md               # gönderim sonrası kontrol listesi — tebligat/noter barkodu, suretler, takvime işlenen süreler, takip
```

## İsimlendirme Kuralları (Slug conventions)

`[tur]-[karsi-taraf]-[yyyy-aa]`. Örnekler:

- `alacak-acme-2026-04`
- `haksizrekabet-rakip-x-2026-04`
- `fesih-tedarikci-2026-04`
- `isten-cikarma-calisan-2026-04`
- `delil-muhafaza-satici-2026-04`

## İş Akışı (Workflow)

1. `/litigation-legal:demand-intake [başlık]` → adaptif bilgi alma sürecini (intake) çalıştırır, `intake.md` dosyasını yazar.
2. `/litigation-legal:demand-draft [kisa-ad]` → Sulh görüşmeleri (arabuluculuk) / Av.K. m.36 gizlilik kontrol listesini çalıştırır, `.docx` taslağını oluşturur, `checklist.md` yazar ve bir "Dava" (matter) oluşturmayı teklif eder.

## Davalarla (Matters) İlişkisi

Bir ihtarname taslağı hazırlandıktan sonra, `demand-draft` süreci ihtarnamenin finansal/hukuki önemini (`CLAUDE.md` içindeki şirket eşiklerine göre) değerlendirir ve bir Dava dosyası (matter) oluşturmayı teklif eder. Cevap evet ise, `matters/_log.yaml` dosyasına `source: demand-letter` notuyla bir satır eklenir ve `matters/[kisa-ad]/matter.md` dosyası bu ihtarnamenin klasörüne geri bağlantı verir.

Düşük önem derecesindeki (Immaterial) ihtarnameler sadece burada kalır. Bunlar hala bir iş-ürünü kaydıdır — sadece portföy bazında (MMS) takip edilmezler.

## Düzeltmeler ve Versiyonlar

Gönderilmiş (noterden çekilmiş/KEP ile iletilmiş) bir taslağın üzerine asla yazmayın (overwrite yapmayın). Eğer bir ihtarname gönderildiyse ve revizyon/ek gerekiyorsa (Örn: Ek/Tamamlayıcı ihtarname), `draft-v2.docx` oluşturarak başlayın. Versiyon geçmişinin kendisi faydalı bir yasal kayıttır.
