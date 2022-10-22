<template>
  <div></div>
  <div class="popup">
    <div class="popup__wrapper">
      <div class="popup__header">
        <div>
          <h3 class="popup__name">{{ lot.picAuth }}</h3>
          <p class="popup__name">{{ lot.picName }}</p>
        </div>
        <p>Цена: {{ lot.trueCost }} $</p>
        <button class="popup__btn-close" @click="closePopup">X</button>
      </div>
      <div class="popup__content">
        <div class="popup__description">
          Lorem ipsum dolor sit amet consectetur adipisicing elit. Quos modi
          error cupiditate alias velit perferendis obcaecati totam voluptas
          quas, iste, laboriosam molestias. Assumenda delectus exercitationem
          harum facilis, voluptate maxime ad.
        </div>
        <div class="popup__slider">
          <slot></slot>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['lot'],
  data() {
    return {};
  },
  methods: {
    closePopup() {
      this.$emit('closePopup');
    },
  },
};
</script>

<style lang="scss">
.popup {
  position: absolute;
  padding: 16px;
  width: 100%;
  max-width: 1600px;
  max-height: 900px;
  bottom: -10%;
  top: -10%;
  // left: 5%;
  // right: 5%;
  // height: inherit;
  background: #9f9f9f;
  z-index: 9;
  box-shadow: 10px 10px 140px 10px;
  overflow: hidden;

  &__wrapper {
    margin: 0 auto;
    border-radius: 6px;
    padding: 16px;
    width: 100%;
    z-index: 3;
  }
  &__header {
    display: flex;
    justify-content: space-between;
  }
  &__content {
    width: 1216px;
  }
  &__description {
    height: 160px;
    width: 600px;
    padding: 24px;
    margin-top: 20px;
    color: #343030;
    background-color: #eceaea;
    border-radius: 36px 6px;
  }
  &__slider {
    display: flex;
    align-items: center;
    justify-content: space-around;
    background-color: inherit;
    margin: 0 auto;
  }
  &__btn-close {
    color: #343030;
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: #c1b4b1;
  }
}
</style>
