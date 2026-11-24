---
name: matter-briefing
description: >
  Tek bir dava veya uyuşmazlık dosyası hakkında kapsamlı özet brifing hazırlar —
  mevcut safahat, son gelişmeler, sıradaki kesin süre, açık sorular ve risk
  yeniden değerlendirme kontrolü. Hukuk Başmüşaviri (GC) brifingi veya dış büro
  toplantısı öncesinde kullanılır.
argument-hint: "[slug]"
---

# /matter-briefing

1. `~/.claude/plugins/config/legal-turkish/litigation-legal/CLAUDE.md` dosyasını (`## 1. Risk Kalibrasyonu`, `## Bunu Kim Kullanıyor`, `## Çıktılar (Outputs)`) oku.
2. `~/.claude/plugins/config/legal-turkish/litigation-legal/matters/[slug]/matter.md`, `history.md` ve `matters/_log.yaml` içindeki ilgili satırı (`uyap_no`, `arabuluculuk`, `next_deadline` dahil) oku.
3. Brifing üret: mevcut usuli durum, son güncellemeden bu yana gelişmeler, yaklaşan kesin süre/duruşma, açık sorular ve "mevcut `risk:` derecesi hâlâ gerçeği yansıtıyor mu?" kontrolü.
4. Güncellik uyarısı: `last_updated` > 30 gün ise dosya başında bayrakla.

---

## Amaç

Avukata veya yöneticiye toplantıya girmeden önce tek bakışta dosyanın gerçek durumunu vermek: safahat, risk, yaklaşan süre ve kritik karar noktaları.

## Çıkar Çatışması Kapısı (Atlanamaz Kural)

Brifing yazmadan önce `matters/_log.yaml` içinde `[slug]` kaydını doğrula. Dosya `_log.yaml` içinde yoksa reddet ve yönlendir:

> "`_log.yaml` içinde `[matter slug]` kaydını bulamıyorum. Çıkar çatışması kontrolü ve matter workspace kurulumu için önce `/litigation-legal:matter-intake` çalıştırın; kayıt altına alınmamış bir dosya için brifing üretmem."

## Brifing Şablonu

```markdown
[GİZLİ HUKUKİ ÇALIŞMA TASLAĞI - bkz. CLAUDE.md ## Çıktılar (Outputs) ve ## Bunu Kim Kullanıyor]

# [Dosya Adı] — Dosya Brifingi ([YYYY-AA-GG])

**UYAP Esas / Dosya No:** [uyap_no veya bekliyor]
**Arabuluculuk:** [arabuluculuk durumu — zorunlu dava şartı / ihtiyari / tamamlandı]
**Durum / Safahat:** [status / stage]
**Risk:** [rating] ([etki] × [olasılık])
**Önemlilik (`materiality`):** [kategori]
**Dış Hukuk Bürosu:** [büro — sorumlu avukat]
**Son Güncelleme:** [tarih] [>30 gün ise ⚠️ ESKİ BİLGİ işareti]
**Çıkar Çatışması (`conflicts`):** [durum — `pending` veya `not-run` ise ⚠️]

---

## Tek Paragraflık Özet
[Mevcut hukuki pozisyon, ne talep edildiği/savunulduğu ve belirleyici kilit olgu.]

## Son Gelişmeler
[history.md içindeki en güncel 3–5 kayıt, yeniden eskiye. İnceyse açıkça belirt.]

## Sırada Ne Var
- **En yakın süre / duruşma:** [`next_deadline` + yasal dayanak (ör. HMK m. 281 bilirkişiye itiraz / istinaf / cevap süresi)]
- **Yaklaşan aşamalar:** [matter.md veya history.md içindeki tarihli adımlar]
- **Bekleyen kararlar:** [açık karar kalemleri]

## Mali Risk ve Karşılık (Exposure & Reserve)
[Talep/risk tutarı (TL/döviz), girişten bu yana değişiklik ve finans/denetim komitesi karşılık eşiği kontrolü.]

## İç Sahipler
[Hukuk içi sorumlu ve dahil edilmesi gereken diğer birimler (İK, Finans, CISO vb.).]

## Risk Yeniden Değerlendirme Kontrolü
*(Cevap değil, kontrol sorusu)*
- `risk: [rating]` hâlâ dosyadaki gerçek seyri yansıtıyor mu?
- `materiality: [category]` güncellenmeli mi (örn. yeni bilirkişi raporu sonrası karşılık ayrılması)?
- Yeni bir teknik/kurumsal paydaş eklenmesi gerekiyor mu?

## Açık Sorular
[Çözülmemiş hukuki veya olgusal noktalar]

## Görüşme Gündemi *(belirli bir toplantı amacı verildiyse)*
[Dış büroya veya yönetime sorulacak somut sorular ve alınacak kararlar]
```

## Güncellik ve Üslup

- `last_updated` > 30 gün ise üstte uyar ve toplantı sonrasında `/litigation-legal:matter-update [slug]` çalıştırmayı öner.
- Süsleme veya şişirme yapma; tarihçe kısaysa brifingi kısa tut, bilinmeyeni açıkça "bilinmiyor" yaz.

## Kapanış

`## Çıktılar (Outputs)` uyarınca Sonraki Adımlar Karar Ağacı ile bitir.

## Yapmadıkları

- Dava sonucuna dair kesin öngörü/tahmin yürütmez; risk derecesi mevcut değerlendirmedir.
- Tek başına strateji kararı vermez veya `_log.yaml` üzerinde yazma işlemi yapmaz (yazma için `/litigation-legal:matter-update` kullanılır).
