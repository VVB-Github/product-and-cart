<!-- пока что статичная информация -->
<template>
    <main class="wrapper">
        <h1>Past Orders</h1>

        <table class="product-table">
          <thead>
            <!-- Тег <tr> (table row) используется в HTML для определения строки таблицы. -->
            <tr>
              <!-- <td><span class="sr-only">Product Image</span></td> -->
              <td>Product</td>
              <td>Price</td>
              <td>Quantity</td>
              <td>Total</td>
              <td><span class="sr-only">Actions</span></td>
            </tr>
          </thead>
          <!-- проходим по отдельным заказам в pastorders -->
          <tbody v-for="(order, index) in pastorders" :key="index" >
            <!-- проходимся по отдельным продуктам в прошлых заказах -->
            <h3>Purchase of {{ getTime(index) }} date</h3>
            <tr v-for="(value, key) in order" :key="key">
              <td>{{ key }}</td>
              <td>${{ getPrice(key) }}</td>
              <td>{{ value }}</td>
              <td>${{ (getPrice(key)*value).toFixed(2) }}</td>
              <td><button class="btn btn-dark">Add</button></td>
            </tr>
            <h4>Total cost is ${{ getOrderPrice(order) }}</h4>
          </tbody>
        </table>
      </main>
</template>

<script>
export default {
  name: 'PastOrders',
  props: ['pastorders', 'inventory'],
  methods: {
    /* функция нахождения итоговой суммы одного заказа */
    getOrderPrice (order) {
      let price = 0
      for (const key in order) {
        price += this.getPrice(key) * order[key]
      }
      return price.toFixed(2)
    },
    getPrice (name) {
      const product = this.inventory.find((p) => {
        return p.name === name
      })
      return product.price.USD
    },
    /* функция преобразования строки со значением времени в UTC в форматированную строку с точностью до часа */
    getTime (time) {
      const timestamp = parseInt(time, 10)
      const date = new Date(timestamp)
      const year = date.getFullYear()
      const month = date.getMonth() + 1 // getMonth() возвращает месяц от 0 до 11
      const day = date.getDate()
      const hours = date.getHours()
      const formattedString = `${year}-${month < 10 ? '0' + month : month}-${day < 10 ? '0' + day : day} ${hours < 10 ? '0' + hours : hours}:00`
      return formattedString
    }
  }
}
</script>
