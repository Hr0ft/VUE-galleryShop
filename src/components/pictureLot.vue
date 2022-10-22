<template>
  <Popup
    v-if="this.popupIsOpen"
    v-bind:lot="lot"
    @closePopup="this.closePicturePopup"
  >
    <Carousel :pictureLists="lot.slides"></Carousel>
  </Popup>

  <div
    class="picture-lot"
    v-bind:class="{ soldLot: lot.sold, hidden: !lot.inSearch }"
  >
    <div class="picture-lot__content" @click="showPicturePopup">
      <div class="picture-lot__img">
        <img :src="lot.picURL" v-bind:alt="`Image ` + lot.picName" />
      </div>
      <div class="picture-lot__info">
        <p class="picture-lot__name">{{ lot.picName }}</p>
        <p class="picture-lot__author">{{ lot.picAuth }}</p>
      </div>
    </div>
    <div v-if="lot.sold" class="picture-lot__sold">Продана на аукционе</div>
    <div v-else class="picture-lot__sale">
      <div class="picture-lot__cost">
        <div
          class="picture-lot__old-price"
          v-bind:class="{ hidden: !lot.sale }"
        >
          {{ lot.oldCost }} $
        </div>
        <div class="picture-lot__actual-price">{{ lot.trueCost }} $</div>
      </div>
      <button
        v-if="lotInBasket || this.lot.inBasket"
        class="picture-lot__basket-btn"
      >
        В корзине
      </button>
      <div v-else-if="loadTobasket" class="picture-lot__download">
        <div class="cssload-loader">
          <div class="cssload-top"></div>
          <div class="cssload-bottom"></div>
          <div class="cssload-line"></div>
        </div>
      </div>
      <button v-else class="picture-lot__buy-btn" @click="putToBasket">
        Купить
      </button>
    </div>
  </div>
</template>

<script>
import Popup from './Popup.vue';
import Carousel from './Carousel.vue';

export default {
  props: ['lot'],
  buildModules: ['vue-ssr-carousel/nuxt'],
  components: { Popup, Carousel },
  data() {
    return {
      lotData: this.lot,
      lotInBasket: this.lot.inBasket,
      loadTobasket: false,
      popupIsOpen: false,
    };
  },

  methods: {
    showPicturePopup() {
      this.popupIsOpen = true;
    },
    closePicturePopup() {
      this.popupIsOpen = false;
    },

    putToBasket() {
      this.loadTobasket = true;
      setTimeout(() => {
        this.lotInBasket = true;
        this.loadTobasket = false;
      }, 2000);

      let localBasket = JSON.parse(localStorage.getItem('pictInBasketID'));

      if (!localBasket) {
        localStorage.setItem('pictInBasketID', JSON.stringify([this.lot.id]));
      } else {
        let newBasket = [...localBasket];
        if (!localBasket.find((el) => el === this.lot.id)) {
          newBasket.push(this.lot.id);
        }
        localStorage.setItem('pictInBasketID', JSON.stringify(newBasket));
      }
    },
  },
};
</script>

<style lang="scss">
.picture-lot {
  position: relative;
  height: 328px;
  width: auto;

  border: 1px solid #e1e1e1;

  & img {
    width: 278px;
  }
  &__img {
    height: 168px;
  }
  &__info {
    display: flex;
    flex-direction: column;
    align-items: flex-start;

    margin: 12px 24px 0px;

    &__name &__author {
      font-family: inherit;
      font-style: normal;
      font-weight: 400;
      font-size: 18px;
      line-height: 150%;
      color: #343030;
    }
  }
  &__sale {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin: 22px 24px 24px;
  }
  &__download,
  &__buy-btn,
  &__basket-btn {
    height: 48px;
    width: 118px;

    display: flex;
    align-items: center;
  }
  &__download {
    justify-content: center;
  }

  &__buy-btn {
    justify-content: center;
    background: #382e2b;
    color: #f4f6f9;
    &:hover {
      background: rgba(119, 103, 99, 1);
    }
  }
  &__basket-btn {
    position: relative;
    display: flex;
    justify-content: end;

    padding-right: 9px;

    background: #5b3a32;
    color: #f4f6f9;
    font-family: 'Merriweather', serif;
    font-size: 14px;
    font-weight: 700;
    line-height: 21px;
    letter-spacing: 0em;
    text-align: center;
    &:hover {
      background: rgba(119, 103, 99, 1);
    }
  }
  &__basket-btn::before {
    content: '';
    position: absolute;
    width: 18px;
    height: 18px;

    left: 11px;
    top: 32%;

    background: url(../assets/checkMark.svg) no-repeat;
  }
  &__old-price {
    opacity: 0.5;
    text-decoration: line-through;
  }
  &__sold {
    margin: 34px 0 26px 24px;
    color: #343030;
    font-family: 'Merriweather';
    font-style: normal;
    font-weight: 700;
    font-size: 16px;
    line-height: 150%;
  }
}
</style>
