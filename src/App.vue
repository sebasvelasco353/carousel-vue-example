<template>
  <div id="app">
    <div class="carousel-container">
      <Carousel
        :controlEnabled="true"
        class="carousel"
        v-slot="{ currentSlide }"
      >
        <Slide v-for="(slide, index) in carouselSlides" :key="index">
          <div v-show="currentSlide === index + 1" class="slide-info">
            hello in slide {{index + 1}}
          </div>
        </Slide>
      </Carousel>
    </div>
  </div>
</template>

<script>
import Carousel from './components/Carousel.vue';
import Slide from './components/Slide.vue';

export default {
  name: 'App',
  data() {
    return {
      carouselSlides: [1, 2, 3, 4],
    };
  },
  components: {
    Carousel,
    Slide,
  },
};
</script>

<style lang="scss">
.carousel-container {
  width: 50vw;
  height: 50vh;
  border: 1px solid red;
  position: absolute;
  top: 25vh;
  left: 25vw;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
