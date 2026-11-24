---
name: matter-workspace
description: >
  Çok müvekkilli hukuk veya marka/patent vekilliği bürolarında her müvekkilin
  ve IP dosyasının bağlamını izole tutmak için matter workspace yönetir (`new`,
  `list`, `switch`, `close`, `none`). "yeni matter", "dosya değiştir", "matter
  listele" istendiğinde çalışır.
argument-hint: "<new | list | switch | close | none> [slug]"
---

# /matter-workspace

Çok müvekkilli çalışan hukuk ve marka/patent vekilliği bürolarında bir müvekkile ait buluş açıklaması, tescil stratejisi veya ihtarname verilerinin başka müvekkile sızmaması için (Av.K. m. 36 ve m. 38) dosya izolasyonu sağlar. Tek şirket içi (in-house) kurulumlarda varsayılan olarak kapalıdır.

## Alt Komutlar

- `/ip-legal:matter-workspace new <slug>` — Yeni matter açar, kısa intake yürütür ve `matter.md` yazar.
- `/ip-legal:matter-workspace list` — Aktif ve arşivlenmiş dosyaları listeler.
- `/ip-legal:matter-workspace switch <slug>` — Aktif matter'ı seçer.
- `/ip-legal:matter-workspace close <slug>` — Dosyayı silmeden `~/.claude/plugins/config/legal-turkish/ip-legal/matters/_archived/<slug>/` klasörüne taşır.
- `/ip-legal:matter-workspace none` — Aktif matter'dan çıkıp genel practice profiline döner.

## Talimatlar

1. `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` → `## Matter Workspaces` bölümünü oku.
2. `Enabled` kapalı (`✗`) ise hata verme; kurum içi tek şirket yapısında bunun beklenen durum olduğunu, çok müvekkilli izolasyon gerekirse `/ip-legal:cold-start-interview --redo` ile açılabileceğini söyle.
3. İlk argümana göre (`new | list | switch | close | none`) işlemi hazırla, kullanıcı onayından sonra yaz.

## Depolama Düzeni

```text
~/.claude/plugins/config/legal-turkish/ip-legal/
├── CLAUDE.md
└── matters/
    ├── <slug>/
    │   ├── matter.md      # müvekkil, karşı taraf, hak/dava türü, olgular, özel sapmalar
    │   ├── history.md     # tarihli işlem günlüğü
    │   ├── notes.md       # çalışma notları
    │   └── outputs/       # bu dosyaya özgü araştırma/FTO/ihtarname çıktıları
    └── _archived/
        └── <slug>/        # kapatılmış (salt okunur) dosyalar
```

Slug küçük harf ve tire içerir: `atlas-marka-itiraz-2026`, `vega-patent-fto`, `fsek-uyar-kaldir-abc`.

## Alt Komut Kuralları

- **`new <slug>`:** Slug hem `matters/` hem `matters/_archived/` altında mevcut olmamalı. Intake sorularıyla (müvekkil, karşı taraf, matter türü: `marka ön araştırma/tescil | patent/FTO | tecavüz/ihtarname | uyar-kaldır/TRABİS | sözleşme/lisans | OSS | diğer`, gizlilik düzeyi: `standart | yüksek | clean-team`, 2–5 cümle olgular, profil sapmaları) `matter.md`, `history.md` ve boş `notes.md` oluştur. Otomatik geçiş yapma; `/ip-legal:matter-workspace switch <slug>` isteyip istemediğini sor.
- **`list`:** `matters/*/matter.md` kayıtlarını tara; aktif olanı `*` ile, `_archived/*` altındakileri ayrı başlıkta listele.
- **`switch <slug>`:** `CLAUDE.md` içindeki `**Active matter:**` satırını güncelle ve `matter.md` özetini göster.
- **`close <slug>`:** `history.md` içine kapanış tarihini ekle, klasörü `_archived/<slug>/` altına taşı ve aktifse `Active matter: none` yap.
- **`Cross-matter context`:** `off` iken bir dosya üzerinde çalışan skill başka dosya klasörünü kesinlikle okumaz.

## `matter.md` Şablonu

```markdown
[GİZLİ ÇALIŞMA ÜRÜNÜ - bkz. CLAUDE.md ## Çıktılar ve ## Kullanıcı Rolü]

# Matter: [Müvekkil] — [kısa açıklama]

**Slug:** [slug] | **Açılış:** [YYYY-AA-GG] | **Durum:** active
**Gizlilik:** [standart / yüksek / clean-team]

## Taraflar
**Müvekkil / İç Birim:** [ad]
**Karşı Taraf / İlgili Kurum:** [ad(lar)]

## IP Dosya Türü
[marka | patent / faydalı model | tasarım | telif (FSEK) | ticari sır | OSS | sözleşme]

## Temel Olgular
[2-5 cümle]

## Dosyaya Özel Kurallar (Profil Sapmaları)
- [örn. Buluş henüz kamuya açıklanmadı (SMK m. 83 yenilik hassasiyeti — haricî paylaşım yasak)]
- [örn. Karşı taraf stratejik tedarikçi — sert ihtar yerine yumuşak temas öncelikli]

## İlgili Matter'lar ve Gizlilik Notu
- [slug — erişim notu]
```

## Yapmadıkları

- Avukatlık Kanunu veya vekillik yönetmeliği kapsamındaki çıkar çatışması (conflicts check) kontrolünü otomatik yürütmez.
- Arşivlenen klasörü silmez; saklama süresi (retention) politikası kapsam dışındadır.
- Çıktının içeriğini değil yalnızca aktif çalışma klasörünü belirler.
