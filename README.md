# Birsen Demir Aile Danışmanlığı · otomatik paylaşım

GitHub Actions üzerinde ücretsiz çalışır. Bilgisayarın açık olması gerekmez.

- `schedule.json`: 30 günlük takvim, 9 Kasım – 8 Aralık 2026 (saatler UTC; Türkiye = UTC+3)
  - Her gün 12:30 TR: Instagram hikâyesi
  - Her gün 19:00 TR: Instagram gönderisi (açıklama, hashtag ve görsel açıklamasıyla)
- `media/posts`: 30 gönderi görseli (1080×1350 JPEG)
- `media/stories`: 30 hikâye görseli (1080×1920 JPEG)
- `posted.json`: neyin paylaşıldığının kaydı (sistem kendisi günceller)
- `scripts/autopost.py`: paylaşım programı
- `ACIKLAMALAR.md`: tüm gönderi metinleri, okuyup düzeltmek için

## Kurulum (bir kez)

0. **Hesap türü:** Instagram uygulamasında @birsendemirailedanismanligi → Ayarlar → Hesap türü ve araçlar →
   **Profesyonel hesaba geç** → İşletme. (API kişisel hesaplarda çalışmaz; takipçiler ve gönderiler etkilenmez.)
1. **Depo:** GitHub'da `birsendemir-autopost` adında **Public** bir depo aç ve bu klasörün içeriğini yükle.
   Instagram görselleri herkese açık bir adresten çektiği için depo açık olmalı.
   `.github/workflows` içindeki iki dosya GitHub'da "Add file → Create new file" ile oluşturulur.
2. **Meta uygulaması:** developers.facebook.com → Uygulama oluştur → İçerik yönetimi → Instagram →
   "API setup with Unified login" → yapılandırma oluştur → hesabı **Instagram Tester** olarak ekle →
   instagram.com/accounts/manage_access adresinden daveti kabul et → **Generate token**.
3. **Secrets:** Depo → Settings → Secrets and variables → Actions → New repository secret
   - `IG_ACCESS_TOKEN` = 2. adımdaki anahtar (kimseyle paylaşma)
   - `IG_USER_ID` = Meta ekranında hesabın yanında görünen Instagram kimlik numarası
4. **Test:** Actions → "Otomatik paylaşım" → Run workflow → command: `check`. Yeşil olmalı.
   İstersen `post` + `day01-story` ile tek bir hikâyeyi hemen dene.

Bundan sonra sistem kendi kendine çalışır. Bir paylaşım başarısız olursa GitHub e-posta gönderir.
GitHub zamanlayıcısı 5–20 dakika gecikebilir. 12 saatten fazla geciken paylaşım atlanır.

## Sık işler

- **Takvimi görmek:** Actions → Run workflow → `status`
- **Durdurmak:** Actions → "Otomatik paylaşım" → ⋯ → Disable workflow
- **Deneme modu:** Settings → Variables → `DRY_RUN` = `true` (hiçbir şey paylaşılmaz)
- **Bir metni düzeltmek:** `schedule.json` içinde ilgili günün `caption` alanını düzenle
- **Yeni içerik eklemek:** `media/` içine görseli koy, `schedule.json`'a bir satır ekle

Hikâyeler API ile paylaşıldığı için üzerine anket ya da soru etiketi eklenemez; hikâyeler "DM'den yazın" çağrısıyla hazırlandı.
