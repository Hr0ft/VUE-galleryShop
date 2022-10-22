<template>
  <form class="header__search" @submit="">
    <input
      type="text"
      v-model="title"
      placeholder="Поиск по названию картины"
    />
    <button type="submit">Найти</button>
  </form>
</template>
<script>
export default {
  methods: {
    onSubmit() {
      this.$emit('onHandle-Change', this.title);
    },
  },
  data() {
    return {
      title: '',
    };
  },
};
</script>

<style lang="scss">
.header {
  &__search {
    display: flex;
    width: $hedarSearchBlockWidth - 1;
    input {
      margin: 0;
      padding: 13px 16px 14px 16px;
      height: 48px;
      width: 294px;

      border: 1px solid $borderColor;

      font-family: inherit;
      font-size: 14px;
      font-weight: 400;
      line-height: 21px;
      letter-spacing: 0em;
      text-align: left;
      color: #343030;
      background-color: #f6f3f3;
      :placeholder-shown {
        color: #9f9f9f;
      }
      &:focus {
        outline: none;
      }
    }
    button {
      height: 48px;
      width: 122px;

      border-radius: 0px;

      background: rgba(64, 52, 50, 1);

      font-weight: 700;
      font-size: 14px;
      line-height: 150%;
      color: #ffffff;
      &:hover {
        background: rgba(119, 103, 99, 1);
      }
    }
  }
}
</style>
