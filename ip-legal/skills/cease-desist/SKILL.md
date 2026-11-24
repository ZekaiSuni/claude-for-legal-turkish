---
name: cease-desist
description: >
  Tecavüzün Men'i İhtarnamesi taslağı hazırlar (`--send`) veya karşı taraftan
  gelen bir ihtarnameyi yapılandırılmış seçeneklerle triyajlar (`--receive`).
  6769 s. SMK (m. 29, 149–151, 154), 5846 s. FSEK (m. 66–70), 6102 s. TTK
  (m. 18/3, 54–56), HMK m. 313–315 ve 6325 s. Arabuluculuk Kanunu (m. 4–5)
  çerçevesinde çalışır.
argument-hint: "<--send | --receive> [bağlam, karşı taraf veya gelen ihtarname metni/yolu]"
---

# /cease-desist

- `--send`: Haklarımıza tecavüz eden tarafa gönderilmek üzere profildeki duruşa (`## Uygulama ve İhtar Duruşu (Enforcement Posture)`) kalibre edilmiş ihtarname (Noter veya KEP) taslağı üretir.
- `--receive`: Bize ulaşan ihtarnamenin ciddiyetini, hak geçerliliğini, savunma/iptal kozlarımızı ve yanıt seçeneklerini analiz eder. *(Yanıtta karşı sert ihtar gerekiyorsa `/ip-legal:cease-desist --send` ile zincirlenebilir.)*

## İş Akışı ve Güvenlik Kapıları

1. `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` dosyasını (`## Şirket Profili`, `## Kullanıcı Rolü`, `## Fikri Mülkiyet (IP) Uygulama Profili`, `## Uygulama ve İhtar Duruşu (Enforcement Posture) → Onay Matrisi`, `## Çıktılar`, `## Öznel Hukuki Değerlendirmelerde Karar Duruşu`, `## Matter Workspaces`) oku.
2. Otomatik eskalasyon tetikleyicilerini kontrol et (karşı taraf müşterimiz/tedarikçimiz mi, patent hükümsüzlük riski veya SMK m. 154 menfi tespit riski doğuruyor mu?).

## `--send` Modu (İhtarname Taslağı)

1. **Karşı Taraf Ön Araştırması:** İhtarname göndermeden önce mutlaka kontrol et: karşı taraf tam ticaret unvanı/adresi (`MERSİS` / ticaret sicili), kendi tescilli marka/patent portföyü var mı (karşı dava açabilir mi?), mevcut ticari ilişkimiz var mı, kullanım gerçek bir ticari tecavüz mü yoksa eleştiri/atıf mı?
2. **İhtarname Duruşu Kalibrasyonu:**
   - `conservative / yumuşak temas`: İş birliği/yanlış anlama ihtimali varsa önce bilgilendirici iletişim veya ılımlı uyarı yazısı.
   - `measured`: Net ihlal özeti, dayanak sicil/eser bilgisi, 7–15 günlük somut cevap/durdurma süresi, ihtirazi kayıt.
   - `aggressive`: Açık hukuki ihtar — Noter veya tacirler arasında KEP (`TTK m. 18/3` temerrüt ve ispat şekli) üzerinden gönderilmek üzere **SMK m. 29, m. 149–151 / FSEK m. 66–70 / TTK m. 54–56** atıflarıyla durdurma, ihtiyati tedbir (`SMK m. 159`) ve tazminat haklarının saklı tutulması; alan adı ihlallerinde **TRABİS `.tr` UÇHS** veya **WIPO UDRP** başvurusu uyarısı.
3. **Asla Fazla İddia Etme:** Marka yalnızca 25. sınıfta tescilliyken 9. sınıftaki yazılıma "tescilli tecavüz" deme (gerekirse SMK m. 6/5 tanınmışlık veya TTK haksız rekabet sınırını `[review]` ile belirt).
4. **Haksız İhtar Sorumluluğu Uyarısı:** Desteksiz veya aşırı geniş ihtar göndermek; karşı tarafın **SMK m. 154 Menfi Tespit Davası** açmasına, **TTK m. 54–56 Haksız Rekabet / ticari itibar zedelenmesi** tazminat talebine ve HMK yargılama giderleri/kötüniyet yaptırımlarına (`HMK m. 327–329`) maruz kalmanıza yol açabilir.
5. **Gönderim Dışı Başlık Kuralı:** `## Çıktılar` çalışma ürünü başlığını taslağın iç hukuk analiz üst bloğunda tut, **ancak karşı tarafa / Noter / KEP'e gidecek nihai ihtarname metninden mutlaka çıkar!**

**Non-lawyer kapısı (`--send`):** Gönderimden önce `## Kullanıcı Rolü` kontrol edilir; avukat değilse sorumlu avukat onayı olmadan göndermemesi için 1 sayfalık özet sunulur.

## `--receive` Modu (Gelen İhtarname Triyajı)

Gelen ihtarnameyi şu 6 başlıkta incele:
1. **İddia edilen haklar gerçek ve aktif mi?** TÜRKPATENT EPATS, WIPO Madrid, EPO Register veya Kültür ve Turizm Bakanlığı telif kayıtlarından tescil/yenileme/sınıf durumunu doğrula (`[doğrula]`). *(ABD TESS/USPTO TSDR kullanma.)*
2. **Kullanmama / Hükümsüzlük Kozu:** İddia edilen marka 5 yılı aşmış ve ciddi kullanılmıyorsa **SMK m. 26 (TÜRKPATENT idari iptal başvurusu)** ve **SMK m. 29/2 kullanmama def'i**; patent/tasarım için **SMK m. 138 hükümsüzlük** sinyali var mı?
3. **Aşırı veya Kötü Niyetli Talep mi?** Hak sahibinin fiilî kapsamını aşan talepler (alan adı devri, yüksek/haksız tazminat) varsa belirt; gerekiyorsa **SMK m. 154 menfi tespit** seçeneğini değerlendir.
4. **Hukuki ve Cezai Sorumluluk Sınırı:** Kasten ihlalin devamı hâlinde **SMK m. 150–151** veya **FSEK m. 68/71** ağırlaşma riskini ölç; delilleri koru (hukuki saklama).
5. **Yanıt ve Sulh Seçenekleri:**
   - **A — Tam Uyum / Değişiklik,**
   - **B — Gerekçeli Ret / Savunma (İlgi kesme veya SMK m. 7/5, kullanmama, FSEK m. 30–40 savunması),**
   - **C — Sulh / Birlikte Var Olma / Lisans Müzakeresi:** Müzakere yazışmalarında **`HMK m. 313–315`** (sulh) ve **`6325 s. Hukuk Uyuşmazlıklarında Arabuluculuk Kanunu m. 4–5`** (arabuluculuk gizliliği) uyarınca bu yazışmaların açıkça **"gizli / arabuluculuk veya sulh müzakeresi kapsamındadır, ikrar teşkil etmez"** şerhiyle yürütülmesi gerekir *(ABD `FRE 408` yazma)*.
   - **D — TÜRKPATENT Nezdinde İptal / Mahkemede Hükümsüzlük veya SMK m. 154 Menfi Tespit Davası.**
6. **Süre ve Eskalasyon:** İhtarnamede verilen cevap süresini, `## Uygulama ve İhtar Duruşu (Enforcement Posture) → Onay Matrisi` uyarınca onay mercisini ve mevzuat doğrulama etiketlerini (`[Mevzuat.gov.tr]` / `[model bilgisi - doğrula]`) raporla. Marka/Patent Vekili ise dava stratejisi için avukata devri işaretle. Analizi Sonraki Adımlar Karar Ağacı ile bitir.
