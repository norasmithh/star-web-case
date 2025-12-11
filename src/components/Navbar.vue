<template>
  <header>
    <!-- 1. ÜST BAR: Hava Durumu - Logo - Tarih/Saat -->
    <div class="top-bar">
      <div class="weather-widget">
        <div class="weather-row-1">
          <span class="city">İSTANBUL</span>
          <span class="temp-values">{{ weather.current }}°C / {{ weather.low }}°C</span>
        </div>
        <div class="weather-desc">{{ weather.desc }}</div>
      </div>

      <div class="logo-area">
        <a href="/" class="logo-link">
          <img src="../assets/starlogo2025.png" alt="Star Gazetesi" class="main-logo" style="width: 193px;" />
        </a>
        <div class="date-hijri">{{ currentDate }} / {{ hijriDate }}</div>
      </div>

      <div class="right-info">
        <div class="mode-toggle" @click="toggleDarkMode">
          <span class="moon-icon">{{ isDarkMode ? '☀️' : '🌙' }}</span> {{ isDarkMode ? 'Gündüz modu' : 'Gece modu' }}
        </div>
        <div class="location-time">
          İSTANBUL <span class="time">{{ currentTime }}</span>
        </div>
        <div class="prayer-time">
          İmsak kalan süre <span class="countdown">04:12:45</span>
        </div>
      </div>
    </div>

    <!-- 2. MENÜ BARI -->
    <nav class="main-nav">
      <div class="nav-container">
        <ul class="nav-links">
          <li class="active">SON DAKİKA</li>
          <li>GÜNCEL</li>
          <li>DÜNYA</li>
          <li>EKONOMİ</li>
          <li>SPOR</li>
          <li>YAŞAM</li>
          <li>BİLİM-TEKNOLOJİ</li>
          <li>AÇIK GÖRÜŞ</li>
          <li>YAZARLAR</li>
          <li>SEYAHAT</li>
        </ul>
        <div class="hamburger-menu">
          <span>☰</span>
        </div>
      </div>
    </nav>

    <!-- 3. SİYAH BAR: Piyasa ve Linkler -->
    <div class="sub-bar">
      <div class="sub-container">
        <div class="market-data">
          <div class="market-item">
            DOLAR <span class="value up">{{ currencies.usd }}</span>
          </div>
          <div class="market-item">
            EURO <span class="value up">{{ currencies.eur }}</span>
          </div>
          <div class="market-item">
            ALTIN <span class="value down">{{ currencies.gold }}</span>
          </div>
        </div>

        <div class="sub-links">
          <a href="#"><span class="icon">📷</span> FOTO GALERİ</a>
          <a href="#"><span class="icon">ws</span> VİDEO GALERİ</a>
          <a href="#"><span class="icon">📺</span> CANLI YAYIN</a>
          
          <div class="social-icons">
            <span class="soc">N</span>
            <span class="soc">f</span>
            <span class="soc">X</span>
            <span class="soc">in</span>
            <span class="soc">yt</span>
          </div>
          <span class="search-icon">🔍</span>
        </div>
      </div>
    </div>

    <!-- 4. KIRMIZI SON DAKİKA BARI -->
    <div class="breaking-news-bar">
      <div class="bn-container">
        <div class="bn-arrows">
          <div class="bn-prev">‹</div>
          <div class="bn-next">›</div>
        </div>
        <div class="bn-label">SON<br>DAKİKA</div>
        <swiper
          :modules="[Navigation, Autoplay]"
          :slides-per-view="auto"
          :space-between="30"
          :autoplay="{ delay: 5000, disableOnInteraction: false }"
          :loop="true"
          :navigation="{
            nextEl: '.bn-next',
            prevEl: '.bn-prev',
          }"
          class="bn-swiper"
        >
          <swiper-slide v-for="(news, index) in breakingNews" :key="index" class="bn-slide">
            <div class="bn-item">
              <span class="time-tag">{{ news.time }}</span>
              {{ news.title }}
            </div>
          </swiper-slide>
        </swiper>
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Navigation, Autoplay } from 'swiper/modules';
import 'swiper/css';
import 'swiper/css/navigation';

// --- HAVA DURUMU ---
const weather = ref({
  current: '--',
  low: '--',
  desc: 'Yükleniyor...'
});

