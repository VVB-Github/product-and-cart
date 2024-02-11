<template>
  <div class="home">
    home
    <div class="splash-container">
      <div class="splash">
        <h1>Splendid Food</h1>
      </div>
    </div>

    <main class="wrapper">

      <h2>Recommended</h2>

      <div class="recommended">

        <!-- проходимся по всему инвентарю и для каждого элемента создаём карточку
        slice - даёт нам лишь 3 верхних элемента -->
        <ProductCard
          v-for="(product, index) in inventory.slice(0,3)"
          :key="product.id"
          class="card"
          :index="index"
          :product=product
          :addToCart="addToCart"
        />

      </div>

    </main>

  </div>
</template>
<script>
import ProductCard from '@/components/ProductCard.vue'

export default {
  name: 'HomeView',
  props: ['inventory', 'addToCart'],
  components: {
    ProductCard
  }
}
</script>
