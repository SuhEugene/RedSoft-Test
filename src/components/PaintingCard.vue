<template lang="html">
  <div class="pcard" :class="{'pcard--sold': !price}">

    <div class="pcard__image" :style="`background-image: url('${image}')`"></div>
    <h2 class="pcard__title">{{ title }}</h2>
    <div class="pcard__bottom">
      <div v-if="price" class="pcard__bottom__prices">
        <div v-if="oldPrice" class="pcard__bottom__price--old">{{ fancyOldPrice }} $</div>
        <div class="pcard__bottom__price">{{ fancyPrice }} $</div>
      </div>

      <div v-if="!price" class="pcard__bottom__sold">
        Продана на аукционе
      </div>

      <Button v-if="price" :light="inCart" :loading="loading" class="pcard__bottom__button" @click="$emit('buy')">
        <CheckIcon v-if="inCart" style="margin-right: 4px;" />
        {{ inCart ? 'В корзине' : 'Купить' }}
      </Button>
    </div>
  </div>
</template>

<script>
import Button from "@/components/Button.vue";
import CheckIcon from "@/components/icons/CheckIcon.vue";

export default {
  name: "PaintingCard",
  props: {
    image: String,
    title: String,
    price: Number,
    oldPrice: Number,
    inCart: Boolean,
    loading: Boolean
  },
  computed: {
    fancyPrice () {
      return this.price ? this.price.toLocaleString("fr-FR") : '';
    },
    fancyOldPrice () {
      return this.oldPrice ? this.oldPrice.toLocaleString("fr-FR") : '';
    }
  },
  components: { Button, CheckIcon }
}
</script>

<style lang="scss">
  $border: 1px solid #E1E1E1;
  .pcard {
    width: 280px;
    border: $border;
    padding-bottom: 26px;
    &--sold { opacity: .5; }
    &__image {
      margin-bottom: 20px;
      width: 100%;
      height: 160px;
      background: #222;
      background-size: cover;
      background-position: center;
      border-bottom: $border;
    }
    &__title {
      padding: 0 24px;
      margin-bottom: 23px;
    }
    &__bottom {
      padding: 0 24px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      &__price {
        font-size:16px;
        &--old {
          font-size: 14px;
          color: #A0A0A0;
          text-decoration: line-through;
        }
      }
      &__sold {
        height: 48px;
        display: flex;
        justify-content: center;
        align-items: center;
      }
    }
  }
</style>
