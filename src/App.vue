<template>
  <header class="top-bar spread">
    <!-- наши кнопки для перемещения между страницами -->
    <nav class="top-bar-nav">
      <!-- <router-link>
          является частью Vue Router, который представляет собой официальную библиотеку
          маршрутизации для Vue.js. Этот тег используется для создания навигационных ссылок в приложении на основе
          Vue.js, позволяя пользователю переходить от одного представления к другому без перезагрузки страницы.
          Он работает аналогично тегу <a> в HTML, но предназначен для работы в контексте одностраничных приложений
          (SPA), где содержимое страницы обновляется динамически без полной перезагрузки.
        to в теге <router-link>
          указывает маршрут, на который будет выполнен переход. Этот маршрут должен
          быть определен в конфигурации маршрутизатора Vue Router приложения. Значение атрибута to может быть
          строкой, представляющей путь, или объектом, описывающим более сложную  -->
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
    <div @click="toggleSidebar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <!-- функция ниже позволяет нам вевыести общее число заказанных товаров -->
      <span>Cart ({{ totalQuantity }})</span>
    </div>
  </header>
  <!-- эта строка передает аргументы инвентори и функцию. Чат-жпт пишет что это якобы не стандартный метод передачи
  пропсов () пропсы inventory и addToCart предполагается передать в компонент, который отображается <router-view>
  в зависимости от текущего маршрута. -->
  <router-view :inventory="inventory" :addToCart="addToCart"/>

  <SideBar
    v-if="show_Sidebar"
    :toggle="toggleSidebar"
    :cart="cart"
    :inventory="inventory"
    :remove="removeItem"
  />
</template>

<script>
import SideBar from './components/SideBar.vue'
/* импорт данных */
import food from './food.json'

export default {
  components: {
    SideBar
  },
  /* в инвентарь кладём данные. А в карте будет что клиент выбрал себе */
  data () {
    return {
      show_Sidebar: false,
      inventory: food,
      cart: {}
    }
  },
  /* computed свойства автоматически пересчитываются, когда зависимые реактивные данные изменяются. Это идеально
  подходит для сложных вычислений, которые должны обновляться в ответ на изменения данных. */
  computed: {
    totalQuantity () {
      /* Object.values(this.cart)
        преобразует значения свойства cart объекта в массив. Если предположить, что cart выглядит
        так: { '1': 3, '2': 5 }, то результатом будет массив [3, 5], где каждое число представляет количество
        товара в корзине.
      reduce((acc, curr) => { return acc + curr }, 0)
        применяется к массиву количеств товаров. Метод reduce используется для получения суммарного количества
        всех товаров в корзине. Здесь acc (аккумулятор) инициализируется нулем и представляет собой текущую сумму
        количества товаров, а curr (текущее значение) — это количество конкретного товара в массиве. Для каждого
        элемента массива выполняется операция сложения acc + curr, что позволяет последовательно суммировать
        количество всех товаров. */
      return Object.values(this.cart).reduce((acc, curr) => {
        return acc + curr
      }, 0)
    }
  },
  methods: {
    addToCart (name, quantity) {
      /* если такого товара нет то инициализируем счётчик товара в ноль */
      if (!this.cart[name]) this.cart[name] = 0
      /* и далее приплюсовываем в значение числа товара quantity - оно вводится?? */
      this.cart[name] += quantity
    },
    /* функция смены флага для показа сайдбара на противоположный */
    toggleSidebar () {
      this.show_Sidebar = !this.show_Sidebar
    },
    /* с помощью функции delete (из нативного js) - удаляем некоторый товар из корзины */
    removeItem (name) {
      delete this.cart[name]
    }
  }
}
</script>
