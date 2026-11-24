---
name: matter-close
description: >
  Tamamlanan bir dava veya uyuşmazlık dosyasını kapatır — sonuç türünü (sulh,
  ret, kabul, feragat, kesinleşme, birleştirme), nihai maliyeti ve çıkarılan
  dersleri kaydedip aktif portföyden arşive alır, ancak kaydı silmez.
argument-hint: "[slug]"
---

# /matter-close

1. `matters/_log.yaml` ve `~/.claude/plugins/config/legal-turkish/litigation-legal/matters/[slug]/` kayıtlarını kontrol et.
2. Sonuç bilgilerini topla: kapanış türü (`settled`, `dismissed`, `judgment-for-us`, `judgment-against-us`, `withdrawn`, `consolidated`, `other`), kesinleşme/kapanış tarihi, nihai maliyet/tazminat ve çıkarılan dersler.
3. Non-lawyer kapanış kapısını ve kullanıcı onayını aldıktan sonra `matters/_log.yaml` satırını güncelle (`status: closed`, `closed: YYYY-AA-GG`, `outcome:`, `final_cost:`, `last_updated:`).
4. `matters/[slug]/history.md` ve `matter.md` sonuna kapanış kaydını ekle. Kaydı ve klasörü **silme** (`/litigation-legal:portfolio-status` kapalı dosyaları aktif toplamdan filtreler).

---

## Çıkar Çatışması Kapısı (Atlanamaz Kural)

Kapatmadan önce `matters/_log.yaml` içinde `[slug]` kaydını kontrol et; yoksa reddet ve `/litigation-legal:matter-intake` öner.

## Kapanışta Toplanacak Bilgiler

### 1. Sonuç Türü (`outcome`)
- `settled` — Sulh / arabuluculuk anlaşması (taraf, ödeme tutarı, feragat/ibra kapsamı).
- `dismissed` — Davanın reddi / usulden ret / açılmamış sayılma (kesinleşip kesinleşmediği).
- `judgment-for-us` — Lehimize hüküm (istinaf/temyiz kesinleşme durumu ve vekâlet ücreti/yargılama gideri tahsili).
- `judgment-against-us` — Aleyhimize hüküm (istinaf/temyiz/icra durumu, tehir-i icra/teminat, ödenen tutar).
- `withdrawn` — Feragat / takipsiz bırakma / müracaata kalma.
- `consolidated` — Başka dosya ile birleştirme (`HMK m. 166` — ana dosyanın slug'ını yaz).
- `other` — Açıklama ile.

### 2. Sonuç Tarihi
Kararın kesinleştiği veya sulh/arabuluculuk tutanağının/anlaşmasının imzalandığı tarih.

### 3. Nihai Mali Risk ve Karşılık Kıyaslaması
- Şirkete/müvekkile fiilî toplam maliyet (asıl alacak + faiz + yargılama gideri + karşı/vekalet ücreti + icra masrafları).
- İlk `matter-intake` sırasındaki öngörülen risk aralığı (`exposure_range`) ve ayrılan muhasebe karşılığı (varsa) ile kıyaslama.

### 4. Çıkarılan Dersler (Lessons)
2–3 dürüst cümle: neyi doğru gördük, nerede yanıldık, sözleşmede veya ilk triyajda ne erken yakalanabilirdi? (Kullanıcı atladıysa uydurma; boş bırak.)

### 5. Kapanış Belgesi (İsteğe Bağlı)
Kesinleşmiş mahkeme ilamı, gerekçeli karar, arabuluculuk anlaşma belgesi veya feragat zaptı yolu.

## Non-Lawyer Onay Kapısı

Yazmadan önce `~/.claude/plugins/config/legal-turkish/litigation-legal/CLAUDE.md` → `## Bunu Kim Kullanıyor` bölümünü kontrol et. Kullanıcı **Non-lawyer** ise şu uyarıyı ver ve açık onay + avukat incelemesi olmadan `_log.yaml`'ı değiştirme:

> Bir uyuşmazlık dosyasını kapatmanın hukuki sonuçları vardır — aktif süre takibini durdurur, varsa ilgili hukuki saklama/delil muhafaza kararını (`/litigation-legal:legal-hold --release` ayrı değerlendirilmelidir) etkiler ve kesinleşen resmî şirket kaydını oluşturur. Bunu sorumlu avukatınızla gözden geçirdiniz mi? Hayırsa avukatınıza götürmeniz için 1 sayfalık kapanış özeti hazırlıyorum; yetkili avukata ulaşmak için bağlı olduğunuz Baro iletişim kanallarından yararlanabilirsiniz.

## Yazılacak Güncellemeler (Onay Sonrası)

### 1. `matters/_log.yaml`
Mevcut tüm alanları (`uyap_no`, `arabuluculuk` vb.) koru; yalnızca şunları güncelle/ekle:
```yaml
status: closed
closed: [YYYY-MM-DD]
outcome: [outcome]
final_cost: "[tutar ve para birimi]"
last_updated: [YYYY-MM-DD]
```

### 2. `matters/[slug]/history.md` en üstüne ekle:
```markdown
## [YYYY-MM-DD] — Dosya Kapatıldı: [outcome]

**Sonuç:** [Özet — kesinleşme/sulh şartları]
**Nihai maliyet:** [tutar ve şartlar]
**İlk öngörüye kıyasla:** [exposure_range kıyaslaması]
**Dersler:** [2-3 cümle]
**İlgili belge:** [kesinleşme şerhi / sulh belgesi yolu]
```

### 3. `matters/[slug]/matter.md` sonuna kapanış bloğu ekle
*(Eski intake bölümlerini değiştirme; tarihî kayıt olarak kalsın.)*

## Yapmadıkları

- Dosya klasörünü veya `_log.yaml` satırını silmez (kapalı dosyalar portföy hafızasıdır).
- Kapanmış dosyayı yeniden açmaz (istinaf/iade/yeni dava açılırsa eski dosyaya atıfla yeni matter açılır).
- Kullanıcının söylemediği dersi veya tutarı uydurmaz.
