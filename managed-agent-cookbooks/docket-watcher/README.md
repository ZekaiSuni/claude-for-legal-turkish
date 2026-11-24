# Docket Watcher — managed-agent template

## Overview

Aktif dava portföyündeki dosyaları izler. Kurumsal özel UYAP bağlantısı (varsa) veya kullanıcı tarafından dışa aktarılan UYAP evrakı/resmî yargı kaynakları üzerinden yeni evrakları kontrol eder. Her aktif dosya (`matter`) için son kontrolden bu yana gelen evrakları alır, evrak tiplerini aday süre kurallarıyla eşleştirir, dosya geçmişi ve açık işlerle karşılaştırır, durum raporu ve yapılandırılmış süre çıktısı üretir.

Same source as the [`docket-watcher`](../../litigation-legal/agents/docket-watcher.md) agent in the litigation-legal Claude Code plugin — this directory is the Managed Agent cookbook for `POST /v1/agents`.

## ⚠️ Before you deploy

- **Computed deadlines are leads, not calendar entries.** Court deadline rules vary by jurisdiction, court, judge, and local rule, and can be modified by standing order or case-specific case management order. Missing a court deadline has malpractice consequences. A licensed attorney verifies every computed deadline against the court's actual rules and any case-specific orders before it is docketed. The agent is upstream of that decision, not a substitute for it.
- **Filing classifications are heuristic.** A filing the agent misclassifies — an administrative motion read as a dispositive motion, a stipulation read as a discovery dispute — can produce a wrong deadline rule. Read the filing; do not trust the label.
- **An unknown court is not a default.** If the jurisdiction-rule table does not cover a court, the mapper must produce `confidence: low` + `needs_verification: true`, never a silent default. If you see a confident deadline on an obscure court, treat the rule table as stale until proven otherwise.
- **Sessiz dosya temiz dosya değildir.** Kalem işlemleri gecikebilir, evrak sisteme olaydan günler sonra düşebilir. "Yeni evrak yok" yalnızca kontrol edilen kaynaklarda yeni kayıt görünmediği anlamına gelir; dosyada risk yok demek değildir.

## Deploy

```bash
export ANTHROPIC_API_KEY=sk-ant-...
export UYAP_MCP_URL=...
export GDRIVE_MCP_URL=...
../../scripts/deploy-managed-agent.sh docket-watcher
```

## Steering events

See [`steering-examples.json`](./steering-examples.json).

## Security & handoffs

Court filings are public records, but they are also UNTRUSTED INPUT. The filer controls the text and can embed prompts, URLs, and instructions aimed at the agent. Three-tier isolation:

| Tier | Touches filings? | Tools | Connectors |
|---|---|---|---|
| **`docket-reader`** | **Yes** | `Read`, `Grep` only | uyap (read-only, varsa) |
| `deadline-mapper` / Orchestrator | No — sees structured JSON only | `Read`, `Grep`, `Glob`, `Agent` | Yok (yalnızca yerel Read/Grep) |
| **`tracker-writer`** (Write-holder) | No | `Read`, `Write`, `Edit` | None |

`docket-reader` returns length-capped, schema-validated JSON. `deadline-mapper` has no MCP and no web — it applies rules the deploying team has configured. `tracker-writer` produces `./out/docket-report-<date>.md` and `./out/deadlines.yaml` and never sees raw filings.

## Adaptation notes

This cookbook is a starting point. It will not work in production until you have done the following:

- **MCP URL'lerini ayarlayın.** `UYAP_MCP_URL` kurumsal UYAP/dava takip endpoint'inizi göstermelidir; platformunuzun gerektirdiği kimlik doğrulama ayrıca yapılandırılmalıdır. `GDRIVE_MCP_URL` veya muadili, usul/süre tablolarınızın yaşadığı yere işaret eder. Bağlı MCP yoksa kullanıcı dışa aktarılan UYAP kayıtlarını sağlar.
- **Load the portfolio.** The agent reads `matters/_log.yaml` plus the per-matter `docket_id` and `court` from the deploying team's litigation-legal configuration. If your docketing system is the source of truth, front it with an MCP or a scheduled sync into the config path.
- **Usul ve mahkeme uygulaması tablolarını yapılandırın.** Deadline-mapper'a portföydeki her mahkeme/daire için uygulanacak süre, yerel uygulama ve özel emir tablolarını verin. Bilinmeyen mahkeme `confidence: low` + `needs_verification: true` üretmelidir; sessiz varsayılan kullanılmaz.
- **Wire delivery.** Decide where the output goes: your docketing system ingests `./out/deadlines.yaml`; the narrative report goes to Slack, email, or your matter management workspace; critical flags route to whoever you want woken up.
- **Set the schedule.** Weekly for most matters; daily for anything with a hearing inside 14 days, duruşma veya tahkikat/bilirkişi aşaması, or any `risk: critical` matter.

## Computed deadlines are leads, not calendar entries

**The computed deadlines this agent produces require human verification against the controlling local rule, standing order, and case management order before they are calendared. Missing a court deadline has malpractice consequences. This agent surfaces deadlines; a human verifies and dockets them.**

Every deadline carries `confidence` and `needs_verification` fields. The report segregates low-confidence entries and stamps a verification callout on anything not derived from an unambiguous statutory/procedural rule. Treat that as the minimum — not the ceiling — of human review. Judges and chambers may override defaults by individual order, local practice may change, and the date the clerk actually records service may differ from the date displayed.

**Not guaranteed:** this agent recommends a deadline; the docketing attorney confirms against the controlling rule and books the date.
