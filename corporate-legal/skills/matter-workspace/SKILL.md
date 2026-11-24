---
name: matter-workspace
description: >
  Çok müvekkilli hukuk büroları veya ayrı işlem/veri odası (deal room) yöneten
  ekip yapılarında her müvekkil ve M&A/kurumsal işlem bağlamını izole tutmak için
  matter workspace yönetir (`new`, `list`, `switch`, `close`, `none`). "yeni
  matter", "matter değiştir", "dosya listele" istendiğinde çalışır.
argument-hint: "<new | list | switch | close | none> [slug]"
---

# /matter-workspace

Çok müvekkilli hukuk büroları veya birden fazla gizli M&A işlemini paralel yürüten ekiplerde bir müvekkil ya da işlemin gizli VDR verilerinin başka dosyaya sızmasını önleyen dosya yönetim katmanıdır. Tek şirket için kurum içi (in-house) kullanımda varsayılan olarak kapalıdır.

## Alt Komutlar

- `/corporate-legal:matter-workspace new <slug>` — Yeni matter açar, kısa intake yürütür, `matter.md` yazar.
- `/corporate-legal:matter-workspace list` — Aktif ve arşivli dosyaları listeler.
- `/corporate-legal:matter-workspace switch <slug>` — Aktif matter'ı seçer.
- `/corporate-legal:matter-workspace close <slug>` — Matter'ı silmeden `_archived/<slug>/` klasörüne taşır.
- `/corporate-legal:matter-workspace none` — Aktif matter'ı kaldırır, genel practice profiline döner.

## Talimatlar

1. `~/.claude/plugins/config/legal-turkish/corporate-legal/CLAUDE.md` → `## Matter workspaces` bölümünü oku.
2. `Enabled` kapalı (`✗`) ise hata verme; tek şirket içi kurulumlarda bunun normal olduğunu, çok müvekkilli/çok işlemli izolasyon için `/corporate-legal:cold-start-interview --redo` çalıştırılabileceğini söyle.
3. İlk argümana göre (`new | list | switch | close | none`) işlemi hazırla, kullanıcıya göster ve onay aldıktan sonra yaz.

## Depolama Düzeni

```text
~/.claude/plugins/config/legal-turkish/corporate-legal/
├── CLAUDE.md
└── matters/
    ├── <slug>/
    │   ├── matter.md      # müvekkil, karşı taraf, işlem türü, olgular, özel kurallar
    │   ├── history.md     # tarihli olay günlüğü
    │   ├── notes.md       # çalışma notları
    │   └── outputs/       # bu işleme özgü diligence/kapanış/tutanak çıktıları
    └── _archived/
        └── <slug>/        # kapatılmış (salt okunur) dosyalar
```

Slug küçük harf ve tire içerir: `alpha-hisse-devri-2026`, `beta-birlesme`, `abc-genel-kurul`.

## Alt Komut Kuralları

- **`new <slug>`:** Slug hem `matters/` hem `matters/_archived/` altında mevcut olmamalı. Intake sorularıyla (müvekkil/iş birimi, karşı taraf, işlem türü: `M&A alıcı | M&A satıcı | yatırım | yönetim kurulu/genel kurul | grup yeniden yapılandırma | entegrasyon | diğer`, gizlilik düzeyi: `standart | yüksek | clean-team`, 2–5 cümlelik özet olgular, playbook sapmaları, ilgili matter'lar) `matter.md`, `history.md` ve boş `notes.md` oluştur. Otomatik olarak yeni dosyaya geçme; `switch <slug>` isteyip istemediğini sor.
- **`list`:** Tüm `matters/*/matter.md` dosyalarını tara; aktif olanı `*` ile, arşivlenenleri ayrı başlıkta listele.
- **`switch <slug>`:** `CLAUDE.md` içindeki `**Active matter:**` satırını güncelle ve `matter.md` özetini göster.
- **`close <slug>`:** `history.md` dosyasına kapanış kaydı ekle, klasörü `_archived/<slug>/` altına taşı ve aktifse `Active matter: none` yap.
- **`Cross-matter context`:** `off` iken bir matter içinde çalışan skill başka bir matter klasörünü asla okumaz; yalnızca `on` olduğunda ve kullanıcı açıkça çapraz karşılaştırma isterse okur.

## `matter.md` Şablonu

```markdown
GİZLİ HUKUKİ ÇALIŞMA TASLAĞI - AVUKAT/HUKUKÇU İNCELEMESİNE TABİDİR
Bu çıktı hukuki görüş, imza onayı, tescil talimatı veya resmi başvuru yerine geçmez.

# Matter: [Müvekkil] — [kısa açıklama]

**Slug:** [slug] | **Açılış:** [YYYY-AA-GG] | **Durum:** active
**Gizlilik:** [standart / yüksek / clean-team]

## Taraflar
**Müvekkil / İç Birim:** [ad]
**Karşı Taraf:** [ad(lar)]

## İşlem Türü
[M&A alıcı | M&A satıcı | yatırım/iştirak | kurumsal yönetim | yeniden yapılandırma | diğer]

## Temel Olgular
[2-5 cümle]

## Matter'a Özel Sapmalar (Playbook Overrides)
- [örn. Sözleşme sorumluluk sınırı kurum standardı %100 yerine %50 olacak]
- [örn. Uygulanacak hukuk: Türk hukuku olmalı; yabancı hukuk seçimi ayrıca eskale edilecek.]

## İlgili Matter'lar ve Gizlilik Notu
- [Clean-team veya yüksek gizlilik varsa erişim sınırı notu]
```

## Yapmadıkları

- Avukatlık Kanunu kapsamında çıkar çatışması (conflicts check) yürütmez.
- Arşivlenen klasörleri silmez; saklama/imha politikası kapsam dışındadır.
- Hangi skill çıktısının nereye yazılacağını yalnızca aktif klasörü belirterek yönlendirir.
