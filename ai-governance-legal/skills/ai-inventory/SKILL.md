---
name: ai-inventory
description: >
  Sistem bazında AI envanteri yönetimi: Türkiye uyumu (KVKK, 7545 s. Kanun, TİHEK,
  sektörel kurallar) ve sınır ötesi AB AI Act kapsamında her yapay zekâ sisteminin
  rolünü (provider, deployer, importer, distributor, yetkili temsilci, ürün
  üreticisi) ve risk katmanını (prohibited, high_risk, limited, minimal, gpai,
  gpai_systemic) kayıt altında tutar. "ai inventory", "AI envanteri", "sistem ekle",
  "bu sistemi sınıflandır" istendiğinde kullanılır.
argument-hint: "[list | add | edit <id> | classify <id> | show <id>]"
---

# /ai-inventory

## Ne Zaman Çalışır

Kullanıcı şirketindeki veya müvekkilindeki yapay zekâ sistemlerinin envanterini yönetmek istediğinde çalışır. Temel ilke: **rol ve risk seviyesi şirket bazında değil, her AI sistemi için ayrı ayrı belirlenir.** Tek bir kurum A sisteminin *geliştiricisi (provider)*, B sisteminin *kullanıcısı (deployer)* ve C sisteminin *ithalatçısı* olabilir. Envanter bu değerlendirmeleri izler; somut hukuki yükümlülükler tablodan otomatik çekilmez, hukukçu denetiminde konuşma içinde ve gerektiğinde `/ai-governance-legal:aia-generation` ile çıkarılır.

## İş Akışı

1. **Profili oku:** `~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md` dosyasını (`## Şirket Profili`, `## AI Sistem Envanteri`, `## Çıktılar`) oku. Dosya yoksa veya `[PLACEHOLDER]` içeriyorsa önce `/ai-governance-legal:cold-start-interview` yönlendirmesi yap.
2. **Envanteri oku:** Kayıtlar `~/.claude/plugins/config/legal-turkish/ai-governance-legal/ai-systems.yaml` dosyasında tutulur. Dosya yoksa ilk `add` işleminde boş `systems: []` yapısıyla oluştur.
3. **Argümana göre yönlendir:**
   - Argüman yoksa veya `list` → Özet envanter tablosunu göster.
   - `add` → **Ekleme Akışı**nı başlat.
   - `edit <id>` → Mevcut kaydı göster, değişecek alanı sor, onay alıp tek alanı güncelle.
   - `classify <id>` → **Sınıflandırma Adımları**nı çalıştır; `role`, `tier`, `role_basis`, `tier_basis` alanlarını güncelle.
   - `show <id>` → Sistem kaydını tüm ayrıntılarıyla göster.
4. **Listelemede pano teklifi:** 10 satırı aşan envanterde `references/dashboard-template.md` yapısında durum/katman/AB bağı (`eu_nexus`) filtreli interaktif HTML pano isteyip istemediğini sor.
5. **Kapanış notu:** Her yazma işlemi sonrası yükümlülüklerin tablodan otomatik türetilmediğini, talep edilirse konuşma içinde `[doğrula]` etiketleriyle çıkarılıp resmî değerlendirme için `/ai-governance-legal:aia-generation` akışına alınabileceğini hatırlat.

## Liste Formatı

| ID | Sistem Adı | Sahip | Durum | AB Bağı | Türkiye Katmanı | Rol | AB Risk Katmanı | Sonraki İnceleme |
|---|---|---|---|---|---|---|---|---|
| sys-001 | CV ön eleme aracı | İK Birimi | in_production | yes | KVKK + TİHEK + 4857 | deployer | high_risk | 2026-08-01 |
| sys-002 | E-posta taslak asistanı | BT Birimi | in_production | no | KVKK m. 9 kontrol | deployer | limited | 2026-12-01 |

Tablo altında katman bazlı sistem sayısını ve "30 gün içinde gözden geçirilecek N sistem var" bilgisini göster.

## Ekleme Akışı (Add)

Tek tek veya toplu yapıştırılan bilgiden şu zorunlu alanları topla (`name`, `owner`, `description`, `status`, `eu_nexus`):
1. **Sistem adı (`name`):** Kısa ve ayırt edici ad.
2. **Sahip (`owner`):** Günlük operasyonundan sorumlu kişi/birim.
3. **Tanım (`description`):** 1-2 cümleyle ne yaptığı ve hangi veriyi işlediği.
4. **Durum (`status`):** `planned | in_development | in_production | deprecated`.
5. **AB/AEA bağı (`eu_nexus`):** Sistem AB/AEA'da mı kuruluyor, oradaki kullanıcılara mı sunuluyor, yoksa çıktıları AB/AEA'daki gerçek kişileri mi etkiliyor? `true` ise AB AI Act analizi devreye girer; `false` ise Türkiye mevzuatı (KVKK, 7545, FSEK, TİHEK, sektörel düzenlemeler) birincildir.
6. **Sınıflandırmaya geçilsin mi?** İster şimdi çalıştır, ister `/ai-governance-legal:ai-inventory classify <id>` ile sonraya bırak.

ID ataması: sıradaki `sys-NNN`.

## Sınıflandırma Adımları

Bu adım `role`, `role_basis`, `tier` ve `tier_basis` alanlarını üretir ve **her zaman** `[doğrula - güncel mevzuat/AB AI Act metni ile teyit et]` etiketi taşır.

