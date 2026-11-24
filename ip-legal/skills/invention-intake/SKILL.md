---
name: invention-intake
description: >
  Buluş bildirim formunun (Invention Disclosure) ilk aşama ön değerlendirmesini
  yapar — yenilik, buluş basamağı, 6769 s. SMK m. 82 patentlenebilirlik
  istisnaları, m. 84 12 aylık hoşgörü süresi, m. 113–122 hizmet/serbest buluş
  bildirim süreci, m. 142 faydalı model ve TTK m. 54–55 ticari sır stratejisi
  açısından inceler. Patent istemi yazmaz ve patentlenebilirlik mütalaası vermez.
argument-hint: "[buluş bildirimini yapıştırın veya başlığı yazın]"
---

# /invention-intake

## ⚠️ BU BİR İLK AŞAMA TARAMASIDIR — PATENTLENEBİLİRLİK MÜTALAASI DEĞİLDİR VE İSTEM YAZMAZ

Buluş sahibinden veya Ar-Ge'den gelen buluş bildirimini 6 süzgeçten geçirerek ön teknik taramaya ve patent vekili incelemesine gitmeye değer olup olmadığını, kaçırılmaması gereken **SMK m. 84** hoşgörü/kamuya açıklama sürelerini ve **SMK m. 113–122** çalışan buluşu prosedürünü raporlar.

## İş Akışı ve 6 Ön Süzgeç

1. `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` dosyasını (`## Şirket Profili`, `## Kullanıcı Rolü`, `## Fikri Mülkiyet (IP) Uygulama Profili`, `## Çıktılar`, `## Matter Workspaces`) oku.
2. Aşağıdaki 6 süzgeci uygula:

### Süzgeç 1 ve 2: Yenilik & Buluş Basamağı Sinyalleri (`6769 s. SMK m. 83`)
- Mevcut çözümden neyi farklı yapıyor; sadece bilinen iki unsurun olağan toplamı mı yoksa öngörülmeyen teknik bir etki/iyileştirme var mı? *(Ön değerlendirmedir; önceki teknik araması için vekil ve Espacenet/Patentscope/TÜRKPATENT taraması gerekir.)*

### Süzgeç 3: Patentlenebilirlik Konusu ve İstisnaları (`SMK m. 82`)
- **Önemli:** Türkiye **SMK m. 82** ve Avrupa **EPC m. 52** birbirine paraleldir: keşifler, bilimsel teoriler, matematik metotları, zihinsel faaliyet/iş metotları ve **tek başına bilgisayar programları** patentlenemez; ancak somut **teknik bir soruna teknik katkı sağlayan (teknik karakter taşıyan)** bilgisayar tabanlı buluşlar patentlenebilir `[doğrula]`.
- Teşhis/tedavi/cerrahi usulleri (m. 82/3-c) ve diğer sınır durumları otomatik olarak 🔴/🟡 ile işaretle ve **TÜRKPATENT / EPO İnceleme Kılavuzu** çerçevesinde uzman patent vekili görüşüne yönlendir (`[review]`). *(Yabancı ABD başvurusu planlanıyorsa ABD `§101` ölçütlerinin farklı olduğu ayrıca not edilir.)*

### Süzgeç 4: Kamuya Açıklama ve Hoşgörü Süresi (`SMK m. 84`) — EN KRİTİK SAAT
- Buluş makale, sunum, fuar, git deposu, satış teklifi veya ürün satışı yoluyla kamuya açıklandı mı?
- **Türkiye / SMK m. 84 (12 Aylık Hoşgörü Süresi):** Buluş sahibi tarafından yapılan açıklamalar başvuru tarihinden önceki **12 ay** içinde kalıyorsa Türkiye'de yeniliği ortadan kaldırmaz; **12 ay geçmişse hak kaybedilmiştir (`🔴`)**.
- **Yurt Dışı (EPO/PCT) Uyarısı:** Avrupa Patent Sözleşmesi (EPO) başta olmak üzere birçok yabancı ülkede Türkiye'deki gibi 12 aylık genel hoşgörü süresi **yoktur** (yalnızca çok dar suistimal/resmî sergi istisnaları vardır) — yurt dışı patent hedefleniyorsa ilk kamuya açıklamadan **önce** başvuru zorunludur!

