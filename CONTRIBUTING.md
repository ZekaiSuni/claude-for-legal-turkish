# Claude Legal Turkish — Katkı ve Tasarım İlkeleri

Bu dosya, repo içindeki eklenti ve skill dosyalarını geliştiren veya uyarlayan hukukçu/geliştiriciler için temel tasarım kurallarını özetler.

## Temel Tasarım İlkesi: Doktrin `SKILL.md` İçindedir, `CLAUDE.md` Emniyet Ağıdır

Her eklenti iki katmandan oluşur:

1. **`<eklenti>/skills/<skill>/SKILL.md`** — Belirli görevi adım adım yöneten dar kapsamlı iş akışı ve somut Türk hukuku kontrol listesi.
2. **`<eklenti>/CLAUDE.md`** — Kurum profili ile ortak emniyet kuralları (`Shared Guardrails`): sessiz tamamlama yasağı, güncellik tetikleyicisi, kullanıcı beyanı doğrulama, kaynak etiketi disiplini, güvenilmez belge/prompt-injection savunması, birebir alıntı sadakati ve önem derecesi tabanı.

**Kural:** Bir skill doğru sonucu yalnızca `CLAUDE.md`'deki genel bir emniyet kuralı devreye girdiği için üretiyorsa, o hukuki kural doğrudan `SKILL.md`'nin kendi kontrol listesine eklenmelidir (`CLAUDE.md` emniyet ağı yine korunur).

Örnekler:
- Yenileme ihbar son günü hafta sonuna/resmî tatile denk geldiğinde veya KEP kullanıldığında (`KEP Yönetmeliği m. 15/2` +1 gün), tarih çekme mantığı doğrudan `renewal-tracker` şema ve talimatında yer almalıdır.
- Tescil öncesi marka incelemesinde kamu düzeni/ahlaka aykırılık (`SMK m. 5/1-(ı)`) veya işten çıkarmada haklı fesih hak düşürücü süresi (`4857 m. 26`: 6 iş günü / 1 yıl) ve `TBK m. 420` ibraname şartları doğrudan ilgili skill'de zorunlu kapı olmalıdır.

## Somut Uygulama Kuralları

- **Doktrini skill içine koy:** "Ayrıca X'i de düşünün" demek yerine somut kanun maddesi, süre veya istisna kontrol listesini yaz.
- **Kaynak etiketini rakamın/iddianın yanına koy:** Paragraf sonu genel uyarılar kaybolur; `[model bilgisi - doğrula]`, `[Mevzuat.gov.tr]`, `[Resmî Gazete]`, `[kullanıcı sağladı]` veya `[review]` etiketi doğrudan kritik tarih, tutar veya maddenin yanında yer almalıdır.
- **Reddetme / durdurma kapısını varsayılan-açık yaz:** Skill kesin hukuki hesap veya imza yetkisi vermiyorsa durdurma kuralı belirsiz bir parantez içinde değil, açık ve aşılamaz bir kapı başlığı olarak yazılmalıdır.
- **Yabancı mevzuatı kör bul-değiştir ile çevirme:** `USPTO → TÜRKPATENT`, `GDPR → KVKK`, `Lanham Act → SMK` gibi mekanik değiştirmeler ters hukuki sonuç doğurur (ör. ABD Fair Use vs. FSEK m. 30–40; GDPR Art. 22 vs. KVKK m. 11/1-(g)). Her kavram Türk hukukundaki gerçek karşılığıyla yazılmalıdır.

## Geliştirme ve Doğrulama Adımları

1. Bir skill'i düzenlemeden önce ilgili eklentinin `CLAUDE.md` ve `README.md` dosyalarını okuyun.
2. Kullanıcı profil yollarında daima `~/.claude/plugins/config/legal-turkish/<eklenti>/...` kullanın; orijinal `claude-for-legal/` diziniyle karıştırmayın.
3. `CLAUDE.md` içindeki ortak emniyet kurallarını (`Shared Guardrails`) asla silmeyin.
4. Değişiklik sonrası eklenti `plugin.json` sürümünü güncelleyin ve her platformda şu iki doğrulama aracını çalıştırın:

```bash
python scripts/lint-tool-scope.py
python scripts/audit_repo.py
```