### Adım 1: Rol ve Türkiye Kapsamı

- **Geliştirici (`provider`):** AI sistemini geliştirir/geliştirtir ve kendi adıyla veya markasıyla piyasaya sürer ya da hizmete sunar.
- **Kullanıcı (`deployer`):** Kişisel/mesleki dışı kullanım dışında kendi yetkisi altında AI sistemini kullanır (şirket içi kullanımların çoğu).
- **İthalatçı (`importer`) / Dağıtıcı (`distributor`) / Yetkili Temsilci (`authorized_rep`) / Ürün Üreticisi (`product_manufacturer`):** Tedarik zinciri rolleri.
- **Çift rol uyarısı:** Kullanıcı, üçüncü taraf bir sistemi ince ayarla (fine-tuning) kendi verisiyle esaslı şekilde değiştirirse, amacını farklılaştırırsa veya kendi markasıyla sunarsa `deployer`'dan **`provider`** konumuna geçebilir (AB AI Act m. 25 uyarısı `[doğrula]`).
- **Türkiye düzenleyici teması:** Sistemde kişisel veri/KVKK m. 11/1-(g), 7545 s. Siber Güvenlik Kanunu kapsamı (kritik altyapı/zafiyet bildirimi), 6701 TİHEK/4857 istihdam, 6502/Reklam Kurulu sentetik içerik veya BDDK/SPK/TİTCK/BTK sektörel teması olup olmadığını işaretle.

### Adım 2: Risk Katmanı

1. **Yasaklı Uygulamalar (`prohibited`):** Yanıltıcı/subliminal manipülasyon, kırılganlık istismarı, kamu sosyal skorlaması, istihdam/eğitimde duygu tanıma, biyometrik kategorizasyon (AB AI Act m. 5 `[doğrula]`; ayrıca Türkiye'de KVKK m. 6 özel nitelikli veri ve kişilik hakkı ihlali riski). Eşleşirse **durdur** ve kırmızı çizgi eskalasyonunu çalıştır.
2. **Yüksek Risk (`high_risk`):** Biyometrik tanıma, kritik altyapı (enerji/ulaşım/dijital altyapı — Türkiye'de ayrıca 7545 s. Kanun kapsamı), eğitim/sınav, İK/işe alım/terfi/işten çıkarma, temel kamu/özel hizmetlere erişim (bireysel kredi skorlama, sağlık/hayat sigortası risk fiyatlaması, acil müdahale), kolluk/göç/yargı (AB AI Act Ek III `[doğrula]`).
3. **Genel Amaçlı Model (`gpai` / `gpai_systemic`):** Geniş ölçekte eğitilmiş, çok amaçlı temel modeller (`gpai_systemic` eşiği için EUR-Lex üzerinden güncel işlem gücü/Komisyon kararı teyit edilir `[doğrula]`).
4. **Sınırlı Risk (`limited`):** Gerçek kişilerle etkileşen sohbet botları, deepfake/sentetik içerik (Türkiye'de Reklam Kurulu ve şeffaflık yükümlülükleri + AB şeffaflık yükümlülükleri).
5. **Düşük/Asgari Risk (`minimal`):** Yukarıdakiler dışındaki iç verimlilik/yardımcı araçlar (KVKK ve ticari sır kuralları yine geçerlidir).

## Kayıt Formatı (`ai-systems.yaml`)

```yaml
systems:
  - id: sys-001
    name: "CV ön eleme aracı"
    owner: "İK Birimi"
    description: "Gelen özgeçmişleri ilan kriterlerine göre sıralar"
    status: in_production          # planned | in_development | in_production | deprecated
    eu_nexus: true                 # true | false
    tr_regimes: ["KVKK", "4857_Is_Kanunu", "6701_TIHEK"]
    role: deployer                 # provider | deployer | importer | distributor | authorized_rep | product_manufacturer
    role_basis: "Üçüncü taraf SaaS lisansıyla şirket içinde kullanılıyor [doğrula]"
    tier: high_risk                # prohibited | high_risk | limited | minimal | gpai | gpai_systemic
    tier_basis: "AB AI Act Ek III(4)(a) istihdam/işe alım + KVKK m. 11/1-(g) & TİHEK yüksek hassasiyet [doğrula]"
    obligations_assessed: false
    obligations_note: "Değerlendirilecek: KVKK aydınlatma/m.11(g), TİHEK ayrımcılık denetimi, insan gözetimi"
    next_review: "2026-08-01"
    review_trigger: "esaslı değişiklikte veya yıllık"
    created: "2026-11-24"
    updated: "2026-11-24"
```

## Guardrails

- **Sessizce sınıflandırma yapma:** Adımları kullanıcıya açıkça göster.
- **`[doğrula]` etiketlerini silme:** Madde ve ek atıflarının hukukçu tarafından kontrol edilmesi gerekir.
- **Esaslı değişiklik uyarısı:** Bir model ince ayarlanıyor veya kullanım amacı değişiyorsa `/ai-governance-legal:ai-inventory classify <id>` yeniden çalıştırılmalıdır.
- **Tablodan yükümlülük icat etme:** Yükümlülük analizi gerekiyorsa konuşmada hukukçu denetimiyle yap ve `/ai-governance-legal:aia-generation` komutuna yönlendir.
