<template lang="html">
  <!-- Копия header по причине возможного изменения наполнения.
       Через slot не реализовал по причине индивидуальности элемента
       (Могу объяснить решенее подробнее при необходимости) -->
  <footer class="footer">

    <a class="footer__logo" href="/"><Logo /></a>

    <a class="footer__link" href="#">Каталог</a>
    <a class="footer__link" href="#">Доставка</a>
    <a class="footer__link" href="#">Оплата</a>
    <a class="footer__link" href="#">Контакты</a>
    <a class="footer__link" href="#">О галерее</a>

    <div class="footer__data">
      <div class="footer__data__el">
        <PhoneIcon class="footer__data__el__icon" />
        +7 (495) 555-55-55
      </div>
      <div class="footer__data__el">
        <MapIcon class="footer__data__el__icon" />
        г. Москва, ул. Расплетина, 24
      </div>
    </div>

  </footer>
</template>

<script>
import Logo from "@/components/Logo.vue";
import PhoneIcon from "@/components/icons/PhoneIcon.vue";
import MapIcon from "@/components/icons/MapIcon.vue";

export default {
  name: "Footer",
  data: () => ({
    search: ""
  }),
  components: { Logo, PhoneIcon, MapIcon }
}
</script>

<style lang="scss">
  .footer {
    flex-shrink: 0;
    height: 96px;
    display: flex;
    justify-content: center;
    align-items: center;
    background: #ECEAEA;
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
    &__data {
      margin-left: 152px;
      display: grid;
      grid-template-columns: 1fr 1fr;
      grid-column-gap: 48px;
      grid-row-gap: 4px;
      @media (max-width: 1430px) {
        grid-template-columns: 1fr;
      }
      &__el {
        display: flex;
        align-items: center;
        &__icon { margin-right: 8px; }
      }
    }
  }
</style>
