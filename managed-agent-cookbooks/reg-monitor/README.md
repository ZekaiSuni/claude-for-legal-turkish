# Reg Monitor — managed-agent template

## Overview

Türkiye düzenleyici kaynaklarını zamanlanmış olarak kontrol eder, önem eşiğine göre sınıflandırır, maddi kalemlerde politika kütüphanesine hızlı gap kontrolü uygular ve digest yazar. Aynı kaynak mantığı [`reg-change-monitor`](../../regulatory-legal/agents/reg-change-monitor.md) ajanı ile [`reg-feed-watcher`](../../regulatory-legal/skills/reg-feed-watcher) / [`policy-diff`](../../regulatory-legal/skills/policy-diff) skill'lerinde kullanılır; bu dizin `POST /v1/agents` için Managed Agent cookbook'tur.

## ⚠️ Before you deploy

- **Digest items are screened leads, not legal conclusions.** The materiality filter applies a configurable threshold, not legal judgment. A regulatory change the agent classifies as "informational" may still be material to your business. A change it flags as "material" may turn out not to apply. Review every digest; a licensed attorney decides whether an item requires action, disclosure, policy change, or escalation.
- **The policy gap check is a first pass, not a legal assessment of applicability.** The gap surface compares new regulatory text against your policy library using heuristics. A "gap" is a lead for a lawyer to evaluate; an "aligned" result does not certify compliance.
- **The materiality threshold is your calibration, not law.** If your `## Materiality threshold` section is stale or was tuned for a different risk posture, the triage is stale. Recheck before enabling scheduled runs.
- **İzleme listesi sizin kapsam beyanınızdır.** Listede olmayan bir kurum yine de maddi bir şey yayımlayabilir. Eksik kurum, kaynak altyapısı değil yapılandırma hatasıdır.

## Deploy

```bash
export ANTHROPIC_API_KEY=sk-ant-...
export GDRIVE_MCP_URL=...
../../scripts/deploy-managed-agent.sh reg-monitor
```

## Steering events

See [`steering-examples.json`](./steering-examples.json). The default weekly sweep uses the first example. The other two cover targeted deep checks on a specific development and gap analysis on a flagged item.

## Security & handoffs

Regülasyon kaynak içeriği (Resmi Gazete kayıtları, Mevzuat sayfaları, kurum duyuruları ve güvenilir hukuk veri tabanı bildirimleri) **güvenilmeyen girdidir.** Üç katmanlı izolasyon:

| Tier | Touches untrusted docs? | Tools | Connectors |
|---|---|---|---|
| **`feed-reader`** | **Yes** | `Read`, `Grep`, `WebFetch` only | None |
| `materiality-filter` / Orchestrator | No | `Read`, `Grep`, `Glob`, `Agent` | gdrive (orchestrator only) |
| **`digest-writer`** (Write-holder) | No | `Read`, `Write`, `Edit` | None |

`feed-reader` length-capped, schema-validated JSON döndürür. `materiality-filter`, bu JSON ve diskteki regulatory-legal yapılandırması üzerinde saf hesaplama yapar — MCP yok, web yok. `digest-writer` `./out/reg-digest-<YYYY-MM-DD>.md` üretir ve Slack teslimi gerekiyorsa `handoff_request` çıkarır.

**Handoffs:** the orchestrator routes the `handoff_request` from `digest-writer` to a Slack send worker using the channel from the deploying team's House style configuration. The agent never sends Slack messages itself.

**Not guaranteed:** this agent surfaces changes and flags potential policy gaps; a lawyer decides whether a regulatory change requires action and who owns the response.

## Adaptation notes

Before you trust the output on your workflow:

- **`feed-reader` için kaynakları belirleyin.** Varsayılan omurga Resmi Gazete, Mevzuat ve ilgili kurum sayfalarıdır. Güvenilir Türk hukuk veri tabanı, sektör birliği veya kurum RSS/HTML kaynağı kullanıyorsanız uçları `web_fetch` allowlist'e ekleyin ve orchestrator tarama planını buna göre ayarlayın.
- **Opsiyonel veri tabanı bağlantılarını ayarlayın.** Lexpera, kurum içi hukuk veri tabanı veya benzeri bir kaynak kullanıyorsanız manifest içinde bağlantıyı açıkça yapılandırın.
- **Configure the digest delivery channel.** The digest-writer emits a `handoff_request` that names a Slack channel. The orchestrator reads that channel from your regulatory-legal configuration's **House style → Reg digest** field. Set it before the first scheduled run or the handoff will dead-letter. Teams that want the digest by email or in a Confluence page instead should swap the handoff target in the orchestrator allowlist.
- **Tune the materiality threshold.** The materiality-filter reads your configuration's `## Materiality threshold` section — always material / review-worthy / FYI. Confirm the tiers reflect your current risk posture before enabling scheduled runs; a threshold set too low floods the digest, too high and you miss obligations with deadlines.
- **Update the watchlist.** The materiality-filter also reads the `## Regulators we watch` table. Add or remove regulators as your footprint changes.
- **Confirm the work-product header.** The headless append in `agent.yaml` instructs the agent to prepend your configuration's work-product header. Verify the header language with your GC before turning this on.
- **Cadence.** Weekly is the default. Active regulatory environments (financial services rulemaking cycles, cross-border AI regulation) may warrant daily. The cadence lives in your own workflow engine — the cookbook does not schedule itself.