const fetchWeather = async () => {
  try {
    // İstanbul koordinatları: 41.0082, 28.9784
    const response = await fetch(
      'https://api.open-meteo.com/v1/forecast?latitude=41.0082&longitude=28.9784&current_weather=true&daily=temperature_2m_max,temperature_2m_min&timezone=auto'
    );
    const data = await response.json();
    
    weather.value = {
      current: Math.round(data.current_weather.temperature),
      low: Math.round(data.daily.temperature_2m_min[0]),
      desc: getWeatherDesc(data.current_weather.weathercode)
    };
  } catch (error) {
    console.error('Hava durumu alınamadı:', error);
    weather.value.desc = 'Hata oluştu';
  }
};

const getWeatherDesc = (code) => {
  // WMO Weather interpretation codes (simplified)
  const codes = {
    0: 'Açık, Güneşli',
    1: 'Az Bulutlu',
    2: 'Parçalı Bulutlu',
    3: 'Kapalı',
    45: 'Sisli',
    48: 'Sisli',
    51: 'Hafif Çiseleme',
    61: 'Yağmurlu',
    71: 'Kar Yağışlı',
    95: 'Fırtınalı'
  };
  return codes[code] || 'Parçalı Bulutlu';
};

// --- DÖVİZ VE ALTIN FİYATLARI ---
const currencies = ref({
  usd: '--',
  eur: '--',
  gold: '--'
});

const fetchCurrencyData = async () => {
  try {
    // TCMB API'si - günlük döviz kurları
    const today = new Date();
    const dateStr = today.toISOString().split('T')[0].replace(/-/g, '');
    
    const response = await fetch(
      `https://www.tcmb.gov.tr/kurlar/${dateStr.slice(0,6)}/${dateStr}.xml`
    );
    const text = await response.text();
    const parser = new DOMParser();
    const xml = parser.parseFromString(text, 'text/xml');
    
    // USD
    const usdNode = xml.querySelector('Currency[CurrencyCode="USD"] ForexSelling');
    if (usdNode) {
      currencies.value.usd = parseFloat(usdNode.textContent).toFixed(4);
    }
    
    // EUR
    const eurNode = xml.querySelector('Currency[CurrencyCode="EUR"] ForexSelling');
    if (eurNode) {
      currencies.value.eur = parseFloat(eurNode.textContent).toFixed(4);
    }
    
    // Altın için alternatif API kullanacağız (TCMB XML'de altın yok)
    // Basit bir placeholder değer - gerçek API entegrasyonu için ayrı endpoint gerekir
    currencies.value.gold = '5855.63'; // Placeholder
    
  } catch (error) {
    console.error('Döviz verileri alınamadı:', error);
    // Hata durumunda varsayılan değerler
    currencies.value = {
      usd: '42.6075',
      eur: '50.2063',
      gold: '5855.63'
    };
  }
};

// --- TARİH VE SAAT ---
const currentTime = ref('');
const currentDate = ref('');
const hijriDate = ref('21 CemaziyelAhir 1447');

const updateTime = () => {
  const now = new Date();
  currentTime.value = now.toLocaleTimeString('tr-TR', { hour: '2-digit', minute: '2-digit', second: '2-digit' });
  
  const options = { day: 'numeric', month: 'long', year: 'numeric', weekday: 'long' };
  currentDate.value = now.toLocaleDateString('tr-TR', options);
};

// --- DARK MODE ---
const isDarkMode = ref(false);

const toggleDarkMode = () => {
  isDarkMode.value = !isDarkMode.value;
  if (isDarkMode.value) {
    document.body.classList.add('dark-mode');
  } else {
    document.body.classList.remove('dark-mode');
  }
};

