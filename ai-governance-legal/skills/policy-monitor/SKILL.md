---
name: policy-monitor
description: >
  Şirketin veya büronun yapay zekâ kullanım politikasını fiilî uygulamayla güncel
  tutar — kaydedilmiş YZED/AIA, triyaj ve tedarikçi incelemelerinde haftalık politika
  sapması (drift) taraması yapar veya önerilen yeni bir AI uygulamasını mevcut
  politikaya karşı doğrudan kontrol eder (--sweep / doğrudan soru).
argument-hint: "[önerilen yeni AI uygulamasını yazın — ya da tarama için boş bırakın / --sweep]"
---

# /policy-monitor

## Modlar

**Tarama Modu (`--sweep` veya argümansız):**
1. `~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md` → `## Çıktılar` (çıktı klasörü, güncel AI politikası dokümanı, `Last policy sweep` tarihi) ve `## AI Politika Taahhütleri` / `## Yapay Zekâ Kullanım Envanteri` bölümlerini oku.
2. Son tarama tarihinden bu yana çıktı klasöründe biriken dosyaları tara (`Last policy sweep` yoksa tümünü tara ve `"İlk tarama"` notunu düş).
3. Onaylanmış YZED/AIA, triyaj ve imzalanmış tedarikçi AI incelemelerini güncel politika metni ve kullanım envanteriyle karşılaştır.
4. Eksikleri sınıfla: `ZORUNLU GÜNCELLEME (REQUIRED)` (politika fiilî uygulamayla çelişiyor veya dış muhatapları etkileyen taahhüt yanlış) vs. `TAVSİYE EDİLEN GÜNCELLEME (ADVISABLE)` (politika sessiz ama güncellemek daha temiz).
5. Envantere henüz işlenmemiş yeni kullanım senaryolarını bayrakla.
6. **Önemli Guardrail:** `Last policy sweep` ve `gaps_found` alanlarını tarama çalışınca otomatik güncelleme — yalnızca kullanıcı bulguları inceleyip açıkça onayladıktan/teyit ettikten sonra güncelle.

**Doğrudan Soru Modu (argüman olarak önerilen AI uygulaması verilirse):**
1. Profildeki güncel politika dokümanını, `## AI Politika Taahhütleri` ve `## Yapay Zekâ Kullanım Envanteri` bölümlerini oku.
2. Önerilen uygulamayı çözümle (ne yapıyor, otomasyon seviyesi, etkilenen kişiler, insan gözetimi, ifşa, tedarikçi veri kullanımı).
3. Politika ve envanterle diff çıkar: Karşılananlar / Eksikler / Çatışanlar + önerilen politika metni + envanter satırı önerisi.

**Zamanlanmış çalışma notu:** Haftalık tekrarlayan hatırlatmaları harici scheduler aracınızda kurabilirsiniz; bu eklenti kendi içinde otomatik cron çalıştırmaz.

## `## Çıktılar` Yapılandırılmamışsa

`## Çıktılar` altında `[PLACEHOLDER]` varsa doğrudan soru modunda yine çalış; ancak tarama (sweep) için çıktı klasörü tanımlamak üzere `/ai-governance-legal:cold-start-interview` öner. Yetkili kaynak summary değil, `**Güncel AI politikası dokümanı:**` yolundaki gerçek politika belgesidir.

## Mod 1: Tarama (Sweep) İnceleme Kriterleri

- **YZED / AIA Çıktıları:** Onaylanan senaryo envanterde var mı? Şartlı onay koşulları (insan gözetimi, müşteriye/çalışana aydınlatma, KVKK m. 11/1-(g) itiraz yolu) politikaya yansımış mı?
- **Triyaj (`CONDITIONAL` / `APPROVED`) Çıktıları:** Yeni bir kategori onaylandıysa politika kapsamını genişletiyor mu?
- **Tedarikçi AI İncelemeleri:** Politikanın "asla veri eğitimi olmaz" dediği yerde istisnalı bir tedarikçi kabul edildiyse politika metni gerçeği yansıtıyor mu?

### Tarama Raporu Formatı

```markdown
[GİZLİ HUKUKİ ÇALIŞMA TASLAĞI - bkz. CLAUDE.md ## Çıktılar]
*(Bu tarama gizli YZED ve sözleşme analizlerinden türetilmiştir; şirket genelinde filtresiz paylaşılmamalıdır.)*

> **⚠️ Reviewer note**
> - **Kaynaklar:** [Güncel AI politikası + N adet çıktı dosyası]
> - **Okuma kapsamı:** [Tarih sonrası N yeni dosya]
> - **Hukukçu kararı gerektirenler:** [Gerekli/Tavsiye karar kalemleri `[review]`]
> - **Güvenmeden önce:** [ZORUNLU güncellemeler canlıya çıkıştan önce karara bağlanmalıdır]

# AI Politika Takibi — Tarama Raporu

**Tarih:** [YYYY-AA-GG] | **Taranan dosya:** [N] | **Yeni dosya:** [N]
**Tespit edilen boşluk:** [N] ZORUNLU | [N] TAVSİYE EDİLEN

## ZORUNLU Güncellemeler (REQUIRED)
### [Boşluk Kısa Adı]
**Tetikleyen kaynak:** [dosya adı]
**Fiilî uygulama:** [kısa tanım]
**Mevcut politika:** [bölüm alıntısı veya "Kapsam yok"]
**Boşluk:** [neden yanıltıcı veya çelişkili]
**Önerilen ekleme/değişiklik:**
> *[Bölüm adı] altına ekleyin:*
> "[Kurum politikasıyla uyumlu, dayanıklı dilde metin]"

## TAVSİYE EDİLEN Güncellemeler (ADVISABLE)
[Aynı kısa format]

## Aksiyon Gerektirmeyenler
[Boşluk çıkmayan dosyalar]

## Yapay Zeka Kullanım Envanteri Eşitlemesi
[Envantere (`## Yapay Zekâ Kullanım Envanteri`) eklenmesi önerilen yeni satırlar]

## Sonraki Adımlar
- [ ] ZORUNLU politika güncellemelerini canlıya çıkıştan önce karara bağla (`[review]`)
- [ ] Yeni kullanım senaryolarını envantere işle
- [ ] İnceleme onaylandıktan sonra `Last policy sweep` ve `gaps_found` alanlarını güncelle
```

## Mod 2: Doğrudan Soru Formatı

Önce belirsizlik varsa tek netleştirici soru sor; uzun form açma. Ardından şu tabloyu doldur ve Rapor/Önerilen Metin/Zamanlama (`Canlıya geçmeden önce` vs. `Sonraki politika revizyonunda`) + Sonraki Adımlar Karar Ağacı ile kapat:

| Kontrol Alanı | Mevcut Politika / Envanter | Önerilen Uygulama | Sonuç |
|---|---|---|---|
| Kullanım Kategorisi | | | 🟢 Kapsamda / 🟡 Eksik / 🔴 Çatışma |
| Otomasyon & İnsan Gözetimi | | | |
| İlgili Kişiye Aydınlatma (KVKK m. 10 / 11-g) | | | |
| Tedarikçi Veri Kullanımı & KVKK m. 9 | | | |

## Yapmadıkları

- Politikayı kendi başına değiştirmez; insan onayı için öneri metni taslaklar.
- Yeni gelen dış mevzuatı takip etmez (bunun için `/ai-governance-legal:reg-gap-analysis` veya `regulatory-legal` kullanılır).
- E-posta veya Slack yazışmalarını taramaz; yalnızca çıktı klasörüne kaydedilmiş yapılandırılmış raporları inceler.
