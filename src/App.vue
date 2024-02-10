<template>
  <header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link>
      <router-link to="/pastorder" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>
    <!-- <router-link @click="toggleSidebar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart ({{ totalQuantity }})</span>
    </router-link> -->
  </header>
  <router-view/>
</template>

<!-- thanks to the scoped keyword, styles described here only affect page in this file -->
<style scoped>
</style>
