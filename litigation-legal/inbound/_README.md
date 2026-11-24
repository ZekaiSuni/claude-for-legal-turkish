# inbound/ — Gelen Hukuki Evraklar ve İhtarnameler

Bu klasör, dış dünyadan gelen her türlü evrakın (bize çekilen ihtarnameler, mahkeme müzekkereleri, savcılık bilgi talepleri, Rekabet Kurumu/KVKK bilgi isteme yazıları, haksız rekabet/ihtar mektupları) triyaj (ilk değerlendirme) ve cevaplanma süreçlerini barındırır.

`demand-letters/` (Giden İhtarnameler) ve `matters/` (Aktif Dava Portföyü) klasörlerinden ayrı tutulmuştur çünkü gelen evrakların kendi iş akışı vardır: Oku → Triyaj Yap → Karar Ver → Cevapla (veya bir Davaya dönüştür). Gelen her evrak otomatik olarak uzun süreli takip edilen bir "Dava/Dosya" (matter) haline gelmez.

## Düzen (Layout)

```
inbound/
├── _README.md
└── [kisa-ad]/
    ├── incoming.pdf              # veya .eml / KEP iletisi — orijinal gelen evrak (veya linki)
    ├── triage.md                 # analiz: kapsam, haklılık payı (merit), seçenekler, tavsiye
    └── response-v1.docx          # eğer cevap verilecekse hazırlanan cevap dilekçesi/ihtarı (v2, v3)
```

## İsimlendirme Kuralları (Slug conventions)

`[tur]-[gonderen]-[yyyy-aa]`. Örnekler:

- `ihtar-acme-2026-04` (alınan bir ihtarname)
- `muzekkere-kisi-a-v-kisi-b-2026-04` (üçüncü kişi mahkeme müzekkeresi)
- `idari-rekabet-bilgi-isteme-2026-04` (kurum soruşturması)
- `muhafaza-tedarikci-2026-04` (delil muhafaza talebi)

## İş Akışı (Workflow)

| Tür | Komut | Çıktılar |
|---|---|---|
| İhtarname Alındı | `/litigation-legal:demand-received [yol]` | triage.md + opsiyonel cevap taslağı |
| Müzekkere/Tebligat | `/litigation-legal:subpoena-triage [yol]` | triage.md + itiraz/cevap muhtırası |
| Kurum İncelemesi | *gelecekte eklenecek* | |

Her triyaj işlemi, bağlantılı davalar (aynı karşı taraf, örtüşen konu) için `matters/_log.yaml` dosyasını çapraz kontrol eder. İlgili bir dava varsa, triyaj bunu bayraklar ve bu evrakı `related_matter` olarak o dosyaya eklemeyi teklif eder. Eğer bu gelen evrak başlı başına takip edilecek bir "Dava"ya dönüşmeliyse, triyaj süreci alanları önceden doldurulmuş şekilde `/matter-intake` komutuna devreder.

## Davalarla (Matters) İlişkisi

- Gelen evrak + mevcut davayla ilgili → `_log.yaml` içindeki `related_matters` alanı üzerinden bağlanır; dosya `inbound/` klasöründe kalır.
- Gelen evrak + davaya dönüşmeli → dava oluşturulur; `matter.md` dosyası geriye dönük olarak `inbound/[slug]/` klasörüne link verir.
- Gelen evrak + halledildi ve kapandı (davaya gerek yok) → kayıt olarak `inbound/` klasöründe kalır.

## Giden İhtarnamelerle (Outbound) İlişkisi

Eğer gelen bir ihtara verilen cevap bizzat karşı bir ihtarname (karşı ihtar) niteliğindeyse, triyaj süreci önceden doldurulmuş şekilde `/demand-intake` komutuna devreder. Giden ihtarname `demand-letters/` klasöründe yaşar ve bu gelen klasöre çapraz link (atıf) barındırır.
