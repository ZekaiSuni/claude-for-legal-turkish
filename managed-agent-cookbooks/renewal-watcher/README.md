# Renewal Watcher — Managed Agent Şablonu

## Genel Bakış

Sözleşme arşivini (`renewal-register.yaml`, Google Drive veya yerel imzalı sözleşmeler klasörü) yaklaşan yenileme ve fesih/yenilememe ihbar süreleri için tarar; `commercial-legal` playbook pozisyonlarıyla karşılaştırır, sapmaları ve eskalasyon tetiklerini işaretleyip `./out/renewal-alerts-<YYYY-MM-DD>.md` uyarısı üretir.

Kaynak eklenti: [`commercial-legal`](../../commercial-legal) (`renewal-watcher` ajanı ve `renewal-tracker` skill'i).

## ⚠️ Yayına Almadan Önce

- **Meta veriden çekilen yenileme ve fesih son tarihleri hatalı olabilir.** Ek protokol veya zeyilnameler nedeniyle tarihler değişmiş olabilir; hukukçu imzalı metin ve KEP/noter/TTK m. 18/3 bildirim şartını doğrulamadan işlem yapılmamalıdır.
- **Eskalasyon yönlendirmesi profil matrisini uygular, hukuki onay vermez.**
- **Sessiz haftalar temiz hafta değildir.** Kayıt defterine işlenmemiş sözleşmeler olabilir.

## Dağıtım (Deploy)

```bash
export ANTHROPIC_API_KEY=sk-ant-...
export GDRIVE_MCP_URL=...
../../scripts/deploy-managed-agent.sh renewal-watcher
```

## Yönlendirme (Steering) Örnekleri

Bkz. [`steering-examples.json`](./steering-examples.json).

## Güvenlik ve El Değiştirme (Handoff)

| Katman | Güvenilmez belge görür mü? | Araçlar | Bağlayıcılar |
|---|---|---|---|
| **`repo-reader`** | **Evet** | `Read`, `Grep` | Google Drive (salt okunur) / yerel arşiv |
| `deadline-calculator` / Orkestratör | Hayır | `Read`, `Grep`, `Glob`, `Agent` | Yok |
| **`alert-writer`** (Yazma yetkili) | Hayır | `Read`, `Write`, `Edit` | Yok |

`alert-writer` doğrudan Slack mesajı atmaz; rapor tamamlandığında `handoff_request` üretir. Ayrıca tüm metin alanlarında Excel formül enjeksiyonu ve Markdown link kaçışı uygulanır.

## Uyarlama Notları

- **Arşiv Bağlantısı:** Google Drive için `GDRIVE_MCP_URL` ayarlayın; bağlı MCP yoksa yerel `renewal-register.yaml` ve sözleşme dosyaları üzerinden çalışır.
- **KEP / Noter Tamponu:** İhbar yöntemine göre `transit_buffer_days` (ör. KEP Yönetmeliği m. 15/2 gereği en az +1 gün; noter/posta için iş günü tamponu) ve `send_by_effective` tarihini kontrol edin.
- **Bildirim Kanalı:** `commercial-legal` profilindeki `## Renewal Tracking` hedef kanalını ayarlayın.
