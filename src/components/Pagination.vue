<template>
  <div class="carousel-pagination carousel-pagination--bottom-overlay">
    <div class="carousel-dot-container" role="tablist">
      <button
        v-for="(page, index) in paginationCount"
        :key="`${page}_${index}`"
        class="carousel-dot"
        aria-hidden="false"
        role="tab"
        :aria-selected="isCurrentDot(index) ? 'true' : 'false'"
        v-bind:class="{ 'carousel-dot--active': isCurrentDot(index) }"
        v-on:click="goToPage(index)"
      ></button>
    </div>
  </div>
</template>

<script>
export default {
  name: "pagination",
  props: {
    carousel: {
      type: Object,
    },
    slides: {
      type: [],
      default: [],
    },
  },
  computed: {
    paginationPropertyBasedOnPosition() {
      return this.carousel.perspective.indexOf("top") >= 0 ? "bottom" : "top";
    },
    paginationCount() {
      return [1, 2, 3, 4, 5];
    },
  },
  methods: {
    /**
     * Change page by index
     * @param {number} index
     * return {void}
     */
    goToPage(index) {
      /**
       * @event paginationclick
       * @type {number}
       */
      this.$emit("paginationclick", index);
    },
    /**
     * Check on current dot
     * @param {number} index - dot index
     * @return {boolean}
     */
    isCurrentDot(index) {
      return index === this.carousel.currentIndex;
    },
  },
};
</script>

<style scoped>
.carousel-pagination {
  width: 100%;
  text-align: center;
  z-index: 999;
}
.carousel-pagination--bottom-overlay {
  position: absolute;
  bottom: 0;
}
.carousel-dot-container {
  display: inline-block;
  margin: 0 auto;
  padding: 0;
}
.carousel-dot {
  background-color: lightblue;
  height: 16px;
  width: 16px;
  margin: 0px 16px;
  display: inline-block;
  cursor: pointer;
  appearance: none;
  border: none;
  background-clip: content-box;
  box-sizing: content-box;
  padding: 0;
  border-radius: 100%;
  outline: none;
}
.carousel-dot--active {
  border: 2px solid orange;
}
</style>