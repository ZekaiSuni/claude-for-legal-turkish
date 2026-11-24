# Launch Radar — Managed Agent Şablonu

## Genel Bakış

Ürün ekibinin yol haritası / lansman takip aracını (Linear veya Asana) önümüzdeki haftalarda çıkacak özellikler için tarar ve Türk ürün hukuku kalibrasyonuna göre (6502 tüketici, 6563 e-ticaret, Reklam Kurulu, KVKK/İYS, BTK/BDDK/SPK/TİTCK sektör düzenlemeleri ve AI) haftalık radar notu üretir.

Kaynak eklenti: [`product-legal`](../../product-legal) (`launch-watcher` ajanı).

## ⚠️ Yayına Almadan Önce

- **Radar triyajı hukuki onay değil, yönlendirme kararıdır.** `"Needs review"` ürün avukatının incelemesi gerektiği anlamına gelir; `"skip"` lansman izni değildir.
- **Ticket başlıkları ve açıklamaları güvenilmez girdidir.** `memo-writer` formül enjeksiyonu ve tıklanabilir link kaçışı uygular.

## Dağıtım (Deploy)

```bash
export ANTHROPIC_API_KEY=sk-ant-...
export LINEAR_MCP_URL=... ASANA_MCP_URL=... GDRIVE_MCP_URL=...
../../scripts/deploy-managed-agent.sh launch-radar
```

Yalnızca kullandığınız araçların URL'lerini tanımlayın; yapılandırılmayanlar atlanır.

## Yönlendirme (Steering) Örnekleri

Bkz. [`steering-examples.json`](./steering-examples.json).

## Güvenlik ve El Değiştirme (Handoff)

| Katman | Güvenilmez ticket görür mü? | Araçlar | Bağlayıcılar |
|---|---|---|---|
| **`tracker-reader`** | **Evet** | `Read`, `Grep` | Linear, Asana (salt okunur) |
| `risk-classifier` / Orkestratör | Hayır | `Read`, `Grep`, `Glob`, `WebFetch`, `Agent` | Linear / Asana / Google Drive (salt okunur) |
| **`memo-writer`** (Yazma yetkili) | Hayır | `Read`, `Write`, `Edit` | Yok |

`memo-writer`, `./out/launch-radar-<tarih>.md` dosyasını üretir. Tam lansman incelemesi gereken işler için orkestratör `handoff_request` ile `launch-review` akışını tetikler.

## Uyarlama Notları

- **Risk Kalibrasyonu:** `product-legal/CLAUDE.md` içindeki Türkiye risk kalibrasyonu ve sektör eşiklerini (`/product-legal:cold-start-interview` ile) doldurun.
- **Tetikleyici Kelimeler:** Türk ürün hukukuna uygun KVKK, İYS, mesafeli satış, abonelik, Reklam Kurulu, sağlık/finans/telekom ve AI anahtar kelimelerini ürün yüzeyinize göre uyarlayın.
