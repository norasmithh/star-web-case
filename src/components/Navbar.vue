<template>
  <nav class="navbar">
    <div class="navbar-top">
      <div class="left">
        <span class="city">İSTANBUL</span>
        <span class="temp">13°C / 8°C</span>
        <span class="desc">Parçalı bulutlu, güneşli</span>
      </div>
       <div class="center logo-wrapper">
        <img src="../assets/star.png" alt="Star Logo" class="logo">
      </div>
      <div class="right">
        <span class="imsak">İstanbul 10:14:24</span>
        <span class="imsak-desc">İmsak kalanı süre</span>
      </div>
    </div>

    <div class="navbar-middle">
      <ul class="menu">
        <li>SON DAKİKA</li>
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

      <div class="icons">
        <!-- MENÜ, SOCIAL ICONS VE ARAMA İKONU BURAYA EKLENECEK -->
        <slot name="icons"></slot>
      </div>
    </div>

    <div class="navbar-bottom">
      <div class="currency">
        <span>DOLAR <strong>42,6141</strong></span>
        <span>EURO <strong>49,6927</strong></span>
        <span>ALTIN <strong>5756.16</strong></span>
      </div>
      <div class="media-links">
        <span><slot name="foto-icon"></slot> FOTO GALERİ</span>
        <span><slot name="video-icon"></slot> VİDEO GALERİ</span>
        <span><slot name="live-icon"></slot> CANLI YAYIN</span>
      </div>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  width: 100%;
  background: #fff;
  border-bottom: 1px solid #ddd;
  font-family: Arial, sans-serif;
}

.navbar-top,
.navbar-middle,
.navbar-bottom {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
}

.navbar-top .left span,
.navbar-top .right span {
  margin-right: 10px;
  font-size: 14px;
  color: #333;
}
.logo-wrapper {
  display: flex;
  justify-content: center;
  align-items: center;
}

.logo {
  height: 75px;
  width: auto;
}
.menu {
  display: flex;
  gap: 20px;
  list-style: none;
  padding: 0;
  margin: 0;
  font-weight: bold;
}

.menu li {
  cursor: pointer;
  font-size: 15px;
  transition: 0.2s;
}

.menu li:hover {
  color: #d40000;
}

.icons {
  display: flex;
  gap: 15px;
}

.navbar-bottom {
  background: #000;
  color: #fff;
  font-size: 14px;
}

.currency span {
  margin-right: 20px;
}

.media-links span {
  margin-left: 20px;
  cursor: pointer;
}
</style>
