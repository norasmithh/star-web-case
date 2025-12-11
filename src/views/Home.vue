<template>
  <div class="headline-slider">
    <!-- BÜYÜK MANŞET -->
    <div
      class="headline-image"
      :style="{ backgroundImage: `url(${mainSlide.image})` }"
    >
      <div class="headline-overlay"></div>

      <div class="headline-text">
        {{ mainSlide.title }}
      </div>
    </div>

    <!-- ALTTAKİ HABER SWIPER -->
    <swiper :slides-per-view="4" :space-between="10" class="thumb-swiper">
      <swiper-slide
        v-for="(slide, index) in slides"
        :key="index"
        @mouseenter="setMainSlide(slide, index)"
        :class="{ activeThumb: activeIndex === index }"
      >
        <div class="thumb-card">
          <img :src="slide.image" />
          <div class="thumb-title">{{ truncate(slide.title, 30) }}</div>
        </div>
      </swiper-slide>
    </swiper>
  </div>
</template>

<script>
import { Swiper, SwiperSlide } from "swiper/vue";
import "swiper/css";
import endonezya from "../assets/endonezya-ile-anlasma-kap-669.webp";
import takeoff from "../assets/bakan-kacir-take-off-ista-573.webp";
import hayal from "../assets/30-yillik-hayal-gercege-d-899.webp";
import erdogan from "../assets/cumhurbaskani-erdogan-ter-823.webp";

export default {
  components: { Swiper, SwiperSlide },

  data() {
    return {
      activeIndex: 0,
      mainSlide: {
        image: endonezya,
        title:
          "Endonezya ile anlaşma kapıyı araladı! Bölge orduları Türkiye'den KAAN'i istiyor",
      },

      slides: [
        {
          image: endonezya,
          title: "Endonezya ile anlaşma kapıyı araladı",
        },
        {
          image: takeoff,
          title: "Bakan Kacır, Take Off İstanbul'da",
        },
        {
          image: hayal,
          title: "30 yıllık hayal gerçeğe dönüşüyor",
        },
        {
          image: erdogan,
          title: "Cumhurbaşkanı Erdoğan: Terörsüz Bölge",
        },
      ],
    };
  },

  methods: {
    setMainSlide(slide, index) {
      this.mainSlide = slide;
      this.activeIndex = index;
    },

    truncate(text, length) {
      return text.length > length ? text.substring(0, length) + "..." : text;
    },
  },
};
</script>

<style scoped>
.headline-slider {
  width: 100%;
  max-width: 1280px;
  margin: 24px auto 0;
  padding: 0 40px;
  position: relative;
}

/* --- BÜYÜK MANŞET --- */
.headline-image {
  width: 100%;
  height: 520px;
  background-size: cover;
  background-position: center;
  position: relative;
}

.headline-overlay {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.45);
}

.headline-text {
  position: absolute;
  bottom: 40px;
  left: 40px;
  font-size: 44px;
  font-weight: 800;
  color: #fff;
  max-width: 850px;
  line-height: 1.2;
}

/* --- ALT HABER SLIDER --- */
.thumb-swiper {
  width: 100%;
  background: #000;
  padding: 0;
}

/* Swiper içindeki elemanlar için scoped nedeniyle :deep kullanıyoruz */
:deep(.swiper-slide) {
  display: flex;
  justify-content: center;
  align-items: center;
}

.thumb-card {
  width: 100%;
  color: white;
  cursor: pointer;
  display: flex;
  text-align: center;
}

.thumb-card img {
  width: 80px;
  height: 80px;
  border-radius: 50%;
  object-fit: cover;
}

.thumb-title {
  margin-top: 5px;
  font-size: 16px;
  max-width: 150px;
  margin-left: auto;
  margin-right: auto;
}

:deep(.activeThumb) {
  border-bottom: 3px solid #d40000;
}
</style>
