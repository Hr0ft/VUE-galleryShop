<template>
  <div class="shop" id="shop">
    <header class="header">
      <div class="header__wrapper">
        <HeaderNavBar></HeaderNavBar>
        <form class="header__search">
          <input
            type="text"
            v-model="searchValue"
            @input="onChangeSearch"
            placeholder="Поиск по названию картины"
          />
          <button type="submit">Найти</button>
        </form>
      </div>
    </header>
    <main class="main">
      <section class="gallery">
        <h1 class="gallery__title">Картины эпохи Возрождения</h1>
        <div class="gallery__container">
          <PictureLot
            v-for="lot in lotLists"
            :key="lot.id"
            v-bind:lot="lot"
          ></PictureLot>
        </div>
      </section>
    </main>
    <Footer></Footer>
  </div>
</template>

<script>
import { list } from 'postcss';
import img1 from './assets/anatomyLesson.png';
import img2 from './assets/theBirthOfVenenra.png';
import img3 from './assets/theCreationOfAdam.png';
import img4 from './assets/theLastSupper.png';
import img5 from './assets/theBirthOfVenenra.jpg';

import Footer from './components/Footer.vue';
import HeaderNavBar from './components/HeaderNavBar.vue';
import PictureLot from './components/pictureLot.vue';

export default {
  components: { Footer, HeaderNavBar, PictureLot },

  methods: {
    showPicturePopup() {
      this.popupIsOpen = true;
    },
    closePicturePopup() {
      this.popupIsOpen = false;
    },
    updateLotLists(arr, lists) {
      let a = arr;
      let l = lists;
      if (l !== null) {
        l.map((item) => {
          let id = item.id;
          if (a.includes(id)) {
            item.inBasket = true;
          }
        });
      }
    },
    onChangeSearch() {
      if (this.searchValue.trim()) {
        this.lotLists.map((item) => {
          let picName = item.picName.toLowerCase();
          let sample = this.searchValue.toLowerCase();

          if (!picName.includes(sample)) return (item.inSearch = false);
          return (item.inSearch = true);
        });
      } else {
        this.lotLists.map((item) => (item.inSearch = true));
      }
    },
  },
  mounted() {
    let basket = localStorage.getItem('pictInBasketID');
    if (basket) {
      this.localBasketIds = JSON.parse(basket);
    }
    this.updateLotLists(this.localBasketIds, this.lotLists);
  },
  data() {
    return {
      popupIsOpen: false,
      localBasketIds: [],
      searchValue: '',
      lotLists: [
        {
          id: 1,
          picName: '«Рождение Венеры»',
          picAuth: 'Сандро Боттичелли',
          picURL: './theBirthOfVenenra.png',
          oldCost: 3000000,
          trueCost: 20000000,
          sale: true,
          sold: false,
          inBasket: false,
          inSearch: true,
          lotModalIsOpen: true,
          slides: [
            { id: 1, pic: './theBirthOfVenenra.jpg' },
            { id: 2, pic: './theLastSupper.png' },
            { id: 3, pic: './theCreationOfAdam.png' },
          ],
        },
        {
          id: 2,
          picName: '«Тайная вечерия»',
          picAuth: 'Леонардо да Винчи',
          picURL: './theLastSupper.png',
          oldCost: null,
          trueCost: 20000000,
          sale: false,
          sold: false,
          inBasket: false,
          inSearch: true,
          lotModalIsOpen: true,
          slides: [
            { id: 1, pic: './theBirthOfVenenra.png' },
            { id: 2, pic: './theBirthOfVenenra.png' },
            { id: 3, pic: './theBirthOfVenenra.png' },
          ],
        },
        {
          id: 3,
          picName: '«Сотворение Адама»',
          picAuth: 'Микеланджело',
          picURL: './theCreationOfAdam.png',
          oldCost: 6000000,
          trueCost: 30000000,
          sale: true,
          sold: false,
          inBasket: false,
          inSearch: true,
          lotModalIsOpen: true,
          slides: [
            { id: 1, pic: './theBirthOfVenenra.png' },
            { id: 2, pic: './theBirthOfVenenra.png' },
            { id: 3, pic: './theBirthOfVenenra.png' },
          ],
        },
        {
          id: 4,
          picName: '«Урок анатомии»',
          picAuth: 'Рембранты',
          picURL: './anatomyLesson.png',
          oldCost: 6000000,
          trueCost: 20000000,
          sale: true,
          sold: true,
          inBasket: false,
          inSearch: true,
          lotModalIsOpen: true,
          slides: [
            { id: 1, pic: './theBirthOfVenenra.png' },
            { id: 2, pic: './theBirthOfVenenra.png' },
            { id: 3, pic: './theBirthOfVenenra.png' },
          ],
        },
        {
          id: 5,
          picName: '«Уроск анатомии»',
          picAuth: 'Сандро Боттичелли',
          picURL: './anatomyLesson.png',
          oldCost: 6000000,
          trueCost: 20000000,
          sale: true,
          sold: true,
          inBasket: false,
          inSearch: true,
          lotModal: { IsOpen: true },
          slides: [
            { id: 1, pic: './theBirthOfVenenra.png' },
            { id: 2, pic: './theBirthOfVenenra.png' },
            { id: 3, pic: './theBirthOfVenenra.png' },
          ],
        },
      ],
    };
  },
};
</script>

<style lang="scss">
@import './sass/constants.scss';
.shop {
  position: relative;
  margin: 0 auto;
  height: 920px;
}
.main {
  height: 100%;
}
.gallery {
  margin: 0 auto;
  width: $body-width + 2;
  height: auto;
  &__title {
    margin-top: 45px;
    height: 36px;
    font-weight: 700;
    font-size: $regularFontSize;
    line-height: 150%;
  }
  &__container {
    position: relative;
    display: grid;
    grid-template-columns: 280px 280px 280px 280px;
    grid-column-gap: 32px;
    grid-row-gap: 32px;

    margin-top: 39px;
  }
}
</style>