### Süzgeç 5: Çalışan Buluşları (Hizmet Buluşu vs. Serbest Buluş — `SMK m. 113–122`)
- Buluş şirketin faaliyet alanında veya kurum deneyimi/imkânlarıyla mı ortaya çıktı (**Hizmet Buluşu** m. 113)?
- Buluşçunun işverene **yazılı bildirim yükümlülüğü** ve işverenin bildirimden itibaren **4 ay içinde tam veya kısmi hak talebinde bulunma** hak düşürücü süresi (`SMK m. 115`) ile bedel/ödül yönetmeliği gereklilikleri hatırlatılır `[doğrula]`. *(AI araçları buluşa katkı verdiyse gerçek kişi buluşçu şartını ayrıca `[review]` bayrakla!)*

### Süzgeç 6: İhlalin Tespit Edilebilirliği ve Ticari Sır vs. Patent (`Faydalı Model m. 142` & `TTK m. 54–56`)
- Rakibin ürününde tersine mühendislik/ürün analiziyle ihlalin görülmesi mümkün mü? Arka planda çalışan bir sunucu algoritmasıysa ve tersine mühendislikle anlaşılamıyorsa **patent (20 yıl sonra kamuya açıklanır)** yerine **TTK m. 54–56 ticari sır koruması** daha rasyonel olabilir.
- Kimyasal maddeler ve usuller dışında, daha hızlı/düşük maliyetli koruma aranan mekanik/ürün yeniliklerinde **Faydalı Model (SMK m. 142 — 10 yıl koruma)** alternatifi not edilir.

## Çıktı Formatı

```markdown
[GİZLİ ÇALIŞMA ÜRÜNÜ - bkz. CLAUDE.md ## Çıktılar ve ## Kullanıcı Rolü]

> **⚠️ Reviewer note**
> - **Kaynaklar:** [Kullanıcının sağladığı buluş bildirimi — önceki teknik MCP bağlı değil]
> - **Hukukçu/Vekil kararı gerektirenler:** [SMK m. 82 teknik katkı, m. 84 açıklama tarihi, m. 115 4 aylık süre `[review]` / `[doğrula]`]

# Buluş Bildirimi Ön Değerlendirmesi: [Buluş Başlığı]

**Ön Tavsiye:** [Önceki Teknik Araştırmasına / Patent Vekiline Yönlendir | Faydalı Model Değerlendir | Ticari Sır Olarak Koru | Bilgi Eksik / Dur]
**Acil Tarih Uyarısı:** [SMK m. 84 12 ay sınırı ve varsa EPO/yurt dışı ön başvuru uyarısı]

## 6 Süzgeç Özeti
| Süzgeç | Durum | Gerekçe |
|---|---|---|
| Yenilik & Buluş Basamağı (SMK m. 83) | | |
| Patentlenebilirlik İstisnası (SMK m. 82) | | |
| Kamuya Açıklama & Hoşgörü (SMK m. 84) | | |
| Hizmet Buluşu Süreci (SMK m. 113–122) | | |
| Tespit Edilebilirlik & Ticari Sır / Faydalı Model | | |

## Patent Vekiline İletilecek Sorular & Sonraki Adımlar
- [TÜRKPATENT siciline kayıtlı Patent Vekili / uzman avukat incelemesi; **bu araç patent istemi yazmaz**]
```

**Non-lawyer kapısı:** Kamuya açıklama planı veya başvuru kararı öncesinde yetkili avukat / TÜRKPATENT Patent Vekili onayı al; kapanışta Sonraki Adımlar Karar Ağacı sun.
