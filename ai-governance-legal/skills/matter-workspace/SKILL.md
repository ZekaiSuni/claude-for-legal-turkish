---
name: matter-workspace
description: >
  Çok müvekkilli hukuk bürosu veya danışmanlık kullanımında her müvekkil ya da AI
  projesi için ayrı matter workspace oluşturur, listeler, aktif eder veya
  arşivler (new, list, switch, close, none). Müvekkiller arası bağlam sızıntısını
  önler.
argument-hint: "<new | list | switch | close | none> [slug]"
---

# /matter-workspace

Çok müvekkilli çalışan hukuk bürolarında veya danışmanlıklarda bir müvekkile ait AI kullanım verisi, sözleşme veya risk notunun başka müvekkile sızmaması için dosya izolasyonu sağlar. Kurum içi (in-house) tek şirket kurulumlarında varsayılan olarak kapalıdır.

## Komutlar

- `/ai-governance-legal:matter-workspace new <slug>` — Yeni matter açar, kısa intake yapar ve `matter.md` üretir.
- `/ai-governance-legal:matter-workspace list` — Aktif ve arşivlenmiş matter dosyalarını listeler.
- `/ai-governance-legal:matter-workspace switch <slug>` — Aktif matter'ı değiştirir.
- `/ai-governance-legal:matter-workspace close <slug>` — Matter'ı silmeden `_archived/<slug>/` altına taşır.
- `/ai-governance-legal:matter-workspace none` — Aktif matter'dan çıkıp genel practice profiline döner.

## İş Akışı

1. `~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md` → `## Matter Workspaces` bölümünü oku.
2. `Enabled: ✗` ise hata verme; kurum içi yapılandırmada bunun normal olduğunu, çok müvekkilli kullanıma geçmek için `/ai-governance-legal:cold-start-interview --redo` çalıştırılabileceğini söyle.
3. `Enabled: ✓` ise ilk argümana göre (`new | list | switch | close | none`) işlemi hazırla, kullanıcı onayından sonra yaz.

## Depolama Düzeni

```text
~/.claude/plugins/config/legal-turkish/ai-governance-legal/
├── CLAUDE.md
└── matters/
    ├── <slug>/
    │   ├── matter.md      # müvekkil, matter türü, olgular, özel sapmalar
    │   ├── history.md     # tarihli işlem günlüğü
    │   ├── notes.md       # çalışma notları
    │   └── outputs/       # bu dosya için üretilen YZED/sözleşme/triyaj çıktıları
    └── _archived/
        └── <slug>/        # kapatılmış (salt okunur) dosyalar
```

Slug küçük harf ve tire içerir: `abc-bank-kredi-ai`, `xyz-copilot-ek`, `saglik-saas-yzed`.

## Alt Komut Kuralları

- **`new <slug>`:** Slug hem `matters/` hem `matters/_archived/` altında mevcut olmamalı. Intake bilgilerini (müvekkil/birim, karşı taraf, matter türü: `iç AI kullanımı | tedarikçi AI incelemesi | YZED/AIA | düzenleme uyumu | politika projesi | diğer`, gizlilik düzeyi: `standart | yüksek | clean-team`, 2–5 cümle olgular, playbook sapmaları) alıp `matter.md`, `history.md` ve boş `notes.md` yaz. Otomatik geçiş yapma; `switch <slug>` isteyip istemediğini sor.
- **`switch <slug>`:** Yalnızca `CLAUDE.md` içindeki `**Active matter:**` satırını günceller.
- **`close <slug>`:** `history.md` sonuna kapanış kaydı düşüp klasörü `_archived/<slug>/` altına taşır; aktifse `Active matter: none` yapar.
- **`Cross-matter context`:** `off` iken bir matter içinde çalışan skill başka bir matter klasörünü asla okumaz.

## `matter.md` Şablonu

```markdown
[GİZLİ HUKUKİ ÇALIŞMA TASLAĞI - bkz. CLAUDE.md ## Çıktılar ve ## Kullanıcı Rolü]

# Matter: [Müvekkil] - [kısa açıklama]

**Slug:** [slug] | **Açılış:** [YYYY-AA-GG] | **Durum:** active
**Gizlilik:** [standart / yüksek / clean-team]

## Taraflar
**Müvekkil / İç Birim:** [ad]
**Karşı Taraf / AI Tedarikçisi:** [ad]

## Matter Türü
[iç AI kullanımı | tedarikçi AI incelemesi | YZED/AIA | düzenleme uyumu | politika projesi | diğer]

## Temel Olgular
[2-5 cümle]

## Matter'a Özel Kurallar (Playbook Sapmaları)
- [örn. Müvekkil tüm LLM çıktılarında Türkiye içi veri barındırma zorunlu tutuyor]

## İlgili Matter'lar ve Gizlilik Notu
- [varsa]
```

## Yapmadıkları

- Avukatlık Kanunu kapsamındaki çıkar çatışması (conflicts check) kontrolünü otomatik yapmaz; yalnızca kullanıcının beyan ettiği ayrımı uygular.
- Arşivlenen klasörü silmez veya saklama süresi (retention) silimi yürütmez.