// --- BREAKING NEWS ---
const breakingNews = ref([
  { time: '20:11', title: 'Beyin kanserinin 7 uyarı işareti kolayca gözden kaçabiliyor' },
  { time: '20:09', title: 'Kyoto Üniversitesi araştırması Newton\'un yasasını sorgulatıyor' },
  { time: '20:07', title: 'Aşkabat\'a kritik ziyaret: Cumhurbaşkanı Erdoğan\'a resmi törenli karşılama' },
  { time: '20:07', title: 'Alzheimer hastalığının sırrı beyin hücrelerinin köprülerinde mi gizli?' },
  { time: '20:06', title: 'Erkeklerdeki gizli DNA tehlikesi yaş ve sağlık ilişkisini nasıl etkiliyor?' },
  { time: '20:03', title: 'Bakan Tunç: Yeni anayasa milletimize borcumuzdur' },
  { time: '20:03', title: 'Bilim insanları bebeklerdeki nadir diyabeti tetikleyen geni buldu' },
  { time: '19:59', title: 'Milyonlarca insanı etkileyen hastalığın sırrı kan testinde mi gizli?' },
]);

onMounted(() => {
  fetchWeather();
  fetchCurrencyData();
  updateTime();
  setInterval(updateTime, 1000);
});
</script>

<style scoped lang="scss">
header {
  font-family: 'Arial', sans-serif;
  width: 100%;
  background-color: var(--header-bg);
  color: var(--header-text);
  transition: background-color 0.3s, color 0.3s;
}

/* --- TOP BAR --- */
.top-bar {
  display: flex;
  justify-content: space-between;
  align-items: flex-start;
  padding: 15px 40px;
  max-width: 1280px;
  margin: 0 auto;
}

.weather-widget {
  text-align: left;
  font-family: 'Arial', sans-serif;
  color: var(--header-text);
}

.weather-row-1 {
  display: flex;
  align-items: center;
  gap: 10px;
  margin-bottom: 2px;
}

.weather-widget .city {
  font-size: 16px;
  font-weight: normal; /* Görselde ince görünüyor */
  text-transform: uppercase;
}

.weather-widget .temp-values {
  font-size: 18px;
  font-weight: 900; /* Görselde kalın */
}

.weather-widget .weather-desc {
  font-size: 13px;
  font-style: italic;
  opacity: 0.9;
}

.logo-area {
  text-align: center;
  display: flex;
  flex-direction: column;
  align-items: center;
}

.motto {
  font-size: 10px;
  font-weight: bold;
  letter-spacing: 1px;
  margin-bottom: 5px;
  color: var(--header-text);
  opacity: 0.9;
}

.main-logo {
  height: auto;
  display: block;
}

.date-hijri {
  font-size: 11px;
  color: var(--header-text);
  opacity: 0.7;
  margin-top: 5px;
}

.right-info {
  text-align: right;
  font-size: 12px;
}

.mode-toggle {
  background: #000;
  color: #fff;
  padding: 4px 10px;
  border-radius: 20px;
  display: inline-flex;
  align-items: center;
  gap: 5px;
  font-size: 11px;
  margin-bottom: 5px;
  cursor: pointer;
  user-select: none;
}

/* Dark mode'da buton rengini tersine çevir */
:global(body.dark-mode) .mode-toggle {
  background: #fff;
  color: #000;
}

.location-time {
  font-weight: bold;
  font-size: 14px;
  margin-bottom: 2px;
}

.prayer-time {
  font-size: 11px;
  color: var(--header-text);
  opacity: 0.7;
}

/* --- NAV BAR --- */
.main-nav {
  border-top: 1px solid var(--border-color);
  border-bottom: 1px solid var(--border-color);
  width: 100%;
  height: 50px;
}

.nav-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100%;
}

.nav-links {
  display: flex;
  list-style: none;
  padding: 0;
  margin: 0;
  flex: 1;
  justify-content: space-between; /* Eşit dağılım */
  margin-right: 40px;
}

.nav-links li {
  font-weight: 900; /* Bold */
  font-size: 15px;
  color: var(--header-text);
  cursor: pointer;
  letter-spacing: -0.3px;
  white-space: nowrap;
}

.nav-links li:hover, .nav-links li.active {
  color: #d40000;
}

.hamburger-menu {
  position: absolute;
  right: 40px;
  font-size: 20px;
  cursor: pointer;
}

/* --- BLACK SUB BAR --- */
.sub-bar {
  background-color: #000;
  color: #fff;
  height: 40px;
  font-size: 12px;
  width: 100%;
}

.sub-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 40px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  height: 100%;
}

.market-data {
  display: flex;
  gap: 20px;
}

.market-item {
  color: #ccc;
}

.market-item .value {
  color: #fff;
  font-weight: bold;
  margin-left: 5px;
}

