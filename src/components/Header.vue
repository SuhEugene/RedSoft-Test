<template lang="html">
  <header class="header">

    <a class="header__logo" href="/"><Logo /></a>

    <a class="header__link" href="#">Каталог</a>
    <a class="header__link" href="#">Доставка</a>
    <a class="header__link" href="#">Оплата</a>
    <a class="header__link" href="#">Контакты</a>
    <a class="header__link" href="#">О галерее</a>

    <SearchInput v-model="search" placeholder="Поиск по названию картины" style="margin-left: 185px;" />

  </header>
</template>

<script>
import Logo from "@/components/Logo.vue";
import SearchInput from "@/components/SearchInput.vue";

export default {
  name: "Header",
  data: () => ({
    search: ""
  }),
  components: { SearchInput, Logo }
}
</script>

<style lang="scss">
  .header {
    height: 96px;
    display: flex;
    justify-content: center;
    align-items: center;
    border-bottom: 1px solid #E1E1E1;
    &__logo {
      height: 48px;
      width: 48px;
    }
    &__link {
      font-size: 14px;
      margin-left: 48px;
      color: #343030;
      text-decoration: none;
      &:hover { text-decoration: underline; }
    }
  }
</style>
