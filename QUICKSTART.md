# Quick Start - Legal Turkish

Bu klasör, **Claude for Legal** yapısının Türk hukuku uyarlama paketidir.

## 1. Marketplace Olarak Ekle

Claude Code içinde:

```text
/plugin marketplace add C:\path\to\claude-for-legal-turkish-main
```

Yol farklıysa `claude-for-legal-turkish-main` klasörünü terminale sürükleyebilirsiniz.

## 2. Plugin Kur

Örnek:

```text
/plugin install commercial-legal@legal-turkish
```

veya:

```text
/plugin install litigation-legal@legal-turkish
```

## 3. Claude Code'u Yeniden Başlat

Plugin komutları yeniden başlatmadan görünmeyebilir.

## 4. Başlangıç Mülakatını Çalıştır

Ticari hukuk için:

```text
/commercial-legal:cold-start-interview
```

Dava / ihtarname / uyuşmazlık işleri için:

```text
/litigation-legal:cold-start-interview
```

## 5. İlk Komutlar

Ticari sözleşme:

```text
/commercial-legal:review
```

Gizlilik sözleşmesi (NDA algılandığında otomatik olarak `nda-review` uzman skill'ini çalıştırır):

```text
/commercial-legal:review "C:\sozlesmeler\gizlilik-sozlesmesi.docx"
```

Yenileme takibi:

```text
/commercial-legal:renewal-tracker
```

İhtarname ön hazırlık:

```text
/litigation-legal:demand-intake
```

İhtarname taslak:

```text
/litigation-legal:demand-draft <slug>
```

## Not

- **Profil Dizini:** Aynı makinede orijinal `claude-for-legal` eklentisiyle çakışmaması için tüm Türk uyarlaması profilleri `~/.claude/plugins/config/legal-turkish/` altında saklanır. Eski `~/.claude/plugins/config/claude-for-legal/` klasöründe profiliniz varsa yeni yola kopyalayabilirsiniz.
- **Komut Adları:** Komut adları şimdilik orijinal repo ile uyumlu kalır (`/commercial-legal:review` vb.). Türkçeleştirme hukuki içerikte ve çıktı dilindedir. Komut adlarını `/ticari-hukuk:*` gibi Türkçeleştirmek istersek bu ayrı bir repo-geneli yeniden adlandırma işidir.

