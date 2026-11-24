---
name: policy-starter
description: >
  Kurum veya hukuk bürosu için Türkiye mevzuatı ve uluslararası referans
  rehberlerden uyarlanan ilk Yapay Zekâ Kullanım Politikası taslağı üretir. Çıktı
  doğrudan yayımlanacak nihai metin değil, yönetici/avukat onayına sunulacak
  taslaktır. "AI politikası taslağı yaz", "AI usage policy hazırla" denince
  kullanılır.
argument-hint: "[isteğe bağlı kapsam notu: örn. 'şirket geneli', 'sadece hukuk ekibi', 'mevcut politikayı güncelle']"
---

# /policy-starter

## İş Akışı

1. `~/.claude/plugins/config/legal-turkish/ai-governance-legal/CLAUDE.md` dosyasını oku; profil doldurulmamışsa önce `/ai-governance-legal:cold-start-interview` yönlendirmesi yap.
2. Taslağa geçmeden **önce Kapsam Görüşmesi yap** (kullanıcı "tam politika yaz" dese bile önce hangi bölümlerin seçildiğini, hedef kitleyi ve kurum yapısını netleştir).
3. Profilin `**Düzenleyici ayak izi:**` (`## Şirket Profili`) alanına göre güncel referans rehber ve standartları belirle/araştır.
4. Yalnızca seçilen bölümleri kaynak göstererek ve her tercih noktasına `[review]` etiketi koyarak taslakla.
5. `TASLAK - DAHİLİ HUKUKİ İNCELEME İÇİNDİR` başlığı, Kaynaklar tablosu, `Reviewer note`, Bölüm sonu Açık Sorular ve Kabul Kontrol Listesi (`Adoption Checklist`) ile sun.
6. `## Çıktılar` altındaki Sonraki Adımlar Karar Ağacı ile bitir.

## Matter Bağlamı

`## Matter Workspaces` altında `Enabled` kapalıysa (şirket içi varsayılan) practice-level bağlamda çalış; açıksa aktif `matter.md` bağlamını yükle.

## Amaç ve Disiplin

Birçok kurum ve hukuk bürosu hâlâ güncel AI politikasına sahip değil ya da yalnızca eski yasaklardan oluşan bir metin kullanıyor. Bu skill'in 4 katı disiplini vardır:
1. **Uydurma politika cümlesi yazma; referans kaynaklardan uyarla.** Türkiye ve uluslararası resmî rehberleri esas al; kaynağı olmayan cümleyi `[review - uyarlama, doğrudan kaynak yok]` olarak işaretle.
2. **Önce kapsamı daralt, sonra yaz.** Kullanıcı seçmediği sürece gereksiz bölümler ekleme.
3. **Her karar noktasını `[review]` olarak işaretle.** Yasaklı araç adları, gizli veri sınırı, ihlal yaptırımı ve onay mercii gibi seçimler avukatın/yönetimin kararıdır; AI seçemez.
4. **Sade dil kullan.** Metin İK, BT ve tüm çalışanlar tarafından okunacaktır.

## Kapsam Görüşmesi (Yazmadan Önce Sor)

Kullanıcıdan hangi bölümleri istediğini seçmesini iste (hiç politikası olmayan kurum için varsayılan başlangıç paketi: **1, 2, 3, 4, 5, 9**):
1. **Kapsam** (kimleri, hangi araçları — üretken AI/tüm AI — ve hangi verileri kapsar)
2. **İzinli ve Yasak Kullanımlar** (onaylı kullanım alanları, kırmızı çizgiler, ön onay gerekenler)
3. **Onay ve İnceleme Süreci** (yeni araç/senaryo talebi, hukuk/CISO/KVKK onay akışı ve SLA)
4. **Şeffaflık ve Bildirim** (müşterilere, müvekkillere, mahkemelere/karşı tarafa ve çalışanlara AI kullanımı ifşası)
5. **Veri İşleme, Gizlilik ve Sır Saklama** (KVKK m. 5–6–9, Av.K. m. 36, TTK ticari sırlar, eğitimden çıkış / Zero Data Retention)
6. **Eğitim ve Farkındalık** (zorunlu eğitim sıklığı ve AI okuryazarlığı)
7. **Siber Olay ve Hata Bildirimi** (7545 s. Kanun / USOM ve KVKK m. 12 uyumlu olay bildirimi)
8. **Politika İhlali ve Yaptırım** (disiplin prosedürü bağlantısı)
9. **Gözden Geçirme Sıklığı ve Sahiplik** (`policy-monitor` döngüsü)
10. **Tanımlar Sözlüğü** (Üretken AI, Onaylı Araç, Yüksek Riskli Kullanım, Hassas Veri vb.)

Ardından iki soru daha sor:
- **Hedef kitle:** Tüm çalışanlar / Yalnızca hukuk ekibi / Avukatlar + idari personel / Müşteri özeti de gerekli mi?
- **Kurum yapısı:** Hukuk bürosu / Şirket içi hukuk (tüm şirket politikası mı yoksa hukuk birimi içi mi) / Kamu veya klinik?

