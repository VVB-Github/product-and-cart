<!-- В этом файле описана и реализована логика единичной карточки товара -->

<!-- тут наш html с списанными в него интерактивными и динамическими компонентами -->
<template>
<!-- проходимся по всему инвентарю и для каждого элемента создаём карточку
    slice - даёт нам лишь 3 верхних элемента -->
    <div class="card">
        <div class="card-title">
        {{ product.name }}
        </div>
        <div class="card-body">
        <!-- тег i часто применяется для вставки иконок -->
        <i class="icofont-10x icofont-{{ product.icon }}"></i>
        <form>
            <div class="row">
                <div class="cell">
                    <label>Type:</label>
                </div>
            <div class="cell">
                <em>{{ product.type }}</em>
            </div>
            </div>
            <div class="row">
            <div class="cell">
                <label>Price:</label>
            </div>
            <div class="cell">
                ${{ product.price.USD }}
            </div>
            </div>
            <div class="row">
            <div class="cell">
                <label>Quantity:</label>
            </div>
            <div class="cell">
                <!-- v-model.number во Vue.js используется для создания двустороннего связывания данных
                    между элементом формы <input> и переменной quantity в экземпляре Vue. Когда вы
                    используете v-model.number с элементом <input type="number">, Vue автоматически
                    преобразует значение ввода из строки в число. -->
                <input type="number" v-model.number="quantity">
            </div>
            </div>
        </form>
        </div>
        <div class="card-footer">
        <!-- метод addToCart обьявлен в файле App.vue. quantity обьявлен тут, а product импортируется из
        product -элемент inventory, который передается в ProductCard при его вызове из ProductList например
        btn-light — это специфический класс, который определяет дополнительную стилизацию для кнопки, делая
        её визуальный вид "светлым".-->
        <button @click="addToCart(product.name, quantity)" class="btn btn-light">
            Add to cart
        </button>
        </div>
    </div>
</template>

<!-- тут прописанна логика управления реактивными и интерактивными компонентами -->
<script>

/* export default в файле компонента Vue.js действительно необходимо для того, чтобы этот компонент мог
быть импортирован и использован в других частях приложения. */
export default {

  /* это регестрирует импорт компонентов из файла вызова Productcard. Тут мы импортируем обьекты,функции,переменные */
  props: ['product', 'index', 'addToCart'],

  /* data является одним из основных опций компонента, которая используется для объявления реактивных
  данных компонента.
  то, что quantity инициализировано значением нуль, не означает, что оно всегда будет равно нулю в работе компонента.
  В Vue.js, значение, заданное в data(), является начальным состоянием данных компонента */
  data () {
    return {
      quantity: 0
    }
  }
}
</script>
