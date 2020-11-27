<template>
  <div id="app">
    <Header />
    <main class="container">
      <h1 class="container__title">Картины эпохи Возрождения</h1>
      <div class="cards">
        <PCard v-for="p in paintings" :key="p.title"
               :title="p.title" :image="p.image"
               :price="p.price" :oldPrice="p.oldPrice"
               :inCart="!!cart.find(i => i.title == p.title)"
               :loading="!!loading.includes(p.title)"
               @buy="toggleCart(p)" />
      </div>
    </main>
    <Footer />
  </div>
</template>

<script>
import axios from 'axios';

import Header from '@/components/Header.vue'
import Footer from '@/components/Footer.vue'
import PCard from '@/components/PaintingCard.vue'

export default {
  name: 'App',
  data: () => ({
    paintings: [
      {
        title: "«Рождение Венеры» Сандро Боттичелли",
        oldPrice: 2000000,
        price: 1000000,
        image: require("@/assets/paintings/born.png")
      },
      {
        title: "«Тайная вечеря»  Леонардо да Винчи",
        price: 3000000,
        image: require("@/assets/paintings/secret.png")
      },
      {
        title: "«Сотворение Адама» Микеланджело",
        oldPrice: 6000000,
        price: 5000000,
        image: require("@/assets/paintings/adam.png")
      },
      {
        title: "«Урок анатомии» Рембрандт",
        image: require("@/assets/paintings/anatomy.png")
      }
    ],
    cart: [],
    loading: []
  }),
  mounted () {
    try {
      this.cart = JSON.parse(localStorage.getItem("cart")) || [];
    } catch (_e) { console.error(_e) }
  },
  methods: {
    // В большом проекте был бы удобнее и практичнее Vuex
    async toggleCart (painting) {
      console.log(this.cart)

      let inCart = !!this.cart.find(item => item.title == painting.title);
      if (inCart) {
        this.cart = this.cart.filter(item => item.title != painting.title);
      } else {
        this.loading.push(painting.title);
        await axios.get("https://jsonplaceholder.typicode.com/posts/1");
        this.loading = this.loading.filter(item => item != painting.title);
        // - Зачем в корзину добавлять объект полностью?
        // - Пригодится в случае создания реальной корзины
        this.cart.push(painting);
      }
      localStorage.setItem("cart", JSON.stringify(this.cart));
    }
  },
  components: { Header, PCard, Footer }
}
</script>

<style lang="scss">

// Merriweather font CDN
@import url('https://fonts.googleapis.com/css2?family=Merriweather:wght@300;400;700&display=swap');

html, body, #app {
  height: 100%;
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Merriweather, serif;
  color: #343030;
  background: #F6F3F3;
}


h1 { font-size: 24px;}
h2 { font-size: 18px;}

// В UI Kit'e написано, что шрифты h4-h6 - 14px, но сами написаны шрифтом 16px
// Связался с HR - сказали, что h4-h6 - 16px
h3, h4, h5, h6 { font-size: 16px;}

h1, h3, h4 { font-weight: bold; }
h2, h5 { font-weight: normal; }
h6 { font-weight: lighter; }

#app {
  display: flex;
  flex-direction: column;
}

.container {
  flex: 1;
  width: 1216px;
  margin: 45px auto;
  &__title {
    margin-bottom: 39px;
  }
}
.cards {
  display: grid;
  grid-template-columns: 282px 282px 282px 282px;
  grid-column-gap: 32px;
  grid-row-gap: 16px;
}
</style>
