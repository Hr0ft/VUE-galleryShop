<template>
  <nav class="header__navBar">
    <ul class="header__nav-menu">
      <li v-for="el in this.links">
        <a href="#">{{ el.link }}</a>
      </li>
    </ul>
  </nav>
</template>
<script>
export default {
  data() {
    return {
      links: [
        { link: 'Каталог' },
        { link: 'Доставка' },
        { link: 'Оплата' },
        { link: 'Контакты' },
        { link: 'О компании' },
      ],
    };
  },
};
</script>
<style lang="scss">
.header {
  &__navBar {
    width: 100%;
    margin: 0 auto;
    display: flex;
    justify-content: center;
  }
  &__nav-menu {
    display: flex;
    justify-content: space-evenly;
    li {
      display: inline-block;
      padding: 0 24px;
    }
    li a {
      font-size: 14px;
      font-style: normal;
      font-weight: 400;
      line-height: 150%;
    }
  }
}
</style>
