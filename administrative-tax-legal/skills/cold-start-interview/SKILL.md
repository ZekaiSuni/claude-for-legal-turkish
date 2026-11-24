---
name: cold-start-interview
description: >
  Yeni bir kurum, mükellef veya hukuk/vergi bürosu için `administrative-tax-legal`
  eklentisinin uyuşmazlık duruşunu, e-tebligat/UETS izleme kurallarını,
  uzlaşma/dava onay eşiklerini ve portföy yollarını etkileşimli görüşme ile
  yapılandırarak `CLAUDE.md` bölümlerini doldurur.
---

# İdare & Vergi Eklentisi İlk Kurulum Görüşmesi (`cold-start-interview`)

Kurumun veya büronun vergi ve idari yargı pratiğine uygun varsayılanlarını belirleyerek `CLAUDE.md` içindeki `## Kurum / Büro Profili`, `## Kullanıcı Rolü`, `## İdare ve Vergi Uyuşmazlık Duruşu` ve `## Dava, Başvuru ve Tebligat Süre Kuralları` bölümlerini yapılandırır.

## Güvenlik ve Çekirdek Kurallar

- `CLAUDE.md` içindeki `## Çekirdek Güvenlik Kuralları (Shared Guardrails)` esas alınır: belirtilmeyen tutar, eşik veya vergi dairesi bilgisi sessizce tamamlanmaz (`[Kullanıcı Doğrulaması Gerekli]`).

## Adım 1 — Profil ve Yetki Soruları (3 Odaklı Blok)

1. **Kurum Kimliği ve Taraf Profili:**
   - Kuruluş tipi (`kurumsal_mukellef`, `holding_finans`, `kobi`, `belediye_ve_kamu`, `hukuk_burosu`) ve kullanıcının rolü (`idare_vergi_avukati`, `in_house_hukuk_musaviri`, `vergi_uyusmazlik_uzmani`, `mali_islerle_koordinasyon`).
   - Dava/uyuşmazlıklarda ağırlıklı duruş: vergi mükellefi/davacı mı, idare/belediye vekili mi, yoksa ikisi de (`karma`) mı?
2. **Ağırlıklı Uyuşmazlık Alanları ve Eskalasyon Eşikleri:**
   - Öncelikli alanlar: VUK vergi incelemesi ve tarhiyat davaları, `6183` ödeme emri/e-haciz savunması, `KVKK/Rekabet/SPK/BTK/EPDK` idari para cezaları, `4734 KİK` kamu ihale şikâyetleri veya tam yargı tazminat davaları.
   - Kıdemli avukat / YMM / yönetim onay eşiği (`TRY` bazlı tutar sınırı) ve `7524 s. K.` sonrası salt ceza uzlaşma / `VUK m. 376` peşin indirim yetki sınırı.
3. **Arşiv, e-Tebligat ve Şablon Tercihleri:**
   - Ana portföy kaydı yolu (`references/idari-vergi-register.yaml` veya Google Drive/yerel dosya) ve özel dilekçe şablonları (`~/.claude/plugins/config/legal-turkish/administrative-tax-legal/`).

## Adım 2 — `CLAUDE.md` Güncellemesi ve Sonraki Adım

Cevaplar doğrultusunda `CLAUDE.md` ve `### Onay ve Eskalasyon Matrisi` eşiklerini güncelle. Değişiklikleri özetle ve mevcut dosyaların taranması için `/administrative-tax-legal:uyusmazlik-portfolio` veya yeni dosya açılışı için `/administrative-tax-legal:matter-workspace` komutunu öner.
