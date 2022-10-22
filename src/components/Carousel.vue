<template>
  <div class="carousel">
    <div
      class="carousel__wrapper"
      :style="{ 'margin-left': '-' + currentSlideIdx * 100 + '%' }"
    >
      <CarouselItem
        v-for="item in pictureLists"
        :key="item.id"
        :itemData="item"
      ></CarouselItem>
    </div>
    <div class="carousel__nav">
      <button class="carousel__btn" v-on:click="prevSlide">prevent</button>
      <button class="carousel__btn" v-on:click="nextSlide">next</button>
    </div>
  </div>
</template>

<script>
import CarouselItem from './CarouselItem.vue';

export default {
  components: {
    CarouselItem,
  },
  props: {
    pictureLists: {
      type: Array,
      default: () => [],
    },
  },
  methods: {
    prevSlide() {
      if (this.currentSlideIdx <= 0) {
        this.currentSlideIdx = this.pictureLists.length - 1;
      } else {
        this.currentSlideIdx--;
      }
    },
    nextSlide() {
      if (this.currentSlideIdx >= this.pictureLists.length - 1) {
        this.currentSlideIdx = 0;
      } else {
        this.currentSlideIdx++;
      }
    },
  },
  data() {
    return {
      currentSlideIdx: 0,
    };
  },
};
</script>

<style lang="scss">
.carousel {
  margin-top: 20px;
  overflow: hidden;
  &__wrapper {
    display: flex;
    width: 448px;
    height: 258px;
    transition: all ease 0.7s;
  }
  &__nav {
    display: flex;
    justify-content: center;
    & button {
      margin: 24px 20px 6px;
      border-radius: 6px;
      color: #f4f6f9;
      background-color: rgba(119, 103, 99, 1);
      border: 1px solid rgba(119, 103, 99, 1);
      box-shadow: 0px 2px 6px 0px rgba(119, 103, 99, 1);
    }
    & button:active {
      box-shadow: 0px 0px 6px 0px #921f1f;
    }
  }
  &__btn {
    margin: 8px;
    width: 60px;
    height: 30px;
    background: rgb(83, 21, 6);
  }
}
</style>
