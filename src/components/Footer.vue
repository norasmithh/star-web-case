<template>
  <footer class="footer">
    <!-- ÜST LİNKLER -->
    <div class="footer-links">
      <a href="#">© 2025 Star.com.tr</a>
      <a href="#">İletişim Ve Künye</a>
      <a href="#">Reklam</a>
      <a href="#">Bilgi Toplum Hizmetleri</a>
      <a href="#">Çerez Politikası</a>
      <a href="#">Gizlilik Politikası</a>
      <a href="#">RSS</a>
    </div>

    <!-- AÇIKLAMA METNİ -->
    <div class="footer-text">
      Sitemizde yayınlanan haberlerin telif hakları gazete ve haber kaynaklarına
      aittir. İzin alınmadan, kaynak gösterilerek dahi iktibas edilemez.
    </div>

    <!-- SOSYAL MEDYA İKONLARI -->
    <div class="footer-social">
      <div class="icon">N</div>
      <div class="icon">f</div>
      <div class="icon">X</div>
      <div class="icon">i</div>
      <div class="icon">▶</div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  width: 100%;
  text-align: center;
  padding: 40px 20px;
  font-family: Arial, sans-serif;
}

/* ÜSTTEKİ LİNK SATIRI */
.footer-links {
  display: flex;
  justify-content: center;
  gap: 30px;
  flex-wrap: wrap;
  margin-bottom: 15px;
}

.footer-links a {
  text-decoration: none;
  color: #000;
  font-size: 15px;
  font-weight: 500;
}

.footer-links a:hover {
  text-decoration: underline;
}

/* AÇIKLAMA YAZISI */
.footer-text {
  font-size: 15px;
  color: #333;
  margin-bottom: 25px;
  max-width: 900px;
  line-height: 1.5;
  margin-left: auto;
  margin-right: auto;
}

/* SOSYAL MEDYA İKONLARI */
.footer-social {
  display: flex;
  justify-content: center;
  gap: 25px;
  margin-top: 10px;
}

/* Yuvarlak ikonlar */
.icon {
  width: 42px;
  height: 42px;
  background: #000;
  color: #fff;
  border-radius: 50%;
  display: flex;
  justify-content: center;
  align-items: center;
  font-weight: 700;
  font-size: 18px;
  cursor: pointer;
  transition: 0.2s;
}

.icon:hover {
  background: #d40000;
}
</style>
