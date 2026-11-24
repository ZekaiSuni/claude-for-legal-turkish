---
name: ip-clause-review
description: >
  İş, danışmanlık, hizmet alımı (SOW), tedarikçi, lisans veya iş birliği
  sözleşmelerindeki Fikri ve Sınai Mülkiyet (IP) hükümlerini Türk hukuku
  (5846 s. FSEK m. 14–18, 48/2, 52; 6769 s. SMK m. 113–122, 148) ekseninde
  inceler. Devir boşluklarını, manevi hak ve yapay zekâ çıktı risklerini saptar
  ve redline önerir.
argument-hint: "[dosya yolu | Drive linki | metni yapıştırın]"
---

# /ip-clause-review

Sözleşmelerdeki fikri ve sınai mülkiyet hükümlerini `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` profiline göre inceler; **devir boşluklarını (`ASSIGNMENT GAP`)**, lisans kapsamı hatalarını ve garanti/tazminat risklerini önceliklendirerek minimal redline önerileri sunar.

## İş Akışı

1. `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` dosyasını (`## Kullanıcı Rolü`, `## Fikri Mülkiyet (IP) Uygulama Profili`, `## Çıktılar`, `## Matter Workspaces`) oku. Eksikse `/ip-legal:cold-start-interview` iste.
2. Sözleşmeyi al ve ilk olarak üç yönü netleştir: sözleşme türü, şirketin IP tarafı (**hak veren/lisans veren** mi, **hak alan/devralan** mı, **her ikisi** mi?), uygulanacak hukuk. *(Taraf konumu sabit değildir; aynı gün iş sözleşmesinde hak alan, müşteri lisansında hak veren olabilirsiniz.)*
3. **Öncelikli Devir Boşluğu Kontrolü (`ASSIGNMENT GAP`):** İş, danışmanlık, yazılım geliştirme, ajans/tasarım, SOW veya eser siparişi sözleşmelerinde önce aşağıdaki Türk hukuku devir kurallarını kontrol et.
4. Her IP maddesini risk seviyesine (`🔴 Kritik` / `🟠 Yüksek` / `🟡 Orta` / `🟢 Düşük`) göre değerlendir; maddeler arası tutarlılığı test et.
5. `## Çıktılar` çalışma başlığı ve `Reviewer note` ile raporu sun; Sonraki Adımlar Karar Ağacı ile kapat.

## ⚠️ Türk Hukukunda Devir Boşluğu (`ASSIGNMENT GAP`) Kontrolü

Yatırım, M&A due diligence veya ihtilafta en ağır bedeli sözleşmedeki zayıf IP devri doğurur. Özellikle şu 6 Türk hukuku tuzağını denetle (`🔴` veya `🟠`):

