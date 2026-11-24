# Diligence Grid — Managed Agent Şablonu

## Genel Bakış

Sanal veri odası (VDR) veya Google Drive/yerel M&A klasörü üzerinde toplu belge incelemesi ve tablo çıkarımı yapar. İki modda çalışır:

- **watch** — Belirli bir tarihten sonra yüklenen yeni belgeleri izler, `corporate-legal` talep listesi (request-list) kategorilerine göre sınıflandırır ve yüksek öncelikli kategorileri (Önemli Sözleşmeler, Dava/Uyuşmazlık, Fikri Mülkiyet, KVKK, Rekabet) bayraklar.
- **grid** — Bir belge klasörü üzerinde sütun şemasına göre tablo incelemesi çalıştırır. Her belge bir satır, her veri noktası bir sütun olur; her hücre birebir metin alıntısına bağlanır.

Kaynak eklenti: [`corporate-legal`](../../corporate-legal). Grid modu, `tabular-review` skill'ini arka planda yürütür.

## ⚠️ Yayına Almadan Önce

- **Her hücre bir inceleme işaretidir (lead), kesin hukuki bulgu değildir.** İlgili avukat dayanak belgeleri okumadan ve onaylamadan tablo tek başına beyan/tekeffül veya due diligence raporu yerine geçmez.
- **Önemlilik ve sütun sınıflandırmaları sezgisel ön elemedir.** Önemsiz görünen bir sözleşme işlemi durdurabilecek kontrol değişikliği veya cezai şart hükmü içerebilir.
- **Karşı tarafın yüklediği belgeler güvenilmez girdidir.** `grid-writer` içindeki CSV formül enjeksiyonu savunması (`=`, `+`, `-`, `@`, tab, CR önek kaçışı) zorunludur.

## Dağıtım (Deploy)

```bash
export ANTHROPIC_API_KEY=sk-ant-...
export GDRIVE_MCP_URL=...
../../scripts/deploy-managed-agent.sh diligence-grid
```

## Yönlendirme (Steering) Örnekleri

Bkz. [`steering-examples.json`](./steering-examples.json).

## Güvenlik ve El Değiştirme (Handoff)

| Katman | Güvenilmez belge görür mü? | Araçlar | Bağlayıcılar |
|---|---|---|---|
| **`doc-reader`** | **Evet** (salt okunur) | `Read`, `Grep` | Google Drive (salt okunur) / yerel VDR |
| **`extractor`** | **Evet** (salt okunur) | `Read`, `Grep` | Yok |
| `normalizer` / Orkestratör | Hayır | `Read`, `Grep`, `Glob`, `Agent` | Yok |
| **`grid-writer`** (Yazma yetkili) | Hayır | `Read`, `Write` | Yok |

`grid-writer` yalnızca `./out/diligence-grid-<tarih>.csv`, `./out/diligence-grid-<tarih>_sources.csv` ve `./out/diligence-grid-<tarih>-summary.md` dosyalarını üretir.

## Uyarlama Notları

- **VDR Kaynağı:** Varsayılan bağlayıcı `GDRIVE_MCP_URL` üzerinden Google Drive'dır; bağlı MCP yoksa belgeler yerel klasör/dışa aktarım üzerinden okunur.
- **Sütun Şeması:** Varsayılan şema Türkiye M&A pratiğine göre uyarlanmış [`ma-diligence-columns.md`](../../corporate-legal/skills/tabular-review/references/ma-diligence-columns.md) dosyasıdır (TİTCK, KİK, SPK, BDDK, TCMB, BTK, EPDK, Rekabet, KVKK ve DVK kontrolleri dahil).
- **Gizli Çalışma Başlığı:** `grid-writer`, `corporate-legal` profilinin `## Çıktı kuralları` bölümündeki başlığı ekler.
- **Bildirim Yönlendirmesi:** Ajan doğrudan Slack'e yazmaz; tamamlandığında `handoff_request` üretir.
