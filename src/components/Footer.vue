<template>
  <div class="footer-main">
    <div class="container">
      <div class="wrapper">
        <div class="footer-top">
          <div class="row">
            <!-- Logo Column -->
            <div class="col-2">
              <a class="logo-link" href="/">
                <img src="../assets/starlogo2025.png" style="width: 155px;" alt="Star Logo">
              </a>
              <ul class="link-list">
                <li><a href="#">Son Dakika</a></li>
                <li><a href="#">Yazarlar</a></li>
                <li><a href="#">Namaz Vakitleri</a></li>
                <li><a href="#">Hava Durumu</a></li>
              </ul>
            </div>

            <!-- Haberler Column -->
            <div class="col-2">
              <ul class="link-list">
                <li class="title"><a href="#">HABERLER</a></li>
                <li><a href="#">Güncel Haberler</a></li>
                <li><a href="#">Dünya</a></li>
                <li><a href="#">Politika</a></li>
                <li><a href="#">Ekonomi</a></li>
                <li><a href="#">Spor</a></li>
                <li><a href="#">Eğitim</a></li>
                <li><a href="#">Bilim - Teknoloji</a></li>
                <li><a href="#">Memur</a></li>
                <li><a href="#">Medya</a></li>
                <li><a href="#">Otomobil</a></li>
              </ul>
            </div>

            <!-- Ekonomi & Bölgeler Column -->
            <div class="col-2">
              <ul class="link-list mb-lg">
                <li class="title"><a href="#">EKONOMİ</a></li>
                <li><a href="#">Şirket - Kobi</a></li>
                <li><a href="#">Emlak</a></li>
                <li><a href="#">Turizm</a></li>
              </ul>
              <ul class="link-list">
                <li class="title"><a href="#">BÖLGELER</a></li>
                <li><a href="#">Ankara</a></li>
                <li><a href="#">Ege</a></li>
              </ul>
            </div>

            <!-- Kültür Sanat & Yaşam Column -->
            <div class="col-2">
              <ul class="link-list mb-lg">
                <li class="title">KÜLTÜR SANAT</li>
                <li><a href="#">Necip Fazıl Ödülleri</a></li>
                <li><a href="#">Sanat</a></li>
              </ul>
              <ul class="link-list">
                <li class="title"><a href="#">YAŞAM</a></li>
                <li><a href="#">Sağlık</a></li>
                <li><a href="#">Kadın</a></li>
                <li><a href="#">Dizi</a></li>
              </ul>
            </div>

            <!-- Popüler Column -->
            <div class="col-2">
              <ul class="link-list">
                <li class="title">POPÜLER</li>
                <li><a href="#">FETÖ darbe girişimi</a></li>
                <li><a href="#">YKS Sınavı</a></li>
                <li><a href="#">MYS Ve LGS Sınavı</a></li>
                <li><a href="#">MEB Giriş</a></li>
                <li><a href="#">AÖF Kayıt</a></li>
                <li><a href="#">E-Devlet Giriş</a></li>
                <li><a href="#">E-Okul Giriş</a></li>
                <li><a href="#">SGK sorgulama</a></li>
                <li><a href="#">ÖSYM</a></li>
                <li><a href="#">KPSS</a></li>
                <li><a href="#">Milli Piyango Bilet Sorgulama</a></li>
              </ul>
            </div>

            <!-- Ekler & Apps Column -->
            <div class="col-2">
              <ul class="link-list mb-lg">
                <li class="title">EKLER</li>
                <li><a href="#">Açık Görüş</a></li>
                <li><a href="#">Star Kitap</a></li>
                <li><a href="#">Cumartesi Eki</a></li>
              </ul>
              
              <div class="app-links">
                <a href="https://itunes.apple.com/tr/app/star-gazetesi/id563927022?l=tr&mt=8" class="app-btn app-store">App Store</a>
                <a href="https://play.google.com/store/apps/details?id=com.star.android" class="app-btn google-play">Google Play</a>
                <a href="https://appgallery.huawei.com/app/C109246175" class="app-btn huawei">Huawei AppGallery</a>
              </div>
            </div>
          </div>
        </div>

        <div class="footer-bottom">
          <ul class="footer-menu">
            <li><a href="#">© 2025 Star.com.tr</a></li>
            <li><a href="#">İletişim Ve Künye</a></li>
            <li><a href="#">Reklam</a></li>
            <li><a href="#">Bilgi Toplum Hizmetleri</a></li>
            <li><a href="#">Çerez Politikası</a></li>
            <li><a href="#">Gizlilik Politikası</a></li>
            <li><a href="#">RSS</a></li>
          </ul>
          
          <div class="info-text">
            Sitemizde yayınlanan haberlerin telif hakları gazete ve haber kaynaklarına aittir. İzin alınmadan, kaynak gösterilerek dahi iktibas edilemez.
          </div>

          <ul class="social-footer">
            <li><a href="https://sosyal.teknofest.app/@stargazete" target="_blank" class="soc-icon">N</a></li>
            <li><a href="https://www.facebook.com/stargazete" class="soc-icon">f</a></li>
            <li><a href="https://twitter.com/stargazete" class="soc-icon">X</a></li>
            <li><a href="https://www.instagram.com/stargazete/" class="soc-icon">in</a></li>
            <li><a href="https://www.youtube.com/channel/UCv4lXYH3XXLUHl54aykON0A?sub_confirmation=1" class="soc-icon">yt</a></li>
          </ul>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="scss">