.sub-links {
  display: flex;
  align-items: center;
  gap: 20px;
}

.sub-links a {
  color: #fff;
  text-decoration: none;
  display: flex;
  align-items: center;
  gap: 5px;
  font-weight: bold;
}

.social-icons {
  display: flex;
  gap: 10px;
}

.soc {
  background: #333;
  width: 20px;
  height: 20px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  font-size: 10px;
  cursor: pointer;
}

/* --- BREAKING NEWS BAR --- */
.breaking-news-bar {
  background-color: #d40000;
  color: #fff;
  height: 40px;
  overflow: hidden;
  width: 100%;
  position: relative;
}

.bn-container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 40px;
  display: flex;
  align-items: center;
  height: 100%;
  position: relative;
}

.bn-label {
  font-weight: 900;
  font-size: 13px;
  margin-right: 20px;
  padding-right: 20px;
  white-space: nowrap;
  line-height: 1.2;
  text-align: center;
  min-width: 60px;
  border-right: 2px solid rgba(255, 255, 255, 0.3);
}

.bn-swiper {
  flex: 1;
  height: 100%;
}

.bn-slide {
  width: auto !important;
  max-width: 600px;
}

.bn-item {
  font-size: 14px;
  font-weight: bold;
  white-space: nowrap;
  overflow: hidden;
  text-overflow: ellipsis;
  display: flex;
  align-items: center;
  height: 100%;
}

.time-tag {
  background: #ffeb3b;
  color: #000;
  padding: 3px 8px;
  border-radius: 3px;
  font-size: 11px;
  margin-right: 10px;
  font-weight: 900;
  flex-shrink: 0;
}

.bn-arrows {
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 100%;
  pointer-events: none;
  z-index: 10;
  opacity: 0;
  transition: opacity 0.3s;
}

.breaking-news-bar:hover .bn-arrows {
  opacity: 1;
}

.bn-prev,
.bn-next {
  position: absolute;
  top: 50%;
  transform: translateY(-50%);
  width: 35px;
  height: 35px;
  background: rgba(0, 0, 0, 0.5);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  font-size: 24px;
  font-weight: bold;
  transition: background 0.2s;
  user-select: none;
  pointer-events: all;
}

.bn-prev {
  left: 10px;
}

.bn-next {
  right: 10px;
}

.bn-prev:hover,
.bn-next:hover {
  background: rgba(0, 0, 0, 0.7);
}

.bn-prev.swiper-button-disabled,
.bn-next.swiper-button-disabled {
  opacity: 0.3;
  cursor: not-allowed;
}

/* Responsive Design - Mobile First Approach */

/* Tablet (768px - 1024px) */
@media (max-width: 1024px) {
  .top-bar,
  .nav-container,
  .sub-container,
  .bn-container {
    max-width: 100%;
    padding: 0 20px;
  }

  .nav-links li {
    font-size: 13px;
  }
}

