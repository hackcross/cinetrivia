# CineTrivia — Google Play Yayınlama Rehberi

## Dosya Yapısı
```
cinetrivia-pwa/
├── index.html      ← Oyun (PWA-ready)
├── manifest.json   ← Uygulama bilgileri
├── sw.js          ← Service Worker (offline destek + görsel cache)
├── icon-192.png   ← Uygulama ikonu (192x192)
├── icon-512.png   ← Uygulama ikonu (512x512)
└── README.md      ← Bu dosya
```

## Adım 1: GitHub'a Yükle
1. github.com'da yeni repo oluştur (örn: `cinetrivia`)
2. Tüm dosyaları repoya yükle
3. Settings → Pages → Source: `main` branch, `/ (root)` → Save
4. Birkaç dakika bekle, site yayınlanacak: `https://KULLANICIADIN.github.io/cinetrivia/`

## Adım 2: PWA'yı Test Et
1. Chrome'dan GitHub Pages URL'ini aç
2. Adres çubuğunda "Install" butonu çıkmalı
3. Lighthouse testini çalıştır (DevTools → Lighthouse → PWA)
4. Tüm PWA kriterlerini geçtiğini doğrula

## Adım 3: Android APK/AAB Oluştur

### Seçenek A: PWABuilder (en kolay)
1. https://www.pwabuilder.com adresine git
2. GitHub Pages URL'ini yapıştır
3. "Package for stores" → "Android" seç
4. TWA (Trusted Web Activity) seçeneğini kullan
5. Signing key oluştur ve kaydet (Play Store'a yüklerken lazım)
6. APK/AAB dosyasını indir

### Seçenek B: Bubblewrap (gelişmiş)
```bash
npm i -g @nicolo-ribaudo/bubblewrap
bubblewrap init --manifest https://KULLANICIADIN.github.io/cinetrivia/manifest.json
bubblewrap build
```

## Adım 4: Google Play Console
1. https://play.google.com/console adresine git
2. Geliştirici hesabı oluştur (25$ tek seferlik ücret)
3. "Create app" → bilgileri doldur:
   - App name: CineTrivia
   - Default language: English
   - App type: Game
   - Category: Trivia
   - Free
4. Store listing:
   - Kısa açıklama: "Guess the movie from the scene!"
   - Uzun açıklama: "Test your movie knowledge..."
   - Screenshots (min 2): Telefondan ekran görüntüsü al
   - Feature graphic (1024x500): Tasarla veya Canva'dan yap
   - App icon: icon-512.png
5. Content rating: IARC anketini doldur
6. Privacy policy: Basit bir gizlilik politikası sayfası oluştur
7. AAB dosyasını yükle → Review'a gönder

## Adım 5: Assetlinks (Digital Asset Links)
TWA için doğrulama gerekli:
1. PWABuilder'dan `.well-known/assetlinks.json` dosyasını al
2. GitHub repo'na `.well-known/assetlinks.json` olarak ekle
3. Bu dosya uygulamanın web sitesiyle bağlantısını doğrular

## Özellikler
- ✅ PWA manifest + Service Worker
- ✅ Offline destek (görseller cache'lenir)
- ✅ Android geri tuşu yönetimi
- ✅ Splash screen
- ✅ Safe area (notch) desteği
- ✅ Portrait orientation kilidi
- ✅ 8 dil desteği
- ✅ Leaderboard (localStorage)
- ✅ 198 film, 344 sahne görseli
- ✅ Classic + Match modları

## Notlar
- Görseller image.tmdb.org CDN'den yükleniyor, ilk oynayışta internet gerekli
- Service Worker görselleri cache'ler, sonraki oynayışlarda offline çalışır
- Leaderboard şu an localStorage tabanlı (cihaz bazlı)
- Firebase entegrasyonu ile global leaderboard eklenebilir
