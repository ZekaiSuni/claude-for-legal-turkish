---
name: customize
description: >
  Employment practice profilinde tekil ayar değiştirir. İşe alım, ücret/çalışma
  süresi, fazla çalışma, izin, fesih, arabuluculuk, SGK/İŞKUR/İSG, iç soruşturma,
  KVKK, politika veya matter workspace ayarlarını tüm cold-start mülakatını
  tekrar etmeden günceller.
argument-hint: "[bölüm adı veya değiştirmek istediğiniz şey]"
---

# /customize

## Akış

1. `~/.claude/plugins/config/legal-turkish/employment-legal/CLAUDE.md` dosyasını oku.
2. Profil yoksa veya placeholder ağırlıklıysa `/employment-legal:cold-start-interview` öner.
3. Değiştirilebilir haritayı göster:
   - **Kurum ve İşyeri Profili**
   - **Kullanıcı Rolü**
   - **İşe Alım ve Sözleşme Playbook**
   - **Ücret ve Çalışma Süresi**
   - **İzin ve Devamsızlık**
   - **Fesih ve Arabuluculuk**
   - **İşyeri Politikaları**
   - **İç Soruşturma**
   - **SGK / İŞKUR / İSG / KVKK Kapıları**
   - **Matter Workspaces**
4. Tek değişiklik seçtir; mevcut değeri göster.
5. Yeni değeri al, etkilenen skill'leri açıkla.
6. Yazmadan önce onay al.

## Aşağı Akış Etkisi

- Fesih kırmızı bayrağı değişirse `termination-review` bunu uygular.
- Fazla çalışma standardı değişirse `wage-hour-qa`, `hiring-review` ve `policy-drafting` etkilenir.
- İzin sistemi değişirse `leave-tracker` ve `log-leave` etkilenir.
- İç soruşturma sahibi değişirse `investigation-*` ve `internal-investigation` etkilenir.
- SGK çıkış kodu onay süreci değişirse `termination-review` bunu gate yapar.

## Guardrails

- İş güvencesi, zorunlu arabuluculuk, SGK bildirimi, İSG bildirimi, KVKK çalışan verisi ve haklı fesih süre kontrollerini kaldırma.
- Kanuni süreyi daha uzun iç hedef gibi kaydetme; iç hedef daha kısa olabilir.
- "Her fesih serbesttir" benzeri Türk hukukuyla çelişen varsayım kurma.
- Bir seferde tek değişiklik yap.

## Çıktı

```markdown
# Employment Profil Güncellemesi

**Değişen bölüm:** [bölüm]
**Eski değer:** [özet]
**Yeni değer:** [özet]

## Etkilenen Skill'ler
- [skill]: [etki]

## Kontrol
- [ ] Çelişki yok
- [ ] İnsan onayı alındı
- [ ] Sonraki çıktı yeni değeri kullanacak
```
