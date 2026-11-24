---
name: fto-triage
description: >
  Faaliyet Serbestisi (Freedom-to-Operate - FTO) ilk geçiş triyajı — potansiyel
  engelleyici patent ve faydalı modelleri (6769 s. SMK m. 82–145), koruma
  durumunu (SMK m. 101), eşdeğerler doktrinini (m. 89) ve bağımsız istem
  unsur-unsur ön analizini çıkarır. Nihai FTO mütalaası değildir ve asla
  "lansmana temiz" sonucu vermez.
argument-hint: "[ürün, süreç veya özelliği ve hedef ülkeleri açıklayın]"
---

# /fto-triage

## ⚠️ BU BİR FTO MÜTALAASI DEĞİLDİR — İLK GEÇİŞ TRİYAJIDIR

Bu skill **ürünün lansmana temiz olduğu sonucuna asla varmaz** ve **patent istemi yazmaz**. Çıktısı; ürün veya teknoloji piyasaya çıkmadan önce patent vekili ve teknik ekibin inceleyeceği yüksek riskli patent sinyallerini ve unsur-unsur ön karşılaştırmasını (`claim-chart first pass`) ortaya koymaktır.

## İş Akışı

1. `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` dosyasını (`## Şirket Profili`, `## Kullanıcı Rolü`, `## Entegrasyonlar`, `## Fikri Mülkiyet (IP) Uygulama Profili`, `## Uygulama ve İhtar Duruşu (Enforcement Posture)`, `## Çıktılar`, `## Öznel Hukuki Değerlendirmelerde Karar Duruşu`, `## Matter Workspaces`) oku.
2. **Teknik ve coğrafi kapsamı al:** Ürün/yazılım/yöntemin teknik çalışma adımları, hangi ülkelerde üretileceği/satılacağı (**Türkiye** dışında üretim/ihracat yapılan AB/EPO/PCT ülkeleri), lansman zamanlaması ve kullanıcının elinde tespit edilmiş rakip patent numaraları.
3. **Kapsam sınırı:** Patent ve faydalı model incelemesidir; tasarım hakları için ayrı tasarım FTO kontrolü gerekeceğini not et.
4. **Araştırma ve Veri Kaynağı Disiplini:** Bağlı bir patent arama MCP'si yoktur. Kullanıcının paylaştığı tam patent metinlerini (`[kullanıcı sağladı]`) veya varsa web aramasıyla ulaşılan **TÜRKPATENT EPATS, EPO Espacenet, WIPO Patentscope, Google Patents** kayıtlarını (`[web search - verify]`) esas al; hiçbir patent numarasını veya istem metnini hafızadan uydurma.

## İncelenecek Türk Patent Hukuku Parametreleri (6769 s. SMK)

Her aday patent için şunları kontrol et:
- **Koruma ve Validasyon Durumu:** Patent/faydalı model **Türkiye'de tescilli mi**, yoksa Türkiye fazı validasyonu yapılmamış (sadece EPO/yabancı ülkede geçerli) bir patent mi? **SMK m. 101** yıllık sicil ücretleri ödenmiş mi yoksa hükümden düşmüş mü? Koruma süresi (patent 20 yıl, faydalı model 10 yıl) dolmuş mu? `[TÜRKPATENT / EPO Register üzerinden doğrula]`
- **Bağımsız İstem (Independent Claim) Unsur-Unsur Karşılaştırması:** İhlal için bağımsız istemin **tüm** unsurlarının üründe bulunması (`all-elements rule`) gerekir; ancak bulunmayan unsur **SMK m. 89 Eşdeğerler Doktrini** kapsamında aynı işlevi aynı yoldan görüp aynı sonucu veriyorsa eşdeğerlik riski vardır (`[review]`).
- **İstisna ve Savunmalar:** Önceki kullanım hakkı (**SMK m. 87**), ticari olmayan/deneme amaçlı fiiller (**SMK m. 85/3-(b)**), ilaç ruhsatlandırma / **Bolar istisnası (SMK m. 85/3-(c))** ve olası hükümsüzlük sinyalleri (**SMK m. 138**).
- **Kasıtlı İhlal ve Tazminat Uyarısı (`SMK m. 150–151`):** Üçüncü kişi patentini bile bile ve önlem almadan lansmana çıkmak yoksun kalınan kazanç ve tazminat riskini büyütür (`[doğrula]`).

## Çıktı Formatı

```markdown
[GİZLİ ÇALIŞMA ÜRÜNÜ - bkz. CLAUDE.md ## Çıktılar ve ## Kullanıcı Rolü]

> **⚠️ Reviewer note**
> - **Kaynaklar:** [Kullanıcının sağladığı patent metinleri / Espacenet / Patentscope `[web search - verify]` — canlı tam patent veri tabanı MCP bağlı değil]
> - **Okuma kapsamı:** [İncelenen bağımsız istemler ve teknik doküman]
> - **Hukukçu/Vekil kararı gerektirenler:** [`[review]` eşdeğerlik ve istem yorumu kalemleri]
> - **Güvenmeden önce:** TÜRKPATENT EPATS & EPO Register üzerinden hukuki durum (yıllık harç/validasyon) ve patent vekili incelemesi zorunludur

# Faaliyet Serbestisi (FTO) Ön İncelemesi: [Ürün / Özellik Adı]

**Hedef Ülkeler:** [Türkiye / AB / diğer]
**İlk Geçiş Sonucu:** [🔴 Yüksek İstem Örtüşmesi / Tasarım Değişikliği Gerekebilir | 🟡 Eşdeğerlik / İstem Yorumu İncelemesi Gerekiyor | 🟢 İncelenen Kayıtlarda Doğrudan Örtüşme Görülmedi — Profesyonel FTO Aramasına Tabidir]

## 1. Tespit Edilen Patent / Faydalı Model Adayları
| Numara | Ülke / Statü (TR Validasyonu?) | Beklenen Bitiş | İlk Risk |
|---|---|---|---|

## 2. Bağımsız İstem Unsur-Unsur Ön Tablosu (`Claim Chart First Pass`)
*(Yalnızca önünüzde tam metni bulunan istemler için kurulur.)*
| İstem Unsuru | Bizim Ürün Özelliği | Birebir / Eşdeğer (SMK m. 89) / Eksik (`[review]`) |
|---|---|---|

## 3. Açık Teknik Sorular ve Azaltım Seçenekleri
- Tasarım etrafından dolanma (Design-around) noktaları, eski tarihli önceki teknik (SMK m. 138 hükümsüzlük adayı), lisanslama veya ürün kapsamı daraltma.

## 4. Önerilen Sonraki Adımlar
1. Yetkili **TÜRKPATENT kayıtlı Patent Vekili / Fikri Mülkiyet Avukatı** ile tam profesyonel FTO taraması (CPC/IPC sınıflarıyla).
```

**Non-lawyer kapısı:** Kullanıcı avukat/patent vekili değilse ürün sevkiyatı öncesi patent vekili/avukat incelemesi için 1 sayfalık brifing ver. Analizi Sonraki Adımlar Karar Ağacı ile bitir.
