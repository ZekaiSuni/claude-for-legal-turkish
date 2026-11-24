---
name: oss-review
description: >
  Bağımlılık listesi (package.json, requirements.txt, go.mod, Cargo.toml, pom.xml,
  SBOM), tek bir kütüphane veya açık kaynak yapılacak kurum içi kod için Açık
  Kaynak (OSS) lisans uyumluluk kontrolü yapar. Copyleft risklerini ve lisans
  uyumsuzluklarını sınıflar.
argument-hint: "[manifest/SBOM dosya yolu | paket adı | repo klasörü | metin]"
---

# /oss-review

`~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` içindeki uygulama profili ve açık kaynak politikasına göre bağımlılık ağaçlarını inceler; lisans ailesini belirler, dağıtım modeline göre yükümlülükleri çıkarır ve somut aksiyon önerir (uyum sağla, değiştir, çıkar, hukuk incelemesine al, ticari lisans ara).

## İş Akışı

1. **Profili oku:** `~/.claude/plugins/config/legal-turkish/ip-legal/CLAUDE.md` (`## Kullanıcı Rolü`, `## Fikri Mülkiyet (IP) Uygulama Profili`, `## Çıktılar`, `## Matter Workspaces`) ve varsa ekteki kurum OSS politikasını oku. Eksikse `/ip-legal:cold-start-interview` iste.
2. **Kapsamı belirle:** Bağımlılık dosyası (`package.json`, `requirements.txt`, `go.mod`, `Gemfile`, `Cargo.toml`, `pom.xml`, SPDX/CycloneDX SBOM, lockfile), tek kütüphane veya dışarı açılacak şirket kodu (`outbound`).
3. **Dağıtım modelini netleştir:** Aynı paket dağıtım şekline göre bambaşka sonuç doğurur:
   - **SaaS / Ağ üzerinden sunulan hizmet:** AGPL ağ tetikleyicisi çalışır; arayüzde/dokümantasyonda atıf; rakip servislerde SSPL/BUSL/Elastic yasağı kritik olabilir.
   - **Dağıtılan İkili Dosya / Mobil & Masaüstü Uygulama (Distributed binary):** GPL, LGPL, MPL, EPL kaynak/değişiklik bildirimleri tetiklenir.
   - **Yalnızca Şirket İçi Kullanım (Internal only):** Çoğu copyleft tetiklenmez; ancak dış kullanıcılar ağ üzerinden etkileşiyorsa AGPL yine devreye girer.
   - **Gömülü Sistem / Firmware:** GPL uyumu (derleme bilgisi ve kaynak paylaşımı) en katı alandır; sevkiyattan önce çözülmelidir.
4. **Sadece paket yöneticisi etiketine değil gerçek `LICENSE` dosyasına bak:** `package.json` MIT deyip kaynak başlığı GPL taşıyabilir; lisans belirsizse (`unknown`) asla permissive varsayma, `"inceleme gerekli"` olarak işaretle.

## Lisans Aileleri ve Önem Dereceleri

| Kategori | Örnekler | Temel Yükümlülük ve Risk |
|---|---|---|
| **Permissive** | MIT, BSD-2/3-Clause, Apache-2.0, ISC, Zlib | Telif ve lisans metnini koruma; Apache-2.0 ek olarak patent lisansı ve `NOTICE` zorunluluğu getirir. |
| **Zayıf Copyleft (Weak)** | LGPL-2.1/3.0, MPL-2.0, EPL-1.0/2.0, CDDL | Dosya veya kütüphane düzeyinde kaynak açma (statik/dinamik bağlama ayrımı kritik: LGPL statik bağlamada 🔴 Kritik risk doğurabilir). |
| **Güçlü Copyleft (Strong)** | GPL-2.0/3.0, AGPL-3.0, OSL, EUPL | Geniş kaynak kodu açma yükümlülüğü; AGPL SaaS ağ erişiminde de tetiklenir. |
| **Public Domain / İthaf** | CC0, Unlicense, WTFPL | Türk hukukunda (5846 s. FSEK) telif hakkının tamamen "kamu malına terki" tartışmalı olabileceği için feragat/geniş lisans okuması `[review]` olarak işaretlenir. |
| **OSI Dışı Kaynak-Açık (Non-OSI)** | SSPL, BUSL, Commons Clause, Elastic License | Gerçek "açık kaynak" değildir; ticari veya rekabetçi kullanımı yasaklar, sözleşme metni mutlaka tek tek okunur. |
| **Belirsiz / Özel (`Unknown`)** | Lisansı yok, başlık/dosya çelişkili | 🔴 Çıkış/sevkiyat durdurma sinyali; izinli varsayma. |

**Ek tarama noktaları:** Çift lisanslı paketler (hangisi seçildi?), GPL-2.0-only ile Apache-2.0 uyumsuzluğu, sonradan lisans değiştiren paket sürümleri (Redis, MongoDB, Elastic vb. — pinlenen sürümü doğrula).

## Dışa Açılacak Kod Kontrolü (`Outbound`)

- Seçilen dışa açma lisansının (örn. MIT/Apache-2.0) kodun içindeki tüm alt bağımlılıklarla uyumlu olduğunu doğrula (ör. içinde GPL kodu varken proje MIT ile açılamaz).
- `LICENSE`, `NOTICE` ve üçüncü kişi lisans metinlerinin eksiksiz olduğunu; gizli ticari kod, müşteri verisi veya API anahtarı sızmadığını; proje adı için marka araştırması (`/ip-legal:clearance`) yapıldığını kontrol et.

## Türk Hukuku ve Çıktı Kuralları

- **Yargı alanı ve mevzuat notu:** GPL-3.0 patent hükmü Türk 6769 s. SMK çerçevesinde, FSEK m. 52 yazılı şekil şartı ve kamuya mal etme (CC0) sınırları Türkiye uyuşmazlıklarında tartışmalı olabilir; tartışmalı copyleft tetikleyicileri (`AGPL network interaction`, `LGPL linking`) sessizce geçilmez, `[review]` ile hukukçuya bırakılır.
- **Çıktı formatı:** Üste `## Çıktılar` çalışma ürünü başlığı + `Reviewer note` koy; ardından Yönetici Özeti (`🔴/🟠/🟡/🟢` sayıları, sevkiyat çağrısı), Üst Uyarılar (`license-unknown`, çakışan başlık, Non-OSI), Paket Bazlı Analiz, Yargı Alanı Notu ve Onay Yönlendirmesi bölümlerini ver.
- **Doğrulama:** Lisans metinleri dosyadan okunduysa `[kullanıcı sağladı]`; genel lisans/rehber yorumları `[model bilgisi - doğrula]` veya `[web search - verify]` etiketiyle verilir.
- **Kapanış ve Pano:** Analizi `## Çıktılar` altındaki Sonraki Adımlar Karar Ağacı ile bitir. İncelenen paket sayısı 10'u aşarsa `` `## Çıktılar → Veri Yoğun Çıktılarda Pano Teklifi` `` uyarınca lisans ailesi dağılımı ve risk tablosu için interaktif HTML pano öner.
