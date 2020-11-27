<template lang="html">
  <div class="s-input">
    <input class="s-input__el" type="text" :placeholder="placeholder" @input="handle" :value="value">
    <Button class="s-input__button">Найти</Button>
  </div>
</template>

<script>
import Button from '@/components/Button.vue';

export default {
  name: "SearchInput",
  components: { Button },
  methods: {
    handle (e) { this.$emit("input", e.target.value) }
  },
  props: {
    value: String,
    placeholder: String
  }
}
</script>

<style lang="scss">
.s-input {
  height: 48px;
  display: flex;
  &__el {
    padding: 0 16px;
    outline: none;
    height: 100%;
    font-size: 14px;
    width: 294px;
    border: 1px solid #E1E1E1;
    box-sizing: border-box;
    background: transparent;
    font-family: inherit;
    &:focus {
      border-color: #B5B5B5;
    }
    &::placeholder{
      color: #9F9F9F;
    }
  }
  &__button {
    height: 100%;
    width: 122px;
  }
}
</style>
