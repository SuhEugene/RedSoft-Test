<template lang="html">
  <button @click="$emit('click', this)" class="button" :disabled="loading" :class="{'button--light': light}">
    <slot v-if="!loading"></slot>
    <div v-else class="button__loading"></div>
  </button>
</template>

<script>
export default {
  props: { light: Boolean, loading: Boolean }
}
</script>

<style lang="scss">
  .button {
    border: none;
    padding: 0;
    margin: 0;
    font-family: inherit;
    outline: none;
    background: #382E2B;
    font-weight: bold;
    font-size: 14px;
    height: 48px;
    width: 118px;
    color: white;
    display: flex;
    justify-content: center;
    align-items: center;
    cursor: pointer;
    &:hover { background: #776763; }
    &[disabled] { background: #C1B4B1; cursor: default; pointer-events: none;}

    &__loading {
      width: 14px;
      height: 14px;
      border: 3px solid white;
      border-left: none;
      animation: spin 1s both infinite linear;
    }

    &--light {
      background: #5B3A32;

      /* Не могу быть уверен что цвет hover'a должен быть именно таким, т.к.
         в UI-Kit'e не указан цвет при наведении из состояния "В корзине"
         При выполнении реального задания я бы обратился к дизайнеру */
      &:hover { background: #776763; }
    }
  }
  @keyframes spin {
    from { transform: rotate(0deg); }
    to   { transform: rotate(360deg); }
  }
</style>