1. **FSEK m. 52 Yazılı Şekil ve Hakların Ayrı Ayrı Sayılması:** Türk hukukunda *"tüm telif/fikri haklar müşteriye aittir"* gibi soyut/genel ifadeler geçersizlik veya dar yorum riski doğurur. Devredilen veya lisanslanan **mali hakların her biri (işleme FSEK m. 21, çoğaltma m. 22, yayma m. 23, temsil m. 24, umuma iletim m. 25)** ile süre, yer ve kapsam yazılı olarak **tek tek sayılmalıdır** `[doğrula]`.
2. **FSEK m. 48/2 Gelecekteki Eser Yasağı:** Henüz vücuda getirilmemiş eserlere ilişkin önceden yapılan devir sözleşmeleri batıldır. Çözüm: *"Devretmeyi taahhüt eder"* (devir taahhüdü) ile birlikte eserin/yazılımın vücuda gelip teslim edildiği anda ayrıca yazılı devir protokolü veya teslim tutanağı ile mali hak devrinin ikmal edilmesidir `[doğrula]`. *(ABD'deki tek cümlelik `"hereby assigns"` formülü Türk hukukunda tek başına FSEK m. 48/2 engelini aşmaz!)*
3. **Çalışan vs. Dış Yüklenici Ayrımı (FSEK m. 18/2 vs. Freelancer):** Çalışanların işlerini görürken meydana getirdikleri eserlerde mali hakları **kullanma yetkisi** kanunen işverene aittir (ancak çalışan sözleşmesinde ek açık düzenleme güvenlik sağlar); buna karşın **dış yüklenici / ajans / danışman (freelancer)** için FSEK m. 18 uygulanmaz, FSEK m. 52'ye uygun yazılı devir şarttır.
4. **Manevi Haklar (FSEK m. 14–17):** Türk hukukunda manevi hakların özünden feragat (`moral rights waiver`) ve devri **hükümsüzdür**. Bunun yerine hak sahibinin, eserde değişiklik/umuma arz/adın belirtilmesi kapsamındaki **manevi hakların kullanma yetkisini** ticari ihtiyaç ölçüsünde devrettiği ve müdahalede bulunmayacağını taahhüt ettiği düzenleme kurulmalıdır.
5. **Sınai Mülkiyet (SMK m. 113–122 ve m. 148):** Çalışan buluşlarında hizmet buluşu bildirimi ve hak talebi kuralları; devir/lisans işlemlerinde ise **SMK m. 148** uyarınca yazılı şekil (devirde noter onaylı imza / sicile kayıt şartı kontrolü `[doğrula]`).
6. **Yapay Zekâ (AI) Çıktı ve Buluş Riski:** Yüklenici kod veya görsel/metin üretiminde AI kullanıyorsa, insan yaratıcılığı bulunmayan AI çıktılarında FSEK kapsamında eser niteliği doğmayabileceği ve devir hükmünün var olmayan hakkı geçiremeyeceği dikkate alınmalıdır. Sözleşmede AI kullanım beyanı, insan katkısı/kayıt zorunluluğu ve eğitim verisi/üçüncü kişi ihlal tazminatı bulunmuyorsa `🟠 Yüksek` olarak bayrakla.

```markdown
## ⚠️ DEVİR BOŞLUĞU TESPİTİ (`ASSIGNMENT GAP`)

**Madde [X]:** Eser/çıktı mülkiyetini devretmeye çalışıyor, ancak: [somut eksik — örn. "FSEK m. 52 kapsamında mali haklar tek tek sayılmamış", "FSEK m. 48/2 gelecekteki eser için yalnızca soyut devir yazılmış", "FSEK m. 14 vd. manevi hak kullanım yetkisi düzenlenmemiş" veya "AI kullanım ifşası yok"].
**Risk:** M&A incelemesinde veya fesihten sonra yüklenicinin çıktı üzerinde hak iddia etme riski.
**Önerilen Cerrahi Revizyon (Redline):** > "[FSEK m. 21-25, m. 48/2, m. 52 uyumlu dar revizyon metni]"
```

## Madde Bazlı İnceleme ve Çapraz Tutarlılık

Şu başlıkları tek tek kontrol et ve birbirleriyle karşılaştır:
- **Önceden Var Olan IP (`Background IP`) vs. Yeni Üretilen IP (`Foreground IP`):** Yeni çıktı içine gömülen Background IP için devredilemez/süresiz/ücretsiz yan lisans var mı?
- **Lisans Kapsamı, Garanti ve Tazminat Uyumu:** Lisans "kullanma ve değiştirme" izni verip garanti sadece "patent" ile sınırlandırılmışsa boşluk vardır; ihlal garantisi olup tazminat (`IP Indemnity`) yoksa yaptırım eksiktir.
- **Fesih Sonrası Etki, Marka Kullanımı ve Ticari Sırlar (TTK m. 54–56):** Peşin ödenmiş lisans fesihle geri mi alınıyor?

**Redline İlkesi (Cerrahi Müdahale):** Mümkün olan en küçük değişiklikle düzelt (cümle veya bütün maddeyi baştan yazmadan önce sözcük/ibare/alt bent değiştir; yalnızca karşı taraf metni hiç kurtarılamıyorsa komple yenile ve nedenini açıkla).

## Çıktı Formatı ve Karar Duruşu

- Üste `## Çıktılar` çalışma başlığı ve `Reviewer note` ekle. (Mevzuat atıflarına `[model bilgisi - doğrula]` veya oturumda açıldıysa `[Mevzuat.gov.tr]` etiketi koy.)
- Bölümler: **Kısa Sonuç** (`🔴/🟠/🟡/🟢` sayıları ve profil onay mercii) · **Devir Boşluğu Kontrolü (`✅ Temiz` / `⚠️ Boşluk Var`)** · **Önem Sırasına Göre Maddeler** · **Maddeler Arası Tutarlılık** · **Uygulanacak Hukuk Notu** · **Onay Yönlendirmesi**.
- **Öznel değerlendirme kuralı:** İki tarafa da çekilebilecek muğlak bir IP paylaşımında sessiz karar verme, `[review]` ile iki yönlü argümanları yaz. Sonunda Sonraki Adımlar Karar Ağacı sun.