/* Mobile (< 768px) */
@media (max-width: 768px) {
  header {
    position: relative;
  }

  /* === TOP BAR === */
  .top-bar {
    flex-direction: column;
    height: auto;
    padding: 12px 16px;
    align-items: center;
    gap: 12px;
    position: relative;
  }

  /* Weather - Compact */
  .weather-widget {
    order: 1;
    width: 100%;
    text-align: left;
    padding: 8px 12px;
    background: rgba(0, 0, 0, 0.03);
    border-radius: 8px;

    .weather-row-1 {
      justify-content: flex-start;
      gap: 8px;
    }

    .city {
      font-size: 13px;
    }

    .temp-values {
      font-size: 15px;
    }

    .weather-desc {
      font-size: 11px;
      margin-top: 2px;
    }
  }

  /* Logo - Centered */
  .logo-area {
    order: 2;
    width: 100%;
    display: flex;
    flex-direction: column;
    align-items: center;
    gap: 8px;
  }

  .logo-link {
    display: block;
  }

  .main-logo {
    width: 140px !important;
    height: auto;
  }

  .date-hijri {
    font-size: 10px;
    text-align: center;
    opacity: 0.8;
  }

  /* Time - Top Right */
  .time-date {
    order: 3;
    position: absolute;
    top: 12px;
    right: 16px;
    font-size: 11px;
    background: rgba(0, 0, 0, 0.05);
    padding: 4px 8px;
    border-radius: 4px;
  }

  /* Dark Mode Toggle - Floating */
  .mode-toggle {
    position: fixed;
    bottom: 20px;
    right: 20px;
    z-index: 1000;
    width: 50px;
    height: 50px;
    border-radius: 50%;
    background: var(--header-bg);
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.15);
    display: flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    transition: transform 0.2s;

    &:active {
      transform: scale(0.95);
    }
  }

  /* === NAVIGATION === */
  .main-nav {
    height: auto;
    min-height: 50px;
  }

  .nav-container {
    padding: 12px 16px;
    justify-content: center;
  }

  .nav-links {
    display: none;
  }

  .hamburger-menu {
    display: flex !important;
    justify-content: center;
    align-items: center;
    width: 100%;
    font-size: 22px;
    cursor: pointer;
    padding: 8px;
    
    span {
      transition: transform 0.2s;
    }

    &:active span {
      transform: scale(0.9);
    }
  }

  /* === SUB BAR === */
  .sub-bar {
    height: auto;
  }

  .sub-container {
    flex-direction: column;
    padding: 12px 16px;
    gap: 12px;
  }

  /* Market Data - Horizontal Scroll */
  .market-data {
    width: 100%;
    justify-content: flex-start;
    gap: 16px;
    overflow-x: auto;
    -webkit-overflow-scrolling: touch;
    scrollbar-width: none;
    
    &::-webkit-scrollbar {
      display: none;
    }
  }

  .market-item {
    font-size: 11px;
    white-space: nowrap;
    flex-shrink: 0;
  }

  /* Sub Links - Simplified */
  .sub-links {
    width: 100%;
    flex-wrap: wrap;
    justify-content: center;
    gap: 8px;
    
    a {
      font-size: 10px;
      padding: 6px 10px;
      background: rgba(255, 255, 255, 0.1);
      border-radius: 4px;
      white-space: nowrap;
    }
  }

  .social-icons {
    display: flex;
    gap: 8px;
    margin-top: 4px;
  }

  .search-icon {
    display: none;
  }

  /* === BREAKING NEWS === */
  .breaking-news-bar {
    height: auto;
    min-height: 50px;
  }

  .bn-container {
    padding: 12px 16px;
    gap: 12px;
  }

  .bn-label {
    font-size: 9px;
    min-width: 40px;
    margin-right: 12px;
    padding-right: 12px;
    line-height: 1.1;
  }

  .bn-swiper {
    flex: 1;
  }

  .bn-slide {
    max-width: 100%;
  }

  .bn-item {
    font-size: 11px;
    white-space: normal;
    line-height: 1.5;
    overflow: visible;
    text-overflow: clip;
  }

  .time-tag {
    font-size: 9px;
    padding: 3px 6px;
    flex-shrink: 0;
  }

  .bn-arrows {
    display: none;
  }
}

/* Small Mobile (< 480px) */
@media (max-width: 480px) {
  .top-bar {
    padding: 10px 12px;
  }

  .weather-widget {
    .city {
      font-size: 12px;
    }

    .temp-values {
      font-size: 14px;
    }

    .weather-desc {
      font-size: 10px;
    }
  }

  .main-logo {
    width: 120px !important;
  }

  .date-hijri {
    font-size: 9px;
  }

  .time-date {
    font-size: 10px;
    padding: 3px 6px;
  }

  .market-item {
    font-size: 10px;
  }

  .sub-links a {
    font-size: 9px;
    padding: 5px 8px;
  }

  .bn-label {
    font-size: 8px;
    min-width: 35px;
  }

  .bn-item {
    font-size: 10px;
  }

  .mode-toggle {
    width: 45px;
    height: 45px;
    bottom: 16px;
    right: 16px;
  }
}

/* Dark Mode Mobile Adjustments */
@media (max-width: 768px) {
  :global(body.dark-mode) {
    .weather-widget {
      background: rgba(255, 255, 255, 0.05);
    }

    .time-date {
      background: rgba(255, 255, 255, 0.05);
    }

    .sub-links a {
      background: rgba(255, 255, 255, 0.05);
    }
  }
}
</style>
