---
name: matter-workspace
description: >
  Çok müvekkilli veya çok ürünlü kullanımda product matter workspace yönetir:
  new, list, switch, close, none. Bağlam sızıntısını önlemek içindir.
argument-hint: "<new | list | switch | close | none> [slug]"
---

# /matter-workspace

## Amaç

Tek bir şirket içi product counsel kullanımında genellikle kapalı kalır. Özel hukuk bürosu, çok müvekkilli danışmanlık veya ayrılması gereken ürün/müvekkil dosyaları varsa matter workspace her dosyanın bağlamını ayrı tutar.

## Subcommands

- `/product-legal:matter-workspace new <slug>` - yeni matter aç, kısa intake yap, `matter.md` yaz.
- `/product-legal:matter-workspace list` - matter'ları listele.
- `/product-legal:matter-workspace switch <slug>` - aktif matter'ı değiştir.
- `/product-legal:matter-workspace close <slug>` - matter'ı arşivle, silme.
- `/product-legal:matter-workspace none` - practice-level bağlama dön.

## Depolama

```text
~/.claude/plugins/config/legal-turkish/product-legal/
├── CLAUDE.md
└── matters/
    ├── <slug>/
    │   ├── matter.md
    │   ├── history.md
    │   ├── notes.md
    │   └── outputs/
    └── _archived/
```

## Intake

Yeni matter için sor:

- Müvekkil veya iç iş birimi (business unit),
- ürün/özellik/kampanya adı,
- matter türü: lansman, reklam claim, abonelik/checkout, KVKK/data, AI, sektör riski, diğer,
- hedef pazarlar,
- gizlilik seviyesi,
- temel olgular,
- practice profilinden sapmalar,
- ilgili dosyalar/ticket'lar.

## `matter.md` Şablonu

```markdown
# Matter: [Müvekkil/İş Birimi] - [kısa açıklama]

**Slug:** [slug]
**Açılış:** [YYYY-MM-DD]
**Durum:** active
**Gizlilik:** [standard / heightened / clean-team]

## Taraflar ve ekip

**Müvekkil / İş Birimi:** [ad]
**Ürün sahipleri:** [adlar]
**Hukuk sahibi:** [ad]

## Matter türü

[lansman | reklam claim | abonelik/checkout | KVKK/data | AI | sektör riski | diğer]

## Temel olgular

[2-5 cümle]

## Matter'a özel override

- [practice profilinden sapma]

## İlgili dokümanlar

- [path/link]
```

## Guardrail

- `Cross-matter context: off` ise başka matter dosyası okunmaz.
- `close` arşivler, silmez.
- Bu skill çıkar çatışması (conflicts check) yapmaz; yalnızca kullanıcının beyan ettiği ayrımları kaydeder.
