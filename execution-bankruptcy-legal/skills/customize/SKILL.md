---
name: customize
description: >
  Kurum veya büronun değişen icra tahsilat politikalarını, eskalasyon para
  sınırlarını, faiz ve teminat duruşunu ya da özel şablon yollarını mevcut
  `CLAUDE.md` dosyası üzerinde günceller.
---

# İcra & İflas Profili ve Politika Özelleştirme (`customize`)

Halihazırda yapılandırılmış `execution-bankruptcy-legal` kurulumunda yalnızca değişen politikaları veya eşikleri güncellemek için kullanılır. Sıfırdan kurulum gerekiyorsa `/execution-bankruptcy-legal:cold-start-interview` tercih edilir.

## Güncellenebilir Alanlar

1. **`## Şirket / Büro Profili` ve `## Kullanıcı Rolü`:** Yeni ekip üyesi yetkileri, imza sınırları veya varsayılan taraf duruşu değişikliği.
2. **`## Takip ve Tahsilat Duruşu (Collection & Defense Posture)` & `### Onay ve Eskalasyon Matrisi`:**
   - Alacaklı takiplerinde tahsilattan sulh/taksit kabulüne (`İİK m. 111`) geçilebilecek minimum peşinat oranı ve kıdemli onay tutarı.
   - `İİK m. 89/1` ihbarnamelerinde cari hesap kontrolü ve cevap için iç eskalasyon SLA süresi (ör. tebliğden sonraki ilk 48 saat).
   - İhtiyati haciz (`İİK m. 257`) teminat mektubu / nakdi teminat onay eşiği.
3. **`## İcra Takip Portföyü ve Süre Kuralları` ve `## Konkordato ve İflas İzleme Politikası`:** Özel erken uyarı gün pencereleri (ör. satış isteme 1 yıllık süresine 60 gün kala alarm) ve güncel mevzuat notları (`references/currency-watch.md`).
4. **Özel Şablonlar (`~/.claude/plugins/config/legal-turkish/execution-bankruptcy-legal/`):** Kuruma özel Örnek 7/10 itiraz dilekçesi, `89/1` standart cevabı veya ibra/taahhüt şablonu yollarının tanımlanması.

## İş Akışı ve Koruma Kuralları

- Önce mevcut `CLAUDE.md` içeriğini oku; kullanıcıyla yalnızca değişecek maddeleri netleştir.
- `## Çekirdek Güvenlik Kuralları (Shared Guardrails)` altındaki güvenlik tabanlarını (**önem derecesi tabanı gerekçesiz düşürülemez**, **sessiz tamamlama yok**, **hedef kitle kontrolü**) asla zayıflatma veya silme.
- Güncelleme tamamlandıktan sonra değiştirilen satırları kısa bir özetle sun.