## Türkiye ve Uluslararası Referans Kaynak Matrisi

Kaynakları profilin `**Düzenleyici ayak izi:**` bölümünden türet:

| Bağlam | Esas Alınacak Model Politika ve Resmî Rehber Kaynakları |
|---|---|
| **Türkiye (Genel & Kurumsal)** | KVKK *Yapay Zekâ Alanında Kişisel Verilerin Korunmasına Dair Tavsiyeler* ve üretken AI rehberleri; 7545 s. Siber Güvenlik Kanunu & USOM güvenlik ilkeleri; Sanayi ve Teknoloji Bakanlığı *Ulusal Yapay Zekâ Stratejisi* güvenilir/etik AI ilkeleri; Reklam Kurulu & TİHEK çerçevesi |
| **Türkiye Hukuk Bürosu / Avukatlık** | 1136 s. Avukatlık Kanunu m. 36 (sır saklama), TBB Meslek Kuralları ve bilişim/yapay zekâ çalışmaları (çıktı doğruluğu ve müvekkil sırrı) |
| **AB / İhracat (`eu_nexus` varsa)** | AB AI Act ((AB) 2024/1689) m. 4 (AI okuryazarlığı), yüksek riskli kullanım gözetimi, EDPB ve ulusal veri otoritesi rehberleri |
| **Uluslararası Teknik Standartlar** | ISO/IEC 42001 (Yapay Zekâ Yönetim Sistemi), NIST AI Risk Management Framework (AI RMF), OECD Yapay Zekâ İlkeleri |

Canlı arama yapılamıyorsa bunu `Reviewer note` içinde `"Canlı web araması yapılamadı — taslak model bilgisinden derlendi; yürürlüğe almadan önce birincil metinlerden doğrulayın"` şeklinde açıkça belirt.

## Taslak Çıktı Yapısı

```markdown
> **⚠️ Reviewer note**
> - **Kaynaklar:** [KVKK rehberleri / Mevzuat.gov.tr / ISO 42001 / NIST AI RMF vb. — canlı doğrulama durumu]
> - **Okuma kapsamı:** Uygulama profili + [N] referans kaynak
> - **Hukukçu kararı gerektirenler:** [N] satır içi `[review]` + bölüm sonu açık sorular
> - **Güncellik:** [`references/currency-watch.md` kontrolü]
> - **Güvenmeden önce:** Bu bir TASLAKTIR — [profildeki onay makamı] incelemeden dağıtmayın veya yayımlamayın

TASLAK — DAHİLİ HUKUKİ İNCELEME İÇİNDİR — DAĞITIMA UYGUN DEĞİLDİR
Hazırlanan Kurum: [Şirket/Büro Adı] | Tarih: [YYYY-AA-GG]
Onay Olmadan Yürürlüğe Konulamaz: [Hukuk Başmüşaviri / Yönetici Ortak / Yönetim Kurulu]
*(Non-lawyer kullanıcı ise: bu taslağı yürürlüğe koymadan veya ekiplere dağıtmadan önce sorumlu avukatınız [ad] ile gözden geçirin.)*

## Kaynaklar Tablosu
| Kaynak | URL / Kurum | Erişim Tarihi | Taslağa Alınan Kural |
|---|---|---|---|

## Yönetici Özeti
[En fazla 3 paragraf: politikanın amacı, kimi bağladığı, kabul öncesi yapılacaklar]

## [Seçilen Bölüm N]
- Kapsam cümlesi ve model kaynaklardan uyarlanmış kurallar (`[Kaynak]`, `[review - araç listesi / eşik belirle]`)
- **Bölüm Sonu Açık Sorular (`[review]`):** Avukatın politika kabulü öncesinde karar vermesi gereken 2–3 temel pozisyon.

## Kabul Kontrol Listesi (Adoption Checklist)
- [ ] Hukuk Başmüşaviri / Yönetici Ortak incelemesi `[review]`
- [ ] KVKK Sorumlusu / DPO ve Bilgi Güvenliği (CISO / 7545 uyumu) incelemesi `[review]`
- [ ] İnsan Kaynakları incelemesi (disiplin/eğitim bölümü varsa) `[review]`
- [ ] Yürürlük tarihi, duyuru ve eğitim planı `[review]`
- [ ] Kabul sonrası `CLAUDE.md → ## AI Politika Taahhütleri` bölümüne işlenmesi
```

## Yapmadıkları

- Avukat/yönetim adına zor kararları seçmez; seçenekleri `[review]` ile sunar.
- Hukuki yeterlilik garantisi vermez.
- Mevcut bir `## AI Politika Taahhütleri` doluysa sıfırdan yazmak yerine **güncelleme taslağı (diff)** olarak ilerler.
