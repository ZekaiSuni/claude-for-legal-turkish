---
name: matter-workspace
description: >
  Çok müvekkilli çalışan hukuk bürolarında her dava/uyuşmazlık dosyasının
  bağlamını izole tutmak için matter workspace yönetir (`new`, `list`, `switch`,
  `close`, `none`). "yeni dosya aç", "dosya değiştir", "matter listele"
  istendiğinde çalışır.
argument-hint: "<new | list | switch | close | none> [slug]"
---

# /matter-workspace

Çok müvekkilli hukuk büroları bir müvekkile ait dava ve sır saklama kapsamındaki verilerin (Av.K. m. 36) başka bir dosyaya karışmaması için dosya izolasyonu kullanır. Kurum içi tek şirket hukuk birimlerinde varsayılan olarak kapalıdır. *(Tek bir aktif dava hakkında özet almak için `/litigation-legal:matter-briefing [slug]` kullanılır.)*

## Alt Komutlar

- `/litigation-legal:matter-workspace new <slug>` — Yeni dosya klasörü açar, kısa intake yapar, `matter.md` yazar.
- `/litigation-legal:matter-workspace list` — Dosyaları durum ve aktiflik bayrağıyla listeler.
- `/litigation-legal:matter-workspace switch <slug>` — Aktif matter'ı seçer.
- `/litigation-legal:matter-workspace close <slug>` — Dosyayı silmeden `~/.claude/plugins/config/legal-turkish/litigation-legal/matters/_archived/<slug>/` klasörüne taşır.
- `/litigation-legal:matter-workspace none` — Aktif dosyadan çıkıp practice-level bağlama döner.

## Talimatlar

1. `~/.claude/plugins/config/legal-turkish/litigation-legal/CLAUDE.md` → `## Matter workspaces` bölümünü oku.
2. `Enabled` kapalı (`✗`) ise hata verme; kurum içi tek şirket yapısında bunun beklenen durum olduğunu ve çok müvekkilli izolasyon gerekirse `/litigation-legal:cold-start-interview --redo` ile açılabileceğini söyle.
3. İlk argümana göre (`new | list | switch | close | none`) işlemi hazırla, kullanıcı onayından sonra yaz.

## Depolama Düzeni

```text
~/.claude/plugins/config/legal-turkish/litigation-legal/
├── CLAUDE.md
└── matters/
    ├── _log.yaml             # portföy takip dizini (uyap_no, arabuluculuk vb.)
    ├── <slug>/
    │   ├── matter.md         # müvekkil, karşı taraf, dava türü, olgular, özel sapmalar
    │   ├── history.md        # tarihli safahat ve olay günlüğü
    │   ├── notes.md          # serbest çalışma notları
    │   └── outputs/          # bu dosyaya özgü dilekçe/kronoloji çıktıları
    └── _archived/
        └── <slug>/           # kapatılmış (salt okunur) dosyalar
```

Slug küçük harf ve tire içerir: `ornek-lojistik-ticari-2026`, `abc-ise-iade`, `marka-tecavuz-2026`.

## Alt Komut Kuralları

- **`new <slug>`:** Slug hem `matters/` hem `matters/_archived/` altında bulunmamalı. Kısa intake bilgilerini (müvekkil/iş birimi, karşı taraf, uyuşmazlık türü: `ticari sözleşme | iş hukuku | fikri mülkiyet | idari/kurum soruşturması | ürün sorumluluğu | seri/topluluk uyuşmazlığı | diğer`, UYAP dosya no/arabuluculuk bilgisi, gizlilik düzeyi: `standart | yüksek | clean-team`, 2–5 cümle olgular, profil sapmaları, ilgili dosyalar) toplayıp `matter.md`, `history.md` ve boş `notes.md` oluştur. Otomatik geçiş yapma; `/litigation-legal:matter-workspace switch <slug>` isteyip istemediğini sor.
- **`list`:** `matters/*/matter.md` dosyalarını oku; aktif olanı `*` ile, `_archived/*` altındakileri ayrı başlıkla göster.
- **`switch <slug>`:** `CLAUDE.md` içindeki `**Active matter:**` satırını güncelle ve `matter.md` özetini göster.
- **`close <slug>`:** `history.md` içine kapanış kaydı düşüp klasörü `_archived/<slug>/` altına taşı; aktifse `Active matter: none` yap.
- **`Cross-matter context`:** `off` iken bir dosya üzerinde çalışan skill başka dosya klasörlerini kesinlikle okumaz.

## `matter.md` Şablonu

```markdown
[GİZLİ HUKUKİ ÇALIŞMA TASLAĞI - bkz. CLAUDE.md ## Çıktılar (Outputs) ve ## Bunu Kim Kullanıyor]

# Matter: [Müvekkil] — [kısa açıklama]

**Slug:** [slug] | **Açılış:** [YYYY-AA-GG] | **Durum:** active
**Gizlilik:** [standart / yüksek / clean-team]

## Taraflar
**Müvekkil / İç Birim:** [ad]
**Karşı Taraf:** [ad(lar)]

## Uyuşmazlık Türü ve Usul Bilgisi
[ticari sözleşme | iş hukuku | fikri mülkiyet | idari/düzenleyici | diğer] — **UYAP:** [bekliyor / esas no] — **Arabuluculuk:** [durum]

## Temel Olgular
[2-5 cümle]

## Dosyaya Özel Kurallar (Playbook Sapmaları)
- [örn. Müvekkil dış büro raporlarında haftalık yazılı özet ister]
- [örn. Uygulanacak hukuk: Türk hukuku; yabancı hukuk veya tahkim seçimi ayrıca eskale edilecek.]

## İlgili Dosyalar ve Gizlilik Notu
- [slug — ilişki ve erişim kısıtı]
```

## Yapmadıkları

- Avukatlık Kanunu kapsamında çıkar çatışması kontrolünü otomatik yürütmez (bunun için `/litigation-legal:matter-intake` kapısı kullanılır).
- Arşivlenen dosyaları silmez.
- Çıktının içeriğini değil yalnızca aktif çalışma klasörünü belirler.
