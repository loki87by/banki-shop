<template>
  <header>
    <ul class="navigation">
      <li class="navigation-link"><h4>Каталог</h4></li>
      <li class="navigation-link"><h4>Доставка</h4></li>
      <li class="navigation-link"><h4>Оплата</h4></li>
      <li class="navigation-link"><h4>Контакты</h4></li>
      <li class="navigation-link"><h4>О компании</h4></li>
    </ul>
    <div class="header-search">
      <input
        type="text"
        class="header-searchInput"
        placeholder="Поиск по названию картины"
      />
      <button type="button">Найти</button>
    </div>
  </header>
</template>

<script>
export default {
  name: 'Header'
}
</script>

<style>
@import url("../../styles/header.css");
</style>
