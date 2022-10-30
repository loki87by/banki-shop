<template>
  <main>
    <h1>Картины эпохи Возрождения</h1>
    <section class="items">
      <div
        :class="item.enabled ? 'item' : 'item item__saled'"
        v-for="item of items"
        :key="item.id"
        @click="(e) => {openPopup(e, item.id)}"
      >
        <img :src="item.src" :alt="item.title" class="item__image" />
        <div class="item__container">
          <h2 class="item__title">{{ item.title }}</h2>
          <article v-if="item.enabled">
            <div class="item__trade">
              <h5 v-if="item.oldPrice !== ''" class="item__oldPrice">
                {{ item.oldPrice }}
              </h5>
              <h3 class="item__price">{{ item.price }}</h3>
            </div>
            <button
              v-if="
                !basket.some(i => i === item.id) &&
                  !addedToBasket.some(i => i === item.id)
              "
              @click="addToBasket(item.id)"
              title="добавить в корзину"
              class="item__price-button"
            >
              Купить
            </button>
            <button
              v-else-if="
                basket.some(i => i === item.id) &&
                  addedToBasket.some(i => i === item.id)
              "
              @click="removeFromBasket(item.id)"
              title="убрать из корзины"
              class="item__price-button item__reserved"
            >
              В корзине
            </button>
            <section v-else>
              <figure class="preloader"></figure>
            </section>
          </article>
          <article v-else>
            <h3 :style="{marginTop: '10px'}">Продана на аукционе</h3>
          </article>
        </div>
      </div>
    </section>
  </main>
</template>

<script>
export default {
  name: 'Main',
  props: [
    'items',
    'basket',
    'addToBasket',
    'removeFromBasket',
    'addedToBasket',
    'openPopup'
  ]
}
</script>

<style>
@import url("../../styles/main.css");
</style>
