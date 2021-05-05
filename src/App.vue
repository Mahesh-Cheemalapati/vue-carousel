<template>
  <div id="app" class="wrapper">
    <div class="box">
      <h3>Image Carousel Gallery 1</h3>
      <p>You can click on slides to navigate</p>
      <carousel :clickable="true" :autoplay="true">
        <slider v-for="(slide, i) in slides" :index="i" :key="i">
          <img :src="slide.source" />
        </slider>
      </carousel>
    </div>
    <!-- ----------------------------------------------------------------------------------------------------- -->
    <div class="box">
      <h3>Image Carousel Gallery 2</h3>

      <carousel
        :controls-visible="true"
        :autoplay="true"
        :controls-prev-html="'&#10092;'"
        :controls-next-html="'&#10093;'"
        :controls-width="30"
        :controls-height="60"
      >
        <slider v-for="(slide, i) in slides2" :index="i" :key="i">
          <img :src="slide.source" />
        </slider>
      </carousel>
    </div>
    <!-- ----------------------------------------------------------------------------------------------------- -->
    <div class="box">
      <h3>Image Carousel Gallery 3</h3>
      <carousel
        :regularView="true"
        :autoplay="true"
        :space="370"
        :clickable="true"
        :controls-visible="true"
      >
        <slider v-for="(slide, i) in slides3" :index="i" :key="i">
          <img :src="slide.source" />
        </slider>
      </carousel>
    </div>
    <!-- ----------------------------------------------------------------------------------------------------- -->
  </div>
</template>

<script>
import Carousel from "../src/components/Carousel";
import Slider from "../src/components/Slider";
import gallery from "./data/gallery";

function getGallery(title) {
  return gallery.find((el) => el.title === title).images;
}

export default {
  name: "App",
  components: {
    Carousel,
    Slider,
  },
  data() {
    return {
      slides: getGallery("Gallery 1"),
      slides2: getGallery("Gallery 2"),
      slides3: getGallery("Gallery 3"),
      slideCount: gallery.length,
    };
  },
  methods: {
    addSlide() {
      this.slideCount++;
    },
    removeSlide() {
      if (this.slideCount > 1) {
        this.slideCount--;
      }
    },
    getGallery,
  },
};
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #4f82b6;
  margin-top: 60px;
}
</style>