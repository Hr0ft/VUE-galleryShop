<template>
  <div class="carousel__item">
    <img :src="itemData.pic" :alt="itemData.id" />
    <div class="carousel__img-shadow"></div>
  </div>
</template>

<script>
export default {
  props: {
    itemData: {
      type: Object,
      default: () => {},
    },
  },
  data() {
    return {};
  },
};
</script>

<style lang="scss">
.carousel__img-shadow {
  margin: 5%;
  width: 90%;
  height: 60px;
  top: 165px;
  // background: #000;
  position: absolute;
  box-shadow: 0 10px 24px 6px rgb(80, 28, 28);
  z-index: -1;
}
.carousel__item {
  position: relative;
  &__img-shadow {
  }
  & img {
    border: 2px solid #382e2b;
    width: 448px;
    // box-shadow: 10px 0 8px 2 rgb(80, 28, 28);
    z-index: 5;
  }
}
</style>
