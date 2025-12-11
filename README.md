# Star Gazetesi - Haber Portalı

Modern, responsive ve kullanıcı dostu bir haber portalı web uygulaması. Vue.js 3 ve Vite ile geliştirilmiştir.

## 📋 İçindekiler

- [Özellikler](#özellikler)
- [Teknoloji Stack](#teknoloji-stack)
- [Kurulum](#kurulum)
- [Geliştirme](#geliştirme)
- [Proje Yapısı](#proje-yapısı)
- [Önemli Bileşenler](#önemli-bileşenler)
- [API Entegrasyonları](#api-entegrasyonları)
- [Responsive Tasarım](#responsive-tasarım)
- [Dark Mode](#dark-mode)
- [Deployment](#deployment)

## ✨ Özellikler

### Header Bileşenleri
- **Top Bar**: Hava durumu widget'ı, logo, tarih/saat gösterimi
- **Main Navigation**: Responsive menü sistemi, hamburger menü (mobil)
- **Sub Bar**: Dinamik döviz kurları (Dolar, Euro, Altın), sosyal medya linkleri
- **Breaking News Bar**: Otomatik kaydırmalı son dakika haberleri (Swiper.js)

### Ana Sayfa
- **Headline Slider**: Büyük manşet görseli ve interaktif thumbnail slider
- **Hover Interaction**: Thumbnail'lere hover ile ana görseli değiştirme
- **Active Indicator**: Seçili thumbnail için kırmızı alt çizgi

### Footer
- 6 kolonlu responsive layout
- Haber kategorileri, uygulama indirme linkleri
- Sosyal medya ikonları
- Dark mode desteği

### Genel Özellikler
- ✅ Tam responsive tasarım (mobil, tablet, desktop)
- ✅ Dark/Light mode toggle
- ✅ Dinamik hava durumu (Open-Meteo API)
- ✅ Gerçek zamanlı döviz kurları (TCMB API)
- ✅ SCSS ile modüler stil yönetimi
- ✅ Vue Router ile sayfa yönlendirme

## 🛠 Teknoloji Stack

### Core
- **Vue.js 3** - Progressive JavaScript framework
- **Vite** - Next generation frontend tooling
- **Vue Router** - Official router for Vue.js

### Styling
- **SCSS** - CSS preprocessor
- **CSS Variables** - Theme management

### Libraries
- **Swiper.js** - Modern touch slider
  - Breaking news carousel
  - Headline thumbnail slider
  - Navigation ve Autoplay modülleri

### APIs
- **Open-Meteo API** - Hava durumu verileri (İstanbul)
- **TCMB API** - Türkiye Cumhuriyet Merkez Bankası döviz kurları

## 📦 Kurulum

### Gereksinimler
- Node.js (v20.13.0 veya üzeri önerilir)
- npm veya yarn

### Adımlar

1. **Projeyi klonlayın**
```bash
git clone <repository-url>
cd home-page
```

2. **Bağımlılıkları yükleyin**
```bash
npm install
```

3. **Geliştirme sunucusunu başlatın**
```bash
npm run dev
```

Uygulama varsayılan olarak `http://localhost:5173` adresinde çalışacaktır.

## 🚀 Geliştirme

### Mevcut Komutlar

```bash
# Geliştirme sunucusu (hot-reload)
npm run dev

# Production build
npm run build

# Production build'i önizleme
npm run preview
```

### Kod Yapısı

```
src/
├── assets/          # Görseller, medya dosyaları
├── components/      # Vue bileşenleri
│   ├── Navbar.vue   # Header ve tüm alt bileşenleri
│   └── Footer.vue   # Footer bileşeni
├── views/           # Sayfa bileşenleri
│   └── Home.vue     # Ana sayfa (headline slider)
├── router/          # Vue Router yapılandırması
├── style.scss       # Global stiller ve CSS variables
├── App.vue          # Ana uygulama bileşeni
└── main.js          # Uygulama giriş noktası
```

## 🧩 Önemli Bileşenler

### Navbar.vue
**Sorumluluklar:**
- Hava durumu widget'ı (Open-Meteo API entegrasyonu)
- Dinamik tarih/saat gösterimi (Gregoryen + Hicri takvim)
- Döviz kurları (TCMB API entegrasyonu)
- Dark mode toggle
- Breaking news carousel (Swiper.js)
- Responsive navigation

**Önemli Özellikler:**
- `fetchWeatherData()`: İstanbul için hava durumu çeker
- `fetchCurrencyData()`: Dolar ve Euro kurlarını çeker
- `updateTime()`: Her saniye tarih/saat günceller
- `toggleDarkMode()`: Dark mode'u açıp kapatır

### Home.vue
**Sorumluluklar:**
- Ana manşet görseli
- Thumbnail slider (Swiper.js)
- Hover ile görsel değiştirme

**Önemli Özellikler:**
- `setMainSlide()`: Hover edilen thumbnail'i ana görsel yapar
- `activeIndex`: Aktif thumbnail'i takip eder

### Footer.vue
**Sorumluluklar:**
- 6 kolonlu responsive layout
- Haber kategorileri ve linkler
- Sosyal medya ve uygulama linkleri
- Dark mode desteği

## 🌐 API Entegrasyonları

### 1. Open-Meteo API (Hava Durumu)
```javascript
// Endpoint
https://api.open-meteo.com/v1/forecast

// Parametreler
latitude: 41.0082  // İstanbul
longitude: 28.9784
current: temperature_2m,weather_code
daily: temperature_2m_max,temperature_2m_min
timezone: Europe/Istanbul
```

### 2. TCMB API (Döviz Kurları)
```javascript
// Endpoint
https://www.tcmb.gov.tr/kurlar/today.xml

// Dönüş: XML formatında günlük döviz kurları
// Parse edilen: USD, EUR
```

**Not:** Altın fiyatı şu anda placeholder olarak gösterilmektedir. TCMB API'si altın fiyatı sağlamadığı için ayrı bir API entegrasyonu gerekebilir.

## 📱 Responsive Tasarım

### Breakpoint'ler
- **Desktop**: > 1024px
- **Tablet**: 768px - 1024px
- **Mobile**: < 768px
- **Small Mobile**: < 480px

### Mobil Optimizasyonlar
- Hamburger menü (768px altı)
- Kompakt header layout
- Floating dark mode toggle (sağ alt köşe)
- Horizontal scroll (market verileri)
- Card-based thumbnail slider
- Touch-friendly button boyutları (min 44px)

### Tablet Optimizasyonlar
- Azaltılmış padding ve margin değerleri
- Küçültülmüş font boyutları
- 2 kolonlu thumbnail slider

## 🌙 Dark Mode

### Implementasyon
- Class-based sistem (`body.dark-mode`)
- CSS Variables ile tema yönetimi
- LocalStorage ile tercih kaydedilmez (her oturum başlangıcında light mode)

### CSS Variables
```scss
// Light Mode
--bg-color: #ffffff
--text-color: #213547
--header-bg: #ffffff

// Dark Mode
--bg-color: #242424
--text-color: #ffffff
--header-bg: #1a1a1a
```

### Kapsam
- ✅ Header (tüm bileşenler)
- ✅ Main content area
- ✅ Headline slider
- ✅ Footer
- ✅ Tüm interaktif elementler

## 🎨 Tasarım Kararları

### Renk Paleti
- **Primary**: #d40000 (Star kırmızısı)
- **Header Dark Mode**: #1a1a1a
- **Body Dark Mode**: #242424
- **Border**: #444 (dark mode), #eee (light mode)

### Typography
- **Font Family**: Arial, sans-serif
- **Headline**: 44px (desktop), 22px (mobile)
- **Navigation**: 15px, font-weight: 900

### Spacing
- **Container Max Width**: 1280px
- **Container Padding**: 40px (desktop), 16px (mobile)
- **Section Gaps**: 24px

## 📂 Önemli Dosyalar

### Konfigürasyon
- `vite.config.js` - Vite yapılandırması
- `package.json` - Proje bağımlılıkları
- `index.html` - HTML template

### Stiller
- `src/style.scss` - Global stiller, CSS variables
- Component-level: `<style scoped lang="scss">`

### Assets
- `src/assets/starlogo2025.png` - Ana logo
- `public/favicon.svg` - Favicon (kırmızı 'S')

## 🚢 Deployment

### Production Build
```bash
npm run build
```

Build çıktısı `dist/` klasöründe oluşturulur.

### Deployment Seçenekleri
- **Vercel**: Otomatik deployment (önerilir)
- **Netlify**: Drag & drop veya Git entegrasyonu
- **GitHub Pages**: Static hosting
- **Heroku**: Container-based deployment

### Environment Variables
Şu anda environment variable kullanılmamaktadır. API'ler public endpoint'lerdir.

## 🐛 Bilinen Sorunlar ve Çözümler

### 1. Node.js Version Warning
```
WARN EBADENGINE Unsupported engine
```
**Çözüm**: Node.js v20.19.0 veya v22.12.0+ kullanın. Mevcut versiyon (v20.13.0) çalışıyor ancak uyarı veriyor.

### 2. SCSS Import
SCSS dosyaları `lang="scss"` attribute'u ile kullanılmalıdır:
```vue
<style scoped lang="scss">
```

### 3. Swiper Dark Mode
Swiper component'leri için hem `body.dark-mode` hem de `:global(body.dark-mode)` selector'ları kullanılmalıdır (Vue scoped CSS nedeniyle).

## 📝 Geliştirme Notları

### Gelecek İyileştirmeler
- [ ] Hamburger menü fonksiyonelliği (mobil)
- [ ] Dinamik Hicri tarih hesaplama
- [ ] Altın fiyatı için API entegrasyonu
- [ ] Haber içerik yönetim sistemi
- [ ] Arama fonksiyonelliği
- [ ] Kategori sayfaları
- [ ] Haber detay sayfası
- [ ] Yorum sistemi
- [ ] Newsletter entegrasyonu

### Performans
- Lazy loading için Vue Router kullanılabilir
- Image optimization (WebP format)
- API response caching
- Service Worker (PWA)

## 👥 Katkıda Bulunma

1. Fork yapın
2. Feature branch oluşturun (`git checkout -b feature/amazing-feature`)
3. Commit yapın (`git commit -m 'feat: Add amazing feature'`)
4. Push yapın (`git push origin feature/amazing-feature`)
5. Pull Request açın

## 📄 Lisans

Bu proje özel bir projedir. Tüm hakları saklıdır.

## 📞 İletişim

Proje ile ilgili sorularınız için issue açabilirsiniz.

---

**Son Güncelleme**: 11 Aralık 2025
**Versiyon**: 1.0.0
