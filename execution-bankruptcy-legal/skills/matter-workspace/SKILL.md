---
name: matter-workspace
description: >
  Yeni bir icra takibi, itiraz/şikâyet davası, 89/1-2-3 süreci veya
  konkordato/iflas masası kaydı için standart dosya çalışma klasörü ve
  `verification-log.md` altyapısı oluşturur.
---

# İcra Dosyası Çalışma Alanı (`matter-workspace`)

Her önemli icra takibi, yüksek tutarlı icra hukuk davası veya konkordato dosyası için izlenebilir, ekip içi devredilebilir ve denetime açık bir klasör yapısı kurar. `CLAUDE.md` içindeki `## Matter Workspaces` ve `## Çekirdek Güvenlik Kuralları (Shared Guardrails)` esas alınır.

## Oluşturulacak Klasör Yapısı

Kullanıcı aksi belirtmedikçe `dosyalar/<dosya_kodu>/` altında aşağıdaki yapı önerilir ve oluşturulur:

```text
dosyalar/<dosya_kodu>/
├── README.md                  # Dosya künyesi, icra dairesi/mahkeme esas no, taraf rolü ve strateji özeti
├── tebligat-ve-sureler.md     # UETS/fiziki tebligat mazbatası tarihleri, 7201 m. 7/a 5. gün hesabı, hak düşürücü süreler
├── hesap-ve-haciz-ozeti.md    # Asıl alacak, faiz türü (3095/avans/temerrüt), haczedilen mallar ve 1 yıllık satış isteme takibi
├── verification-log.md        # Doğrulama günlüğü: kanun maddesi, dayanak belge ve güven düzeyi kaydı
└── ekler/                     # PDF/tarama tebligat, çek/senet sureti, UYAP kapak hesabı (salt okunur veri)
```

## İş Akışı

1. **Temel Bilgileri Al (Eksik Bilgi Uydurulmaz):** Dosya adı/kodu, icra dairesi ve esas numarası, takip türü (`ilamsiz`, `kambiyo`, `ilamli`, `kira_tahliye`, `rehin`, `konkordato`), taraf rolü (`alacakli`, `borclu`, `ucuncu_kisi_89`), takip çıkışı tutarı ve biliniyorsa UETS/tebligat tarihi. Eksik alanlar dosyaya **`[Kullanıcı Doğrulaması Gerekli]`** olarak yazılır.
2. **Dosya Şablonlarını Üret:**
   - `README.md` içinde hızlı özet tablosu ve `1136 s. Av.K. m. 36` uyarınca yalnızca dahili ekibe özel strateji alanı (dışarıya paylaşılacak metinlerden ayrı).
   - `tebligat-ve-sureler.md` içinde UETS ulaşma + 5. gün sonu formülü (`7201 s. TK m. 7/a`) ve ilgili İİK itiraz/şikâyet/kanun yolu (`7499 s. K.`) son tarihleri.
   - `verification-log.md` içine ilk kontrol satırları (`| Tarih | İddia / Süre | Dayanak Belge / Kanun | Güven | Kontrol Eden |`).
3. **Portföy Senkronizasyonu:** Kullanıcı isterse `references/takip-register.yaml` kaydına da bu dosya için yeni bir kayıt bloğu eklemeyi teklif et.
