<template>
  <footer class="footer">
    <div class="footer__wrapper">
      <ul class="footer__nav">
        <li><a href="#">Каталог</a></li>
        <li><a href="#">Доставка</a></li>
        <li><a href="#">Оплата</a></li>
        <li><a href="#">Контакты</a></li>
        <li><a href="#">О компании</a></li>
      </ul>
      <div class="contacts">
        <div class="contacts__phone">+7 (812) 555-55-55</div>
        <div class="contacts__location">г. Санкт-Петербург, ул. Ефимова, 3</div>
      </div>
    </div>
  </footer>
</template>
<script>
export default {};
</script>

<style lang="scss">
.footer {
  height: 96px;

  display: flex;
  align-items: center;

  background: #eceaea;
  width: 100%;

  &__wrapper {
    position: relative;
    margin: 0 auto;

    display: flex;
    align-items: inherit;
    justify-content: center;

    font-size: 14px;
    font-weight: 400;
    line-height: 21px;
    letter-spacing: 0em;
    text-align: left;
  }
  &__nav {
    position: absolute;
    left: -540px;

    display: flex;
    justify-content: flex-end;

    width: 600px;

    & li {
      margin: 0 24px;
    }
    & li a {
      color: #555555;
    }
  }
}
.contacts {
  position: absolute;

  left: 180px;
  display: flex;
  justify-content: space-around;

  width: 496px;
  height: 22px;

  color: #555555;
  &__phone,
  &__location {
    position: relative;
    text-align: left;
  }

  &__phone::before {
    background: url(../assets/phone.svg) no-repeat;
  }

  &__location {
    margin-left: 75px;
    &::before {
      background: url(../assets/location.svg) no-repeat;
    }
  }
  &__phone::before,
  &__location::before {
    content: '';
    position: absolute;
    width: 20px;
    height: 22px;
    left: -20px;
    top: 3px;
  }
}
</style>
