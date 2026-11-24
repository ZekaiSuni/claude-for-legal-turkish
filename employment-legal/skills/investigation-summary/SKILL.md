---
name: investigation-summary
description: >
  İç soruşturma notundan hedef kitleye uygun özet üretir. Hukuk, İK, yönetim,
  çalışanla paylaşılacak sınırlı metin veya dış danışman özeti için gizlilik,
  KVKK ve iş hukuku risklerini ayrıştırır.
argument-hint: "[slug] [hedef kitle]"
---

# /investigation-summary

1. Memo ve kaynak dosyaları oku.
2. Hedef kitleyi belirle: hukuk, İK, yönetim, dış danışman, çalışanla paylaşılacak sınırlı metin.
3. İç hukuki kanaatleri dışa gidecek metinden çıkar.
4. Kişisel veri ve hassas ayrıntıları minimumda tut.

Çıktı:

```markdown
# Soruşturma Özeti - [hedef kitle]

## Ne oldu
## Ne biliyoruz
## Ne bilmiyoruz
## Riskler
## Önerilen aksiyon
```
