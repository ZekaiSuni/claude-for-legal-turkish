---
name: cold-start-interview
description: >
  Yeni bir kurum veya hukuk bürosu için `execution-bankruptcy-legal` eklentisinin
  taraf duruşunu, UETS/tebligat izleme kurallarını, onay eşiklerini ve
  portföy dosya yollarını etkileşimli görüşme ile yapılandırır ve `CLAUDE.md`
  bölümlerini doldurur.
---

# İcra & İflas Eklentisi İlk Kurulum Görüşmesi (`cold-start-interview`)

Bu beceri, eklentiyi kullanacak kurumun veya hukuk bürosunun çalışma profilini tespit ederek `CLAUDE.md` içindeki `## Şirket / Büro Profili`, `## Kullanıcı Rolü`, `## Takip ve Tahsilat Duruşu (Collection & Defense Posture)` ve `## İcra Takip Portföyü ve Süre Kuralları` bölümlerini yapılandırır.

## Güvenlik ve Çekirdek Kurallar

- `CLAUDE.md` içindeki `## Çekirdek Güvenlik Kuralları (Shared Guardrails)` geçerlidir: kullanıcının belirtmediği hiçbir eşik, taraf rolü veya faiz tercihi sessizce tamamlanmaz (`[Kullanıcı Doğrulaması Gerekli]` olarak bırakılır).

## Adım 1 — Profil ve Taraf Duruşu Soruları (3 Blokta Kısa Görüşme)

Kullanıcıya tek seferde boğucu soru listesi vermek yerine aşağıdaki başlıklarda net ve kısa seçenekler sun:

1. **Kurum / Büro Kimliği ve Ağırlıklı Taraf Duruşu:**
   - Kuruluş türü (`hukuk_bürosu`, `banka_finans`, `kurumsal_şirket`, `kobi`, `belediye_kamu_iştiraki`) ve kullanıcının rolü (`icra_ve_iflas_avukati`, `in_house_hukuk_musaviri`, `alacak_takip_uzmani`, `konkordato_alacakli_temsilcisi`).
   - Dosyaların çoğunluğundaki taraf duruşu: ağırlıklı **Alacaklı** takibi mi, **Borçlu** savunması/itirazı mı, üçüncü kişi banka/şirket sıfatıyla **89/1 haciz ihbarnamesi** yönetimi mi, yoksa **Karma** mı?
2. **Alacak Türleri, Teminat ve Arabuluculuk Eşikleri:**
   - Sıklıkla karşılaşılan takip türleri: fatura/cari hesap (Örnek 7), çek/senet/bono (Örnek 10), kira/tahliye (Örnek 13), ipotek/ticari rehin (`İİK m. 45`), ilamlı (`Örnek 4-5`) veya konkordato masası (`İİK m. 285+`).
   - Kıdemli avukat / yönetim kurulu eskalasyon para sınırı (ör. `250.000 TRY`, `1.000.000 TRY` veya döviz bazlı eşikler) ve ihtiyatî hacizde teminat onay yetkisi.
3. **Portföy ve Belge Düzeni:**
   - Ana takip listesinin nerede tutulduğu (`references/takip-register.yaml`, özel Google Drive tablosu veya yerel klasör) ve varsa özel icra takip şablonlarının `~/.claude/plugins/config/legal-turkish/execution-bankruptcy-legal/` dizinine alınıp alınmayacağı.

## Adım 2 — `CLAUDE.md` Güncellemesi ve Özet

Kullanıcının cevaplarına göre `CLAUDE.md` dosyasındaki ilgili profil bloklarını ve `### Onay ve Eskalasyon Matrisi` eşiklerini güncelle. Değişiklikleri özetle ve portföy taraması için `/execution-bankruptcy-legal:takip-portfolio` veya yeni dosya açılışı için `/execution-bankruptcy-legal:matter-workspace` komutunu öner.
