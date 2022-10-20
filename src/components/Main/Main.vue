<template>
  <main>
    <h1>Картины эпохи Возрождения</h1>
    <section class="items">
      <div class="item" v-for="(item, index) of items" :key="index">
        <img :src="item.src" :alt="item.title" class="item-image" />
        <div class="item-container">
          <h2 class="item-title">{{ item.title }}</h2>
          <article v-if="item.enabled">
            <div class="item-trade">
              <h5 v-if="item.oldPrice !== ''" class="item-oldPrice">
                {{ item.oldPrice }}
              </h5>
              <h3 class="item-price">{{ item.price }}</h3>
            </div>
            <button v-if="item.available">Купить</button>
            <button v-else class="item-reserved">В корзине</button>
          </article>
          <article v-else>
            <h3>Продана на аукционе</h3>
          </article>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
import { ITEMS } from '../../utils/consts.js'

export default {
  name: 'Main',
  data: function () {
    return {
      items: ITEMS
    }
  },
  methods: {}
}
</script>

<style>
@import url("../../styles/main.css");
</style>
