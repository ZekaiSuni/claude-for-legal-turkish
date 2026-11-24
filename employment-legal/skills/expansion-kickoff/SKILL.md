---
name: expansion-kickoff
description: >
  Yeni ülke/şehir/çalışma modeli istihdam genişleme dosyası başlatır. Türkiye'de
  ilk çalışan, yeni işyeri/şube, uzaktan çalışan, yabancı çalışan, EOR/payroll
  veya Türkiye dışı istihdam planında tracker ve ilk aksiyon listesini kurar.
argument-hint: "[ülke/şehir/model]"
---

# /expansion-kickoff

`international-expansion` playbook'unu kullanarak yeni tracker başlat.

## Tracker

```markdown
# Employment Expansion Tracker - [Yer/Model]

**Açılış:** [YYYY-MM-DD]
**Model:** [local payroll / remote / EOR / danışman / şube]
**Durum:** açık

## Kapılar

| Kapı | Sahip | Durum | Not |
|---|---|---|---|
| Yerel hukuk | | | |
| SGK/vergi/payroll | | | |
| İş sözleşmesi | | | |
| KVKK | | | |
| İSG | | | |
| Politika | | | |

## Açık Sorular

- [soru]
```

Dosya yolu: `~/.claude/plugins/config/legal-turkish/employment-legal/expansion/<slug>/tracker.md`