.footer-main {
  background-color: #fff;
  border-top: 1px solid #444;
  padding: 40px 0 20px;
  font-family: 'Arial', sans-serif;
  font-size: 12px;
  color: #333;
  margin-top: 40px;
}

.container {
  max-width: 1280px;
  margin: 0 auto;
  padding: 0 40px;
}

.row {
  display: flex;
  flex-wrap: wrap;
  margin: 0 -15px;
}

.col-2 {
  width: 16.666%; /* 100% / 6 columns */
  padding: 0 15px;
  box-sizing: border-box;
}

.logo-link {
  display: block;
  margin-bottom: 20px;
}

.link-list {
  list-style: none;
  padding: 0;
  margin: 0;
  line-height: 2;
}

.link-list li a {
  color: #333;
  text-decoration: none;
  transition: color 0.2s;
  font-size: 12px;
}

.link-list li a:hover {
  color: #d40000;
}

.link-list .title {
  font-size: 15px;
  font-weight: 900;
  margin-bottom: 15px;
  padding-bottom: 10px;
  text-transform: uppercase;
  color: #000;
  border-bottom: 2px solid #d40000;
}

.link-list .title a {
  color: #000;
  font-weight: 900;
}

.mb-lg {
  margin-bottom: 30px;
}

/* App Links */
.app-links {
  display: flex;
  flex-direction: column;
  gap: 10px;
  margin-top: 10px;
}

.app-btn {
  display: block;
  background: #000;
  color: #fff;
  padding: 10px 15px;
  border-radius: 5px;
  text-align: center;
  text-decoration: none;
  font-weight: bold;
  font-size: 11px;
  transition: background 0.2s;
}

.app-btn:hover {
  background: #d40000;
}

/* Footer Bottom */
.footer-bottom {
  margin-top: 40px;
  border-top: 1px solid #eee;
  padding-top: 20px;
  text-align: center;
}

.footer-menu {
  display: flex;
  justify-content: center;
  gap: 15px;
  list-style: none;
  padding: 0;
  margin-bottom: 20px;
  flex-wrap: wrap;
}

.footer-menu li a {
  color: #333;
  text-decoration: none;
  font-weight: 500;
  font-size: 12px;
  padding: 5px 10px;
  display: block;
}

.footer-menu li a:hover {
  color: #d40000;
}

.info-text {
  color: #666;
  margin-bottom: 20px;
  font-size: 11px;
  line-height: 1.6;
  max-width: 800px;
  margin-left: auto;
  margin-right: auto;
}

.social-footer {
  display: flex;
  justify-content: center;
  gap: 15px;
  list-style: none;
  padding: 0;
  margin-bottom: 20px;
}

.soc-icon {
  width: 35px;
  height: 35px;
  background: #000;
  color: #fff;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  text-decoration: none;
  font-weight: bold;
  font-size: 14px;
  transition: background 0.2s;
}

.soc-icon:hover {
  background: #d40000;
}

/* Dark Mode Support */
body.dark-mode .footer-main,
:global(body.dark-mode) .footer-main {
  background-color: #242424 !important;
  border-top-color: #444 !important;
  color: #ffffff !important;
}

body.dark-mode .link-list li a,
:global(body.dark-mode) .link-list li a {
  color: #ffffff !important;
}

body.dark-mode .link-list .title,
:global(body.dark-mode) .link-list .title {
  color: #ffffff !important;
}

body.dark-mode .link-list .title a,
:global(body.dark-mode) .link-list .title a {
  color: #ffffff !important;
}

body.dark-mode .footer-menu li a,
:global(body.dark-mode) .footer-menu li a {
  color: #ffffff !important;
}

body.dark-mode .link-list li a:hover,
body.dark-mode .footer-menu li a:hover,
:global(body.dark-mode) .link-list li a:hover,
:global(body.dark-mode) .footer-menu li a:hover {
  color: #d40000 !important;
}

body.dark-mode .info-text,
:global(body.dark-mode) .info-text {
  color: #aaa !important;
}

body.dark-mode .footer-bottom,
:global(body.dark-mode) .footer-bottom {
  border-top-color: #444 !important;
}

body.dark-mode .app-btn,
:global(body.dark-mode) .app-btn {
  background: #fff !important;
  color: #000 !important;
}

body.dark-mode .soc-icon,
:global(body.dark-mode) .soc-icon {
  background: #fff !important;
  color: #000 !important;
}

/* Responsive */
@media (max-width: 768px) {
  .col-2 {
    width: 50%;
    margin-bottom: 30px;
  }
}

@media (max-width: 480px) {
  .col-2 {
    width: 100%;
  }
}
</style>
