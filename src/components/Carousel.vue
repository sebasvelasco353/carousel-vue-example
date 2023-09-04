<template>
  <div class="carousel">
    <slot :currentSlide="currentSlide" />

    <div v-if="controlEnabled" class="carousel-controls">
       <div class="toggle-page left">
         <i @click="prevSlide" class="fas fa-chevron-left"></i>
       </div>
       <div class="pagination">
         <span
           @click="goToSlide(index)"
           v-for="(slide, index) in slideCount"
           :key="index"
           :class="{ active: index + 1 === currentSlide }"
         >
         </span>
       </div>
       <div class="toggle-page right">
         <i @click="nextSlide" class="fas fa-chevron-right"></i>
       </div>
    </div>

  </div>
</template>

<script>
export default {
  name: 'CarouselComponent',
  props: {
    controlEnabled: {
      type: Boolean,
      default: true,
    },
  },
  data() {
    return {
      currentSlide: 1,
      slideCount: null,
    };
  },
  methods: {
    goToSlide(index) {
      this.currentSlide = index + 1;
    },
    nextSlide() {
      if (this.currentSlide === this.slideCount) {
        this.currentSlide = 1;
        return;
      }
      this.currentSlide += 1;
    },
    prevSlide() {
      if (this.currentSlide === 1) {
        this.currentSlide = this.slideCount;
        return;
      }
      this.currentSlide -= 1;
    },
  },
  mounted() {
    this.slideCount = document.querySelectorAll('.slide').length;
  },
};
</script>

<style lang="scss">
.carousel {
  width: 100%;
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
}
.carousel-controls {
  padding: 0 16px;
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;

  .toggle-page {
    display: flex;
    flex: 1;
  }

  .right {
    justify-content: flex-end;
  }

  i {
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 50%;
    width: 40px;
    height: 40px;
    background-color: red;
    color: #fff;
  }
}

.pagination {
  width: 100%;
  display: flex;
  gap: 16px;
  justify-content: center;
  align-items: center;

  span {
    cursor: pointer;
    width: 20px;
    height: 20px;
    border-radius: 50%;
    background-color: #fff;
    box-shadow: 0 1px 3px 0 rgba(0, 0, 0, 0.1), 0 1px 2px 0 rgba(0, 0, 0, 0.06);
  }

  .active {
    background-color: red;
  }
}
</style>
