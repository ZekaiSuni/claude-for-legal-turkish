---
name: matter-workspace
description: >
  Yeni bir vergi incelemesi/tarhiyatı, idari işlem/para cezası iptal davası,
  6183 ödeme emri itirazı veya 4734 KİK şikâyeti için standart çalışma
  klasörü ve `verification-log.md` oluşturur.
---

# İdare & Vergi Dosyası Çalışma Alanı (`matter-workspace`)

Her yeni vergi tarhiyatı, idari işlem veya ihale uyuşmazlığı için izlenebilir, YMM/avukat işbirliğine uygun standart klasör yapısı kurar. `CLAUDE.md` içindeki `## Matter Workspaces` ve `## Çekirdek Güvenlik Kuralları (Shared Guardrails)` esas alınır.

## Oluşturulacak Klasör Yapısı

`dosyalar/<dosya_kodu>/` altında aşağıdaki yapı oluşturulur:

```text
dosyalar/<dosya_kodu>/
├── README.md                  # Dosya künyesi, vergi dairesi/idare, esas no, uyuşmazlık türü ve özet
├── tebligat-ve-sureler.md     # UETS / VUK m. 107/A 5. gün hesabı, İYUK m. 61 kontrolü ve son günler
├── tarhiyat-ve-mali-etki.md   # Vergi aslı, ceza tutarı, gecikme faizi/zammı, teminat ve uzlaşma/376 kıyası
├── verification-log.md        # Doğrulama günlüğü: kanun maddesi, dayanak evrak ve güven seviyesi
└── ekler/                     # VİR, ihbarname, ödeme emri, YD kararı, makbuz (salt okunur veri)
```

## İş Akışı

1. **Veri Toplama (`Sessiz Tamamlama Yok`):** Dosya kodu, karşı idare/vergi dairesi, işlem/belge türü (`vergi_ihbarnamesi`, `odeme_emri_6183`, `idari_para_cezasi`, `idari_islem`, `kik_ihale`), tutar kırılımı (vergi aslı vs. ceza) ve elektronik ulaşma/tebliğ tarihi alınır. Eksik alanlar **`[Kullanıcı Doğrulaması Gerekli]`** yazılır.
2. **Dosya Şablonlarını Üret:**
   - `README.md` içine `1136 s. Av.K. m. 36` ve `VUK m. 5` kapsamında dışa aktarılmayacak dahili strateji alanı ayrıştır.
   - `tebligat-ve-sureler.md` içine 5. gün sonu formülü (`7201 m. 7/a` veya `VUK m. 107/A`), `İYUK m. 61` çalışmaya ara verme kontrolü ve yargı merciini (`İdare` vs. `Vergi` vs. `Sulh Ceza`) yaz.
   - `verification-log.md` içine doğrulama tablosunu oluştur.
3. **Portföy Senkronizasyonu:** İsteğe bağlı olarak `references/idari-vergi-register.yaml` kaydına ekleme teklif et.
