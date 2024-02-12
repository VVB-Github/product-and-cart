<!-- домашняя страница -->
<template>
  <div class="home">
    <div class="splash-container">
      <div class="splash">
        <h1>Splendid Food</h1>
      </div>
    </div>

    <main class="wrapper">

      <h2>Recommended</h2>

      <div class="recommended">

        <!-- проходимся по всему инвентарю и берём 3-и верхних элемента. И параметры в основном берутся из product
        и передаются в страницу ProductCard-->
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

/* @ означает, что компонент ProductCard.vue импортируется из директории components, которая находится в корне проекта.
когда вы используете псевдоним @, он обычно уже предварительно настроен на указание папки src вашего проекта. */
import ProductCard from '@/components/ProductCard.vue'

export default {
  name: 'HomeView',

  /* props — это пользовательские атрибуты, которые вы можете зарегистрировать на компоненте. */
  props: ['inventory', 'addToCart'],

  /* Во Vue.js, когда вы видите конструкцию components: { ProductCard } внутри объекта export default компонента,
  это означает регистрацию дочернего компонента для использования в шаблоне (template) родительского компонента.
  Таким образом, вы можете использовать компонент ProductCard внутри шаблона родительского компонента, как если бы
  это был обычный HTML-элемент. */
  components: {
    ProductCard
  }
}
</script>
